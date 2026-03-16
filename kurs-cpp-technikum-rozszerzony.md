# Kurs Podstaw C++ dla Klasy I Technikum
## Przygotowanie do Egzaminu INF.03
### Czas trwania: ~2 godziny

---

## 1. Wprowadzenie do C++

C++ to język programowania, który łączy możliwości programowania niskopoziomowego (bliskiego systemowi) z abstrakcją wysokopoziomową. Jest używany w aplikacjach wymagających wydajności i kontroli nad zasobami.

### Dlaczego C++?
- Wydajność i szybkość wykonania
- Szeroka zastosowanie w systemach (gry, systemy operacyjne, aplikacje serwerowe)
- Wymaga zrozumienia fundamentalnych konceptów programowania
- Walidacja w egzaminie INF.03

### Struktura Programu C++

```cpp
#include <iostream>           // Biblioteka wejścia/wyjścia
using namespace std;          // Przestrzeń nazw

int main()                    // Funkcja główna
{
    // Kod programu
    return 0;                 // Zakończenie programu
}
```

---

## 2. Zmienne i Typy Danych

Zmienna to pojemnik na wartość. Każda zmienna musi mieć określony typ.

### Podstawowe Typy Danych

| Typ | Rozmiar | Zakres | Przykład |
|-----|---------|--------|---------|
| `int` | 4 bajty | -2,147,483,648 do 2,147,483,647 | `int wiek = 18;` |
| `float` | 4 bajty | Liczby zmiennoprzecinkowe (~7 cyfr) | `float cena = 19.99f;` |
| `double` | 8 bajtów | Liczby zmiennoprzecinkowe (~15 cyfr) | `double pi = 3.14159;` |
| `char` | 1 bajt | Pojedynczy znak | `char litera = 'A';` |
| `bool` | 1 bajt | `true` lub `false` | `bool aktywny = true;` |
| `string` | Zmienny | Tekst (ciąg znaków) | `string imie = "Jan";` |

### Deklaracja i Inicjalizacja Zmiennych

```cpp
int liczba;              // Deklaracja (wartość nieokreślona)
liczba = 10;             // Przypisanie wartości
int liczba2 = 20;        // Deklaracja z inicjalizacją
int liczba3 = 30, liczba4 = 40;  // Wiele zmiennych jednocześnie
```

### Konwersja Typów

```cpp
int x = 10;
double y = x;            // Konwersja niejawna int → double (y = 10.0)
int z = (int)3.14;       // Konwersja jawna double → int (z = 3)
```

---

## 3. Operacje Matematyczne

### Operatory Arytmetyczne

| Operator | Znaczenie | Przykład | Wynik |
|----------|-----------|---------|-------|
| `+` | Dodawanie | `5 + 3` | 8 |
| `-` | Odejmowanie | `5 - 3` | 2 |
| `*` | Mnożenie | `5 * 3` | 15 |
| `/` | Dzielenie | `15 / 3` | 5 |
| `%` | Reszta z dzielenia (modulo) | `17 % 5` | 2 |

### Kolejność Wykonywania Operacji (PEMDAS/BODMAS)

```cpp
int wynik = 2 + 3 * 4;     // Wynik: 14 (nie 20!)
int wynik2 = (2 + 3) * 4;  // Wynik: 20
```

### Operatory Przypisania i Skrócone Formy

```cpp
int x = 10;
x += 5;      // x = x + 5;  →  x = 15
x -= 3;      // x = x - 3;  →  x = 12
x *= 2;      // x = x * 2;  →  x = 24
x /= 3;      // x = x / 3;  →  x = 8
x %= 5;      // x = x % 5;  →  x = 3
```

### Inkrementacja i Dekrementacja

```cpp
int x = 5;
x++;         // Inkrementacja: x = 6
x--;         // Dekrementacja: x = 5
++x;         // Pre-inkrementacja (zwiększ najpierw, potem użyj)
x++;         // Post-inkrementacja (użyj, potem zwiększ)
```

---

## 4. Operatory Logiczne i Porównania

### Operatory Porównania

| Operator | Znaczenie | Przykład | Wynik |
|----------|-----------|---------|-------|
| `==` | Równy | `5 == 5` | `true` |
| `!=` | Nierówny | `5 != 3` | `true` |
| `<` | Mniejszy | `3 < 5` | `true` |
| `>` | Większy | `5 > 3` | `true` |
| `<=` | Mniejszy lub równy | `5 <= 5` | `true` |
| `>=` | Większy lub równy | `5 >= 3` | `true` |

### Operatory Logiczne

| Operator | Znaczenie | Tabela Prawdy |
|----------|-----------|---------------|
| `&&` | AND (i) | `true && true = true`<br/>`true && false = false` |
| `\|\|` | OR (lub) | `true \|\| false = true`<br/>`false \|\| false = false` |
| `!` | NOT (negacja) | `!true = false`<br/>`!false = true` |

### Przykłady

```cpp
int wiek = 18;
bool doroslym = (wiek >= 18);           // true
bool mlody = (wiek > 65);               // false
bool mozeSieSprawdzic = (wiek >= 18 && wiek <= 65);  // true
bool nieaktualny = !(wiek >= 18);       // false
```

---

## 5. Instrukcje Warunkowe

### if - else if - else

```cpp
int ocena = 4;

if (ocena == 5) {
    cout << "Bardzo dobrze!" << endl;
}
else if (ocena == 4) {
    cout << "Dobrze!" << endl;
}
else if (ocena >= 3) {
    cout << "Dostatecznie" << endl;
}
else {
    cout << "Niedostatecznie" << endl;
}
```

### switch - case

```cpp
int dzien = 3;

switch (dzien) {
    case 1:
        cout << "Poniedziałek" << endl;
        break;
    case 2:
        cout << "Wtorek" << endl;
        break;
    case 3:
        cout << "Środa" << endl;
        break;
    default:
        cout << "Inny dzień" << endl;
}
```

### Operator Trójkowy (?)

```cpp
int x = 10;
int y = 20;
int max = (x > y) ? x : y;    // max = 20
string wynik = (x > 5) ? "Większe" : "Mniejsze lub równe";
```

---

## 6. Pętle

### Pętla for

```cpp
// Wersja klasyczna
for (int i = 1; i <= 5; i++) {
    cout << i << " ";  // wydruk: 1 2 3 4 5
}

// Pętla od 10 do 1 (opadająco)
for (int i = 10; i >= 1; i--) {
    cout << i << " ";
}

// Pętla z krokiem 2
for (int i = 0; i <= 20; i += 2) {
    cout << i << " ";  // wydruk: 0 2 4 6 8 10 12 14 16 18 20
}
```

### Pętla while

```cpp
int i = 1;
while (i <= 5) {
    cout << i << " ";
    i++;
}
// wydruk: 1 2 3 4 5

// Pętla nieskończona (ostrożnie!)
int licznik = 0;
while (true) {
    licznik++;
    if (licznik == 10) break;  // Wyjście z pętli
    cout << licznik << endl;
}
```

### Pętla do - while

```cpp
int i = 1;
do {
    cout << i << " ";
    i++;
} while (i <= 5);
// wydruk: 1 2 3 4 5

// Różnica: pętla do-while wykonuje się zawsze przynajmniej raz
int x = 10;
do {
    cout << "Wykonam się!" << endl;
} while (x < 5);  // Warunek fałsz, ale kod się wykona
```

### break i continue

```cpp
// break - wyjście z pętli
for (int i = 1; i <= 10; i++) {
    if (i == 5) break;
    cout << i << " ";
}
// wydruk: 1 2 3 4

// continue - przejście do następnej iteracji
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    cout << i << " ";
}
// wydruk: 1 2 4 5
```

---

## 7. Wejście i Wyjście (I/O)

### Wyjście - cout

```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Cześć świat!" << endl;
    cout << "5 + 3 = " << (5 + 3) << endl;
    
    int wiek = 18;
    cout << "Mój wiek: " << wiek << endl;
    
    return 0;
}
```

### Wejście - cin

```cpp
#include <iostream>
using namespace std;

int main() {
    int liczba;
    cout << "Podaj liczbę: ";
    cin >> liczba;
    cout << "Podałeś: " << liczba << endl;
    
    string imie;
    cout << "Podaj imię: ";
    cin >> imie;
    cout << "Cześć " << imie << "!" << endl;
    
    return 0;
}
```

---

## 8. Kompleksowy Przykład: Program Kalkulator

```cpp
#include <iostream>
using namespace std;

int main() {
    double x, y;
    char operacja;
    double wynik;
    
    cout << "=== KALKULATOR ===" << endl;
    cout << "Podaj pierwszą liczbę: ";
    cin >> x;
    
    cout << "Podaj operację (+, -, *, /): ";
    cin >> operacja;
    
    cout << "Podaj drugą liczbę: ";
    cin >> y;
    
    if (operacja == '+') {
        wynik = x + y;
    }
    else if (operacja == '-') {
        wynik = x - y;
    }
    else if (operacja == '*') {
        wynik = x * y;
    }
    else if (operacja == '/') {
        if (y != 0) {
            wynik = x / y;
        }
        else {
            cout << "Błąd: Dzielenie przez zero!" << endl;
            return 1;
        }
    }
    else {
        cout << "Nieznana operacja!" << endl;
        return 1;
    }
    
    cout << x << " " << operacja << " " << y << " = " << wynik << endl;
    
    return 0;
}
```

---

## 9. Dobra Praktyka i Wskazówki

### Nazewnictwo Zmiennych

```cpp
// ✗ Złe
int a, b, zzzz;

// ✓ Dobre
int wiek, cena;
int liczbaStudentow;
bool jestAktywny;
```

### Komentarze

```cpp
// Jednoliniowy komentarz
int x = 5;  // Liczba zamówień

/* Wieloliniowy komentarz
   użyteczny dla dłuższych wyjaśnień */
```

### Formatowanie Kodu

```cpp
// ✓ Czytelny kod
if (x > 5) {
    cout << "Większe" << endl;
}

// ✗ Nieczytelny kod
if(x>5){cout<<"Większe"<<endl;}
```

---

## 10. Tablice (Zmienne Tablicowe)

Tablica to struktura danych przechowująca wiele wartości tego samego typu pod jedną nazwą. Dostęp do elementów odbywa się przez indeks (numer elementu), **licząc od zera**.

### Deklaracja i Inicjalizacja Tablic

```cpp
int oceny[5];                          // Tablica 5 elementów (wartości nieokreślone)
int liczby[5] = {10, 20, 30, 40, 50};  // Tablica z inicjalizacją
int dane[] = {1, 2, 3, 4};             // Rozmiar wynika z liczby elementów (4)
int zerowa[10] = {0};                  // Wszystkie elementy = 0
```

### Indeksowanie — Dostęp do Elementów

```cpp
int tab[4] = {10, 20, 30, 40};

// Indeksy:    [0]  [1]  [2]  [3]
// Wartości:    10   20   30   40

cout << tab[0] << endl;    // 10 (pierwszy element)
cout << tab[3] << endl;    // 40 (ostatni element)

tab[1] = 99;               // Zmiana drugiego elementu na 99
cout << tab[1] << endl;    // 99
```

> **UWAGA EGZAMINACYJNA:** Na egzaminie INF.03 bardzo często pojawia się pytanie o indeksowanie od 0. Tablica `tab[5]` ma indeksy od 0 do 4, NIE od 1 do 5.

### Iterowanie po Tablicy (Pętla + Tablica)

```cpp
int tab[5] = {3, 7, 2, 9, 5};

// Wypisanie wszystkich elementów
for (int i = 0; i < 5; i++) {
    cout << "tab[" << i << "] = " << tab[i] << endl;
}

// Wczytywanie elementów od użytkownika
int dane[5];
for (int i = 0; i < 5; i++) {
    cout << "Podaj element " << i << ": ";
    cin >> dane[i];
}
```

### Operacje na Tablicach

#### Suma i Średnia Elementów

```cpp
int tab[5] = {10, 20, 30, 40, 50};
int suma = 0;

for (int i = 0; i < 5; i++) {
    suma += tab[i];
}

double srednia = suma / 5.0;
cout << "Suma: " << suma << endl;         // 150
cout << "Średnia: " << srednia << endl;    // 30.0
```

#### Szukanie Wartości Maksymalnej i Minimalnej

```cpp
int tab[5] = {3, 7, 2, 9, 5};

int maks = tab[0];     // Zakładamy, że pierwszy element jest największy
int mini = tab[0];     // Zakładamy, że pierwszy element jest najmniejszy

for (int i = 1; i < 5; i++) {
    if (tab[i] > maks) {
        maks = tab[i];
    }
    if (tab[i] < mini) {
        mini = tab[i];
    }
}

cout << "Maksimum: " << maks << endl;    // 9
cout << "Minimum: " << mini << endl;     // 2
```

#### Zliczanie Elementów Spełniających Warunek

```cpp
int tab[6] = {4, 7, 2, 8, 1, 6};
int ileWiekszych = 0;

for (int i = 0; i < 6; i++) {
    if (tab[i] > 5) {
        ileWiekszych++;
    }
}
cout << "Elementów > 5: " << ileWiekszych << endl;  // 3
```

### Tablice Dwuwymiarowe (Macierze)

Tablica dwuwymiarowa to tablica tablic — dane zorganizowane w wiersze i kolumny (jak tabela).

```cpp
// Deklaracja tablicy 3 wiersze × 4 kolumny
int macierz[3][4] = {
    {1, 2, 3, 4},      // wiersz 0
    {5, 6, 7, 8},      // wiersz 1
    {9, 10, 11, 12}     // wiersz 2
};

// Dostęp: macierz[wiersz][kolumna]
cout << macierz[0][0] << endl;   // 1  (wiersz 0, kolumna 0)
cout << macierz[1][2] << endl;   // 7  (wiersz 1, kolumna 2)
cout << macierz[2][3] << endl;   // 12 (wiersz 2, kolumna 3)

// Wypisanie całej macierzy
for (int w = 0; w < 3; w++) {
    for (int k = 0; k < 4; k++) {
        cout << macierz[w][k] << "\t";
    }
    cout << endl;
}
```

> **UWAGA EGZAMINACYJNA:** Tablica dwuwymiarowa `tab[3][4]` oznacza: 3 wiersze i 4 kolumny. W każdej komórce znajduje się wartość, a NIE inna tablica. To częsty dystraktor w pytaniach.

---

## 11. Funkcje

Funkcja to wydzielony fragment kodu, który wykonuje określone zadanie. Pozwala unikać powtarzania kodu i organizować program w logiczne bloki.

### Definiowanie i Wywoływanie Funkcji

```cpp
#include <iostream>
using namespace std;

// Definicja funkcji (przed main lub z deklaracją - prototypem)
void powitanie() {
    cout << "Witaj w programie!" << endl;
}

int main() {
    powitanie();   // Wywołanie funkcji
    powitanie();   // Można wywołać wielokrotnie
    return 0;
}
```

### Funkcje z Parametrami

```cpp
void powitaj(string imie) {
    cout << "Cześć " << imie << "!" << endl;
}

void wypiszSume(int a, int b) {
    cout << a << " + " << b << " = " << (a + b) << endl;
}

int main() {
    powitaj("Anna");           // Cześć Anna!
    powitaj("Marcin");         // Cześć Marcin!
    wypiszSume(5, 3);          // 5 + 3 = 8
    return 0;
}
```

### Funkcje Zwracające Wartość (return)

```cpp
// Funkcja zwraca wartość typu int
int dodaj(int a, int b) {
    return a + b;           // Zwraca wynik do miejsca wywołania
}

double obliczSrednia(int x, int y) {
    return (x + y) / 2.0;  // Zwraca double
}

bool czyParzysta(int n) {
    return (n % 2 == 0);   // Zwraca true lub false
}

int main() {
    int wynik = dodaj(10, 20);
    cout << "Suma: " << wynik << endl;           // 30
    
    cout << "Średnia: " << obliczSrednia(7, 3) << endl;  // 5.0
    
    if (czyParzysta(6)) {
        cout << "Liczba parzysta" << endl;
    }
    return 0;
}
```

> **UWAGA EGZAMINACYJNA:** Na egzaminie często pojawia się pytanie w stylu: "Jaką wartość zwróci funkcja X wywołana z parametrem Y?" — trzeba prześledzić kod krok po kroku.

### void vs Typ Zwracany

```cpp
void procedura()  { /* Nie zwraca wartości */ }
int  funkcja()    { return 42; /* Zwraca int */ }
```

- `void` — funkcja wykonuje akcję, ale nic nie zwraca (np. wypisuje tekst)
- `int`, `double`, `bool`, `string` — funkcja oblicza i **zwraca** wynik

### Prototypy Funkcji (Deklaracja przed main)

```cpp
#include <iostream>
using namespace std;

// Prototypy (deklaracje) — informują kompilator o istnieniu funkcji
int kwadrat(int n);
double potega(double podstawa, int wykladnik);

int main() {
    cout << kwadrat(5) << endl;          // 25
    cout << potega(2.0, 10) << endl;     // 1024
    return 0;
}

// Definicje funkcji (mogą być po main)
int kwadrat(int n) {
    return n * n;
}

double potega(double podstawa, int wykladnik) {
    double wynik = 1;
    for (int i = 0; i < wykladnik; i++) {
        wynik *= podstawa;
    }
    return wynik;
}
```

### Przekazywanie Tablicy do Funkcji

```cpp
// Tablica jest przekazywana przez wskaźnik (bez kopii)
void wypiszTablice(int tab[], int rozmiar) {
    for (int i = 0; i < rozmiar; i++) {
        cout << tab[i] << " ";
    }
    cout << endl;
}

int sumaTablicy(int tab[], int rozmiar) {
    int suma = 0;
    for (int i = 0; i < rozmiar; i++) {
        suma += tab[i];
    }
    return suma;
}

int main() {
    int dane[5] = {1, 2, 3, 4, 5};
    wypiszTablice(dane, 5);                    // 1 2 3 4 5
    cout << "Suma: " << sumaTablicy(dane, 5);  // 15
    return 0;
}
```

---

## 12. Podstawowe Algorytmy

Na egzaminie INF.03 pojawiają się pytania wymagające analizy algorytmów zapisanych jako kod, pseudokod lub lista kroków. Poniżej najczęściej spotykane algorytmy.

### Wyszukiwanie Liniowe (Sekwencyjne)

Przegląda tablicę element po elemencie, aż znajdzie szukaną wartość.

```cpp
int szukajLiniowo(int tab[], int rozmiar, int szukana) {
    for (int i = 0; i < rozmiar; i++) {
        if (tab[i] == szukana) {
            return i;       // Zwraca indeks znalezionego elementu
        }
    }
    return -1;              // Nie znaleziono
}

int main() {
    int tab[] = {4, 7, 2, 9, 1, 5};
    int indeks = szukajLiniowo(tab, 6, 9);
    
    if (indeks != -1) {
        cout << "Znaleziono na pozycji: " << indeks << endl;  // 3
    } else {
        cout << "Nie znaleziono" << endl;
    }
    return 0;
}
```

### Sortowanie Bąbelkowe (Bubble Sort)

Porównuje sąsiednie elementy i zamienia je miejscami, jeśli są w złej kolejności. Powtarza przejścia aż tablica jest posortowana.

```cpp
void sortBabelkowe(int tab[], int rozmiar) {
    for (int i = 0; i < rozmiar - 1; i++) {
        for (int j = 0; j < rozmiar - 1 - i; j++) {
            if (tab[j] > tab[j + 1]) {
                // Zamiana miejscami (swap)
                int temp = tab[j];
                tab[j] = tab[j + 1];
                tab[j + 1] = temp;
            }
        }
    }
}

int main() {
    int tab[] = {5, 3, 8, 1, 2};
    int n = 5;
    
    sortBabelkowe(tab, n);
    
    for (int i = 0; i < n; i++) {
        cout << tab[i] << " ";   // 1 2 3 5 8
    }
    return 0;
}
```

### Odwracanie Tablicy

```cpp
void odwrocTablice(int tab[], int rozmiar) {
    for (int i = 0; i < rozmiar / 2; i++) {
        int temp = tab[i];
        tab[i] = tab[rozmiar - 1 - i];
        tab[rozmiar - 1 - i] = temp;
    }
}
```

### Algorytm Euklidesa (NWD — Największy Wspólny Dzielnik)

```cpp
int nwd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    cout << "NWD(12, 8) = " << nwd(12, 8) << endl;   // 4
    cout << "NWD(24, 36) = " << nwd(24, 36) << endl;  // 12
    return 0;
}
```

### Suma Cyfr Liczby

```cpp
int sumaCyfr(int n) {
    int suma = 0;
    while (n > 0) {
        suma += n % 10;     // Dodaj ostatnią cyfrę
        n /= 10;            // Usuń ostatnią cyfrę
    }
    return suma;
}
// sumaCyfr(1234) → 1 + 2 + 3 + 4 = 10
```

> **UWAGA EGZAMINACYJNA:** Na egzaminie pojawia się pytanie "Co oblicza przedstawiony algorytm?" z odpowiedziami typu: a) sumę cyfr, b) liczbę cyfr, c) NWD, d) sumę liczb. Trzeba umieć przeanalizować działanie pętli while z operatorami `%` i `/`.

---

## 13. Pojęcia Programistyczne (Teoria do Egzaminu)

Te pojęcia pojawiają się na egzaminie pisemnym INF.03 jako pytania teoretyczne.

### Kompilator vs Interpreter

| Cecha | Kompilator | Interpreter |
|-------|-----------|-------------|
| Działanie | Tłumaczy **cały** kod na kod maszynowy **przed** uruchomieniem | Tłumaczy kod **instrukcja po instrukcji** w trakcie wykonywania |
| Wynik | Tworzy plik wykonywalny (.exe) | Nie tworzy pliku wykonywalnego |
| Szybkość wykonania | Szybsze (kod już przetłumaczony) | Wolniejsze (tłumaczenie na bieżąco) |
| Wykrywanie błędów | Przed uruchomieniem (na etapie kompilacji) | W trakcie wykonania |
| Przykłady języków | C, C++, Java (częściowo) | Python, PHP, JavaScript |

### Debugowanie

Debugowanie to proces **wyszukiwania i naprawiania błędów** w kodzie programu. Narzędzia do debugowania pozwalają wykonywać kod krok po kroku i obserwować wartości zmiennych.

### Rodzaje Błędów

| Rodzaj | Opis | Przykład |
|--------|------|---------|
| Błąd składniowy (syntax error) | Naruszenie reguł języka — kod się nie skompiluje | Brak średnika: `int x = 5` |
| Błąd logiczny (logic error) | Kod się kompiluje, ale daje złe wyniki | Użycie `<` zamiast `<=` w warunku |
| Błąd wykonania (runtime error) | Błąd w trakcie działania programu | Dzielenie przez zero |

### Biblioteka Programistyczna

Biblioteka to **zestaw gotowych funkcji i klas**, które można wykorzystywać w programach. Nie jest plikiem wykonywalnym ani kodem kompilowanym jednorazowo — to zasób wielokrotnego użytku.

### Pseudokod i Lista Kroków

Na egzaminie algorytmy mogą być zapisane w pseudokodzie (uproszczonym zapisie przypominającym język programowania) lub jako lista kroków. Przykład:

```
Algorytm: Szukanie maximum w tablicy
Dane: tablica T[n]
1. max ← T[0]
2. Dla i = 1, 2, ..., n-1 wykonuj:
   2.1. Jeżeli T[i] > max to max ← T[i]
3. Wypisz max
```

---

# CZĘŚĆ PRAKTYCZNA

## Ćwiczenie 1: Program "Sprawdzacz Wieku i Kategorii"

### Zadanie
Napisz program, który:
1. Pyta użytkownika o jego wiek
2. Wczytuje wiek (int)
3. Na podstawie wieku klasyfikuje osobę:
   - Poniżej 13: "Dziecko"
   - 13-17: "Nastolatek"
   - 18-64: "Dorosły"
   - 65+: "Senior"
4. Sprawdza, czy osoba jest uprawniona do prowadzenia samochodu (min. 18 lat)
5. Wyświetla komunikat z klasą wiekową i uprawnieniami

### Wskazówka
Użyj instrukcji `if-else if-else` do klasyfikacji wieku. Operator `&&` może być przydatny do sprawdzenia zakresu.

### Punkt wyjścia
```cpp
#include <iostream>
using namespace std;

int main() {
    int wiek;
    
    cout << "Podaj swój wiek: ";
    cin >> wiek;
    
    // Tutaj wpisz swój kod
    
    return 0;
}
```

---

## Ćwiczenie 2: Program "Tablica Mnożenia i Średnia"

### Zadanie
Napisz program, który:
1. Pyta użytkownika o liczbę (int, z zakresu 1-10)
2. Wyświetla tabelę mnożenia (podana liczba × 1 do 10)
3. Oblicza sumę wszystkich iloczynów z tabeli mnożenia
4. Oblicza średnią arytmetyczną z tych iloczynów
5. Wyświetla wyniki w czytelny sposób

### Przykład
```
Podaj liczbę (1-10): 3
Tabela mnożenia dla liczby 3:
3 × 1 = 3
3 × 2 = 6
3 × 3 = 9
...
3 × 10 = 30

Suma iloczynów: 165
Średnia: 16.5
```

### Wskazówka
Użyj pętli `for` do iteracji przez liczby 1-10. Zmienne pomocnicze do przechowywania sumy będą niezbędne.

### Punkt wyjścia
```cpp
#include <iostream>
using namespace std;

int main() {
    int liczba;
    
    cout << "Podaj liczbę (1-10): ";
    cin >> liczba;
    
    // Walidacja danych (opcjonalnie)
    if (liczba < 1 || liczba > 10) {
        cout << "Liczba poza zakresy!" << endl;
        return 1;
    }
    
    // Tutaj wpisz swój kod
    
    return 0;
}
```

---

## Ćwiczenie 3: Program "Analiza Tablicy Ocen"

### Zadanie
Napisz program, który:
1. Wczytuje od użytkownika 5 ocen (int, z zakresu 1-6) do tablicy
2. Wyświetla wszystkie wczytane oceny
3. Oblicza i wyświetla średnią arytmetyczną ocen
4. Znajduje najwyższą i najniższą ocenę
5. Zlicza ile ocen jest powyżej średniej
6. Wykorzystuje osobne **funkcje** do: obliczania średniej, szukania max/min, zliczania

### Przykład
```
Podaj ocenę 1: 4
Podaj ocenę 2: 5
Podaj ocenę 3: 3
Podaj ocenę 4: 5
Podaj ocenę 5: 2

Oceny: 4 5 3 5 2
Średnia: 3.8
Najwyższa ocena: 5
Najniższa ocena: 2
Ocen powyżej średniej: 2
```

### Wskazówka
Napisz funkcje: `obliczSrednia()`, `znajdzMax()`, `znajdzMin()`, `zliczPowyzej()`. Każda przyjmuje tablicę i jej rozmiar jako parametry.

### Punkt wyjścia
```cpp
#include <iostream>
using namespace std;

// Tutaj zdefiniuj funkcje

int main() {
    const int ROZMIAR = 5;
    int oceny[ROZMIAR];
    
    // Wczytywanie ocen
    for (int i = 0; i < ROZMIAR; i++) {
        cout << "Podaj ocenę " << (i + 1) << ": ";
        cin >> oceny[i];
    }
    
    // Tutaj wpisz swój kod (wywołania funkcji)
    
    return 0;
}
```

---


---

## Sprawdzenie Wiedzy - Pytania do Przeanalizowania

1. Jakie są różnice między typami `int`, `float` i `double`?
2. Co to jest reszta z dzielenia (modulo) i kiedy się ją stosuje?
3. Kiedy używamy `if-else`, a kiedy `switch`?
4. Jaka jest różnica między pętlą `while` i `do-while`?
5. Co robi instrukcja `break` i `continue` wewnątrz pętli?
6. Czy wyrażenie `5 / 2` da nam `2` czy `2.5`? Dlaczego?
7. Jak działają operatory `&&`, `||` i `!`?
8. Od jakiego indeksu zaczynają się elementy tablicy? Jaki jest ostatni indeks tablicy `tab[10]`?
9. Jaka jest różnica między funkcją `void` a funkcją zwracającą wartość?
10. Co robi instrukcja `return` w funkcji?
11. Jaka jest różnica między kompilatorem a interpreterem?
12. Jakie są trzy rodzaje błędów w programowaniu i czym się różnią?
13. Co robi algorytm: `while (n > 0) { s += n % 10; n /= 10; }`?

---

## Materiały Dodatkowe

### Kompilacja i Uruchamianie Programu C++

#### Na systemie Windows (Visual Studio, Code Blocks):
```bash
g++ program.cpp -o program.exe
program.exe
```

#### Na systemie Linux/Mac:
```bash
g++ program.cpp -o program
./program
```

### Przydatne Biblioteki

```cpp
#include <iostream>      // Wejście/wyjście (cin, cout)
#include <cmath>         // Funkcje matematyczne (sqrt, pow, abs)
#include <string>        // Operacje na tekstach
#include <cstdlib>       // Funkcje systemowe (rand, abs)
```

### Funkcje Matematyczne

```cpp
#include <cmath>

double pierwiastek = sqrt(16);      // 4.0
double potega = pow(2, 3);          // 8.0
int wartosc_bezwzgledna = abs(-5);  // 5
double zaokruszenie = floor(3.7);   // 3.0
```

---

## Wskazówki do Egzaminu INF.03

1. **Czytaj uważnie zadanie** - Zrozum dokładnie, co program ma robić
2. **Zdefiniuj zmienne** - Określ jakie zmienne będą potrzebne
3. **Przepisz logikę** - Narysuj schemat blokowy lub wypunktuj kroki
4. **Kod krok po kroku** - Pisz i testuj część po części
5. **Waliduj dane** - Sprawdź czy użytkownik podał sensowe wartości
6. **Testuj przypadki skrajne** - Co jeśli liczba to 0? Czy pętla się wykona?
7. **Czytelność** - Dobrze sformatowany kod jest łatwiejszy w debugowaniu

---

## Podsumowanie Tematów

Kurs obejmuje:
- ✓ Zmienne i typy danych (int, float, double, char, bool, string)
- ✓ Operacje matematyczne i operatory
- ✓ Operatory porównania i logiczne
- ✓ Instrukcje warunkowe (if, else if, else, switch)
- ✓ Pętle (for, while, do-while)
- ✓ Instrukcje break i continue
- ✓ Wejście/wyjście (cin, cout)
- ✓ **Tablice jednowymiarowe i dwuwymiarowe** *(NOWE)*
- ✓ **Funkcje — parametry, return, void, prototypy** *(NOWE)*
- ✓ **Algorytmy — wyszukiwanie, sortowanie bąbelkowe, NWD, suma cyfr** *(NOWE)*
- ✓ **Pojęcia: kompilator vs interpreter, debugowanie, rodzaje błędów** *(NOWE)*
- ✓ Praktyczne ćwiczenia z rozwiązaniami (3 ćwiczenia)
- ✓ Wskazówki do egzaminu

---

**Powodzenia w nauce i na egzaminie INF.03!**

** miejsce na pliki z ćwiczeń** https://www.dropbox.com/request/IvIo6UNbKC1tmlpFabkv
