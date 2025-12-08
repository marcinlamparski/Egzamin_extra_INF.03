# Zbiór zadań JavaScript dla egzaminu INF.03

## Instrukcja

Poniżej znajduje się **10 zadań** na poziomie trudności typowym dla egzaminu INF.03 zawodowego. Każde zadanie dotyczy umiejętności programowania w JavaScript, które są wymagane na egzaminie z kwalifikacji **INF.03** (Tworzenie aplikacji internetowych i baz danych).

### Wymagania ogólne:
- Wszystkie skrypty powinny działać w przeglądarce internetowej
- Kod powinien być czytelny i skomentowany
- Zalecane jest testowanie w różnych przeglądarkach
- Każde zadanie można wykonać w osobnym pliku HTML lub w jednym pliku ze wszystkimi zadaniami

### Zakres tematyczny:
- Obsługa zdarzeń (addEventListener, onclick, onsubmit)
- Manipulacja DOM (getElementById, querySelector, innerHTML, textContent)
- Walidacja formularzy i danych wejściowych
- Obliczenia matematyczne
- Konwersje jednostek
- Formatowanie wyników
- Przetwarzanie danych tekstowych (metody string)
- Praca z liczbami (parseInt, parseFloat, toFixed)
- Warunkowe wyświetlanie informacji
- Obsługa błędów

---

## ZADANIE 1: Kalkulator BMI (Body Mass Index)

### Opis:
Stwórz aplikację obliczającą wskaźnik BMI (Body Mass Index). Aplikacja powinna zawierać:
- Formularz z polami do wpisania: wagę (kg) i wzrostu (cm)
- Przycisk "Oblicz BMI"
- Wyświetlenie wyniku z kategorią (niedowaga, waga prawidłowa, nadwaga, otyłość)
- Zmianę koloru tekstu wyniku w zależności od wyniku (zielony dla prawidłowej wagi, żółty dla nadwagi, czerwony dla otyłości)

### Wzór:
BMI = waga (kg) / (wzrost w metrach)²

### Kategorie:
- BMI < 18,5 - Niedowaga (niebieski)
- 18,5 ≤ BMI < 25 - Waga prawidłowa (zielony)
- 25 ≤ BMI < 30 - Nadwaga (żółty)
- BMI ≥ 30 - Otyłość (czerwony)

### Wskazówki:
Przydatne funkcje i metody:
- `document.getElementById()` - pobranie elementu
- `parseInt()` lub `parseFloat()` - konwersja tekstu na liczbę
- `addEventListener()` - dodanie nasłuchiwacza zdarzenia
- `toFixed(2)` - zaokrąglanie do 2 miejsc po przecinku
- Instrukcja warunkowa `if...else if...else`
- Manipulacja `classList` lub `style` do zmiany koloru

---

## ZADANIE 2: Walidacja formularza rejestracji

### Opis:
Stwórz formularz rejestracji z walidacją. Formularz powinien zawierać:
- Pole na imię (minimum 3 znaki)
- Pole na e-mail (poprawny format)
- Pole na hasło (minimum 8 znaków, musi zawierać cyfrę i dużą literę)
- Pole na potwierdzenie hasła
- Przycisk "Zarejestruj"
- Wyświetlenie komunikatów o błędach pod każdym polem
- Zmianę koloru ramki pola na czerwony w przypadku błędu, zielony w przypadku poprawności

### Warunki poprawności:
- Imię: minimum 3 znaki, tylko litery
- E-mail: zawiera @ i .
- Hasło: minimum 8 znaków, co najmniej 1 cyfra, co najmniej 1 duża litera
- Potwierdzenie: identyczne z hasłem

### Wskazówki:
Przydatne funkcje i metody:
- `querySelector()` - selektor CSS do pobrania elementu
- `addEventListener('submit', ...)` - obsługa wysłania formularza
- `preventDefault()` - zapobieganie domyślnemu wysłaniu
- `value.length` - długość tekstu
- Wyrażenia regularne do walidacji
- `.match()` lub `.includes()` - sprawdzenie zawartości tekstu
- Pętla `forEach()` - walidacja wszystkich pól
- `addEventListener('input', ...)` - walidacja na bieżąco podczas pisania

---

## ZADANIE 3: Konwerter temperatur

### Opis:
Stwórz konwerter umożliwiający konwersję temperatur między skalami:
- Celsius ↔ Fahrenheit
- Celsius ↔ Kelvin
- Fahrenheit ↔ Kelvin

Aplikacja powinna zawierać:
- 3 pola tekstowe dla trzech skal
- Automatyczne aktualizowanie pozostałych pól po wpisaniu wartości w jednym polu
- Możliwość wyczyszczenia wszystkich pól przyciskiem "Wyczyść"
- Wyświetlenie ostrzeżenia, jeśli temperatura jest poniżej zera absolutnego (-273,15°C)

### Wzory:
- C na F: (C × 9/5) + 32
- C na K: C + 273.15
- F na C: (F - 32) × 5/9
- K na C: K - 273.15

### Wskazówki:
Przydatne funkcje i metody:
- `addEventListener('input', ...)` - reagowanie na zmianę w polu
- `value` - pobieranie wartości z pola
- `parseInt()` lub `parseFloat()` - konwersja na liczbę
- `toFixed(2)` - zaokrąglanie
- Instrukcje warunkowe do sprawdzenia poprawności
- Operacje matematyczne do obliczeń

---

## ZADANIE 4: Generator kolorów losowych

### Opis:
Stwórz aplikację do generowania losowych kolorów w formacie HEX. Aplikacja powinna:
- Wyświetlać aktualny kolor jako prostokąt na stronie
- Wyświetlać kod HEX koloru
- Wyświetlać kod RGB koloru
- Posiada przycisk "Generuj nowy kolor"
- Posiada przycisk "Kopiuj HEX do schowka"
- Wyświetla komunikat potwierdzenia po skopiowaniu

### Dodatkowe funkcjonalności:
- Historia ostatnich 5 wygenerowanych kolorów (kliknięcie na kolor z historii go wybiera)
- Przycisk do wyczyszczenia historii

### Wskazówki:
Przydatne funkcje i metody:
- `Math.random()` - generowanie liczby losowej
- `Math.floor()` - zaokrąglanie w dół
- `toString(16)` - konwersja liczby na heksadecymalny
- `padStart()` - uzupełnianie zerami
- `addEventListener('click', ...)` - obsługa kliknięcia
- `navigator.clipboard.writeText()` - kopiowanie do schowka
- Tablica do przechowywania historii
- Pętla `forEach()` lub `map()` - generowanie elementów historii
- `style.backgroundColor` - zmiana koloru tła

---

## ZADANIE 5: Kalkulator wydatków

### Opis:
Stwórz aplikację do zarządzania wydatkami. Aplikacja powinna umożliwiać:
- Dodawanie wydatków z opisem, kwotą i kategorią (Jedzenie, Transport, Rozrywka, Inne)
- Usuwanie wydatków z listy
- Wyświetlenie łącznej sumy wydatków
- Wyświetlenie sumy wydatków dla każdej kategorii
- Sortowanie wydatków (po dacie dodania, po kwocie - rosnąco/malejąco)
- Wyczyszczenie wszystkich wydatków przyciskiem "Wyczyść listę"

### Struktura wydatku:
- Opis (np. "Obiad")
- Kwota (liczba)
- Kategoria (select z opcjami)
- Data dodania (automatycznie)

### Wskazówki:
Przydatne funkcje i metody:
- Obiekty do przechowywania danych wydatków
- Tablica do przechowywania listy wydatków
- `push()` - dodawanie do tablicy
- `filter()` - usuwanie elementu
- `reduce()` - sumowanie wydatków
- `forEach()` - iterowanie po wydatkach
- `slice()` - sortowanie bez mutacji
- `sort()` - sortowanie tablicy
- `toFixed(2)` - formatowanie kwoty
- DOM manipulation - dodawanie/usuwanie elementów
- `addEventListener()` - obsługa formularza i przycisków

---

## ZADANIE 6: Licznik słów i znaków

### Opis:
Stwórz aplikację do analizy tekstu. Aplikacja powinna:
- Zawierać pole textarea do wpisywania tekstu
- Na bieżąco wyświetlać liczbę: słów, znaków, znaków bez spacji
- Wyświetlać liczbę linii
- Wyświetlać najczęściej występujące słowo
- Pokazać czas czytania (średni czas to 200 słów na minutę)
- Przycisk "Wyczyść" do wyczyszczenia pola

### Dodatkowe funkcjonalności:
- Wyszukiwanie konkretnego słowa (ile razy się pojawia)
- Wyświetlenie statystyk (najdłuższe słowo, najkrótsze słowo)

### Wskazówki:
Przydatne funkcje i metody:
- `addEventListener('input', ...)` - reagowanie na zmianę tekstu
- `trim()` - usunięcie spacji na początku i końcu
- `split()` - dzielenie tekstu na części
- `length` - długość tekstu/tablicy
- `replace()` - usunięcie spacji
- `toLowerCase()` - konwersja na małe litery
- `match()` - wyszukiwanie wzoru
- Obiekty do liczenia słów
- `Object.entries()` - konwersja obiektu na tablicę
- `sort()` - sortowanie

---

## ZADANIE 7: Gra "Zgadnij liczbę"

### Opis:
Stwórz grę, w której użytkownik zgaduje liczbę od 1 do 100. Aplikacja powinna:
- Wylosować liczbę na początek gry
- Pozwolić na wpisanie liczby w pole tekstowe
- Po kliknięciu "Sprawdź" wyświetlić:
  - "Za wysoko" jeśli liczba jest większa niż szukana
  - "Za nisko" jeśli liczba jest mniejsza niż szukana
  - "Brawo! Wpadłeś!" jeśli liczba jest prawidłowa
- Wyświetlić liczbę prób
- Przycisk "Nowa gra" do resetowania gry

### Dodatkowe funkcjonalności:
- Historia ostatnich 5 gier (ile prób zajęło zgadnięcie liczby)
- System poziomów trudności (łatwy: 1-50, średni: 1-100, trudny: 1-1000)

### Wskazówki:
Przydatne funkcje i metody:
- `Math.random()` - losowanie liczby
- `Math.floor()` - zaokrąglanie
- Warunki `if...else if...else` - sprawdzenie liczby
- `parseInt()` - konwersja na liczbę
- `addEventListener('click', ...)` - obsługa przycisków
- Zmienne do przechowywania stanu gry
- `disabled` - wyłączanie przycisków
- Tablica do przechowywania historii

---

## ZADANIE 8: Harmonogram zadań (TODO List)

### Opis:
Stwórz aplikację do zarządzania listą zadań. Aplikacja powinna umożliwiać:
- Dodawanie nowych zadań z opisem i terminem
- Oznaczanie zadania jako wykonane (checkbox)
- Usuwanie zadania
- Filtrowanie zadań (Wszystkie, Wykonane, Niewykonane, Przeterminowane)
- Sortowanie zadań (po dacie, po alfabecie)
- Wyświetlanie liczby zadań (wszystkich, wykonanych, niewykonanych)
- Wyczyszczenie wszystkich wykonanych zadań

### Struktura zadania:
- Opis zadania
- Termin wykonania (data)
- Status (wykonane/niewykonane)
- Data dodania

### Wskazówki:
Przydatne funkcje i metody:
- Obiekty do reprezentacji zadań
- Tablica do przechowywania listy
- `push()` - dodawanie
- `filter()` - filtrowanie
- `map()` - mapowanie elementów
- `sort()` - sortowanie
- `splice()` lub `filter()` - usuwanie
- DOM manipulation - dodawanie/usuwanie elementów HTML
- `addEventListener()` - obsługa zdarzeń
- Obiekty `Date` - praca z datami
- `toLocaleDateString()` - formatowanie daty

---

## ZADANIE 9: Kalkulator rat kredytowych

### Opis:
Stwórz kalkulator do obliczania rat kredytowych. Aplikacja powinna zawierać pola do wpisania:
- Kwota kredytu (w zł)
- Oprocentowanie roczne (w %)
- Okres spłaty (liczba miesięcy)

Po kliknięciu "Oblicz" wyświetlić:
- Miesięczną ratę
- Łączną kwotę do spłacenia
- Łączne odsetki
- Tabelę z harmonogramem rat (numer raty, kwota raty, odsetki, kapitał, pozostała do spłaty kwota)

### Dodatkowe funkcjonalności:
- Możliwość wydruku harmonogramu

### Wzór na ratę:
Rata = P × [r(1+r)^n] / [(1+r)^n - 1]
Gdzie: P - kwota pożyczki, r - oprocentowanie miesięczne, n - liczba miesięcy

### Wskazówki:
Przydatne funkcje i metody:
- `parseFloat()` - konwersja na liczbę
- `Math.pow()` - podnoszenie do potęgi
- `toFixed(2)` - zaokrąglanie do 2 miejsc
- Pętla `for` - generowanie harmonogramu
- Tworzenie elementów HTML dynamicznie
- `addEventListener()` - obsługa obliczenia
- `innerHTML` - wstawienie tabeli
- `style` - formatowanie

---

## ZADANIE 10: Aplikacja do nauki słówek (Flashcards)

### Opis:
Stwórz aplikację do nauki słówek z wykorzystaniem kart (flashcards). Aplikacja powinna:
- Wyświetlać słówko w jednym języku (np. angielskim)
- Po kliknięciu pokazać tłumaczenie
- Przycisk "Następna karta" - przejście do kolejnego słówka
- Przycisk "Poprzednia karta" - powrót do poprzedniego słówka
- Wyświetlanie aktualnego numeru karty
- Przycisk "Shuffle" - losowe tasowanie kolejności kart
- Przycisk "Reset" - powrót do początkowej karty

### Dane (przykład - słówka angielskie):
```
[
  { question: "apple", answer: "jabłko" },
  { question: "book", answer: "książka" },
  { question: "computer", answer: "komputer" },
  { question: "door", answer: "drzwi" },
  { question: "elephant", answer: "słoń" }
]
```

### Dodatkowe funkcjonalności:
- Możliwość dodawania nowych kart
- Możliwość zaznaczania kart do powtórzenia
- Licznik zaliczonych kart

### Wskazówki:
Przydatne funkcje i metody:
- Tablica obiektów do przechowywania kart
- Zmienna do śledzenia bieżącej karty
- `addEventListener('click', ...)` - obsługa przycisków
- `innerHTML` - wyświetlanie karty
- `classList.toggle()` - pokazywanie/ukrywanie odpowiedzi
- `Math.random()` i `.sort()` - tasowanie kart
- Warunki do sprawdzenia czy jesteśmy na pierwszej/ostatniej karcie
- `disabled` - wyłączanie przycisków gdy to potrzebne
- Zmienne do śledzenia stanu aplikacji

---

## Podsumowanie

Wszystkie zadania zostały przygotowane na bazie typowych wymagań egzaminu INF.03 zawodowego. Stanowią one reprezentatywny zbiór zagadnień JavaScript, które mogą pojawić się na egzaminie. Każde zadanie skupia się na innym aspekcie programowania w JavaScript i wymaga praktycznego zastosowania różnych technik i metod.

Powodzenia w nauce!