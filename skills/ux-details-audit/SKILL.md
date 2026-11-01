---
name: ux-details-audit
description: Use when asked to polish an app or website so it feels high quality, to audit it for missing UX details, or to make it feel faster, more native or more "Apple-like" or "Linear-like". Also use when a spinner, a confirmation dialog, a plain OTP input, a bottom sheet, a hover menu, a price or counter that changes, a payment or submit button, or a large image is about to be built, and before a release of a React, Next.js, Flutter or Electron UI.
---

# UX-Details-Audit

Audit einer App oder Website auf die unsichtbaren Details, die ein Produkt hochwertig wirken lassen, und Umsetzung der fehlenden. Grundlage sind 20 konkrete Details, die in Apple-, Linear-, Gmail-, Stripe- und Amazon-Produkten wiederkehren. Jedes einzelne wird kaum bemerkt, ihr Fehlen summiert sich zu dem Gefühl "fühlt sich billig an".

**Kernprinzip:** Ein Detail zählt nur, wenn es im laufenden Produkt wirkt. Ein importiertes Paket oder ein CSS-Property im Stylesheet ist kein Beleg. Geprüft wird, ob der Nutzer das Verhalten tatsächlich bekommt, und nicht, ob das Wort im Code vorkommt.

## Abgrenzung

- **Timing, Easing, Springs, Choreografie** gehören nicht hierher. Wo ein Detail Bewegung braucht (View Transitions, Sheets, unterbrechbare Animationen), nennt dieser Skill nur, dass sie fehlt, und verweist für die Ausführung auf `emil-design-eng`, `apple-design` und `motion-design`, falls installiert. Dauern und Kurven werden hier nicht wiederholt.
- **Barrierefreiheit im Ganzen** (Kontrast, Screenreader, Fokusführung) ist Sache von `accessibility`. Hier erscheinen nur die Überschneidungen: Tap-Ziele, `prefers-reduced-motion`, Tastaturkürzel.
- **Ladezeit und Core Web Vitals** misst `web-quality-audit` bzw. `core-web-vitals`. Hier geht es um gefühlte Geschwindigkeit (Skeletons, Prefetch, Platzhalter), nicht um Messwerte.
- **Visuelles Design und Marke** (Typografie-Wahl, Farben, Layout) sind nicht Teil des Audits.

## Ablauf

1. **Stack erkennen** (unten). Davon hängt ab, welche Details überhaupt relevant sind und welche Suchmuster gelten.
2. **Jedes der 20 Details prüfen.** Suchmuster in der Tabelle unten, Kriterium für "vorhanden" und Umsetzung in `references/details.md`. Die Referenzdatei vor der Umsetzung eines Details lesen, nicht aus dem Gedächtnis arbeiten: Browser-Support und Flutter-APIs ändern sich.
3. **Bericht** als Tabelle ausgeben (Format unten). Zuerst nur den Bericht, nichts umbauen.
4. **Priorisiert umsetzen**, sobald der Auftrag das hergibt. Lautet der Auftrag ausdrücklich "setze die fehlenden um", direkt nach Priorität; sonst die gewünschten Stufen abfragen.
5. **Verifizieren.** Jedes umgesetzte Detail im laufenden Produkt auslösen (Browser, Emulator oder Gerät), mit `prefers-reduced-motion: reduce` gegenprüfen und Build bzw. Tests laufen lassen. "Fertig" gilt erst danach.

## Stack erkennen

| Merkmal | Stack | Folge |
|---|---|---|
| `package.json` mit `next` | Web, React, Next.js | Alle Web-Details; Prefetch und Platzhalter vieles schon eingebaut, trotzdem prüfen |
| `package.json` mit `react` ohne `next` | Web, React (Vite, CRA) | Alle Web-Details; Prefetch und Routing selbst bauen |
| nur `index.html`, kein Framework | Web, statisch | CSS-Details und Autofill; Daten-Details (2, 6, 19) nur falls es Fetches gibt |
| `pubspec.yaml` mit `flutter` | Flutter | Mobile Details (10, 12, 13, 14, 15); Web-Hover-Details (3, 4, 20) nur bei Desktop- oder Web-Target |
| `package.json` mit `electron` | Electron | Web-Details im Renderer; 12 und 14 entfallen; 3 und 4 sind hier besonders wichtig |
| `android/` und `ios/` neben `lib/` | Flutter mobil | Plattformdateien prüfen (Manifest für 12, Info.plist nur für Statusleisten) |

Mehrere Stacks im Repo (etwa Next.js-Web plus Flutter-App) werden getrennt geprüft, mit je eigener Spalte im Bericht.

## Suchmuster

Zeigt, wo man hinschauen muss. Jeder Treffer ist ein Hinweis, kein Beleg. Ob das Detail wirklich wirkt, entscheidet das Kriterium in `references/details.md`. Mehrere Begriffe je Zeile sind Alternativen.

| Nr | Detail | Web (React, Next, CSS) | Flutter |
|---|---|---|---|
| 1 | Skeleton Loader | `Skeleton`, `shimmer`, `animate-pulse`, `loading.tsx`, `Suspense`; gegen: `Spinner`, `isLoading &&`, `CircularProgress` | `Skeletonizer`, `Shimmer`; gegen: `CircularProgressIndicator` als Seiteninhalt |
| 2 | Optimistic Updates | `useOptimistic`, `onMutate`, `optimisticData`, `setQueryData` | optimistischer State vor `await`, Rollback im `catch` |
| 3 | Command Menu | `cmdk`, `kbar`, `CommandDialog`, `metaKey`, `ctrlKey`, `"k"` | `CallbackShortcuts`, `Shortcuts`, `Actions`, `SingleActivator` |
| 4 | Shortcut Hints | `<kbd>`, `aria-keyshortcuts`, `title=` mit Kürzel, Tooltip mit Kürzel | `MenuItemButton`, `shortcut:`, `Tooltip` mit Kürzel |
| 5 | Undo statt Bestätigung | `toast` mit `action`, `sonner`, `Undo`, `Rückgängig`; gegen: `window.confirm`, `confirm(`, `Are you sure`, `Wirklich löschen` | `SnackBarAction`, `showSnackBar`; gegen: `AlertDialog` vor Löschen |
| 6 | Stale-while-revalidate | `staleTime`, `useSWR`, `stale-while-revalidate`, `revalidate`, `keepPreviousData`, `placeholderData` | Cache-Schicht (Drift, Hive, `cached_`), Repository mit Cache-Stream |
| 7 | Prefetch | `prefetch`, `router.prefetch`, `onMouseEnter`, `speculationrules`, `rel="prefetch"` | `precacheImage`, Daten beim Navigieren vorladen |
| 8 | BlurHash/LQIP | `blurhash`, `blurDataURL`, `placeholder="blur"`, `thumbhash`, `lqip` | `flutter_blurhash`, `FadeInImage`, `placeholder:` |
| 9 | View Transitions | `startViewTransition`, `view-transition-name`, `@view-transition`, `<ViewTransition` | `Hero`, `OpenContainer`, `animations`-Paket |
| 10 | Swipe-to-dismiss Sheet | `vaul`, `Drawer`, `onPointerMove` mit Sheet; gegen: Modal nur mit X-Button | `showModalBottomSheet`, `enableDrag`, `DraggableScrollableSheet`, `Dismissible` |
| 11 | Unterbrechbare Animation | `transition:` statt `@keyframes` für Zustandswechsel, `useSpring`, `animate(`, Motion | `AnimationController` mit `.animateTo` aus aktuellem Wert, implizite `Animated*`-Widgets; gegen: `forward(from: 0)` |
| 12 | Predictive Back | nicht relevant | `PredictiveBackPageTransitionsBuilder`, `PopScope`, `enableOnBackInvokedCallback` im Manifest; gegen: `WillPopScope` |
| 13 | Hit Slop | `min-height: 44px`, `min-h-11`, `min-h-[44px]`, `pointer: coarse`, `inset: -`, `::after` mit negativem Offset | `kMinInteractiveDimension`, `MaterialTapTargetSize`, `minimumSize`, `hitSlop` (React Native), `Padding` um `GestureDetector` |
| 14 | Safe Area Insets | `env(safe-area-inset`, `viewport-fit=cover`, `100dvh`; gegen: `100vh` bei fixierten Leisten | `SafeArea`, `MediaQuery.viewPaddingOf`, `viewInsetsOf`, `SystemChrome.setEnabledSystemUIMode` |
| 15 | One-time-Code-Autofill | `autocomplete="one-time-code"`, `autoComplete="one-time-code"`, `inputmode="numeric"`, `WebOTP`, `OTPCredential` | `AutofillHints.oneTimeCode`, `AutofillGroup`, `smart_auth`, `sms_autofill` |
| 16 | Tabular Numbers | `tabular-nums`, `font-variant-numeric`, `font-feature-settings` mit `tnum` | `FontFeature.tabularFigures` |
| 17 | `text-wrap: balance` | `text-wrap`, `text-balance`, `text-pretty`, `balance-text` | `TextWidthBasis.longestLine`, manuelle Umbrüche |
| 18 | Continuous Corners | `corner-shape`, `squircle`, `superellipse`, `smooth-corners`, SVG-Maske | `RoundedSuperellipseBorder`, `ContinuousRectangleBorder`; gegen: `RoundedRectangleBorder` überall |
| 19 | Idempotency Keys | `Idempotency-Key`, `idempotencyKey`, `randomUUID`, serverseitige Dedupe-Tabelle | `Idempotency-Key`, `Uuid().v4()` pro Absicht, nicht pro Versuch |
| 20 | Safe Triangle | `safePolygon`, `NavigationMenu`, `pointer-grace`, `clip-path: polygon` auf Submenü, `onMouseLeave` mit `setTimeout` | `MenuAnchor`, `SubmenuButton`, `MouseRegion` mit Verzögerung |

Fehlende Treffer sind der Normalfall und kein Beweis. Bei Details ohne eigene Codespur (8, 17, 20, teils 10 und 11) zusätzlich die laufende Oberfläche ansehen.

## Bericht

Eine Tabelle mit allen 20 Zeilen, in der Reihenfolge der Nummern, kein Detail weglassen.

| Nr | Detail | Status | Beleg | Wirkung | Aufwand |
|---|---|---|---|---|---|

- **Status:** `vorhanden`, `fehlt` oder `nicht relevant`. Eine halbe Umsetzung zählt als `fehlt`; die Lücke steht im Beleg ("Skeleton nur auf Startseite, Listen zeigen Spinner").
- **Beleg:** Datei und Zeile oder die beobachtete Stelle in der Oberfläche. Bei `nicht relevant` der Grund in einem Halbsatz ("kein Android-Target", "keine Zahlungen", "keine Hover-Menüs").
- **Wirkung:** hoch, mittel, niedrig. Gemeint ist der Effekt für die Nutzer dieses Produkts, nicht der Effekt in der Theorie.
- **Aufwand:** S (unter einer Stunde, eine Datei), M (mehrere Dateien oder ein Paket), L (Architekturänderung, etwa Cache-Schicht oder Server-Endpunkt).

Unter der Tabelle: eine Zeile je Annahme, die der Bericht trifft (etwa "Mobile Web zählt, App wird nur als PWA genutzt"), und eine Liste dessen, was nur mit laufender App prüfbar war und nicht geprüft wurde.

## Priorisierung

Reihenfolge der Umsetzung, nach Schaden bei Fehlen, nicht nach Effekt auf dem Screenshot:

1. **Doppelbuchung und Datenverlust:** 19 Idempotency Keys, 5 Undo statt Bestätigung, 2 Optimistic Updates (nur mit Rollback).
2. **Eingabe und Navigation funktionieren überhaupt gut:** 15 One-time-Code, 13 Hit Slop, 14 Safe Areas, 12 Predictive Back (Android). Fehlen hier Details, scheitern echte Nutzer, nicht nur Perfektionisten.
3. **Gefühlte Geschwindigkeit:** 1 Skeletons, 6 Stale-while-revalidate, 7 Prefetch, 8 Platzhalter. Hohe Wirkung bei kleinem Risiko; 6 braucht Cache-Invalidierung und ist deshalb vorsichtig anzugehen.
4. **Orientierung und Tempo für Geübte:** 3 Command Menu, 4 Shortcut Hints, 9 View Transitions, 10 Swipe-Sheets, 11 unterbrechbare Animationen, 20 Safe Triangle.
5. **Politur:** 16 Tabular Numbers, 17 `text-wrap: balance`, 18 Continuous Corners. Je ein bis zwei Zeilen CSS, aber ohne Folgen für die Funktion; 16 und 17 wegen des Preis-Aufwand-Verhältnisses gern vorziehen.

Innerhalb einer Stufe zuerst die Details mit Aufwand S. Pro Detail ein eigener Commit, damit Rückbau einzeln möglich bleibt.

## Harte Regeln

- **Nichts ungefragt umbauen.** Ohne Auftrag zur Umsetzung endet der Skill beim Bericht.
- **Jede Bewegung respektiert `prefers-reduced-motion`.** Bei Flutter `MediaQuery.disableAnimationsOf(context)`. Das gilt für 1, 9, 10 und 11 ohne Ausnahme.
- **Keine Optimistic Updates ohne Rückweg.** Schlägt die Anfrage fehl, kehrt die Oberfläche in den alten Zustand zurück und der Nutzer erfährt es. Für Zahlungen und andere nicht umkehrbare Aktionen ist 2 ausgeschlossen, dort gilt nur 19.
- **Kein Undo ohne echte Verzögerung.** Ein Undo-Toast ist nur ehrlich, wenn die Löschung wirklich zurückgenommen werden kann: entweder wird sie bis zum Ablauf des Toasts zurückgehalten oder als Soft Delete umgesetzt.
- **Feature-Detection statt Browser-Annahme** bei `startViewTransition`, `corner-shape`, `text-wrap` und Speculation Rules. Fehlt die Unterstützung, bleibt das Produkt vollständig benutzbar, nur ohne den Effekt.
- **Nicht zu viel auf einmal.** Fünf gut verifizierte Details schlagen zwanzig halbe. Details, die nicht zum Produkt passen (Command Menu in einer Ein-Seiten-Landingpage), sind `nicht relevant`, kein Mangel.
- **Keine erfundenen Belege.** Ein Status `vorhanden` braucht eine Fundstelle oder eine Beobachtung. Ohne beides: `fehlt` oder in die Liste "nicht geprüft".

## Referenzen

- `references/details.md`: alle 20 Details mit Zweck, Erkennungskriterium, Umsetzung für Web und Flutter und Fallstricken
