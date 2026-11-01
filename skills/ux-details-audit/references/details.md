# Die 20 Details

Pro Detail: was es ist, warum es wirkt, woran man sein Vorhandensein erkennt, die Umsetzung für Web (CSS, React) und Flutter, und die Fallstricke. Die Snippets sind Ausgangspunkte, keine Drop-in-Lösungen. Paketnamen und Versionsangaben vor dem Einbau gegen die aktuelle Dokumentation prüfen.

**Zu Bewegung:** Dauer, Easing und Springs stehen hier nicht. Dafür `emil-design-eng`, `apple-design` und `motion-design`. Jede Animation in diesem Dokument ist mit `prefers-reduced-motion` (Flutter: `MediaQuery.disableAnimationsOf(context)`) abzusichern.

Gliederung: A Wartezeit und Daten (1, 2, 5, 6, 7, 8, 19), B Bedienung (3, 4, 20), C Bewegung und Übergänge (9, 10, 11, 12), D Touch und Eingabe (13, 14, 15), E Typografie und Form (16, 17, 18).

---

## A. Wartezeit und Daten

### 1. Skeleton Loaders statt Spinner

**Was.** Während Inhalt lädt, zeigt die Oberfläche graue Platzhalter in der Form des späteren Inhalts statt eines zentrierten Spinners.

**Warum.** Das Layout steht sofort, nichts springt beim Eintreffen der Daten, und die Wartezeit wirkt kürzer, weil der Nutzer schon Struktur sieht. Ein Spinner sagt nur "warte", ohne zu sagen worauf.

**Erkennung.** Vorhanden, wenn jede Liste, Karte und Detailansicht mit asynchronen Daten einen Platzhalter in der Größe des Inhalts zeigt. Ein Skeleton nur auf der Startseite bei Spinnern in allen anderen Ansichten zählt als fehlend. Spinner bleiben richtig für Aktionen (Button nach Klick, Speichern), nicht für Inhalt.

**Web.**
```css
.skeleton {
  background: linear-gradient(90deg, var(--sk-a) 25%, var(--sk-b) 50%, var(--sk-a) 75%);
  background-size: 200% 100%;
  animation: sk 1.4s linear infinite;
  border-radius: 6px;
}
@keyframes sk { to { background-position: -200% 0; } }
@media (prefers-reduced-motion: reduce) { .skeleton { animation: none; } }
```
In Next.js App Router: `loading.tsx` neben `page.tsx` oder `<Suspense fallback={<ListSkeleton />}>`. Der Platzhalter übernimmt Höhe und Breite des echten Inhalts, sonst springt das Layout trotzdem.

**Flutter.** Paket `skeletonizer` (`Skeletonizer(enabled: isLoading, child: realWidget)`) baut den Platzhalter aus dem echten Widget-Baum und vermeidet doppelte Layout-Pflege. Alternativ `shimmer`.

**Fallstricke.** Skeleton und Inhalt müssen dieselben Abmessungen haben, sonst entsteht Layout Shift. Bei Ladezeiten unter etwa 200 ms flackert ein Skeleton nur kurz auf; dann entweder gar nichts zeigen oder eine Mindestanzeigedauer setzen. Shimmer-Animation bei reduzierter Bewegung abschalten. Für Screenreader `aria-busy="true"` am Container und ein sichtbar verstecktes "Lädt".

---

### 2. Optimistic Updates

**Was.** Die Oberfläche zeigt das Ergebnis einer Aktion sofort und gleicht erst danach mit dem Server ab. Schlägt die Anfrage fehl, wird zurückgerollt.

**Warum.** Aktionen wie Liken, Abhaken, Verschieben und Umbenennen fühlen sich instantan an, statt 200 bis 800 ms zu zögern.

**Erkennung.** Vorhanden, wenn nach einem Klick der neue Zustand erscheint, bevor die Antwort da ist (im Netzwerk-Tab auf "Slow 3G" prüfen), und ein Fehlschlag sichtbar zurückrollt. Nur ein Button, der sofort in den Ladezustand geht, ist kein Optimistic Update.

**Web.**
```tsx
// React 19
const [optimisticTodos, addOptimistic] = useOptimistic(todos,
  (state, newTodo: Todo) => [...state, { ...newTodo, pending: true }]);

async function action(formData: FormData) {
  addOptimistic({ id: crypto.randomUUID(), title: String(formData.get("title")) });
  await createTodo(formData);   // wirft bei Fehler, State fällt auf `todos` zurück
}
```
Mit TanStack Query: `onMutate` (Cache sichern und überschreiben), `onError` (Rollback aus dem gesicherten Stand), `onSettled` (`invalidateQueries`).

**Flutter.** State sofort ändern, Anfrage absetzen, im `catch` den vorherigen State wiederherstellen und per `SnackBar` melden. Bei Riverpod/Bloc den alten Wert vor der Mutation festhalten.

**Fallstricke.** Nur für Aktionen, die fast immer gelingen und umkehrbar sind. Nie für Zahlungen, Löschen ohne Soft Delete oder Aktionen mit Serverlogik, die das Ergebnis ändert (dort 19 und ein ehrlicher Ladezustand). Reihenfolge bei schnellen Mehrfachklicks beachten: Rollback eines älteren Fehlers darf einen neueren Erfolg nicht überschreiben. Temporäre IDs durch die Server-ID ersetzen.

---

### 5. Undo-Toasts statt Bestätigungsdialog

**Was.** Eine destruktive Aktion läuft sofort, ein Toast bietet für einige Sekunden "Rückgängig" an, statt vorher "Wirklich löschen?" zu fragen.

**Warum.** Bestätigungsdialoge werden aus Gewohnheit weggeklickt und schützen deshalb kaum, kosten aber bei jeder Aktion einen Klick. Undo schützt tatsächlich und stört nicht.

**Erkennung.** Fehlt, wenn `confirm(`, ein `AlertDialog` oder ein "Sind Sie sicher?"-Modal vor Löschen, Archivieren oder Verschieben liegt, obwohl die Aktion umkehrbar wäre. Vorhanden nur, wenn "Rückgängig" den Zustand wirklich wiederherstellt.

**Web.**
```tsx
import { toast } from "sonner";

function remove(item: Item) {
  const timer = setTimeout(() => api.delete(item.id), 5000); // Löschung erst nach Ablauf
  hideLocally(item.id);
  toast("Eintrag gelöscht", {
    duration: 5000,
    action: { label: "Rückgängig", onClick: () => { clearTimeout(timer); showLocally(item); } },
  });
}
```
Alternativ Soft Delete (`deleted_at`) mit späterem Aufräumjob; dann gilt Undo auch nach Seitenwechsel.

**Flutter.**
```dart
ScaffoldMessenger.of(context).showSnackBar(SnackBar(
  content: const Text('Eintrag gelöscht'),
  action: SnackBarAction(label: 'Rückgängig', onPressed: () => restore(item)),
));
```

**Fallstricke.** Wird die Seite geschlossen, bevor der Timer feuert, geht die Löschung verloren oder läuft doppelt: besser Soft Delete serverseitig. Bestätigungsdialog bleibt richtig bei Unumkehrbarem (Konto löschen, Zahlung auslösen, Versand an Dritte), dann aber mit benannter Aktion im Button ("Konto löschen") statt "OK". Toast braucht `role="status"` bzw. `aria-live="polite"`, der Undo-Button muss per Tastatur erreichbar sein, und die Anzeigedauer darf bei Hover/Fokus pausieren.

---

### 6. Stale-while-revalidate

**Was.** Beim erneuten Besuch zeigt die Oberfläche sofort die zuletzt bekannten Daten und aktualisiert sie im Hintergrund.

**Warum.** Zurücknavigieren, Tab-Wechsel und App-Start zeigen sofort Inhalt statt eines Ladezustands. Die Daten sind kurz veraltet, aber sofort da.

**Erkennung.** Vorhanden, wenn nach Wechsel auf eine andere Seite und zurück kein Ladezustand erscheint und im Netzwerk-Tab trotzdem eine Revalidierung läuft. Fehlt, wenn jede Ansicht beim Betreten bei null anfängt.

**Web.** TanStack Query: sinnvolles `staleTime`, `placeholderData: keepPreviousData` bei Paginierung und Filtern. SWR: `useSWR(key, fetcher)` ist von Haus aus so. HTTP: `Cache-Control: max-age=60, stale-while-revalidate=600` für öffentliche GETs. Next.js: `fetch(url, { next: { revalidate: 60 } })` bzw. `revalidateTag`.

**Flutter.** Repository, das zuerst aus einem lokalen Speicher (Drift, Isar, Hive) streamt und dann das Netz nachlädt: `yield* local.watch(); await refresh();`.

**Fallstricke.** Cache-Schlüssel müssen Nutzer und Filter enthalten, sonst erscheinen fremde oder falsche Daten. Nach Mutationen invalidieren. Kein SWR für Daten, bei denen veraltet falsch wäre (Kontostand vor einer Überweisung, Lagerbestand im Warenkorb). Beim Abmelden den Cache leeren. Ein kleiner Hinweis "aktualisiert vor 2 Min" oder ein dezenter Revalidierungsindikator hilft, wenn die Daten sich sichtbar ändern.

---

### 7. Pre-rendering und Prefetch bei Hover

**Was.** Die nächste Seite wird geladen, bevor geklickt wird: beim Hover, beim Sichtbarwerden des Links oder beim Touch-Start.

**Warum.** Zwischen Hover und Klick vergehen oft einige hundert Millisekunden. Diese Zeit reicht oft, damit die Navigation ohne Wartezeit wirkt.

**Erkennung.** Vorhanden, wenn der Netzwerk-Tab beim Überfahren eines Links bereits Requests der Zielseite zeigt. In Next.js ist `<Link>` im Produktionsbuild standardmäßig mit Viewport-Prefetch; ein `<a href>` ersetzt das nicht. Prüfen, ob irgendwo `prefetch={false}` oder rohe Anker stehen.

**Web.**
```html
<script type="speculationrules">
{ "prerender": [{ "where": { "href_matches": "/produkte/*" }, "eagerness": "moderate" }] }
</script>
```
`moderate` löst bei Hover aus. Als Fallback in React: `onMouseEnter={() => router.prefetch(href)}`. Bei Nicht-Next-Stacks `<link rel="prefetch">` oder das Router-eigene Prefetch (React Router: `<Link prefetch="intent">`).

**Flutter.** Bilder mit `precacheImage` laden, Daten der Zielroute beim `onTapDown` anstoßen statt erst im `build` der neuen Seite.

**Fallstricke.** Nicht prefetchen: Abmelden, Löschen, Bestätigungslinks und alles mit Seiteneffekt per GET. Prerender führt JavaScript der Zielseite aus, also auch Analytics und Zähler: auf Consent und Seiteneffekte achten. Mobil gibt es kein Hover; dort `touchstart`/Sichtbarkeit nutzen und Datensparmodus (`navigator.connection.saveData`) respektieren.

---

### 8. BlurHash und LQIP als Platzhalter

**Was.** Bilder erscheinen zuerst als winzige, verschwommene Vorschau in den Farben des Originals (BlurHash, ThumbHash, Low-Quality Image Placeholder), die in das Bild überblendet.

**Warum.** Keine leeren Flächen und kein Layout Shift, die Seite wirkt von Anfang an gefüllt.

**Erkennung.** Vorhanden, wenn Bilder über der Falz oder in Galerien nicht von weiß auf voll springen. Zwei Voraussetzungen: feste Seitenverhältnisse (`width`/`height` oder `aspect-ratio`) und ein Platzhalter.

**Web.** Next.js: `<Image src placeholder="blur" blurDataURL={...} />`; lokale Importe bekommen den Platzhalter automatisch. Sonst `blurhash` oder `thumbhash` zur Build- bzw. Upload-Zeit berechnen, als Feld am Bild speichern und im Client rendern. Reines CSS-Minimum: `aspect-ratio` plus `background-color` in der Hauptfarbe des Bildes.

**Flutter.** `flutter_blurhash` (`BlurHash(hash: img.blurHash, image: img.url)`), oder `FadeInImage` mit kleinem Platzhalter.

**Fallstricke.** Hash beim Upload berechnen und speichern, nicht bei jedem Aufruf. LCP-Bild nicht lazy laden und mit `fetchpriority="high"` markieren. Der Platzhalter gehört in den Dokumentfluss mit demselben Seitenverhältnis, sonst springt es. Das Dekodieren eines BlurHash im Client kostet Rechenzeit: in Listen mit Dutzenden Bildern auf Canvas/`thumbhash` oder ein Inline-WebP von wenigen hundert Bytes ausweichen.

---

### 19. Idempotency Keys bei Zahlungen und Formularen

**Was.** Jede Anfrage, die etwas auslöst (Zahlung, Bestellung, Formular), trägt einen vom Client erzeugten eindeutigen Schlüssel. Der Server führt die Aktion pro Schlüssel höchstens einmal aus und liefert bei Wiederholung dasselbe Ergebnis.

**Warum.** Doppelklick, Netzabbruch mit automatischem Retry und Zurück-Taste führen sonst zu doppelten Abbuchungen oder doppelten Datensätzen.

**Erkennung.** Vorhanden, wenn der Header `Idempotency-Key` gesendet wird oder serverseitig eine Dedupe-Tabelle existiert, und der Submit-Button während des Sendens gesperrt ist. Ein reines `disabled` am Button ohne Schlüssel schützt nicht vor Retry und Mehrfach-Tabs.

**Web.**
```ts
// Schlüssel pro Absicht (beim Öffnen des Checkouts), nicht pro Klick
const [key] = useState(() => crypto.randomUUID());

await fetch("/api/orders", {
  method: "POST",
  headers: { "Content-Type": "application/json", "Idempotency-Key": key },
  body: JSON.stringify(order),
});
```
Server: Schlüssel plus Anfrage-Hash und Antwort speichern (Unique-Constraint auf Nutzer plus Schlüssel), bei Wiederholung die gespeicherte Antwort liefern, bei gleichem Schlüssel mit anderem Body einen Fehler. Stripe unterstützt den Header direkt, Schlüssel dort bis 255 Zeichen und 24 Stunden gültig; bei Zahlungsanbietern deren Doku prüfen.

**Flutter.** Paket `uuid`: Schlüssel beim Betreten des Bezahlbildschirms erzeugen und in den State legen; alle Wiederholungen derselben Absicht senden denselben Header.

**Fallstricke.** Ein neuer Schlüssel pro Versuch hebt den Schutz auf. Nach erfolgreicher Aktion den Schlüssel verwerfen, damit die nächste Bestellung einen neuen bekommt. Schlüssel gehören nur auf nicht idempotente Methoden (POST, PATCH); PUT und DELETE sind es ohnehin. Das Speichern der Antwort darf Zahlungsdaten nicht im Klartext ablegen. Zusätzlich den Button sperren und im UI den Zustand "wird verarbeitet" zeigen.

---

## B. Bedienung

### 3. Command Menu (Cmd/Ctrl+K)

**Was.** Ein Dialog, der per Tastenkürzel öffnet, durchsuchbar ist und Navigation sowie Aktionen enthält.

**Warum.** Geübte Nutzer erreichen jede Stelle ohne Mausweg; Linear, Notion und GitHub haben das als Standard etabliert. Es entlastet auch die Navigation bei vielen Funktionen.

**Erkennung.** Vorhanden, wenn `Ctrl+K` bzw. `Cmd+K` einen Dialog öffnet, Fuzzy-Suche funktioniert und mindestens Navigation plus die häufigsten Aktionen drinstehen. Nicht relevant bei Seiten mit wenigen Zielen (Landingpage, einfache Formular-App).

**Web.**
```tsx
useEffect(() => {
  const onKey = (e: KeyboardEvent) => {
    if ((e.metaKey || e.ctrlKey) && e.key.toLowerCase() === "k") {
      e.preventDefault();
      setOpen((o) => !o);
    }
  };
  window.addEventListener("keydown", onKey);
  return () => window.removeEventListener("keydown", onKey);
}, []);
```
Dialog mit `cmdk` (`<Command.Dialog>`) oder shadcn/ui `CommandDialog`; es bringt Fokusfalle, Pfeiltasten und Filter mit. Eintragsliste aus derselben Quelle wie die Navigation speisen, nicht doppelt pflegen.

**Flutter.** Nur bei Desktop- oder Web-Targets. `CallbackShortcuts` mit `SingleActivator(LogicalKeyboardKey.keyK, control: true)` (macOS: `meta: true`), darin `showDialog` mit Suchfeld und gefilterter Liste.

**Fallstricke.** Nicht in Eingabefeldern abfangen, wo Ctrl+K selbst eine Bedeutung hat (Rich-Text-Editoren, Link einfügen), oder dort bewusst überschreiben. Auf macOS Cmd, sonst Ctrl: Plattform erkennen und in der UI das richtige Symbol zeigen. Ergebnisse per Tastatur bedienbar und mit `role="combobox"` bzw. `listbox` für Screenreader auszeichnen. Zuletzt benutzte Einträge zuerst anzeigen.

---

### 4. Shortcut Hints in Tooltips und Menüs

**Was.** Wo eine Aktion ein Tastenkürzel hat, steht es neben dem Namen im Tooltip oder rechts im Menüeintrag.

**Warum.** Kürzel werden nur gelernt, wenn man sie dort sieht, wo man mit der Maus klickt. So wird aus einem Mausnutzer nach und nach ein Tastaturnutzer.

**Erkennung.** Vorhanden, wenn Tooltips und Menüeinträge für Aktionen mit Kürzel dieses mitzeigen und das Kürzel im Code tatsächlich dieselbe Aktion auslöst. Hinweis ohne funktionierendes Kürzel ist schlimmer als keiner.

**Web.**
```tsx
<button aria-keyshortcuts="Control+Shift+P" title="Befehl senden (Ctrl+Umschalt+P)">
  Senden <kbd>⌃⇧P</kbd>
</button>
```
`<kbd>` für die Darstellung, `aria-keyshortcuts` für assistive Technik. Anzeige je Plattform (`⌘` auf macOS, `Ctrl` sonst) aus einer zentralen Kürzel-Tabelle, die auch das Binden übernimmt.

**Flutter.**
```dart
MenuItemButton(
  shortcut: const SingleActivator(LogicalKeyboardKey.keyS, control: true),
  onPressed: save,
  child: const Text('Speichern'),
)
```
Flutter zeigt das Kürzel im Menü selbst an; der Shortcut muss zusätzlich über `Shortcuts`/`Actions` oder die Menüleiste wirklich gebunden sein.

**Fallstricke.** Nicht mit Browser- und Betriebssystemkürzeln kollidieren (Ctrl+W, Ctrl+T, Cmd+Q). Ein-Tasten-Kürzel ohne Modifikator verletzen WCAG 2.1.4, wenn sie sich nicht abschalten oder umbelegen lassen. Auf Touchgeräten keine Kürzel anzeigen. Tooltip muss auch bei Tastaturfokus erscheinen, nicht nur bei Hover.

---

### 20. Safe Triangle bei Hover-Menüs

**Was.** Fährt die Maus diagonal von einem Menüeintrag zu seinem Untermenü, bleibt das Untermenü offen, solange sich der Zeiger im Dreieck zwischen Startpunkt und Untermenü bewegt. Bekannt aus dem Amazon-Hauptmenü.

**Warum.** Ohne diesen Schutz springt das Untermenü auf den Eintrag unter dem Zeiger um, sobald die Maus schräg über Nachbareinträge streift.

**Erkennung.** Test im laufenden Produkt: Menüeintrag mit Untermenü überfahren, dann in gerader Linie diagonal zum Untermenü ziehen. Wechselt das Menü unterwegs, fehlt das Detail. Nicht relevant ohne Hover-Untermenüs.

**Web.** Fertige Lösungen bevorzugen: Radix (`DropdownMenu` mit Submenüs) bringt eine Pointer-Grace-Zone mit; Floating UI bietet `safePolygon()` als Hover-Handler. Selbstbau nur, wenn nötig:
```ts
// Grundidee: Bewegung nur dann als Wechsel werten, wenn der Zeiger
// das Dreieck (letzter Punkt, oberste/unterste Ecke des Untermenüs) verlässt.
function inTriangle(p: Pt, a: Pt, b: Pt, c: Pt) { /* Vorzeichen-Test der drei Kanten */ }
```
Einfacherer Behelf: Schließen um 100 bis 200 ms verzögern und bei erneutem Betreten abbrechen.

**Flutter.** Betrifft nur Desktop/Web. `MenuAnchor` und `SubmenuButton` bringen Hover-Untermenüs mit; ob die Pfadtoleranz reicht, im laufenden Produkt testen. Sonst `MouseRegion` mit verzögertem Schließen.

**Fallstricke.** Zu lange Verzögerung lässt das Menü träge wirken. Die Logik gilt nur für Maus; Touch und Tastatur öffnen Untermenüs per Tippen bzw. Pfeil rechts. Menüs, die per Klick öffnen, brauchen es nicht.

---

## C. Bewegung und Übergänge

Zur Ausführung (Dauer, Kurven, Spring-Parameter, Gesten-Handling) gelten `emil-design-eng` und `apple-design`. Hier steht nur, wann das Detail vorhanden ist.

### 9. View Transitions

**Was.** Der Wechsel zwischen Ansichten wird als zusammenhängende Überblendung oder Verwandlung dargestellt, statt hart umzuschalten. Gemeinsame Elemente (Vorschaubild zu Detailbild) bewegen sich von einer Stelle zur anderen.

**Warum.** Der Nutzer behält die räumliche Orientierung: er sieht, woher die neue Ansicht kommt.

**Erkennung.** Vorhanden, wenn Routenwechsel oder Listen-zu-Detail-Wechsel animiert sind und gemeinsame Elemente erkennbar mitwandern.

**Web.**
```css
@view-transition { navigation: auto; }           /* Multi-Page: Übergang bei normaler Navigation */
.card-img { view-transition-name: hero; }        /* pro Seite nur ein Element mit diesem Namen */
@media (prefers-reduced-motion: reduce) {
  ::view-transition-group(*), ::view-transition-old(*), ::view-transition-new(*) { animation: none; }
}
```
SPA: `document.startViewTransition(() => update())` mit Feature-Detection (`if (!document.startViewTransition) { update(); return; }`). In React gibt es eine `<ViewTransition>`-Komponente und in Next.js ein Opt-in; beides war zuletzt noch experimentell bzw. versionsabhängig, Stand in der aktuellen Doku prüfen.

**Flutter.** `Hero` für gemeinsame Elemente, Paket `animations` für Container Transform, Shared Axis und Fade Through.

**Fallstricke.** Eindeutiger `view-transition-name` pro Moment, sonst bricht der Übergang ab. Während des Übergangs sind Inhalte nicht interaktiv: kurz halten. Nicht jeder Wechsel braucht einen Übergang; häufige Aktionen wirken mit Animation zäh. Fallback ohne Unterstützung ist harter Wechsel, nie ein Fehler.

---

### 10. Swipe-to-dismiss Sheets

**Was.** Bottom Sheets, Drawer und Modale lassen sich wegwischen, die Bewegung folgt dem Finger und entscheidet nach Distanz und Geschwindigkeit, ob geschlossen wird.

**Warum.** Auf Touchgeräten ist Wischen die erwartete Geste; ein Sheet nur mit X-Button wirkt wie eine Webseite im Gerätegehäuse.

**Erkennung.** Vorhanden, wenn ein Sheet sich mitziehen lässt, bei losgelassener Geste zurückfedert oder schließt und der Hintergrund mitgeht. Fehlt bei Modalen, die auf Mobilgeräten nur per Button schließen.

**Web.** Paket `vaul` (`<Drawer.Root>`, Drag und Snap Points eingebaut) oder shadcn/ui `Drawer`. Selbstbau: Pointer Events, `touch-action: none` am Griff, Bewegung per `transform` direkt aus der Pointer-Position, beim Loslassen Geschwindigkeit auswerten. Details dazu in `apple-design`.

**Flutter.** `showModalBottomSheet(enableDrag: true, ...)` ist Standard; `DraggableScrollableSheet` für Sheets mit Snap-Höhen; `Dismissible` für Listeneinträge. `isDismissible` und `enableDrag` bei Formularen mit ungespeicherten Eingaben bewusst abwägen (`PopScope`).

**Fallstricke.** Scrollender Inhalt im Sheet konkurriert mit der Wischgeste: nur vom oberen Rand oder Griff aus schließen, wenn der Inhalt oben angekommen ist. Immer eine nicht-gestenbasierte Alternative anbieten (Schließen-Button, Esc). Ungespeicherte Eingaben dürfen nicht stumm verloren gehen (Detail 5). Keine CSS-Transitions für die Geste selbst.

---

### 11. Unterbrechbare Animationen

**Was.** Eine laufende Animation lässt sich jederzeit umkehren oder neu starten, ohne dass sie erst zu Ende läuft oder zum Anfang springt. Neue Animationen starten beim aktuellen Wert.

**Warum.** Wer ein Menü öffnet und sofort wieder schließt, soll nicht warten oder einen Sprung sehen. Das ist der Unterschied zwischen "reagiert" und "spielt ein Video ab".

**Erkennung.** Test im laufenden Produkt: Zustand umschalten und mitten in der Animation zurückschalten. Springt es oder läuft es erst durch, fehlt das Detail. Im Code: `@keyframes` für Zustandswechsel (nicht unterbrechbar) gegen `transition` (unterbrechbar); in Flutter `controller.forward(from: 0)` gegen `controller.animateTo`/`reverse()` vom aktuellen Wert.

**Web.** Zustandswechsel mit `transition` auf Eigenschaften (`transform`, `opacity`), `@keyframes` nur für Endlosschleifen und Einstiege. Bei Federn und Gesten eine Animationsbibliothek mit Geschwindigkeitsübernahme (Motion, React Spring). Ausführung siehe `apple-design`.

**Flutter.** Implizite Widgets (`AnimatedContainer`, `AnimatedOpacity`, `AnimatedSlide`) sind unterbrechbar. Bei `AnimationController` vom aktuellen `value` weiter animieren und `SpringSimulation` mit der Gestengeschwindigkeit füttern.

**Fallstricke.** `animation-fill-mode` und Endzustand in CSS-Klassen statt in Keyframes halten. Beim Umkehren die Dauer nicht verdoppeln: proportional zur Restdistanz. `prefers-reduced-motion` ersetzt Bewegung durch Überblenden oder Sofortwechsel, nicht durch gar nichts, wenn der Zustand sonst unlesbar wird.

---

### 12. Predictive Back (Android)

**Was.** Bei der Android-Zurück-Geste zeigt das System eine Vorschau des Ziels, während der Finger zieht, und führt die Navigation erst beim Loslassen aus.

**Warum.** Der Nutzer sieht vor dem Loslassen, wohin Zurück führt, und kann die Geste abbrechen. Das System bietet das ab Android 13 als Opt-in an. Apps, die Zurück noch über das alte Key-Event abfangen, bekommen die Vorschau nicht oder verlieren Eingaben, weil die Entscheidung zu spät fällt.

**Erkennung.** Nur für Android relevant. Vorhanden, wenn im Manifest `android:enableOnBackInvokedCallback="true"` steht, Flutter die Seitenübergänge für Predictive Back verwendet und Zurück-Abfangen über `PopScope` statt `WillPopScope` läuft. Auf einem Gerät oder Emulator mit aktivierter Entwickleroption "Predictive back animations" testen.

**Flutter.**
```xml
<!-- android/app/src/main/AndroidManifest.xml, im <application>-Tag -->
android:enableOnBackInvokedCallback="true"
```
```dart
MaterialApp(
  theme: ThemeData(
    pageTransitionsTheme: const PageTransitionsTheme(builders: {
      TargetPlatform.android: PredictiveBackPageTransitionsBuilder(),
    }),
  ),
)

PopScope(
  canPop: !hasUnsavedChanges,
  onPopInvokedWithResult: (didPop, result) { if (!didPop) confirmDiscard(); },
  child: ...,
)
```
Verfügbarkeit und Opt-in hängen an der Flutter-Version; Stand in der aktuellen Flutter-Doku zu Predictive Back prüfen.

**Web.** Nicht relevant. Für Web-Apps als PWA greift das Browserverhalten.

**Fallstricke.** `WillPopScope` ist veraltet und mit Predictive Back unvereinbar, weil die Entscheidung vor der Geste fallen muss: `canPop` muss synchron den Stand kennen. Kein `Navigator.pop` im `onPopInvoked` für den Normalfall. Eigene Übergänge, die den Back-Fortschritt nicht kennen, brechen den Effekt.

---

## D. Touch und Eingabe

### 13. Hit Slop: Tap-Ziele von mindestens 44 px

**Was.** Interaktive Elemente haben eine Trefferfläche von mindestens etwa 44 mal 44 Punkten, auch wenn die sichtbare Fläche kleiner ist.

**Warum.** Kleine Ziele werden verfehlt, besonders mit dem Daumen. Apple verlangt 44 pt, Material 48 dp; WCAG 2.2 fordert in SC 2.5.8 (AA) mindestens 24 mal 24 CSS-Pixel und empfiehlt in SC 2.5.5 (AAA) 44 mal 44.

**Erkennung.** Elemente messen (DevTools, Flutter Inspector, oder `getBoundingClientRect()`). Kritisch: Icon-Buttons, Schließen-Kreuze, Checkboxen, Links in Listen, Tab-Leisten, dicht beieinander liegende Aktionen.

**Web.**
```css
.icon-btn { position: relative; inline-size: 24px; block-size: 24px; }
.icon-btn::after {            /* sichtbar 24 px, tippbar 44 px */
  content: ""; position: absolute; inset: -10px;
}
@media (pointer: coarse) { .link-row { min-block-size: 44px; } }
```
Die vergrößerte Fläche per Pseudo-Element erhält das Layout. Keine zusätzlichen Hover-Zustände in der Erweiterung.

**Flutter.** Material-Widgets halten 48 dp ein (`kMinInteractiveDimension`, `MaterialTapTargetSize.padded`). Eigene Widgets mit `GestureDetector` auf kleinem Icon bekommen die Fläche durch `Padding` oder `SizedBox` innerhalb des Detectors, oder `behavior: HitTestBehavior.opaque`. In React Native: `hitSlop`.

**Fallstricke.** Erweiterte Flächen dürfen sich nicht mit Nachbarn überlappen, sonst werden Taps mehrdeutig. Ziele mit weniger als 8 px Abstand zusammenlegen oder Abstand erhöhen. Bei Dichte-Optionen (`VisualDensity.compact`) auf Touchgeräten nicht unter die Mindestgröße gehen. Text-Links im Fließtext sind von der Mindestgröße ausgenommen, in Listen und Navigation nicht.

---

### 14. Safe Area Insets

**Was.** Inhalte und fixierte Leisten halten Abstand zu Notch, Dynamic Island, Home-Indikator, Kamera-Ausschnitten und System-Leisten.

**Warum.** Sonst liegen Buttons unter dem Home-Indikator oder Text unter der Notch. Bei Android 15 (Target SDK 35) ist Edge-to-Edge Standard, wodurch Apps, die das nicht berücksichtigen, plötzlich unter System-Leisten zeichnen.

**Erkennung.** Auf Gerät oder Emulator mit Notch bzw. Gestennavigation ansehen: fixierte Fußleisten, Tab-Bars, Vollbild-Modale, Landscape. Im Code: `env(safe-area-inset-*)` und `viewport-fit=cover` bzw. `SafeArea`.

**Web.**
```html
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
```
```css
.bottom-bar { padding-bottom: max(12px, env(safe-area-inset-bottom)); }
.app { min-block-size: 100dvh; }   /* dvh statt vh: berücksichtigt die einblendende Browserleiste */
```
Ohne `viewport-fit=cover` liefert `env()` immer 0.

**Flutter.** `SafeArea` um Seiten oder fixierte Elemente; `Scaffold` übernimmt es für `AppBar` und `bottomNavigationBar`. Bei Edge-to-Edge: `SystemChrome.setEnabledSystemUIMode(SystemUiMode.edgeToEdge)` und Insets bewusst über `MediaQuery.viewPaddingOf(context)` bzw. `viewInsetsOf` (Tastatur) einrechnen.

**Fallstricke.** Tastatur-Inset (`viewInsets`) ist nicht dasselbe wie Safe Area: Eingabefelder am unteren Rand müssen mit der Tastatur hochwandern. `100vh` ist auf Mobile oft höher als der sichtbare Bereich. Bei Querformat auch links und rechts Inset beachten. Hintergrundfarben bis an den Rand ziehen, Inhalt nach innen setzen.

---

### 15. One-time-Code-Autofill

**Was.** Eingabefelder für SMS- und E-Mail-Codes werden so ausgezeichnet, dass das Betriebssystem den Code von der eingegangenen Nachricht in die Tastatur vorschlägt oder automatisch einsetzt.

**Warum.** Der Nutzer muss den Code nicht abtippen oder die App wechseln. Das senkt Abbrüche bei Login und Verifizierung spürbar.

**Erkennung.** Das Feld trägt `autocomplete="one-time-code"` und `inputmode="numeric"`. Fehlt, wenn ein Code-Feld ein normales Textfeld ohne Attribute ist, oder wenn der Code auf sechs einzelne Eingabefelder verteilt wurde, ohne dass Einfügen und Autofill funktionieren.

**Web.**
```html
<input type="text" inputmode="numeric" autocomplete="one-time-code"
       pattern="[0-9]*" maxlength="6" name="otp">
```
Für Android-Chrome zusätzlich die WebOTP API (`navigator.credentials.get({ otp: { transport: ["sms"] } })`), wofür die SMS mit `@beispiel.de #123456` enden muss (Domain-gebundenes Format). In React: `autoComplete="one-time-code"` (camelCase).

**Flutter.** `TextField(autofillHints: const [AutofillHints.oneTimeCode], keyboardType: TextInputType.number)` innerhalb einer `AutofillGroup`. iOS füllt den Vorschlag über die Tastatur. Android-SMS-Retrieval/User Consent braucht ein Plug-in (z. B. `smart_auth`); der Aufbau hängt an der Plugin-Version.

**Fallstricke.** Sechs Einzelfelder brechen Autofill, weil es nur ein Feld füllt: ein einzelnes Feld verwenden und optisch in Kästchen darstellen, oder `onPaste` und Autofill in die Felder verteilen. `type="number"` vermeiden (entfernt führende Nullen, zeigt Spinner). Nach vollständiger Eingabe automatisch absenden, aber Fehler und erneutes Senden sichtbar machen.

---

## E. Typografie und Form

### 16. Tabular Numbers bei wechselnden Zahlen

**Was.** Ziffern haben feste, gleiche Breite, sodass sich Zahlen in Tabellen, Zählern, Uhren und Preisen beim Ändern nicht seitlich verschieben.

**Warum.** Mit proportionalen Ziffern zappelt ein laufender Timer, Spalten richten sich nicht an der Einerstelle aus, und Beträge lassen sich schlecht vergleichen.

**Erkennung.** Alles, was sich ändert oder untereinander steht: Zähler, Countdown, Fortschritt in Prozent, Preislisten, Tabellen, Zeitstempel. Vorhanden, wenn dort `font-variant-numeric: tabular-nums` bzw. `FontFeature.tabularFigures()` gesetzt ist.

**Web.**
```css
.num, td.amount, .timer { font-variant-numeric: tabular-nums; }
```
Tailwind: `tabular-nums`. Schrift muss das OpenType-Feature `tnum` enthalten; sonst passiert nichts.

**Flutter.**
```dart
Text('12:34', style: const TextStyle(fontFeatures: [FontFeature.tabularFigures()]))
```

**Fallstricke.** Nicht global setzen: im Fließtext sehen proportionale Ziffern besser aus. Viele Systemschriften unterstützen es, manche Webfonts nicht (Subset-Optimierung entfernt `tnum` gelegentlich). Rechtsbündig ausrichten für Beträge. Zusätzlich `Intl.NumberFormat` mit richtiger Locale für Dezimal- und Tausendertrennzeichen; dazu `i18n-locale-correctness`, falls installiert.

---

### 17. `text-wrap: balance` für Überschriften

**Was.** Der Browser verteilt die Zeilen einer Überschrift gleichmäßig, statt in der letzten Zeile ein einzelnes Wort stehen zu lassen.

**Warum.** Schlankere, gleichmäßigere Überschriften ohne manuelle Umbrüche. Eine Zeile CSS.

**Erkennung.** Vorhanden, wenn Überschriften und kurze zentrierte Texte `text-wrap: balance` haben. Fehlt, wenn Headlines Witwen ("Wörter allein in der letzten Zeile") zeigen oder mit `<br>` umbrochen wurden.

**Web.**
```css
h1, h2, h3, .balance { text-wrap: balance; }
p, li { text-wrap: pretty; }   /* vermeidet Witwen in Absätzen */
```
Tailwind: `text-balance`, `text-pretty`. Browser ohne Unterstützung ignorieren die Eigenschaft; es entsteht kein Schaden.

**Flutter.** Kein Gegenstück. Für zentrierte Texte hilft `textWidthBasis: TextWidthBasis.longestLine`, das die Breite des `Text`-Widgets auf die längste Zeile zieht. Für Schlüsselüberschriften manuelle Umbrüche setzen und mit Lokalisierung prüfen.

**Fallstricke.** Wirkt nur bei wenigen Zeilen: Chromium begrenzt auf 6, Firefox auf 10 Zeilen. Nicht auf lange Absätze setzen (`pretty` dort). Bei `display: flex` auf dem Textcontainer greift es teils nicht wie erwartet; Wrapper nutzen. Übersetzungen ändern die Umbrüche: in jeder Sprache ansehen.

---

### 18. Continuous Corners (Squircles)

**Was.** Ecken sind keine Kreisbögen, sondern gehen weich in die Kante über (wie Apples App-Icons und Karten). Das wirkt weniger "gestanzt".

**Warum.** Der Übergang vom Kreisbogen zur Geraden ist bei normalem `border-radius` sichtbar abrupt. Bei großen Radien fällt es am stärksten auf.

**Erkennung.** Nur bei Elementen mit größerem Radius relevant (Karten, Buttons, Icons, Bilder). Vorhanden, wenn `corner-shape: squircle` bzw. `RoundedSuperellipseBorder` verwendet wird. Bei kleinen Radien von 2 bis 4 px ist der Unterschied nicht erkennbar; dann `nicht relevant`.

**Web.**
```css
.card { border-radius: 24px; }
@supports (corner-shape: squircle) {
  .card { corner-shape: squircle; }
}
```
`corner-shape` ist neu und war zuletzt nur in Chromium verfügbar: Unterstützung prüfen und `border-radius` immer als Fallback lassen. Älteres Muster per SVG-Maske oder `clip-path` mit Pfad nur für feste Größen sinnvoll.

**Flutter.** `RoundedSuperellipseBorder` (in neueren Flutter-Versionen, Version prüfen), ältere `ContinuousRectangleBorder` ist eine Annäherung mit anderem Radius-Verhalten und braucht deutlich höhere Radiuswerte.
```dart
Container(decoration: ShapeDecoration(
  color: color,
  shape: const RoundedSuperellipseBorder(borderRadius: BorderRadius.all(Radius.circular(24))),
))
```

**Fallstricke.** Eigenschaften wie `overflow: hidden` und `box-shadow` müssen der Form folgen; bei Flutter `ClipPath`/`ShapeDecoration` mit demselben `ShapeBorder` nutzen, sonst stehen Schatten und Clip im alten Kreisradius. Konsistenz: überall oder nirgends, ein Mix wirkt unruhig. Nie für Funktionales opfern: Fallback mit Kreisradius ist akzeptabel.

---

## Gemeinsame Prüfregeln

- **Reduzierte Bewegung:** `@media (prefers-reduced-motion: reduce)` bzw. `MediaQuery.disableAnimationsOf`. Gilt für 1, 9, 10, 11 und jede Skalier-, Verschiebe- und Überblend-Animation.
- **Feature-Detection:** `CSS.supports(...)`, `@supports (...)`, `if (document.startViewTransition)`. Nie nach User-Agent entscheiden.
- **Tastatur und Screenreader:** Jedes neue Element (Command Menu, Toast, Sheet, Untermenü) per Tastatur erreichbar und mit passender Rolle ausgezeichnet. Bei Zweifel `accessibility`.
- **Messen statt glauben:** Netzwerk-Drossel auf "Slow 3G" für 1, 2, 6, 7, 8; Gerät oder Emulator für 10, 12, 13, 14, 15; zwei Browser (Chromium, Safari) für 9, 17, 18.
- **Verbleibende Unsicherheit ehrlich benennen:** APIs mit Hinweis "Version prüfen" sind nicht gegen die aktuelle Doku verifiziert; wer sie einbaut, schaut dort nach (z. B. mit `context7`, falls verfügbar).
