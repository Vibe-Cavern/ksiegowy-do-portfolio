# Spec: [BRAND] — strona-portfolio premium studia stron www

**Data**: 2026-04-25
**Status**: zatwierdzone przez użytkownika, gotowe do planu implementacji
**Token brand-name**: `[BRAND]` — placeholder do swap'u po decyzji ekipy (finaliści: MADS HQ / ECHO MADS / HELLO MADS / MADS Studio)

## Kontekst

Czterech wspólników (struktura płaska, każdy prowadzi pełen proces akwizycja → sprzedaż → dostarczenie) buduje **studio premium stron www**. Pierwszą stroną w ich portfolio jest demo "Biuro Rachunkowe Kowalski & Partnerzy" (repo `Vibe-Cavern/ksiegowy-do-portfolio`, spec z 2026-04-23). Ten dokument opisuje **drugą stronę** — własną stronę firmową studia, która pełni rolę **portfolio i lead-magnetu post-cold-call**.

Strona [BRAND] to **odrębny projekt** od księgowego — własne repo (`Vibe-Cavern/[brand]`), inny stack (Astro vs single-HTML), inny target (potencjalni klienci studia, nie klienci końcowi). Ten spec NIE zmienia istniejącego księgowego projektu.

Kluczowe ograniczenia wynikające z [CLAUDE.md](CLAUDE.md):
- Polski język UI i języka odpowiedzi w pracy
- Commity opisowe (`feat:`, `fix:`, `chore:`)
- Bez bezpośredniego push'a na `main` — wszystko przez PR
- Sekrety w `.env` (`.gitignore`'owane)
- Bez nowych zależności bez zgody — Astro/Tailwind/GSAP są zaakceptowane w tym specu jako baza

## Cele

1. **Domknięcie po cold-callu**: klient rozmawiał z [BRAND] przez telefon → otwiera URL → w 2 sekundy widzi "to są poważni ludzie" → zostawia kontakt zwrotny.
2. **Dowód kompetencji**: sama strona [BRAND] musi wyglądać top, bo jest *meta-case-study* dla każdego potencjalnego klienta ("jeśli ich strona wygląda tak, to nasza też tak będzie").
3. **Galeria portfolio z podstawami SEO**: 4 case studies, każdy z osobnym URL-em, do dzielenia w mailu / cold-callu ("zobacz tę stronę: [brand].pl/portfolio/firma-ai").
4. **Ścieżka skalowalna**: gdy zespół zbuduje 10-20 case studies, strona musi obronić się architekturą (multi-page, nie monolit).

## Pozycjonowanie

**Studio premium stron www dla wysoko-płatnych profesjonalistów.** Target: notariusze, kancelarie, kliniki, doradcy fin., specjaliści techniczni, butikowe klinki medyczne. Cena referencyjna ~5k zł.

Wartość propozycji jednym zdaniem: *"Twoja strona = dowód, że jesteś profesjonalistą, któremu warto zaufać."*

Strona NIE sprzedaje od zera — to robi cold call. Strona **domyka i potwierdza**.

## Model sprzedaży (kontekst dla designu)

| Etap | Kanał | Cel strony |
|---|---|---|
| 1. Pozyskanie | Cold call | (strona nie uczestniczy) |
| 2. Pierwsza interakcja | "Wejdź na [brand].pl, zobacz nasze portfolio" | **Wow w 2 sekundy** — potwierdzenie kompetencji |
| 3. Weryfikacja | Klient googluje "[brand]" po telefonie | **SEO podstawy** — nasza strona pierwsza w wynikach |
| 4. Decyzja | Klient ogląda portfolio + pakiety | **Konkretne case studies + jasne ceny** |
| 5. Konwersja | Klient zostawia kontakt | **Krótki form** (4 pola), bezpośredni telefon |

## Architektura informacji

Strona główna (`/`) — single-scroll z 6 sekcjami MUST + 1 OPTIONAL.

```
01 Hero            → wow + tagline + CTA "Zobacz portfolio"
02 Portfolio       → 4 kafelki case studies (klik → /portfolio/<slug>)
03 Pakiety         → 3 karty cenowe (Wizytówka 2999 / Premium 4999 / Indywidualny)
04 Proces          → 3-4 kroki "jak pracujemy"
05 Zespół          → 4 osoby, równa rola
06 Kontakt         → krótki form + bezpośredni nr tel + email
07 FAQ (opcj.)     → odłożone do v2 po zebraniu pytań z cold-calli
```

### Podstrony (multi-page przewaga vs single-HTML księgowego)

```
/                          → strona główna (sekcje wyżej)
/portfolio/ksiegowy        → case study: Biuro Rachunkowe Kowalski & Partnerzy
/portfolio/platforma-ai    → case study: Platforma szkoleniowa AI
/portfolio/sklep-zabawki   → case study: Sklep z zabawkami
/portfolio/[brand]         → meta case study: nasza własna strona
/polityka-prywatnosci      → wymagane RODO
/regulamin                 → opcjonalne, jeśli sprzedaż przez stronę
```

Każdy case study ma osobny URL (krytyczne dla cold-call workflow: "zobacz tę konkretną pracę: [brand].pl/portfolio/platforma-ai").

### Layout case study (`/portfolio/<slug>`)

```
- Hero case study: nazwa klienta, branża, 1-zdaniowy problem
- Bloki "co zrobiliśmy": projekt, copy, technologie
- Galeria zrzutów (2-4 zrzuty desktop + mobile)
- Cytat klienta (gdy będzie) lub link do live
- CTA "Chcę podobną stronę" → wraca do /#kontakt
```

## Pakiety

| | Wizytówka | Premium ★ | Indywidualny |
|---|---|---|---|
| **Cena** | 2 999 PLN | **4 999 PLN** | Wycena |
| **Typ** | One-page (do 6 sekcji) | Multi-page indywidualny | Indywidualny + ekosystem |
| **Projekt** | Modular framework | Indywidualny graficzny | Pełny indywidualny |
| **Copy** | Twoje teksty + nasz redakt. | Copywriting pod branżę | Strategia + content |
| **SEO** | Podstawy techniczne | Podstawy + analytics | Pełna strategia + content |
| **Hosting** | 12 mc + domena | 12 mc + domena | 12 mc + domena |
| **Dostawa** | 7 dni | 14 dni | Indywidualnie |
| **Po starcie** | — | 30 dni poprawek | Stała opieka (abonament) |
| **Dodatki** | — | — | Sklep online, kampanie reklamowe, social media, dedykowany opiekun |
| **CTA** | "Wybieram Wizytówkę" | "Wybieram Premium" | "Porozmawiajmy" |
| **Dla kogo** | Rozpoczynający praktykę | 8 z 10 naszych klientów | Skalujące się marki |

**Logika pricingu** (decoy effect): Wizytówka jako kotwica dolna, Premium jako "obvious choice" (visual-highlight + "najczęściej wybierany"), Indywidualny jako kotwica górna i otwarcie na recurring revenue.

## Portfolio na start (4 case studies)

| # | Nazwa | Status | Branża | Slug |
|---|---|---|---|---|
| 1 | Biuro Rachunkowe Kowalski & Partnerzy | demo (real ready-to-rebrand) | usługi finansowe / księgowość | `/portfolio/ksiegowy` |
| 2 | Platforma szkoleniowa AI | real | edukacja / tech | `/portfolio/platforma-ai` |
| 3 | Sklep z zabawkami | real | e-commerce / dziecko | `/portfolio/sklep-zabawki` |
| 4 | [BRAND] sama strona | real (meta) | studio web | `/portfolio/nasza-strona` |

**Strategia roadmapy:** gdy ekipa zbuduje 1-2 strony premium dla typowych high-pay klientów (kancelaria, klinika, dentysta), podmieniamy 1-2 z istniejących na bardziej trafione branżowo.

## Kierunek wizualny

**Luminous Tech** — czerpiemy z estetyki Stripe / Vercel / Linear, ale **bez deweloperskich sygnałów** (terminal, monospace overload, code snippets), żeby trafić do nie-tech high-pay klienta.

### Paleta

| Rola | Hex | Użycie |
|---|---|---|
| Tło główne | `#0a0a0c` | Body, hero, sekcje |
| Tło karty | `#15181d` | Karty case study, pakietów, zespołu |
| Tło karty (gradient border) | `linear-gradient(180deg,#15181d,#0f1218)` | Karty wyróżnione |
| Akcent mint (glow) | `#7afcb1` | Highlights, gradienty, hover, CTA secondary |
| Akcent violet (glow) | `#9b87ff` | Drugi gradient, akcent karty Premium |
| Tekst primary | `#ffffff` | Nagłówki, key text |
| Tekst body | `#c8ccd4` | Akapity, opisy |
| Tekst muted | `#aab0bc` | Subtitles, helpers |
| Tekst label | `#7a8090` | Mikro-tekst, eyebrow |
| Border | `#2a2e36` | Karty, dzielniki |
| Error | `#fc7a8a` | Błędy w formie |

**Gradient-glow signature**: `linear-gradient(135deg,#7afcb1 0%,#9b87ff 100%)` — używany na badge'ach, gradient borders, gradient text w CTA.

### Typografia

- **Sans primary**: `Inter` (variable) — UI, body, headings. Załadowany z Google Fonts (`display=swap`).
- **Mono accent**: `JetBrains Mono` lub system mono — labele, eyebrows, "01·02·03" numbery sekcji. Sparingly.
- **Skala** (mobile-first):
  - h1 (hero): 48px desktop / 36px mobile, weight 700, letter-spacing -0.03em
  - h2 (sekcje): 36px / 28px, weight 700, letter-spacing -0.02em
  - h3 (karty): 20px, weight 600
  - body: 16px, line-height 1.6
  - small: 13px, color muted
  - label: 11px, uppercase, letter-spacing 0.2em

### Motion

- Hero: subtelny radial gradient pulsujący (8s loop), tekst fade-in z lekkim slide-up
- Scroll: sekcje fade-in przy wejściu w viewport (Intersection Observer + GSAP). Brak parallax (zabija performance i czuje się staro).
- Karty: subtle hover-lift (translateY(-4px), 0.2s ease)
- CTA: gradient-shift on hover

**Cel motion'a**: pomaga skupiać wzrok i sygnalizuje "to nowoczesne". NIE: animacja per-scroll efekciarska, NIE: confetti, NIE: cursor effects.

### Wzorce komponentów

- **Card** (portfolio, pakiet, team-member): border 1px `#2a2e36`, radius 12px, padding 24px, hover lift
- **Card.featured** (Premium pakiet, główne case study): gradient-border (mint→violet), translateY(-8px), badge "★ NAJCZĘŚCIEJ"
- **Button.primary**: białe tło, czarny tekst, radius 10px, padding 12px 20px
- **Button.secondary**: transparent + border `#2a2e36`, white text
- **Eyebrow**: 11px uppercase mono, color `#9b87ff`, letter-spacing 0.2em
- **Form input**: dark bg `#15181d`, border `#2a2e36`, focus glow mint

## Stack technologiczny

### Framework: **Astro 4.x**

Powody (vs single-HTML jak księgowy):
- Multi-page case studies = osobne URL-e, krytyczne dla cold-call workflow
- Komponenty (Astro components) = czysta struktura, łatwe dorabianie kolejnych case studies
- Output static HTML = łatwy hosting, brak runtime'u
- SEO out-of-box: sitemap, OG tags per strona, meta tags
- Polski community Astro silny

### Dependencje

| Paczka | Wersja | Cel |
|---|---|---|
| `astro` | 4.x | Framework |
| `@astrojs/tailwind` | latest | Integracja Tailwind |
| `@astrojs/sitemap` | latest | Auto-sitemap dla SEO |
| `tailwindcss` | 3.x | CSS utility |
| `gsap` | 3.x | Motion (ScrollTrigger dla fade-in) |
| `@fontsource-variable/inter` | latest | Inter local (offline-friendly) |

Brak: React, Vue, Svelte. Astro components wystarczą — zero JS na stronach, motion dodajemy targetowo.

### Repo i deploy

- **Repo**: `Vibe-Cavern/[brand]` (nowe public repo, oddzielne od `ksiegowy-do-portfolio`)
- **Hosting**: **Netlify** (free tier, custom domain, auto-deploy z GitHuba)
- **Dev URL** (przed zakupem domeny): `[brand].netlify.app`
- **Branching**: `main` = produkcja (auto-deploy), feature branches przez PR (zgodnie z CLAUDE.md)

### Struktura projektu

```
[brand]/
├── README.md
├── astro.config.mjs
├── package.json
├── tailwind.config.cjs
├── tsconfig.json
├── public/
│   ├── og/             → static OG images per strona
│   └── favicon/
├── src/
│   ├── components/
│   │   ├── Hero.astro
│   │   ├── PortfolioGrid.astro
│   │   ├── PortfolioCard.astro
│   │   ├── PakietyGrid.astro
│   │   ├── PakietCard.astro
│   │   ├── ProcesSteps.astro
│   │   ├── ZespolGrid.astro
│   │   ├── ZespolCard.astro
│   │   ├── KontaktForm.astro
│   │   ├── Footer.astro
│   │   ├── Nav.astro
│   │   └── ui/
│   │       ├── Button.astro
│   │       ├── Eyebrow.astro
│   │       ├── GradientBorder.astro
│   │       └── BrandMark.astro     → wordmark + glow SVG, single source of brand visual
│   ├── layouts/
│   │   ├── BaseLayout.astro      → meta, OG, fonts, dark bg
│   │   └── CaseStudyLayout.astro → wrapper case study
│   ├── pages/
│   │   ├── index.astro           → strona główna
│   │   ├── portfolio/
│   │   │   ├── ksiegowy.astro
│   │   │   ├── platforma-ai.astro
│   │   │   ├── sklep-zabawki.astro
│   │   │   └── nasza-strona.astro    → meta case study; URL /portfolio/nasza-strona (slug niezależny od finalnej nazwy)
│   │   ├── polityka-prywatnosci.astro
│   │   └── 404.astro
│   ├── content/
│   │   └── case-studies/         → MD per case study (frontmatter + opis)
│   ├── styles/
│   │   └── globals.css           → Tailwind base + custom utility
│   └── data/
│       ├── brand.json            → wszystkie tokeny brand'u (nazwa, logo, kolory)
│       ├── pakiety.json          → 3 pakiety jako data
│       └── zespol.json           → 4 osoby
└── .github/
    └── workflows/                → opcjonalne: PR checks (build, lint)
```

### `brand.json` (kluczowy dla [BRAND] swap'u)

```json
{
  "name": "[BRAND]",
  "tagline": "Strony premium dla profesjonalistów.",
  "domain": "[brand].pl",
  "email": "kontakt@[brand].pl",
  "phone": "+48 XXX XXX XXX",
  "social": {
    "linkedin": "...",
    "instagram": "..."
  },
  "founded": 2026,
  "team_size": 4
}
```

Po decyzji ekipy o nazwie: jeden find-replace `[BRAND]` → finalna nazwa we wszystkich plikach + edycja `brand.json`.

## Brand — stan placeholder

| Element | Status | Plan |
|---|---|---|
| Nazwa | PENDING | Decyzja ekipy. Finaliści: MADS HQ / ECHO MADS / HELLO MADS / MADS Studio. Token `[BRAND]` w spec/kodzie. |
| Logo | PENDING | Po nazwie. Plan: prosty wordmark z subtelnym gradient-glow (mint→violet). SVG inline w `Nav.astro` i `Footer.astro`. |
| Domena | PENDING | Zakup po nazwie + UPRP/EUIPO check. Wymóg: .pl + .com obie wolne. Dla finalistów: madshq, echomads, hellomads — wszystkie spełniają. |
| Trademark | PENDING | UPRP (Polska) + EUIPO (UE) — sprawdzenie klas nicejskich 35 (reklama) i 42 (web design). Zwykle 5 min na uprp.gov.pl + euipo.europa.eu. |
| Paleta | LOCKED | mint `#7afcb1` + violet `#9b87ff` na tle `#0a0a0c`. Niezależne od nazwy. |
| Email biz. | PENDING | `kontakt@[brand].pl` po zakupie domeny. Tymczasowo formularz → email bramki (Formspree/Netlify Forms free). |

## Czego ŚWIADOMIE NIE robimy w v1

- **Bloga** — odłożony do v2 po pierwszych 5-10 klientach (treści o procesie, case studies w blog-formie)
- **Sekcji "wartości firmy" / "manifest"** — premium agencje pokazują, nie deklarują
- **Testimoniali** — brak realnych = puste (i fake testimoniale niszczą zaufanie szybciej niż ich brak)
- **Licznika klientów** — "1+ klient" boli; dodajemy gdy będzie 10+
- **Tabeli porównawczej z konkurencją** — premium nie atakuje, premium pokazuje
- **Multi-language** — PL only na start; EN dorabiamy gdy pojawi się 1. zagraniczny klient
- **Animacji per scroll** — minimal motion, performance > efekciarstwo
- **Cookie banner skomplikowany** — Netlify nie zbiera cookies, wystarczy proste info (poliytka prywatności)
- **Newsletter signup** — nie mamy co wysyłać, dodamy z blogiem
- **Live chat** — cold-call traffic = wysoki intent, kontakt form wystarczy

## Akceptacja i kryteria sukcesu

### Visual / UX
- [ ] Hero ładuje się <1.5s (Lighthouse Performance ≥90)
- [ ] Strona wygląda top na desktop ≥1440px AND mobile 375px (responsive)
- [ ] Dark theme wymuszony (brak light mode w v1)
- [ ] Każda sekcja ma jasny eyebrow + headline + content
- [ ] Każde case study ma osobny URL i fade-in motion na scroll

### Funkcjonalne
- [ ] Form kontaktowy wysyła do email (Netlify Forms)
- [ ] CTA "Wybieram Premium" prefilluje pakiet w formie (jak w księgowym)
- [ ] Linki bezpośredniego telefonu (`tel:`) i mail (`mailto:`) działają
- [ ] Sitemap.xml generowane automatycznie
- [ ] OG image per case study (custom JPG/PNG dla pięknego share'a w mailu)

### SEO/meta
- [ ] Title + description per strona
- [ ] OG tags (title, description, image) per strona
- [ ] Schema.org `Organization` w `<head>` z `name`, `url`, `logo`, `email`, `telephone`, `address` (po decyzji o adresie biura)
- [ ] Schema.org `Service` w sekcji Pakiety (3× — po jednej na pakiet, z `offers.price` i `offers.priceCurrency: "PLN"`)
- [ ] Schema.org `CreativeWork` per case study
- [ ] robots.txt + sitemap.xml (auto z `@astrojs/sitemap`)

### Brand-swap readiness
- [ ] `[BRAND]` token jako jedyne miejsce nazwy (find-replace ready)
- [ ] `brand.json` jako single source of truth dla danych marki
- [ ] Logo SVG jako component (`<BrandMark.astro>`) — łatwa podmiana

## Ryzyka i mitygacje

| Ryzyko | Prawdop. | Wpływ | Mitygacja |
|---|---|---|---|
| Ekipa zmieni nazwę po ukończeniu kodu | Średnie | Niski | `[BRAND]` token + `brand.json` = 5-min swap |
| Trademark conflict (np. Mads Nørgaard fashion) | Niskie | Wysoki | UPRP/EUIPO check przed zakupem domeny; klasy nicejskie 25 (fashion) ≠ 42 (web) |
| Performance score <90 z powodu motion'a | Niskie | Średni | Motion z `prefers-reduced-motion` fallbackiem; brak heavy animation libs |
| Cold-call traffic googluje "MADS" → trafia na Mads Mikkelsen | Średnie | Niski | Akceptujemy — nasz target nie pomyli aktora ze studiem web |
| Astro build break przy update'cie | Niskie | Niski | Pinning major versions w package.json, lockfile w repo |

## Następne kroki

1. **User review tego dokumentu** — czy wszystko trafia, czy coś poprawić
2. **Hand-off do `superpowers:writing-plans`** — generacja konkretnego planu implementacji w fazach (setup → komponenty → strony → motion → SEO → deploy)
3. **Implementacja w fazach** (zgodnie z planem)
4. **W międzyczasie**: ekipa decyduje o nazwie → swap `[BRAND]` token + zakup domeny + UPRP/EUIPO check
5. **Deploy v1** na `[brand].netlify.app`, potem custom domain po zakupie

---

**Powiązane dokumenty**:
- [`docs/superpowers/specs/2026-04-23-biuro-rachunkowe-landing-design.md`](2026-04-23-biuro-rachunkowe-landing-design.md) — spec strony księgowego (poprzedni projekt, niezależny)
- [`CLAUDE.md`](../../../CLAUDE.md) — konwencje projektu

**Wkład w portfolio**: ten dokument + repo `Vibe-Cavern/[brand]` (do utworzenia) = case study #4 w samym sobie ("zobacz, jak my pracujemy nad własną stroną").
