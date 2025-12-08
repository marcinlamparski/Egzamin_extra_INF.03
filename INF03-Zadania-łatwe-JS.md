# Zbiór zadań JavaScript dla egzaminu INF.03 - WERSJA ŁATWA (Bez odpowiedzi)

## Instrukcja

Poniżej znajduje się **10 zadań** na łatwiejszym poziomie trudności, idealne dla osób, które zaczynają pracę z JavaScript. Każde zadanie zawiera **szczegółowe wskazówki krok po kroku**, co ma ułatwić samodzielną pracę.

### Wymagania ogólne:
- Wszystkie skrypty powinny działać w przeglądarce internetowej
- Kod powinien być czytelny i skomentowany
- Każde zadanie można wykonać w osobnym pliku HTML
- Jeśli coś Ci nie wychodzi - przeczytaj wskazówki dokładnie krok po kroku

### Zakres tematyczny (najprostsze wersje):
- Pobieranie wartości z pól formularza
- Wyświetlanie tekstu na stronie
- Dodawanie nasłuchujących zdarzeń (onclick, addEventListener)
- Proste operacje matematyczne
- Zmiana koloru i tekstu elementów
- Pętle for do powtórzenia czynności
- Tablice do przechowywania danych
- Walidacja (sprawdzenie czy coś zostało wpisane)

---

## ZADANIE 1: Powitanie - Pierwsze JavaScript

### Opis:
Stwórz stronę, która wyświetli powitanie z wpisanym imieniem. Użytkownik wpisuje swoje imię, kliknie przycisk, a na stronie pojawi się komunikat "Cześć [IMIĘ]!"

### Przykład działania:
- Użytkownik wpisuje: "Marta"
- Klika przycisk "Powitaj"
- Na stronie pojawia się: "Cześć Marta!"

### Wskazówki krok po kroku:

**Krok 1:** Utwórz pole tekstowe
```html
<input type="text" id="imie" placeholder="Wpisz swoje imię">
```

**Krok 2:** Utwórz przycisk
```html
<button id="powitajBtn">Powitaj</button>
```

**Krok 3:** Utwórz miejsce na wynik
```html
<div id="wynik"></div>
```

**Krok 4:** W JavaScript:
- Pobierz przycisk: `document.getElementById('powitajBtn')`
- Dodaj nasłuchiwacza: `.addEventListener('click', function() { ... })`
- Pobierz wartość z pola: `document.getElementById('imie').value`
- Wyświetl wynik: `document.getElementById('wynik').textContent = '...'`

### Funkcje do wykorzystania:
- `document.getElementById()` - pobranie elementu
- `.value` - pobieranie tekstu z pola
- `.textContent` - wyświetlanie tekstu
- `.addEventListener('click', ...)` - obsługa kliknięcia

---

## ZADANIE 2: Kalkulator dodawania - Dwa liczby

### Opis:
Stwórz prosty kalkulator, który dodaje dwie liczby. Użytkownik wpisuje dwie liczby, klika przycisk, a program wyświetla sumę.

### Przykład działania:
- Wpisuje 5 i 3
- Klika "Dodaj"
- Wyświetla się: "Wynik: 8"

### Wskazówki krok po kroku:

**Krok 1:** Utwórz dwa pola na liczby
```html
<input type="number" id="liczba1" placeholder="Pierwsza liczba">
<input type="number" id="liczba2" placeholder="Druga liczba">
```

**Krok 2:** Utwórz przycisk i miejsce na wynik
```html
<button id="dodajBtn">Dodaj</button>
<div id="wynik"></div>
```

**Krok 3:** W JavaScript:
- Pobierz pierwszą liczbę i zamień na liczbę: `parseInt(document.getElementById('liczba1').value)`
- Pobierz drugą liczbę: `parseInt(document.getElementById('liczba2').value)`
- Dodaj je do siebie: `const suma = liczba1 + liczba2;`
- Wyświetl wynik: `document.getElementById('wynik').textContent = 'Wynik: ' + suma;`

### Funkcje do wykorzystania:
- `parseInt()` - zmienia tekst na liczbę całkowitą
- `parseFloat()` - zmienia tekst na liczbę dziesiętną (jeśli potrzebujesz)
- Operator `+` do dodawania
- Złączanie tekstu: `'Wynik: ' + liczba`

---

## ZADANIE 3: Zmiana koloru tła

### Opis:
Stwórz stronę z przyciskami, które zmieniają kolor tła strony. Kliknięcie przycisków zmienia tło na inny kolor.

### Przykład działania:
- Użytkownik widzi 3 przyciski: "Czerwony", "Zielony", "Niebieski"
- Klika "Zielony"
- Tło strony zmienia się na zielone

### Wskazówki krok po kroku:

**Krok 1:** Utwórz 3 przyciski
```html
<button id="czerwonyBtn">Czerwony</button>
<button id="zielonyBtn">Zielony</button>
<button id="niebieskyBtn">Niebieski</button>
```

**Krok 2:** W JavaScript dla każdego przycisku:
- Pobierz przycisk: `document.getElementById('czerwonyBtn')`
- Dodaj nasłuchiwacza: `.addEventListener('click', function() { ... })`
- Zmień kolor tła: `document.body.style.backgroundColor = 'red';`

**Krok 3:** Różne kolory:
- 'red' - czerwony
- 'green' - zielony
- 'blue' - niebieski
- 'yellow' - żółty
- '#FF5733' - szesnastkowy kod koloru

### Funkcje do wykorzystania:
- `.style.backgroundColor` - zmiana koloru tła
- `document.body` - całe ciało strony
- `.addEventListener('click', ...)` - obsługa kliknięcia

---

## ZADANIE 4: Lista zakupów - Dodawanie elementów

### Opis:
Stwórz aplikację do listy zakupów. Użytkownik wpisuje przedmiot, klika "Dodaj", a przedmiot pojawia się na liście.

### Przykład działania:
- Wpisuje "Mleko"
- Klika "Dodaj"
- Na liście pojawia się "Mleko"
- Wpisuje "Chleb"
- Klika "Dodaj"
- Na liście pojawia się "Mleko" i "Chleb"

### Wskazówki krok po kroku:

**Krok 1:** Utwórz pole, przycisk i listę
```html
<input type="text" id="przedmiot" placeholder="Wpisz przedmiot">
<button id="dodajBtn">Dodaj</button>
<ul id="lista"></ul>
```

**Krok 2:** W JavaScript:
- Pobierz wartość z pola: `const przedmiot = document.getElementById('przedmiot').value;`
- Utwórz nowy element listy: `const li = document.createElement('li');`
- Ustaw tekst: `li.textContent = przedmiot;`
- Dodaj do listy: `document.getElementById('lista').appendChild(li);`
- Wyczyść pole: `document.getElementById('przedmiot').value = '';`

**Krok 3:** Dodaj walidację:
- Sprawdź czy pole nie jest puste: `if (przedmiot === '') { alert('Wpisz przedmiot!'); return; }`

### Funkcje do wykorzystania:
- `document.createElement('li')` - tworzenie nowego elementu
- `.appendChild()` - dodawanie elementu do listy
- `.value = ''` - czyszczenie pola

---

## ZADANIE 5: Licznik kliknięć

### Opis:
Stwórz prostą aplikację, która liczy ile razy użytkownik kliknął przycisk.

### Przykład działania:
- Użytkownik widzi przycisk i napis "Kliknięcia: 0"
- Klika przycisk
- Napis zmienia się na "Kliknięcia: 1"
- Klika znowu
- Napis zmienia się na "Kliknięcia: 2"

### Wskazówki krok po kroku:

**Krok 1:** Utwórz zmienną licznika (przed przyciskami)
```javascript
let licznikKlikniecia = 0;
```

**Krok 2:** Utwórz przycisk i miejsce na wynik
```html
<button id="klikBtn">Kliknij mnie</button>
<div id="liczba">Kliknięcia: 0</div>
```

**Krok 3:** W JavaScript:
- Pobierz przycisk
- Dodaj nasłuchiwacza `addEventListener('click', ...)`
- Wewnątrz funkcji: `licznikKlikniecia = licznikKlikniecia + 1;`
- Wyświetl: `document.getElementById('liczba').textContent = 'Kliknięcia: ' + licznikKlikniecia;`

**Krok 4:** Dodaj przycisk resetowania
- Utwórz nowy przycisk "Reset"
- Wewnątrz jego nasłuchiwacza: `licznikKlikniecia = 0;`
- Wyświetl: `document.getElementById('liczba').textContent = 'Kliknięcia: 0';`

### Funkcje do wykorzystania:
- Zmienne do przechowywania liczb
- `+=` lub `= + 1` - zwiększanie licznika
- `= 0` - resetowanie licznika

---

## ZADANIE 6: Pokazywanie i ukrywanie elementu

### Opis:
Stwórz dwa przyciski - jeden pokazuje element, drugi go ukrywa.

### Przykład działania:
- Użytkownik widzi przycisk "Pokaż" i przycisk "Ukryj"
- Pod spodem jest napis lub zdjęcie (na początku niewidoczne)
- Klika "Pokaż"
- Napis/zdjęcie się pojawia
- Klika "Ukryj"
- Napis/zdjęcie znika

### Wskazówki krok po kroku:

**Krok 1:** Utwórz elementy
```html
<button id="pokazBtn">Pokaż</button>
<button id="ukryjBtn">Ukryj</button>
<div id="tajny">To jest tajny tekst!</div>
```

**Krok 2:** Ustaw CSS aby element był na początku ukryty
```css
#tajny { display: none; }
```

**Krok 3:** W JavaScript dla przycisku "Pokaż":
- `document.getElementById('tajny').style.display = 'block';`

**Krok 4:** W JavaScript dla przycisku "Ukryj":
- `document.getElementById('tajny').style.display = 'none';`

### Funkcje do wykorzystania:
- `.style.display = 'block'` - pokazywanie elementu
- `.style.display = 'none'` - ukrywanie elementu
- CSS `display: none;` - ukrywanie na początek

---

## ZADANIE 7: Wiadomość powinna być wielka lub mała

### Opis:
Stwórz dwa przyciski, które zmieniają rozmiar tekstu. Jeden robi go większy, drugi mniejszy.

### Przykład działania:
- Użytkownik widzi tekst: "Tekst testowy"
- Klika "Powiększ"
- Tekst staje się większy
- Klika "Pomniejsz"
- Tekst staje się mniejszy

### Wskazówki krok po kroku:

**Krok 1:** Utwórz zmienną na rozmiar tekstu
```javascript
let rozmiarTekstu = 16; // domyślny rozmiar w pikselach
```

**Krok 2:** Utwórz elementy
```html
<button id="powiekszBtn">Powiększ</button>
<button id="pomniejszBtn">Pomniejsz</button>
<div id="tekst">Tekst testowy</div>
```

**Krok 3:** W JavaScript dla przycisku "Powiększ":
- `rozmiarTekstu = rozmiarTekstu + 2;` (zwiększ o 2 piksele)
- `document.getElementById('tekst').style.fontSize = rozmiarTekstu + 'px';`

**Krok 4:** W JavaScript dla przycisku "Pomniejsz":
- `rozmiarTekstu = rozmiarTekstu - 2;` (zmniejsz o 2 piksele)
- `document.getElementById('tekst').style.fontSize = rozmiarTekstu + 'px';`

### Funkcje do wykorzystania:
- `.style.fontSize` - zmiana rozmiaru czcionki
- `+= 2` - zwiększanie
- `-= 2` - zmniejszanie

---

## ZADANIE 8: Weryfikacja czy pole jest wypełnione

### Opis:
Stwórz formularz, który sprawdza czy użytkownik wpisał coś w polu przed wysłaniem. Jeśli nie wpisał - pokazujesz błąd.

### Przykład działania:
- Pole jest puste
- Użytkownik klika "Wyślij"
- Pojawia się komunikat "Błąd: Wpisz coś!"
- Użytkownik wpisuje tekst
- Klika "Wyślij"
- Pojawia się "OK! Tekst zapisany"

### Wskazówki krok po kroku:

**Krok 1:** Utwórz pole, przycisk i miejsce na wiadomość
```html
<input type="text" id="pole" placeholder="Wpisz tekst">
<button id="wyslijBtn">Wyślij</button>
<div id="wiadomosc"></div>
```

**Krok 2:** W JavaScript:
- Pobierz wartość: `const tekst = document.getElementById('pole').value;`
- Sprawdź czy jest puste: `if (tekst === '') { ... }`
- Jeśli puste: `document.getElementById('wiadomosc').textContent = 'Błąd: Wpisz coś!';`
- Jeśli nie puste: `document.getElementById('wiadomosc').textContent = 'OK! Tekst zapisany';`

**Krok 3:** Dodaj formatowanie CSS do wiadomości
```css
.blad { color: red; }
.ok { color: green; }
```

**Krok 4:** Zmień kolor wiadomości
- Dla błędu: dodaj klasę 'blad' lub ustaw kolor na czerwony
- Dla OK: dodaj klasę 'ok' lub ustaw kolor na zielony

### Funkcje do wykorzystania:
- `if (...) { ... }` - sprawdzenie warunku
- `===` - porównanie czy coś jest równe
- `.textContent` - wyświetlanie tekstu

---

## ZADANIE 9: Pętla - Wypisanie liczb od 1 do 10

### Opis:
Stwórz program, który wypisze wszystkie liczby od 1 do 10 na stronie, każdą w nowej linii.

### Przykład działania:
Kliknięcie przycisku "Wypisz liczby" wyświetla:
```
1
2
3
4
5
6
7
8
9
10
```

### Wskazówki krok po kroku:

**Krok 1:** Utwórz przycisk i miejsce na wyniki
```html
<button id="wyspliszBtn">Wypisz liczby</button>
<div id="wynik"></div>
```

**Krok 2:** W JavaScript użyj pętli `for`:
```javascript
let wynik = '';
for (let i = 1; i <= 10; i++) {
    wynik = wynik + i + '<br>'; // <br> to przejście do nowej linii
}
document.getElementById('wynik').innerHTML = wynik;
```

**Krok 3:** Wyjaśnienie pętli:
- `let i = 1;` - start od 1
- `i <= 10;` - kontynuuj dopóki i jest mniejsze lub równe 10
- `i++` - zwiększ i o 1 przy każdej iteracji
- `<br>` - tag HTML do nowej linii

### Funkcje do wykorzystania:
- Pętla `for` - do powtórzenia czynności
- `.innerHTML` - wstawianie kodu HTML
- `+=` - dodawanie do zmiennej

---

## ZADANIE 10: Tablica - Lista imion

### Opis:
Stwórz program, który przechowuje listę imion w tablicy i wyświetla je wszystkie na stronie.

### Przykład działania:
Po kliknięciu "Pokaż imiona" wyświetla:
```
Imiona w mojej klasie:
1. Anna
2. Bartosz
3. Cześć
4. Dominika
5. Ewa
```

### Wskazówki krok po kroku:

**Krok 1:** Utwórz tablicę z imionami (przed skryptem)
```javascript
const imiona = ['Anna', 'Bartosz', 'Cześć', 'Dominika', 'Ewa'];
```

**Krok 2:** Utwórz przycisk i miejsce na wynik
```html
<button id="pokazBtn">Pokaż imiona</button>
<div id="lista"></div>
```

**Krok 3:** W JavaScript użyj pętli do przejścia przez tablicę:
```javascript
let wynik = '<strong>Imiona w mojej klasie:</strong><br>';
for (let i = 0; i < imiona.length; i++) {
    wynik = wynik + (i + 1) + '. ' + imiona[i] + '<br>';
}
document.getElementById('lista').innerHTML = wynik;
```

**Krok 4:** Wyjaśnienie:
- `imiona.length` - liczba elementów w tablicy
- `imiona[i]` - pobranie i-tego elementu z tablicy
- `(i + 1)` - numer od 1 (bo i zaczyna się od 0)

### Funkcje do wykorzystania:
- Tablice do przechowywania danych
- `.length` - liczba elementów
- Pętla `for` - przejście przez wszystkie elementy
- `.innerHTML` - wstawianie HTML

---

## Podsumowanie

Wszystkie zadania są łatwe i mają szczegółowe instrukcje krok po kroku. Powodzenia w nauce JavaScript! 

### Kolejność trudności:
1. ⭐ Powitanie - najłatwsze
2. ⭐ Kalkulator dodawania
3. ⭐ Zmiana koloru tła
4. ⭐⭐ Lista zakupów
5. ⭐⭐ Licznik kliknięć
6. ⭐⭐ Pokazywanie/ukrywanie
7. ⭐⭐ Zmiana rozmiaru czcionki
8. ⭐⭐⭐ Weryfikacja pola
9. ⭐⭐⭐ Pętla - liczby
10. ⭐⭐⭐ Tablica - imiona