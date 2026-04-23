# Spec: Landing page "Biuro Rachunkowe Kowalski & Partnerzy" — demo sprzedażowe

**Data**: 2026-04-23
**Status**: zatwierdzone przez użytkownika, gotowe do planu implementacji

## Kontekst

Użytkownik buduje **portfolio sprzedażowe** — stronę prezentowaną potencjalnym klientom (księgowym / biurom rachunkowym) jako przykład "co mogę zrobić dla Twojego biura". Ma to być **uniwersalne demo** (fikcyjna marka, łatwo podmieniana pod realnego klienta), nie strona dla konkretnej osoby.

Projekt zastępuje aktualny `index.html` (jednoekranowy smoke-test "Działa!" z poprzedniej sesji). Nowy plik jest docelowym landingiem — smoke-test spełnił swoją rolę i nie jest już potrzebny.

Kluczowe ograniczenia wynikające z `CLAUDE.md`:
- Zero nowych zależności bez dodatkowej zgody
- Polski język UI
- Commity opisowe
- `.env` dla sekretów (nie dotyczy tego projektu)

## Cele

1. **Wygląd**: wysokiej jakości, konserwatywny landing B2B dla branży księgowej — buduje zaufanie, sygnalizuje powagę i kompetencje.
2. **Konwersja**: jasne CTA ("Umów konsultację") powtórzone w kilku miejscach.
3. **Przenośność**: jeden samowystarczalny plik — łatwo podesłać mailem, łatwo zbrandować pod konkretnego klienta (3-5 podstawowych zmian tekstowych/kolorystycznych).
4. **Zero tarcia technicznego**: bez build-stepu, bez `npm install`, bez internetu po otwarciu.

## Architektura

### Podejście techniczne

**One-page landing w jednym pliku `index.html`** — wszystko inline (CSS w `<style>`, JS w `<script>`, ikony SVG inline).

Powody wyboru tego podejścia (ponad multi-page i stack z build-stepem):
- Zgodność z dotychczasową konwencją (statyczny HTML, zero deps)
- Standard branżowy dla landingów B2B — one-page z powtarzanym CTA konwertuje lepiej niż multi-page
- Jeden plik = łatwo podesłać, łatwo skopiować i podmienić pod konkretnego klienta

### Stan plików

| Plik | Akcja | Opis |
|---|---|---|
| `index.html` | **nadpisanie** | Aktualny smoke-test zostaje zastąpiony docelowym landingiem |
| `docs/superpowers/specs/2026-04-23-biuro-rachunkowe-landing-design.md` | nowy | Ten dokument |

Żadnych `package.json`, `node_modules`, `assets/`, zewnętrznych obrazków — wszystko w jednym HTML.

## Marka (placeholder)

| Element | Wartość |
|---|---|
| Nazwa firmy | Biuro Rachunkowe Kowalski & Partnerzy |
| Slogan | Księgowość bez stresu dla Twojej firmy |
| Logo | Tekstowy lockup: monogram "KP" w zaokrąglonym kwadracie (SVG inline) + nazwa obok |
| Rok założenia (demo) | 2009 |
| Lat doświadczenia (demo) | 15+ |
| Liczba klientów (demo) | 120+ |

Wszystkie te wartości to "łatwe do podmiany" stałe — podczas brandingu pod realnego klienta wymieniamy 5 stringów i kolor akcentu.

## Kierunek wizualny

### Paleta

| Rola | Light | Dark |
|---|---|---|
| Tło | `#F8F6F1` (kremowe) | `#0B1220` (navy-czarny) |
| Tło karty | `#FFFFFF` | `#111827` |
| Główny / tekst nagłówków | `#0F2847` (głęboki granat) | `#E5E7EB` |
| Tekst body | `#1F2937` | `#D1D5DB` |
| Tekst pomocniczy | `#4B5563` | `#9CA3AF` |
| Akcent (CTA, podkreślenia) | `#C9A961` (stonowany złoty) | `#D4B87A` (jaśniejszy złoty) |
| Obramowania / dividery | `#E5E7EB` | `#1F2937` |

Tryb ciemny przez `@media (prefers-color-scheme: dark)` — zero przełącznika w UI.

### Typografia

- **Body / UI**: `system-ui, -apple-system, "Segoe UI", Roboto, sans-serif`
- **Nagłówki**: `Georgia, "Times New Roman", serif`
- **Liczby (trust row, cennik)**: `font-variant-numeric: tabular-nums`
- Brak `@font-face` ani zewnętrznych fontów — wszystko to, co ma użytkownik w systemie.

### Mood

Zaufanie, precyzja, przestrzeń. Dużo white-space. Subtelne cienie (`0 10px 30px rgba(0,0,0,0.06)`). Zero gradientów krzyczących, zero "web 2.0 glossy" efektów.

## Struktura strony (sekcje w kolejności)

### 1. Nav (sticky top)

- Lewa strona: logo (SVG + nazwa)
- Prawa strona: linki do kotwic — `Usługi`, `O nas`, `Cennik`, `FAQ`, `Kontakt`
- Skrajnie prawo: przycisk CTA "Umów konsultację" (akcent złoty)
- Mobile (≤768px): hamburger menu → full-screen overlay z tymi samymi linkami
- Zachowanie: przy scrollu > 20px dodaje subtelny cień i bardziej nieprzezroczyste tło

### 2. Hero

- `<h1>`: "Księgowość bez stresu dla Twojej firmy"
- Podtytuł: "Pełna obsługa księgowa, kadrowo-płacowa i doradztwo podatkowe dla małych i średnich firm. Zero papierologii — wszystko online."
- 2 CTA obok siebie:
  - Primary (złoty): "Bezpłatna konsultacja" → scroll do `#kontakt`
  - Secondary (outline): "Zobacz pakiety" → scroll do `#cennik`
- Trust row poniżej: "**120+ firm nam zaufało** · **15 lat doświadczenia** · **Licencja MF nr 12345**"
- Prawa strona (desktop) / pod spodem (mobile): grafika SVG (abstrakcyjny wykres/dokumenty, inline SVG, bez zewnętrznych plików)

### 3. Usługi (`#uslugi`)

- Nagłówek sekcji: "Nasze usługi"
- Podtytuł: "Kompleksowa obsługa — wszystko w jednym miejscu"
- Grid 2×3 (desktop) / 1 kolumna (mobile), 6 kafli:
  1. **Pełna księgowość** — "Księgi handlowe dla spółek, pełna sprawozdawczość, rozliczenia z US i ZUS."
  2. **KPiR** — "Podatkowa księga przychodów i rozchodów dla JDG i spółek cywilnych."
  3. **Ryczałt** — "Prowadzenie ewidencji i rozliczenia dla ryczałtowców."
  4. **Kadry i płace** — "Umowy, listy płac, ZUS, PIT-11, deklaracje — obsługa kompleksowa."
  5. **Doradztwo podatkowe** — "Optymalizacja, interpretacje, wsparcie przy kontroli skarbowej."
  6. **JPK i e-faktury** — "Implementacja KSeF, pliki JPK_V7, pomoc techniczna."
- Każdy kafel: ikona SVG (24px, monokolor akcent), tytuł serif, opis sans.

### 4. O nas (`#o-nas`)

- 2 kolumny (desktop) / stack (mobile)
- Lewa: nagłówek "Doświadczenie, któremu zaufało 120 firm" + 2 akapity:
  - Akapit 1: "Od 2009 roku prowadzimy biuro, które łączy tradycyjny profesjonalizm z nowoczesnym podejściem do pracy. Obsługujemy firmy na każdym etapie — od jednoosobowych działalności po spółki z kilkudziesięcioma pracownikami."
  - Akapit 2: "Wierzymy, że dobra księgowość to nie tylko zgodność z przepisami, ale realne wsparcie dla przedsiębiorcy. Nasz zespół stale się szkoli, a każdy klient ma dedykowanego opiekuna, który zna specyfikę jego biznesu."
- Prawa: 3 "key facts" w karcie:
  - **Licencja MF nr 12345** (ikona certyfikatu)
  - **Członkostwo w SKwP** (ikona odznaki)
  - **15 lat na rynku** (ikona kalendarza)

### 5. Opinie klientów (`#opinie`)

- Nagłówek: "Co mówią nasi klienci"
- Grid 3-kolumnowy (desktop) / 1-kolumnowy (mobile), 3 karty:
  - **"Przeszliśmy do K&P rok temu i nie wyobrażam sobie powrotu."** — Anna Nowak, właścicielka "Studio Projekt"
  - **"Zawsze odpowiadają tego samego dnia. Polecam każdemu przedsiębiorcy."** — Marek Zieliński, "TechSoft Sp. z o.o."
  - **"Profesjonalizm i cierpliwość do moich pytań."** — Katarzyna Wójcik, "KW Design"
- Każda karta: 5 złotych gwiazdek (SVG) + cytat (serif, italic) + imię + firma (sans, mniejsze, szare)

### 6. Cennik (`#cennik`)

- Nagłówek: "Przejrzyste pakiety, bez ukrytych kosztów"
- Grid 3-kolumnowy (desktop) / stack (mobile), 3 karty:
  - **Samozatrudniony** — od **199 zł/mies** — KPiR lub ryczałt · 1 pracownik · podstawowe doradztwo · obsługa online
  - **Mała firma** ⭐ (wyróżniona kartą z akcentem) — od **499 zł/mies** — wszystkie formy · do 10 pracowników · rozszerzone doradztwo · dostęp do panelu klienta
  - **Spółka z o.o.** — od **899 zł/mies** — pełna księgowość · bez limitu pracowników · dedykowany opiekun · pełna obsługa kadrowa
- Pod spodem wyśrodkowane CTA: "Potrzebujesz indywidualnej wyceny? Napisz do nas →" (link do #kontakt)
- Każda karta: nazwa · cena · lista 4 bullet pointów (ikona checkmark) · przycisk "Wybierz pakiet" (link do #kontakt)

### 7. FAQ (`#faq`)

- Nagłówek: "Często zadawane pytania"
- Lista 6 pytań w accordion (pytanie + krótka odpowiedź, każda 1-3 zdania):
  1. **"Jak wygląda zmiana biura rachunkowego?"** — "Przejęcie zajmuje 2-3 dni robocze. Odbieramy dokumentację, pełnomocnictwa podpisujemy elektronicznie, a Ty zajmujesz się biznesem. Zmianę można zgłosić do US w dowolnym momencie roku."
  2. **"Obsługujecie zarówno JDG jak i spółki z o.o.?"** — "Tak, prowadzimy wszystkie formy: JDG na KPiR lub ryczałcie, spółki cywilne, jawne, komandytowe oraz z o.o. z pełną księgowością."
  3. **"Jak wygląda współpraca na co dzień?"** — "Dostajesz dedykowanego opiekuna, dostęp do panelu klienta i możliwość kontaktu telefonicznego lub mailowego w godzinach pracy. Raz w miesiącu dostajesz podsumowanie i deklaracje do akceptacji."
  4. **"Czy mogę przesyłać dokumenty elektronicznie?"** — "Jak najbardziej. Wspieramy skany, zdjęcia z telefonu, KSeF oraz bezpośrednie podpinanie kont bankowych. Papier przyjmujemy tylko wtedy, gdy Ty tego chcesz."
  5. **"Jak chronicie tajemnicę zawodową i dane klientów?"** — "Jesteśmy zobowiązani tajemnicą zawodową księgowych. Dane przechowujemy zgodnie z RODO, mamy polisę OC na 1 mln zł, a dostęp do dokumentów jest szyfrowany i logowany."
  6. **"Jakie są terminy na przekazanie dokumentów?"** — "Dokumenty za dany miesiąc najlepiej przekazać do 5. dnia kolejnego miesiąca. To daje nam czas na rzetelne zaksięgowanie i przygotowanie deklaracji przed terminami US i ZUS."
- Każde pytanie: `<details>` + `<summary>` (natywny accordion — działa bez JS, wzbogacony przez JS do "jedno otwarte na raz")

### 8. Kontakt (`#kontakt`)

- Nagłówek: "Porozmawiajmy"
- Podtytuł: "Bezpłatna konsultacja. Odpowiadamy w ciągu 24 godzin."
- 2 kolumny (desktop) / stack (mobile):
  - Lewa: formularz
    - Pola: Imię i nazwisko (required, text), Email (required, email), Telefon (optional, tel), Wiadomość (required, textarea)
    - Przycisk submit: "Wyślij wiadomość" (akcent złoty)
    - Po submit: JS przechwytuje, waliduje, pokazuje komunikat sukcesu "Dziękujemy! Odezwiemy się w 24h" — **nie wysyła realnie** (komentarz w kodzie to jasno oznacza)
  - Prawa: blok z danymi kontaktowymi
    - Adres: ul. Przykładowa 12 / 00-001 Warszawa (ikona pin)
    - Telefon: +48 22 123 45 67 (ikona słuchawki) — klikalny `tel:`
    - Email: kontakt@kowalski-partnerzy.pl (ikona koperty) — klikalny `mailto:`
    - Godziny: Pn–Pt 8:00–17:00 (ikona zegara)

### 9. Footer

- 3 kolumny (desktop) / stack (mobile):
  - Lewa: logo skrócone + 1 zdanie opisu + NIP/REGON placeholder
  - Środek: "Nawigacja" — linki do kotwic
  - Prawa: "Kontakt" — skrócone dane
- Cienka linia dzieląca
- Dół: `© 2026 Biuro Rachunkowe Kowalski & Partnerzy · Polityka prywatności · RODO` (linki-placeholdery, nie prowadzą nigdzie — `href="#"` z komentarzem)

## Interakcje

| Interakcja | Implementacja | Notatki |
|---|---|---|
| Smooth scroll do kotwic | CSS `scroll-behavior: smooth` na `<html>` | Zero JS |
| Sticky nav z cieniem | CSS `position: sticky` + JS toggle klasy `.scrolled` po `window.scrollY > 20` | Prosty listener |
| Mobile hamburger menu | JS toggle klasy `.nav-open` na `<body>`, full-screen overlay | ESC zamyka, klik w link też zamyka |
| FAQ accordion | `<details>`/`<summary>` + JS "jedno otwarte na raz" (wzbogacenie) | Działa bez JS (graceful degradation) |
| Walidacja formularza | Natywne HTML5 (`required`, `type="email"`) + JS custom komunikat sukcesu | Po submit: `preventDefault`, sprawdzenie `form.checkValidity()`, pokaż sukces |
| Fade-in sekcji | `IntersectionObserver` + CSS `opacity`/`translateY` transition | Respektuje `prefers-reduced-motion: reduce` — wtedy brak animacji |

## Responsywność

Mobile-first. Breakpointy:
- `sm`: 640px (większe telefony)
- `md`: 768px (tablety / moment gdy hamburger → nav)
- `lg`: 1024px (desktop — pełny grid 3-kol)

Kontener: `max-width: 1200px; margin: 0 auto; padding: 0 1.5rem;` (na mobile `1rem`).

## Dostępność

- Semantyczny HTML: `<header>`, `<nav>`, `<main>`, `<section aria-labelledby>`, `<footer>`
- Hierarchia nagłówków: jeden `<h1>` (hero), `<h2>` dla tytułów sekcji, `<h3>` dla kafli
- Widoczny focus ring (`:focus-visible`) w kolorze akcentu
- Ikony dekoracyjne: `aria-hidden="true"`; ikony informacyjne: `<title>` w SVG
- Kontrast WCAG AA dla wszystkich par tekst/tło (granat na kremowym: ~13:1; złoty na kremowym: uważnie — używany tylko w dużym tekście lub jako bg przycisków, nie do body)
- Formularz: `<label for>` dla każdego pola, komunikaty błędów `aria-live`
- `lang="pl"`, odpowiednie `lang` atrybuty jeśli trafią się zapożyczenia

## Szacowany rozmiar

- HTML struktura: ~300 linii
- Inline CSS: ~400-500 linii
- Inline JS: ~100-150 linii
- SVG ikony (6 usług + 4 kontakty + logo + accordion chevron + gwiazdki): ~50-80 linii
- **Łącznie**: ~850-1000 linii, ~30-40 KB nieskompresowane

## Weryfikacja

Po implementacji testujemy end-to-end:

### 1. Istnienie i wielkość pliku
```bash
ls -la "/Users/szymondunaj/Desktop/Claude projekty/index.html"
# Oczekiwane: plik istnieje, ~30-40 KB
```

### 2. Walidacja HTML
- Otwórz plik w przeglądarce
- Brak błędów w DevTools → Console
- HTML waliduje się (opcjonalnie: https://validator.w3.org/ — wklej kod)

### 3. Smoke test wizualny (desktop, Chrome/Safari)
```bash
open "/Users/szymondunaj/Desktop/Claude projekty/index.html"
```
Checklist:
- [ ] Nav na górze z logo i linkami
- [ ] Hero z nagłówkiem, 2 CTA, trust row
- [ ] Wszystkie 9 sekcji obecne w kolejności
- [ ] Cennik: 3 karty, "Mała firma" wyróżniona
- [ ] FAQ: kliknięcie pytania rozwija odpowiedź
- [ ] Formularz: próba submita pustego → walidacja; wypełnienie + submit → komunikat sukcesu
- [ ] Footer z linkami i copyright

### 4. Responsywność
- DevTools → toggle mobile view (iPhone 12 Pro, iPad)
- Hamburger pokazuje się <768px, znika ≥768px
- Wszystkie sekcje czytelne na 375px szerokości
- Żadnego horizontal scrolla

### 5. Interakcje
- Klik w link nawigacji → smooth scroll do sekcji
- Scroll > 20px → nav dostaje cień
- Hamburger → overlay otwiera się, ESC zamyka, klik w link zamyka
- FAQ: otwarcie drugiego pytania zamyka pierwsze
- Formularz: submit → `preventDefault` zadziałał, nie było page reload

### 6. Dostępność
- Nawigacja klawiaturą (Tab przez wszystkie interaktywne elementy, Enter aktywuje, ESC zamyka overlay)
- Focus ring widoczny
- DevTools → Lighthouse → Accessibility ≥95

### 7. Ciemny tryb
- DevTools → Rendering → Emulate `prefers-color-scheme: dark`
- Strona przełącza się na wariant dark, wszystko czytelne

## Co jest poza zakresem (świadomie)

- **Realne wysyłanie formularza** (wymaga backendu lub usługi typu Formspree)
- **Google Maps embed** (wymaga klucza API / iframe zewnętrzny)
- **Polityka prywatności / RODO** jako osobne podstrony (linki w footerze prowadzą do `#`)
- **Blog / aktualności**
- **Wielojęzyczność** (tylko polski)
- **Animacje wow** (Parallax, video background itp.)
- **Build step / bundler**
- **Analytics / piksele**

Te rzeczy można dołożyć później, jeśli demo się "sprzeda" i będzie prawdziwy klient.

## Ryzyka / rzeczy do pilnowania podczas implementacji

1. **Czytelność pojedynczego pliku 800-1000 linii** — używać sekcji oddzielonych komentarzami (`/* === HERO === */`), nazwy klas semantyczne (`.hero`, `.hero__title`), nie utility-first.
2. **Kontrast akcentowego złota** — `#C9A961` na kremowym ma niski kontrast dla body tekstu; używać go tylko na dużych elementach (CTA bg, podkreślenia) lub ciemnym tle.
3. **Dark mode konsystencja** — każdy kolor zdefiniowany w paletcie musi mieć odpowiednik w `@media (prefers-color-scheme: dark)`; testować WSZYSTKIE sekcje.
4. **SVG inline rozdyma plik** — upewnić się, że ikony są proste (stroke-based, ~10-20 linii każda), nie kopiować wielkich SVG z Figmy.
5. **Formularz bez backendu** — w kodzie zostawić komentarz `// DEMO: nie wysyła realnie. Do podpięcia: endpoint na Formspree / własny backend.` żeby było jasne dla czytającego kod.
