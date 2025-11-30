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
    cout << i << " ";  // Wydruka: 1 2 3 4 5
}

// Pętla od 10 do 1 (opadająco)
for (int i = 10; i >= 1; i--) {
    cout << i << " ";
}

// Pętla z krokiem 2
for (int i = 0; i <= 20; i += 2) {
    cout << i << " ";  // Wydruka: 0 2 4 6 8 10 12 14 16 18 20
}
```

### Pętla while

```cpp
int i = 1;
while (i <= 5) {
    cout << i << " ";
    i++;
}
// Wydruka: 1 2 3 4 5

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
// Wydruka: 1 2 3 4 5

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
// Wydruka: 1 2 3 4

// continue - przejście do następnej iteracji
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    cout << i << " ";
}
// Wydruka: 1 2 4 5
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

## Rozwiązania Ćwiczeń

### Rozwiązanie Ćwiczenia 1

```cpp
#include <iostream>
using namespace std;

int main() {
    int wiek;
    
    cout << "Podaj swój wiek: ";
    cin >> wiek;
    
    string kategoria;
    bool mozeProwadzic = false;
    
    if (wiek < 13) {
        kategoria = "Dziecko";
    }
    else if (wiek >= 13 && wiek <= 17) {
        kategoria = "Nastolatek";
    }
    else if (wiek >= 18 && wiek <= 64) {
        kategoria = "Dorosły";
        mozeProwadzic = true;
    }
    else {
        kategoria = "Senior";
        mozeProwadzic = true;
    }
    
    cout << "\n=== WYNIK ===" << endl;
    cout << "Twoja kategoria wiekowa: " << kategoria << endl;
    
    if (mozeProwadzic) {
        cout << "Uprawnienie do prowadzenia samochodu: TAK" << endl;
    }
    else {
        cout << "Uprawnienie do prowadzenia samochodu: NIE" << endl;
    }
    
    return 0;
}
```

### Rozwiązanie Ćwiczenia 2

```cpp
#include <iostream>
using namespace std;

int main() {
    int liczba;
    
    cout << "Podaj liczbę (1-10): ";
    cin >> liczba;
    
    if (liczba < 1 || liczba > 10) {
        cout << "Liczba poza zakresem!" << endl;
        return 1;
    }
    
    cout << "\nTabela mnożenia dla liczby " << liczba << ":" << endl;
    
    int suma = 0;
    for (int i = 1; i <= 10; i++) {
        int iloczyn = liczba * i;
        suma += iloczyn;
        cout << liczba << " × " << i << " = " << iloczyn << endl;
    }
    
    double srednia = suma / 10.0;  // Dzielenie przez 10.0 dla wyniku float
    
    cout << "\n=== WYNIKI ===" << endl;
    cout << "Suma iloczynów: " << suma << endl;
    cout << "Średnia arytmetyczna: " << srednia << endl;
    
    return 0;
}
```

---

## Sprawdzenie Wiedzy - Pytania do Przeanalizowania

1. Jakie są różnice między typami `int`, `float` i `double`?
2. Co to jest reszta z dzielenia (modulo) i kiedy się ją stosuje?
3. Kiedy używamy `if-else`, a kiedy `switch`?
4. Jaka jest różnica między pętlą `while` i `do-while`?
5. Co robi instrukcja `break` i `continue` wewnątrz pętli?
6. Czy wyrażenie `5 / 2` da nam `2` czy `2.5`? Dlaczego?
7. Jak działają operatory `&&`, `||` i `!`?

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
- ✓ Praktyczne ćwiczenia z rozwiązaniami
- ✓ Wskazówki do egzaminu

---

**Powodzenia w nauce i na egzaminie INF.03!**
