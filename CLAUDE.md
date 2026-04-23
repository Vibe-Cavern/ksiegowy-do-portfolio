# CLAUDE.md

Ten plik jest automatycznie wczytywany do kontekstu Claude Code przy każdej sesji uruchamianej w tym katalogu. Trzymaj go krótki i konkretny — to nie dokumentacja, to instrukcja dla asystenta.

## Projekt

_Krótki opis (1–2 zdania): co to jest, po co powstaje, dla kogo._

## Stack

_Język(i), framework(i), baza danych, kluczowe biblioteki — uzupełnij, gdy zostaną wybrane._

## Uruchomienie

```bash
# install:
# run:
# test:
```

## Konwencje

- Język odpowiedzi: polski.
- Commity: zwięzłe, opisowe (np. "fix: ...", "feat: ...").
- Przed zmianami szerszymi niż jeden plik — zapytaj.

## Czego NIE robić

- Nie dodawać zależności bez zgody.
- Nie pushować na `main` bez PR. Wyjątek: jednorazowy bootstrap push do nowo utworzonego (pustego) zdalnego repo — żeby zainicjalizować jego historię. Wszystkie kolejne zmiany przez PR.
- Nie zapisywać sekretów w repo — używać `.env` (ignorowany).

## Struktura

_Uzupełnij, gdy pojawi się kod (np. `src/`, `tests/`, `docs/`)._
