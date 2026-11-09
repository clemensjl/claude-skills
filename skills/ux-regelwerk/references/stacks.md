# Umsetzung und Suchmuster je Stack

Spalte "Richtig" ist das Muster beim BAUEN, Spalte "Befund-Suchmuster" der Grep-Ansatz beim PRÜFEN. Ein Treffer ist ein Hinweis, kein Beleg: die Stelle lesen und im laufenden Produkt bestätigen. API-Namen vor dem Einbau gegen die aktuelle Doku prüfen (context7), besonders bei React Native, Expo und Flutter, die zwischen Versionen umbenennen.

## Stack erkennen

| Merkmal | Stack |
|---|---|
| `package.json` mit `next` | Web, Next.js |
| `package.json` mit `react`, ohne `next` und ohne `react-native` | Web, React (Vite u. a.) |
| `package.json` mit `expo` oder `react-native` | React Native / Expo; mit `react-native-web` auch Web-Build, dann Web-Regeln (Fokus, Tastatur, URL) zusätzlich |
| `pubspec.yaml` mit `flutter` | Flutter; Plattformen unter `android/`, `ios/`, `web/`, `windows/` |
| nur `index.html` | Web, statisch |

---

## Web (React, Next.js, HTML/CSS)

| Regel | Richtig | Befund-Suchmuster |
|---|---|---|
| Z1 Tap-Feedback | `:active { transform: scale(0.97) }`, Tailwind `active:scale-[0.97]` | klickbare Elemente ohne `active:`; `onClick` auf `div`/`span` |
| Z2 Doppel-Submit | `if (pending) return; setPending(true)` vor `await`; `useFormStatus`/`useActionState`; Button `disabled={pending}` + Text "Wird gespeichert…" | `onSubmit`/`onClick` mit `await` ohne Pending-Guard |
| Z5 Undo | `toast("Gelöscht", { action: { label: "Rückgängig", … } })` (sonner) | `confirm(`, `window.confirm`, "Wirklich löschen" |
| Z8 Hover | `@media (hover: hover) and (pointer: fine)`; Tailwind v4 `hover:` ist bereits so kompiliert | `:hover` außerhalb der Media Query (Tailwind v3 ohne `hoverOnlyWhenSupported`); `group-hover:opacity-100` auf Aktionen |
| FO1 Label | `<label for>` sichtbar über dem Feld | `placeholder=` ohne zugehöriges `<label>`; `aria-label` statt sichtbarem Label bei Formularfeldern |
| FO2 Validierung | `onBlur` setzt `touched`, Fehler nur bei `touched`; nach erstem Fehler `onChange` revalidiert. react-hook-form: `mode: "onTouched"` | `mode: "onChange"`/`"all"` ab dem ersten Zeichen; Validierung nur in `onSubmit` |
| FO3 Fehler | `aria-invalid`, `aria-describedby`, Text mit Lösung | nur `border-red-*` ohne Text |
| FO4 Layout | Hilfezeile mit fester `min-height` unter jedem Feld | Fehler-`<p>` erscheint bedingt ohne reservierten Platz |
| FO5 Ziffern | `inputmode="numeric" autocomplete="postal-code"` bzw. `"one-time-code"`, `pattern="[0-9]*"` | `type="number"` |
| FO6 Dezimal | `inputmode="decimal"`, `parseFloat(v.replace(",", "."))` | `parseFloat(v)` / `Number(v)` direkt auf Eingabe |
| FO7 Autofill | `autocomplete`, `type="email"`, `autocapitalize="none"`, `spellcheck={false}`, `enterkeyhint` | Auth-Felder ohne `autocomplete` |
| FO8 Einfügen | — | `onPaste` + `preventDefault` |
| FO9 Autofill-Stil | `input:-webkit-autofill { box-shadow: 0 0 0 1000px var(--surface) inset; -webkit-text-fill-color: var(--text) }` | dunkles Formular ohne `autofill`-Regel |
| FO15 16 px | `font-size: 16px` an `input, textarea, select` | `text-sm`/`text-xs` an Inputs; `maximum-scale=1`, `user-scalable=no` |
| T1 Trefferfläche | `min-h-11 min-w-11` (44 px) oder `::after { inset: -10px }` | `h-6 w-6`/`size-4` an `<button>` mit nur Icon |
| T3/T4 Safe Area | `viewport-fit=cover`, `env(safe-area-inset-bottom)`, `100dvh` | `100vh`, `h-screen` bei fixer Leiste; `env(` ohne `viewport-fit=cover` |
| L1 Skeleton | `loading.tsx`, `<Suspense fallback={<Skeleton/>}>`, `aria-busy` | `isLoading && <Spinner/>` als Seiteninhalt |
| E1 Empty | Leerzweig vor `.map()` | `.map(` ohne `length === 0`-Zweig |
| E4 Überlauf | `min-w-0`, `truncate`, `break-words`/`[overflow-wrap:anywhere]`, `shrink-0` | Flex-Zeile mit Text ohne `min-w-0` |
| E5 Zahlen | `Intl.NumberFormat("de-AT")`, `Intl.PluralRules` | `toFixed(` für Anzeige, `+ " Einträge"` |
| A1 Fokus | `focus-visible:ring-2` | `outline-none`/`outline: none` ohne `focus-visible` |
| A3 Name | `aria-label` an Icon-Buttons, `aria-hidden` am Icon | `<button>` mit nur `<svg>` |
| A5 Live | `role="status"`, `aria-live="polite"` | Toast-Container ohne Live-Region |
| M5/M7 Motion | `transition: transform 200ms var(--ease-out)`; `@media (prefers-reduced-motion: reduce)`; Motion `useReducedMotion()` | `transition: all`, `transition-all`, `ease-in`, `scale(0)`, keine `prefers-reduced-motion`-Regel |

---

## React Native / Expo

| Regel | Richtig | Befund-Suchmuster |
|---|---|---|
| Z1 Tap-Feedback | `Pressable` mit `style={({ pressed }) => [s.btn, pressed && { opacity: 0.85, transform: [{ scale: 0.97 }] }]}` oder `android_ripple` | `TouchableWithoutFeedback`; `Pressable` ohne `pressed`-Stil; `onPress` auf `View`/`Text` |
| Z2 Doppel-Submit | `useRef`-Flag (`if (busy.current) return; busy.current = true`), weil `useState` erst im nächsten Render greift; `disabled` + `accessibilityState={{ busy: true }}` | `onPress={async () => { await …` ohne Guard |
| Z3 Fehlerpfad | `try/catch` mit sichtbarer Meldung | `catch {}`; `.catch(() => {})`; Supabase `const { data } = await …` ohne `error`-Auswertung |
| Z5 Undo | eigener Toast mit "Rückgängig", Löschung per `setTimeout` verzögert oder Soft Delete | `Alert.alert(` vor umkehrbarem Löschen |
| FO1 Label | sichtbarer `<Text>` über `TextInput`, `accessibilityLabel`/`aria-label` am Input, `nativeID` + `accessibilityLabelledBy` (Android) | `TextInput` nur mit `placeholder` |
| FO5 Ziffern | `inputMode="numeric"` bzw. `keyboardType="number-pad"`, Wert als String | `keyboardType="numeric"` bei Codes (zeigt auf iOS Sonderzeichen), `Number(text)` beim Tippen |
| FO6 Dezimal | `inputMode="decimal"`/`keyboardType="decimal-pad"`, Komma tolerant parsen | `parseFloat(text)` ohne `replace(",", ".")` |
| FO7 Autofill | `autoComplete="email"`/`"current-password"`/`"new-password"`/`"one-time-code"`, iOS `textContentType`, `autoCapitalize="none"`, `autoCorrect={false}`, `returnKeyType="next"` + `onSubmitEditing={() => next.current?.focus()}` | Auth-Felder ohne `autoComplete`/`textContentType` |
| FO11 Zähler | `maxLength` + sichtbarer Zähler `{text.length}/{max}` | `maxLength` ohne Anzeige |
| FO13 Verlassen | `usePreventRemove` (React Navigation 7) bzw. `beforeRemove`-Listener | Formularscreens ohne Schutz |
| FO14 Tastatur | `KeyboardAvoidingView behavior={Platform.OS === "ios" ? "padding" : "height"}` oder `react-native-keyboard-controller`; `keyboardShouldPersistTaps="handled"` an ScrollViews mit Buttons | Formular in `ScrollView` ohne beides |
| T1 Trefferfläche | `hitSlop={10}` oder `minWidth/minHeight: 44` (iOS) / 48 (Android) | `Pressable` mit Icon `size={16..24}` ohne `hitSlop`/Padding |
| T3 Safe Area | `useSafeAreaInsets()` bzw. `SafeAreaView` aus `react-native-safe-area-context` | `SafeAreaView` aus `react-native` (nur iOS, veraltet); fixe Leisten ohne Insets |
| T10 Schriftgröße | `maxFontSizeMultiplier` gezielt | `allowFontScaling={false}` global; `Text.defaultProps` |
| L1 Skeleton | Platzhalter-Views in Inhaltsmaßen | `<ActivityIndicator` als einziger Ladezustand eines Screens |
| L6 Refresh | `refreshControl={<RefreshControl …/>}` an Listen | Serverlisten ohne Refresh |
| E1 Empty | `FlatList ListEmptyComponent={…}` | `FlatList` ohne `ListEmptyComponent`; `.map(` ohne Leerzweig |
| E4 Überlauf | `numberOfLines`, `flexShrink: 1` am Text, `flexShrink: 0` am Icon | Text in `flexDirection: "row"` ohne `flexShrink` |
| E6 Ziffern | `fontVariant: ["tabular-nums"]` | wechselnde Zahlen ohne `fontVariant` |
| A1 Fokus (Web-Build) | Fokusstil über `:focus-visible` im Web-CSS oder sichtbarer Fokusrahmen | `outlineStyle: "none"`, `outlineWidth: 0` |
| A3 Name/Rolle | `accessibilityRole="button"`/`role="button"`, `accessibilityLabel` | Icon-`Pressable` ohne Label |
| A5 Ansage | `AccessibilityInfo.announceForAccessibility(…)`, Android `accessibilityLiveRegion="polite"` | Toasts ohne Ansage |
| A6 Zustand | `accessibilityState={{ selected, disabled, checked, busy }}` | Tabs/Chips ohne `selected` |
| M7 Reduced Motion | Reanimated `useReducedMotion()` bzw. `.reduceMotion(ReduceMotion.System)`; `AccessibilityInfo.isReduceMotionEnabled()` | `withSpring`/`withTiming`/`entering=` ohne Reduced-Motion-Zweig |
| Haptik | `expo-haptics` sparsam (Erfolg, Fehler, Einrasten), gleichzeitig mit der visuellen Reaktion | Haptik bei jedem Tap |

Expo Web: Was als `Pressable` gebaut ist, wird ein `div` mit `role="button"`. Tastaturbedienung (Enter, Leertaste, Tab-Reihenfolge) und Fokusring im Web-Build gesondert prüfen.

---

## Flutter

| Regel | Richtig | Befund-Suchmuster |
|---|---|---|
| Z1 Tap-Feedback | `InkWell`/`FilledButton`/`IconButton` (unter `Material`) | `GestureDetector(onTap:` auf sichtbaren Buttons |
| Z2 Doppel-Submit | `bool _busy` vor dem `await` setzen, `onPressed: _busy ? null : _submit` | `onPressed: () async { await …` ohne Guard |
| Z5 Undo | `SnackBar(action: SnackBarAction(label: 'Rückgängig', …))` | `showDialog` vor umkehrbarem Löschen |
| FO1 Label | `InputDecoration(labelText:, hintText:)` | nur `hintText` |
| FO2 Validierung | Blur über `FocusNode`-Listener, danach `onChanged` | `AutovalidateMode.always`; `onUserInteraction` (validiert ab erstem Zeichen, W9) |
| FO5 Ziffern | `keyboardType: TextInputType.number`, `inputFormatters: [FilteringTextInputFormatter.digitsOnly]` | `int.parse` beim Tippen |
| FO6 Dezimal | `TextInputType.numberWithOptions(decimal: true)`, Komma ersetzen | `double.parse(text)` ohne Komma-Behandlung |
| FO7 Autofill | `autofillHints: [AutofillHints.email]`, `AutofillGroup`, `textInputAction: TextInputAction.next` | Auth-Felder ohne `autofillHints` |
| FO11 Zähler | `maxLength:` (Zähler kommt automatisch) | `LengthLimitingTextInputFormatter` ohne Anzeige |
| FO13 Verlassen | `PopScope(canPop: !dirty, …)` | `WillPopScope` (veraltet) |
| T1 Trefferfläche | `IconButton` (48 dp), `MaterialTapTargetSize.padded`, `kMinInteractiveDimension` | `materialTapTargetSize: shrinkWrap`, `VisualDensity.compact` auf Touch, `GestureDetector` um kleines Icon |
| T3 Safe Area | `SafeArea`, `MediaQuery.viewPaddingOf`, `viewInsetsOf` | fixe Leisten ohne `SafeArea` |
| T10 Schrift | Layout wächst mit `MediaQuery.textScalerOf` | `textScaler: TextScaler.noScaling`; `SizedBox(height:)` um Text |
| L1 Skeleton | `Skeletonizer(enabled: loading, child: …)` | `Center(child: CircularProgressIndicator())` als Seiteninhalt |
| L6 Refresh | `RefreshIndicator` | — |
| E1 Empty | Leerzweig vor `ListView.builder` | `ListView.builder` ohne `itemCount == 0`-Zweig |
| E4 Überlauf | `Expanded`/`Flexible` + `overflow: TextOverflow.ellipsis`, `maxLines` | `Row` mit `Text` ohne `Expanded` (gelb-schwarzer Overflow-Balken) |
| E6 Ziffern | `FontFeature.tabularFigures()` | — |
| A3 Semantik | `Semantics(label:, button: true)`, `tooltip:` an `IconButton` | `IconButton` ohne `tooltip`; `GestureDetector` ohne `Semantics` |
| A5 Ansage | `SemanticsService.announce` (Nachfolger je nach Version prüfen) | — |
| M7 Reduced Motion | `MediaQuery.disableAnimationsOf(context)` | `AnimationController` ohne Abfrage |
