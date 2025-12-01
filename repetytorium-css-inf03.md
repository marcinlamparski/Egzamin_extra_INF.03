# 📘 Repetytorium CSS – Egzamin Zawodowy INF.03
**Cel:** Szybka powtórka zagadnień CSS, które najczęściej występują w pytaniach testowych.

## 1. Sposoby Dodawania Stylów do HTML
Egzamin często sprawdza, gdzie i jak prawidłowo umieścić CSS.

*   **Styl lokalny (inline):**
    *   Atrybuty `style` bezpośrednio w znaczniku HTML
    *   `<p style="color: red; font-size: 16px;">Tekst</p>`
    *   **Najniższy priorytet** (ale najwyższa specyficzność – przebija wszystko inne)

*   **Wewnętrzny arkusz stylów:**
    *   Umieszczony między `<style>` i `</style>` w sekcji `<head>`
    *   ```html
        <head>
            <style>
                body { background-color: bisque; }
                p { color: red; }
            </style>
        </head>
        ```

*   **Zewnętrzny arkusz stylów:**
    *   Osobny plik `.css` dołączany do HTML
    *   `<link rel="stylesheet" type="text/css" href="arkusz.css">`
    *   **Rekomendowana metoda** (łatwo zarządzać stylem dla wielu stron)

*   **Import stylów:**
    *   `@import url("inne_style.css");` wewnątrz `<style>` lub w pliku CSS

> **Typowe pytanie:** "Jaki ma priorytet styl lokalny vs. wewnętrzny?"
> **Odp:** Styl lokalny (inline) ma najwyższy priorytet i przebija wewnętrzny i zewnętrzny.

## 2. Kaskadowość i Specyficzność (WAŻNE!)
Kaskadowość to jedno z najczęściej pytanych zagadnień.

**Kolejność ważności stylów (od najniższej do najwyższej):**
1. Domyślne style przeglądarki
2. Zewnętrzny arkusz stylów
3. Wewnętrzny arkusz stylów (`<style>`)
4. Styl lokalny (atrybut `style=`)

**Jeśli dwa style mają ten sam priorytet, wygrywa ten wymieniony OSTATNI w pliku.**

*   `p { color: red; }` a następnie `p { color: blue; }` → **niebieski wygrywający**

> **Typowe pytanie:** "Dokładna kolejność ważności stylów w HTML"
> **Odp:** Zapamiętaj mnemotechnikę: **DWWS** (Domyślne, Zewnętrzny, Wewnętrzny, Style lokalne)

## 3. Selektory CSS
Egzamin często daje fragment CSS i pyta, które elementy będą stylizowane.

| Selektor | Przykład | Co stylizuje |
|:---------|:---------|:------------|
| **Typ (element)** | `p { }` | Wszystkie `<p>` |
| **Klasa** | `.nazwa { }` | Elementy z `class="nazwa"` |
| **Identyfikator** | `#id { }` | Element z `id="id"` |
| **Uniwersalny** | `* { }` | Wszystkie elementy |
| **Potomek** | `div p { }` | Wszystkie `<p>` wewnątrz `<div>` |
| **Dziecko** | `div > p { }` | Tylko bezpośrednie `<p>` w `<div>` |
| **Siebie** | `p + h1 { }` | `<h1>` bezpośrednio po `<p>` |
| **Atrybut** | `input[type="text"] { }` | Elementy z danym atrybutem |
| **Pseudoklasa** | `a:hover { }` | Efekt po najechaniu myszką |
| **Pseudoelement** | `p::first-line { }` | Pierwszy wiersz paragrafu |

*   **Pseudoklasy (najczęstsze):**
    *   `:hover` – po najechaniu myszką
    *   `:active` – podczas klikania
    *   `:visited` – dla odwiedzonych linków
    *   `:focus` – gdy element ma fokus (np. zaznaczone pole)
    *   `:first-child`, `:last-child` – pierwszy/ostatni element

## 4. Właściwości Tekstu i Czcionek
Te pytania pojawiają się prawie na każdym egzaminie.

| Właściwość | Wartości | Opis |
|:-----------|:---------|:-----|
| `color` | `red`, `#FF0000`, `rgb(255,0,0)` | Kolor tekstu |
| `font-family` | `Arial, sans-serif` | Czcionka (lista zapasowych) |
| `font-size` | `16px`, `1.5em`, `large` | Rozmiar czcionki |
| `font-weight` | `bold`, `700`, `normal` | Grubość (od 100–900) |
| `font-style` | `italic`, `normal` | Pochylenie |
| `text-align` | `left`, `center`, `right`, `justify` | Wyrównanie tekstu |
| `text-decoration` | `underline`, `overline`, `line-through`, `none` | Linie na tekście |
| `line-height` | `1.5`, `20px` | Wysokość linii |
| `text-transform` | `uppercase`, `lowercase`, `capitalize` | Transformacja liter |
| `letter-spacing` | `2px` | Odstęp między literami |
| `word-spacing` | `5px` | Odstęp między wyrazami |

> **Typowe pytanie:** "Jak zapisać tekst wielkimi literami za pomocą CSS?"
> **Odp:** `text-transform: uppercase;`

## 5. Box Model (Model Pudełka) – KLUCZOWY
To najczęściej pojawiane zagadnienie na egzaminie. Każdy element HTML to "pudełko" z czterema warstwami:

```
┌─────────────────────────────┐
│         MARGIN              │ (zewnętrzny margines)
│  ┌───────────────────────┐  │
│  │ BORDER (obramowanie)  │  │
│  │ ┌─────────────────┐   │  │
│  │ │ PADDING (wypełn)│   │  │
│  │ │ ┌────────────┐  │   │  │
│  │ │ │  CONTENT   │  │   │  │
│  │ │ └────────────┘  │   │  │
│  │ └─────────────────┘   │  │
│  └───────────────────────┘  │
└─────────────────────────────┘
```

*   **Margin (margines zewnętrzny):**
    *   `margin: 10px;` – wszystkie strony
    *   `margin: 10px 20px;` – góra/dół 10px, prawo/lewo 20px
    *   `margin: 10px 20px 15px 25px;` – góra, prawo, dół, lewo (GPDL)
    *   `margin-top`, `margin-right`, `margin-bottom`, `margin-left` – indywidualnie
    *   **Może być ujemny** (`margin: -5px`)

*   **Border (obramowanie):**
    *   `border: 2px solid red;` – (grubość, styl, kolor)
    *   Styl: `solid`, `dashed`, `dotted`, `double`, `groove`, `ridge`, `inset`, `outset`
    *   `border-radius: 5px;` – zaokrąglone rogi
    *   Indywidualnie: `border-top`, `border-right`, `border-bottom`, `border-left`

*   **Padding (wypełnienie wewnętrzne):**
    *   Działa jak margin, ale **wewnątrz** elementu
    *   `padding: 10px;` – wszystkie strony
    *   `padding: 10px 20px;` – góra/dół, prawo/lewo
    *   Atrybuty: `padding-top`, `padding-right`, `padding-bottom`, `padding-left`
    *   **Nie może być ujemny**

*   **Content (zawartość):**
    *   Sam tekst, obrazy lub inne elementy

*   **Width i Height:**
    *   `width: 300px;` – szerokość
    *   `height: 200px;` – wysokość
    *   `box-sizing: border-box;` – szer./wysok. uwzględnia border i padding (bardzo użyteczne!)

## 6. Kolor i Tło
Pytania o kolory i tło pojawiają się regularnie.

| Właściwość | Wartości | Opis |
|:-----------|:---------|:-----|
| `background-color` | `red`, `#FF0000`, `rgb()` | Kolor tła |
| `background-image` | `url("obraz.jpg")` | Obrazek jako tło |
| `background-repeat` | `repeat`, `no-repeat`, `repeat-x`, `repeat-y` | Powtarzanie obrazu |
| `background-position` | `top`, `bottom`, `left`, `right`, `center` | Pozycja obrazu |
| `background-size` | `100px`, `50%`, `cover`, `contain` | Rozmiar obrazu |
| `background-attachment` | `scroll`, `fixed` | Czy tło porusza się ze stroną |

*   **Skrót `background`:**
    *   `background: red url("bg.jpg") no-repeat fixed center;`

## 7. Display (Wyświetlanie Elementów)
Jedno z kluczowych zagadnień dla struktury strony.

| Wartość | Opis | Przykład |
|:--------|:-----|:---------|
| `block` | Element zajmuje całą szerokość, z nową linią | `<div>`, `<p>`, `<h1>` |
| `inline` | Element zajmuje tylko tyle miejsca, co potrzebuje | `<span>`, `<a>`, `<strong>` |
| `inline-block` | Połączenie: inline, ale może mieć width/height | `<img>`, `<button>` |
| `none` | Element się nie wyświetla (ale zajmuje miejsce) | Ukrywanie elementów |
| `flex` | Elastyczne rozmieszczenie (bardzo nowoczesne) | Responsywne layouty |
| `grid` | Dwuwymiarowa siatka | Zaawansowane layouty |
| `list-item` | Wyświetlenie jako element listy | Konwertowanie `<span>` na listę |

> **Typowe pytanie:** "Jaka jest domyślna wartość `display` dla `<span>`?"
> **Odp:** `inline`

## 8. Position (Pozycjonowanie)
Egzamin czasem pyta o pozycjonowanie elementów.

| Wartość | Opis |
|:--------|:-----|
| `static` | **Domyślna** – element w normalnym przepływie |
| `relative` | Pozycja względem swojej normalnej pozycji (`top`, `left`, `right`, `bottom`) |
| `absolute` | Pozycja względem najbliższego pozycjonowanego rodzica |
| `fixed` | Pozycja względem okna przeglądarki (zostaje na miejscu przy scrollowaniu) |
| `sticky` | Lepka pozycja (zmienia się z `relative` na `fixed` przy scrollowaniu) |

*   Atrybuty: `top`, `right`, `bottom`, `left`, `z-index` (kolejność warstw)

## 9. Float i Clear
Starszy system rozmieszczania (teraz zastępowany flexbox/grid).

*   `float: left;` – element pływa w lewo, tekst opływa go z prawej
*   `float: right;` – element pływa w prawo
*   `clear: left;` – element nie będzie pływać w lewo
*   `clear: both;` – element nie będzie pływać nigdzie

## 10. Stylizacja Tabel i List
Egzamin testuje stylizowanie tabel i list, co jest ważne dla UX.

*   **Tabele:**
    *   `border-collapse: collapse;` – złącza obramowania sąsiadujących komórek
    *   `border-spacing: 10px;` – odstęp między komórkami
    *   `text-align: center;` – wyrównaj tekst w `<td>` i `<th>`

*   **Listy:**
    *   `list-style-type: none;` – ukryj punkty
    *   `list-style-image: url("icon.png");` – własna ikonka zamiast punktu
    *   `list-style-position: inside;` – pozycja punktu wewnątrz/na zewnątrz

## 11. Responsywność – Media Queries
Coraz częściej pojawia się na egzaminach.

```css
@media (max-width: 768px) {
    body { font-size: 14px; }
    div { width: 100%; }
}

@media (max-width: 480px) {
    h1 { font-size: 18px; }
}
```

*   `@media` – reguła medioum
*   `(max-width: 768px)` – jeśli ekran jest węższy niż 768px
*   `(min-width: 768px)` – jeśli ekran jest szerszy niż 768px
*   `(orientation: landscape)` – jeśli orientacja jest pozioma

## 12. Efekty i Transformacje
Nowoczesne CSS, które czasem pojawia się na egzaminie.

| Właściwość | Opis |
|:-----------|:-----|
| `opacity` | Przezroczystość (0–1, gdzie 1 to w pełni widoczne) |
| `transform` | Rotacja, skalowanie, przesunięcie: `rotate(45deg)`, `scale(1.5)`, `translate(10px, 20px)` |
| `transition` | Płynna animacja zmian: `transition: all 0.3s ease;` |
| `box-shadow` | Cień: `box-shadow: 5px 5px 10px rgba(0,0,0,0.5);` |
| `text-shadow` | Cień tekstu: `text-shadow: 2px 2px 4px gray;` |

---

### 🔥 Szybki test wiedzy (Sprawdź się!)

1.  **Pytanie:** Co to jest `box-sizing: border-box;`?
    *   **Odp:** Zmienia sposób obliczania szerokości – uwzględnia padding i border w danej szerokości (bardzo przydatne do responsywności)

2.  **Pytanie:** Jaki jest priorytet stylów: styl lokalny vs. wewnętrzny vs. zewnętrzny?
    *   **Odp:** Styl lokalny > wewnętrzny > zewnętrzny

3.  **Pytanie:** Jak ukryć listę punktów w `<ul>`?
    *   **Odp:** `list-style-type: none;`

4.  **Pytanie:** Jaka jest domyślna wartość `display` dla `<div>`?
    *   **Odp:** `block`

5.  **Pytanie:** Co oznacza `margin: 0 auto;`?
    *   **Odp:** Zerowy margines górny/dolny, automatyczny margines lewy/prawy (wyśrodkowuje element horyzontalnie)

6.  **Pytanie:** Jak zdefiniować tabelę ze złączonymi granicami?
    *   **Odp:** `border-collapse: collapse;`

7.  **Pytanie:** Jakie są cztery warstwy Box Model (od wewnątrz na zewnątrz)?
    *   **Odp:** Content → Padding → Border → Margin

### Jak korzystać z bazy pytań?
Rozwiązując testy na zawodowe.edu.pl:
1.  **Szukaj fragmentów CSS** – zwróć uwagę na selektory i właściwości
2.  **Ćwicz rozpoznawanie** – nauczysz się szybko identyfikować, który styl wpłynie na konkretny element
3.  **Testuj w praktyce** – twórz małe pliki HTML + CSS i eksperymentuj
4.  **Zapamiętaj priorytety** – specyficzność i kaskadowość to fundament CSS
