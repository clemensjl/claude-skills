# Quellen

## Skills (Kürzel in `regeln-bedienung.md`)

| Kürzel | Quelle |
|---|---|
| UDA | `ux-details-audit`, Nummer = Detail 1 bis 20 |
| EMIL | `emil-design-eng` |
| APL | `apple-design`, Paragrafennummer |
| A11Y | `accessibility` und WCAG 2.2, Nummer = Erfolgskriterium |
| WIG | Vercel Web Interface Guidelines (über `web-design-guidelines`) |
| SU | `signup` |
| ON | `onboarding` |
| RA | `review-animations`, `improve-animations` |
| MD | `motion-design` |
| BU | `break-ui` und dessen `CATALOG.md` |
| MN | `mobile-native` |

## Reels (Instagram, gespeichert von Clemens; ausgewertet 31.10. und 15.11.2026)

Kurzcode = Instagram-Post `instagram.com/p/<code>/`. Reels sind Anlass, nicht Beleg: Wo eine Reel-Zahl ohne Quelle war, steht in der Regel eine Primärquelle daneben oder die Regel ist als Praxis markiert.

| ID | Code | Konto | Inhalt |
|---|---|---|---|
| R01 | De7CN1WIxnF | mhmdnabdev | Skeleton statt Spinner |
| R06 | DfZ_Kuugh8R | mobistack.co | Jeden Tap in 0,1 s beantworten, Doppelbestellung |
| R09 | DfXhLLvlMxR | designmotionhq | 5 Signup-Fehler: Label, Blur-Validierung, Submit springt, Autofill, inputmode |
| R10 | DfXKRDQRBS_ | charles.unemployed | Motion-Werte: Ease, 150 bis 250 ms, Stagger 30 ms, Scale 0,97/0,95, Exit 20 % kürzer, Handheld nicht tweenen |
| R11 | DfVHQ-4giKL | redcheck2026 | WCAG 2.2 Target Size 24 × 24 |
| R17 | Derh6MRlvot | brochbuilds | Hick's Law, eine Hauptaktion |
| R20 | DfQKaecIliX | hofmann_julian | Hit Slop |
| R22 | DYyzrdpIixM | synsation_ | 6 Formularregeln |
| R24 | DfP3G_1tMT- | thealexyorgov | Speed-Checkliste (Skeleton, WebP, Debounce, Fonts, Streaming) |
| R25 | Dfuxj8Ej4Hk | winviboolvorakul | Checkout vorhersehbar machen: was passiert nach dem Kauf |
| R26 | DfvX42tovIV | uxy.app | Dialog-Fixes: echte Frage, ein Satz, sprechende Buttons, 24 pt |
| R27 | DfjX8-XBGMY | ek_software | IKEA-Effekt, Konfigurator |
| R28 | De2WSZDohDe | hofmann_julian | HSL-Palette: Hintergrund 8 % (dunkel) bzw. 96 % (hell) Lightness, Text 94 % bzw. 8 %, nie reines Schwarz/Weiß |
| R29 | DfqThAwI_lW | uxy.app | Deutsch bis 2× länger, Buttons stapeln statt kürzen |
| R30 | DfsGj_Rh49_ | zen_ux | Squircle, Bounce am Listenende, Dunkelgrau, optische Mitte |
| R31 | DcjkR2PSkml | synsation_ | Sechs Button-Zustände |
| R32 | DfphRvFBx54 | charles.unemployed | UX-Gesetze: Doherty 400 ms, Fitts, Hick, Miller, Postel, Jakob |
| R34 | Dfvja0XCyIi | theglidestudio | Animationsdauer: Press, Reveal < 1 s, Szene ≈ 1 s |
| R35 | De7aochhik3 | murphmaxxing | 20 UI-Tipps (nur im Bild): Optimistic, Command-Menü, Undo-Toast, SWR, BlurHash, View Transitions, Predictive Back, Safe Triangle, Idempotency |
| R36 | Dctqa5ih5in | dantekakhadze | 19 Dinge, die einer "vibe-coded" Seite fehlen (nur im Bild): 404, CTA, Meta, OG, Favicon, robots, Sitemap, Alt, Sticky-CTA, Lade- und Fehlerzustände, Danke-Seite, Rechtliches, Analytics, echte Adresse |
| R37 | Db15Zn0hSmH | yatesvids | Pre-Launch-Liste Betriebs-Website |
| R38 | Dfrdu92t4WA | levilayernn | Gratisversand-Fortschrittsbalken |
| R39 | DfhabhTNW1- | harting.pascal | H1 und Überschriften-Hierarchie |
| R41 | DfSOWtfBSBa | buildwithnico | Bilder über 1 MB, Lazy Loading, Lighthouse |
| R42 | DdcbiG5AUjd | moneymindnews | Abo-Preis sinkt mit Treue (Idee ohne Daten) |

Ausgewertet, ohne neue Regel: Ddi5_OkoiDa (Tastatur, Alt-Text; deckt A2/A8, Zahlen Clickbait), DezZ8h7AnWZ (Werbung für Apple-HIG-Skills). 21 Grenzfälle (Tool-Listen, Inspirationsseiten) nicht aufgenommen.

## Primärquellen (Recherche 15.11.2026)

| Kürzel | Quelle |
|---|---|
| Baymard | baymard.com: Cart Abandonment Rate (10/2026), Checkout Flow UX, Payment UX, Current State of Checkout UX, Perceived Security |
| NNG | nngroup.com: Scrolling and Attention, Layer-Cake Scanning, Hamburger Menus, Homepage Design Principles, How Long Users Stay, 3-Click Rule, Auto-Forwarding, Show Price, Comparison Tables, Push Notifications, Onboarding Tutorials |
| BUT | Butterick's Practical Typography (Line Length, Typography in Ten Minutes, Summary of Key Rules) |
| WCAG | W3C WCAG 2.2 und Understanding-Dokumente |
| MAT1/MAT2/MAT3 | Material Design 1/2/3 (Notifications Pattern, Dark Theme, Color Roles, Type Scale, Window Size Classes) |
| web.dev | LCP, Optimize LCP, Fetch Priority, Viewport Units, Carousels |
| Stripe | docs.stripe.com: Idempotent Requests, Payment Intents, Decline Codes, 3-D Secure |
| Duolingo | blog.duolingo.com: Improving the Streak, How Streaks Keep Learners Committed |
| Recht AT | RIS: FAGG (§ 4, § 8, § 13a, § 19, § 20 idF BGBl. I 59/2026), KSchG § 6c, PrAG § 9/§ 9a, ZaDiG 2018 § 56, TKG 2021 § 174, UWG § 1a und Anhang (idF BGBl. I 58/2026), ECG § 5 |
| Recht EU | VRRL 2011/83/EU idF 2023/2673 und 2024/825, RL 98/6/EG Art. 6a, UCPD 2005/29/EG, DSA Art. 25, DSGVO Art. 4/7/20, EDPB Guidelines 03/2022, EuGH C-249/21, C-330/23, Kommissionsleitlinie 2021/C 526/02, CPC-Sweep 2022, DFA-Vorschlag COM(2026) 1100 |
| Hersteller | Recurly, Recharge, Churnkey/ChurnWard, ChartMogul, Airship: nur Größenordnung, keine Kausalität |

Die Rechtsnormen wurden am 15.11.2026 von einem unabhängigen Prüfer am RIS bzw. EUR-Lex gegengeprüft (u. a. Stichtag § 13a FAGG = Verträge ab 01.10.2026, § 6c KSchG für Zusatzzahlungen).
