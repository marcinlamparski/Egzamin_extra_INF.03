# WCAG 2.1 — Standard dostępności stron internetowych
## Pod kątem egzaminu INF.03

---

## Czym jest WCAG?

**WCAG** (Web Content Accessibility Guidelines) to zestaw wytycznych opracowanych przez organizację **W3C** (World Wide Web Consortium), określających jak tworzyć strony internetowe dostępne dla wszystkich użytkowników — w tym osób z różnymi niepełnosprawnościami.

> 💡 Na egzaminie INF.03 (część pisemna) pojawia się pytanie:
> *"Zalecenia dotyczące ułatwień dostępności serwisów internetowych dla osób niepełnosprawnych są zawarte w..."*
> **Odpowiedź: wytycznych WCAG** (nie IEEE, nie RFC, nie rekomendacjach W3C jako osobnym dokumencie)

---

## Trzy poziomy zgodności

| Poziom | Nazwa | Opis |
|--------|-------|------|
| **A** | Minimalny | Absolutne minimum — spełnienie go usuwa najpoważniejsze bariery |
| **AA** | Zalecany ✅ | Optymalny kompromis — **wymagany prawnie w Polsce** dla podmiotów publicznych |
| **AAA** | Najwyższy | Bardzo rygorystyczny — trudny do pełnego wdrożenia na każdej stronie |

**Poziom AA = A + AA** — żeby osiągnąć AA, strona musi spełniać kryteria z obu poziomów.

W Polsce poziom AA jest obowiązkowy na mocy **Ustawy o dostępności cyfrowej z 2019 roku** (wdrożenie Dyrektywy UE 2016/2102). Dotyczy wszystkich instytucji publicznych — w tym szkół.

---

## Cztery zasady WCAG — skrót **POUR**

Każde kryterium WCAG należy do jednej z czterech zasad:

### 1. Postrzegalność (Perceivable)
Treść musi być dostępna dla zmysłów użytkownika — nie tylko dla wzroku.

**Przykłady wymagań:**
- Każdy obraz musi mieć atrybut `alt` z opisem tekstowym
- Filmy wideo muszą mieć napisy dla niesłyszących
- Treść nie może być przekazywana **wyłącznie** przez kolor (np. błąd oznaczony tylko czerwonym kolorem — bez ikony lub opisu tekstowego)
- Kontrast tekstu względem tła: minimum **4,5:1** dla normalnego tekstu (poziom AA)

### 2. Funkcjonalność (Operable)
Użytkownik musi móc obsługiwać stronę — nie tylko myszą.

**Przykłady wymagań:**
- Wszystkie funkcje strony muszą być dostępne z **klawiatury** (bez myszy)
- Użytkownik musi mieć wystarczająco dużo czasu na reakcję — nie mogą być stosowane limity czasowe bez możliwości ich wydłużenia
- Strona nie może zawierać treści **migających szybciej niż 3 razy na sekundę** (ryzyko ataku epilepsji)
- Nawigacja musi być przewidywalna i spójna

### 3. Zrozumiałość (Understandable)
Treść i obsługa muszą być zrozumiałe.

**Przykłady wymagań:**
- Strona musi mieć zadeklarowany język: `<html lang="pl">`
- Komunikaty błędów w formularzach muszą jasno opisywać co poszło nie tak
- Nawigacja musi być spójna na wszystkich podstronach
- Nie może dochodzić do automatycznych, nieoczekiwanych zmian kontekstu (np. automatyczne wysyłanie formularza po wyborze opcji)

### 4. Solidność (Robust)
Treść musi działać z różnymi technologiami — w tym technologiami asystującymi.

**Przykłady wymagań:**
- Kod HTML musi być **poprawny** i przechodzić walidację (validator.w3.org)
- Elementy interaktywne muszą mieć odpowiednie role ARIA jeśli nie wynikają z semantyki HTML
- Komunikaty o stanie (np. "zapisano", "błąd") muszą być dostępne dla czytników ekranu

---

## Najważniejsze wymagania AA — praktyczna ściągawka

| Wymaganie | Poziom | Jak spełnić w HTML/CSS? |
|-----------|--------|------------------------|
| Tekst alternatywny dla obrazów | A | `<img alt="opis">` |
| Napisy dla wideo, audiodeskrypcja | A | `<track kind="captions">` |
| Dostęp z klawiatury | A | Semantyczny HTML (button, a, input) |
| Brak migania >3 Hz | A | Unikaj animacji błyskających |
| Tytuł strony | A | `<title>` w każdym dokumencie |
| Język strony | A | `<html lang="pl">` |
| Kontrast tekstu 4,5:1 | **AA** | Ciemny tekst na jasnym tle |
| Kontrast dużego tekstu 3:1 | **AA** | Duży tekst (18px+ lub 14px bold) |
| Zmiana rozmiaru tekstu do 200% | **AA** | Bez utraty treści (RWD, em/rem) |
| Widoczny fokus klawiatury | **AA** | Nie usuwaj `outline: none` bez alternatywy |
| Spójna nawigacja | **AA** | Menu w tym samym miejscu na każdej stronie |
| Etykiety formularzy | **AA** | `<label for="id">` przy każdym polu |

---

## Na co zwrócić uwagę w HTML — konkretne błędy

### ❌ Naruszenia WCAG — typowe na egzaminie

```html
<!-- BŁĄD: brak alt -->
<img src="foto.jpg">

<!-- BŁĄD: brak lang -->
<html>

<!-- BŁĄD: brak title -->
<head><meta charset="UTF-8"></head>

<!-- BŁĄD: link bez treści -->
<a href="strona.html"><img src="ikona.png"></a>
<!-- (brak alt na obrazku w linku = link bez etykiety) -->

<!-- BŁĄD: informacja przekazana TYLKO kolorem -->
<p style="color: red;">Błąd w formularzu</p>
<!-- Brak ikony lub słowa "Błąd:" — niewidoczne dla niewidomych -->
```

### ✅ Poprawna wersja

```html
<!-- Poprawny obraz -->
<img src="foto.jpg" alt="Budynek Technikum nr 5 w Warszawie">

<!-- Poprawny dokument -->
<html lang="pl">

<!-- Poprawny tytuł -->
<title>Strona kontaktowa — Technikum nr 5</title>

<!-- Poprawny link z obrazkiem -->
<a href="strona.html">
    <img src="ikona.png" alt="Przejdź do strony głównej">
</a>

<!-- Poprawny komunikat błędu -->
<p>❌ Błąd: Pole e-mail jest wymagane.</p>
```

---

## Kontekst prawny (wersja skrócona)

- **W3C** opracowuje standard WCAG (opublikowany w 1999, aktualny 2.1 z 2018, 2.2 z 2023)
- **Ustawa z 4 kwietnia 2019 r.** o dostępności cyfrowej — nakłada obowiązek WCAG 2.1 AA na wszystkie podmioty publiczne w Polsce (szkoły, urzędy, uczelnie)
- **Dyrektywa UE 2016/2102** — europejska podstawa prawna
- Naruszenie może skutkować skargą do organu nadzorczego

---

## Typowe pytania z egzaminu INF.03

**P: Skrót WCAG oznacza:**
O: Web Content Accessibility Guidelines

**P: Zalecenia WCAG opracowała organizacja:**
O: W3C (World Wide Web Consortium)

**P: Który poziom WCAG jest obowiązkowy w Polsce dla instytucji publicznych?**
O: Poziom AA

**P: Która zasada WCAG wymaga by treść była dostępna dla zmysłów?**
O: Postrzegalność (Perceivable)

**P: Jakie są cztery zasady WCAG?**
O: Postrzegalność, Funkcjonalność, Zrozumiałość, Solidność (POUR)

**P: Jaki minimalny kontrast tekstu względem tła wymagany jest na poziomie AA?**
O: 4,5:1 dla normalnego tekstu, 3:1 dla dużego tekstu

---

## Przydatne narzędzia

| Narzędzie | Do czego? | Adres |
|-----------|-----------|-------|
| W3C Validator | Walidacja HTML | validator.w3.org |
| WAVE | Audyt dostępności strony | wave.webaim.org |
| Contrast Checker | Sprawdzanie kontrastu kolorów | webaim.org/resources/contrastchecker |
| Oficjalne WCAG 2.1 PL | Pełna treść standardu | w3.org/Translations/WCAG21-pl |

---

*Dokument przygotowany na potrzeby kursu HTML5+CSS | INF.03 Technikum Informatyczne*
