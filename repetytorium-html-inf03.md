# 📘 Repetytorium HTML – Egzamin Zawodowy INF.03
**Cel:** Szybka powtórka zagadnień, które najczęściej występują w pytaniach testowych.

## 1. Struktura Dokumentu i Sekcja `<head>`
Pytania z tego działu sprawdzają znajomość szkieletu strony oraz tego, co jest widoczne dla użytkownika, a co dla przeglądarki.

*   **Szkielet:** Każdy dokument musi zaczynać się od `<!DOCTYPE html>` (informuje przeglądarkę o wersji HTML5).
*   **Sekcja `<head>`:** 
    *   `<meta charset="UTF-8">` – kodowanie znaków (polskie ogonki)
    *   `<title>` – tytuł strony widoczny na pasku karty przeglądarki
    *   `<link rel="stylesheet" href="styl.css">` – dołączanie zewnętrznego arkusza stylów
    *   `<script src="skrypt.js"></script>` – dołączanie skryptu JS
    *   `<meta name="description" content="...">` – opis strony dla wyszukiwarek
    *   `<meta name="author" content="...">` – autor strony

> **Typowe pytanie:** "W której sekcji dokumentu HTML należy umieścić znacznik `<meta charset="...">`?"
> **Odp:** W sekcji `<head>`.

## 2. Formatowanie Tekstu i Listy
Egzamin często sprawdza znajomość rzadziej używanych znaczników formatowania oraz atrybutów list.

*   **Znaczniki fizyczne i logiczne:**
    *   `<b>` / `<strong>` – pogrubienie
    *   `<i>` / `<em>` – pochylenie
    *   `<sup>` – indeks górny
    *   `<sub>` – indeks dolny
    *   `<br>` – przełamanie linii
    *   `<hr>` – pozioma linia
*   **Listy (bardzo częste pytania!):**
    *   **Uporządkowana `<ol>`**
        *   Atrybut `type="1"`, `type="a"`, `type="A"`, `type="i"`, `type="I"`
        *   Atrybut `start="5"` – rozpoczyna numerowanie od 5
    *   **Nieuporządkowana `<ul>`**
        *   Atrybut `type="disc"`, `type="circle"`, `type="square"`
    *   **Definicji `<dl>`**
        *   `<dt>` – termin
        *   `<dd>` – opis definicji

## 3. Obrazy i Multimedia
Pytania dotyczą atrybutów znacznika `<img>` oraz ścieżek.

*   **Znacznik `<img>`:**
    *   `src="..."` – ścieżka do pliku
    *   `alt="..."` – tekst alternatywny
    *   `title="..."` – dymek z podpowiedzią
*   **Ścieżki:**
    *   `foto.jpg` – plik w tym samym folderze
    *   `grafika/foto.jpg` – plik w podfolderze
    *   `../foto.jpg` – plik w folderze nadrzędnym

## 4. Tabele (Kluczowe zagadnienie)
Jeden z najtrudniejszych elementów na teście teoretycznym. Musisz umieć rozpoznać kod scalający komórki.

*   `<table>` – kontener tabeli
*   `<tr>` – wiersz
*   `<td>` – komórka danych
*   `<th>` – komórka nagłówkowa
*   **Scalanie:**
    *   `rowspan="2"` – scalanie w pionie
    *   `colspan="2"` – scalanie w poziomie

> **Typowe pytanie:** Zobaczysz tabelkę z jedną dużą komórką po lewej stronie i dwoma mniejszymi po prawej.
> **Odp:** Musisz szukać w kodzie atrybutu `rowspan="2"` w pierwszej komórce `<td>`.

## 5. Formularze (Najwięcej pytań)
Egzaminy INF.03 bardzo mocno skupiają się na formularzach.

*   **Znacznik `<form>`:**
    *   `method="POST"`
    *   `method="GET"`
    *   `action="..."`
*   **Znacznik `<input>` i jego typy (`type`):**
    *   `type="text"`
    *   `type="password"`
    *   `type="checkbox"`
    *   `type="radio"` – muszą mieć ten sam atrybut `name="..."`
    *   `type="file"`
    *   `type="hidden"`
    *   `type="submit"`
    *   `type="reset"`
*   **Inne elementy formularza:**
    *   `<select>` + `<option>` – lista rozwijana. Atrybut `selected` w `<option>`
    *   `<textarea>`
*   **Atrybuty pól:**
    *   `required`
    *   `disabled`
    *   `placeholder="..."`
    *   `checked`

## 6. Semantyka HTML5
CKE lubi pytać o znaczenie nowych znaczników wprowadzonych w HTML5.

| Znacznik   | Zastosowanie                                            |
|:-----------|:-------------------------------------------------------|
| `<header>` | Nagłówek strony lub sekcji                             |
| `<nav>`    | Główna nawigacja (menu z linkami)                      |
| `<main>`   | Główna, unikalna treść (powinien być jeden na stronie) |
| `<article>`| Samodzielna treść (np. wpis na blogu)                  |
| `<section>`| Sekcja tematyczna                                      |
| `<aside>`  | Treść poboczna (np. pasek boczny)                      |
| `<footer>` | Stopka (prawa autorskie, kontakt)                      |

## 7. Kolory i Jednostki
Często pojawiają się pytania o zapis kolorów.

*   **HEX:** `#FF0000`, `#000000`, `#FFFFFF`
*   **Nazwy:** `red`, `blue`, `green`
*   **RGB:** `rgb(255, 0, 0)`

---
### 🔥 Szybki test wiedzy (Sprawdź się!)

1.  **Pytanie:** Jaki atrybut pozwala na otwarcie linku w nowej karcie?
    *   **Odp:** `target="_blank"` w `<a>`
2.  **Pytanie:** Jak zdefiniować listę, w której punkty są kwadratami?
    *   **Odp:** `<ul type="square">`
3.  **Pytanie:** Który znacznik służy do grupowania opcji w liście rozwijanej `<select>`?
    *   **Odp:** `<optgroup>`
4.  **Pytanie:** Jakim znacznikiem wstawiamy film wideo w HTML5?
    *   **Odp:** `<video>`
5.  **Pytanie:** Co oznacza kod `&nbsp;`?
    *   **Odp:** Twarda spacja (Non-Breaking Space)

### Jak korzystać z bazy pytań?
Przeglądając te 61 stron na zawodowe.edu.pl, szukaj pytań, w których pojawiają się fragmenty kodu. Zwracaj szczególną uwagę na:
1.  **Różnice w atrybutach**
2.  **Poprawność zamykania znaczników**
3.  **Zagnieżdżanie znaczników**
