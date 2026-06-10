# 📘 Repetytorium PHP – Egzamin Zawodowy INF.03
**Cel:** Szybka powtórka zagadnień PHP, które najczęściej występują w pytaniach testowych.

## 1. Podstawy PHP
PHP to język skryptowy wykonywany **po stronie serwera** – HTML zostaje wygenerowany dla klienta.

*   **Tag PHP:** `<?php ... ?>` – kod wewnątrz tych tagów jest wykonywany na serwerze
*   **Zmienne:** `$nazwa_zmiennej` – zawsze zaczynają się od `$`
*   **Komentarze:**
    *   Jednoliniowy: `// komentarz`
    *   Wieloliniowy: `/* komentarz */`

> **Typowe pytanie:** "Gdzie jest wykonywany kod PHP – na kliencie czy na serwerze?"
> **Odp:** Na serwerze. Klient otrzymuje tylko wygenerowany HTML.

## 2. Zmienne i Typy Danych
Egzamin pyta o typy danych i operacje na zmiennych.

*   **Typy danych w PHP:**
    *   `string` – tekst `"Hello"`
    *   `int` – liczba całkowita `123`
    *   `float` – liczba zmiennoprzecinkowa `3.14`
    *   `boolean` – `true` lub `false`
    *   `array` – tablica `[1, 2, 3]`
    *   `NULL` – brak wartości

*   **Zmienne specjalne:**
    *   `$_GET` – dane przesłane metodą GET (widoczne w URL)
    *   `$_POST` – dane przesłane metodą POST (ukryte)
    *   `$_REQUEST` – zarówno GET jak i POST
    *   `$_SESSION` – sesja użytkownika
    *   `$_SERVER` – informacje o serwerze
    *   `$_FILES` – przesłane pliki

> **Typowe pytanie:** "Do czego służy zmienna `$_POST`?"
> **Odp:** Do przechowywania danych przesłanych z formularza metodą POST.

## 3. Operatory
Podstawowe operacje w PHP.

| Operator | Opis | Przykład |
|:---------|:-----|:---------|
| `+` | Dodawanie | `5 + 3` = 8 |
| `-` | Odejmowanie | `5 - 3` = 2 |
| `*` | Mnożenie | `5 * 3` = 15 |
| `/` | Dzielenie | `6 / 2` = 3 |
| `%` | Reszta z dzielenia | `7 % 3` = 1 |
| `.` | Konkatenacja (łączenie tekstów) | `"Hej " . "Ty"` = "Hej Ty" |
| `=` | Przypisanie | `$x = 5` |
| `==` | Porównanie wartości | `5 == "5"` = true |
| `===` | Porównanie wartości i typu | `5 === "5"` = false |
| `!=` | Różne | `5 != 3` = true |
| `>`, `<`, `>=`, `<=` | Porównanie | `5 > 3` = true |
| `&&` | Logiczne AND | `true && true` = true |
| `\|\|` | Logiczne OR | `true \|\| false` = true |
| `!` | Logiczne NOT | `!true` = false |
| `++` | Inkrementacja | `$x++` lub `++$x` |
| `--` | Dekrementacja | `$x--` lub `--$x` |
| `.=` | Konkatenacja do zmiennej | `$x .= "tekst"` |
| `+=` | Dodaj do zmiennej | `$x += 5` |

## 4. Łańcuchy Znaków (Strings)
Pracy z tekstem jest wiele na egzaminie.

```php
$tekst = "Hello World";

// Uwaga: '' vs ""
$zmienna = "Jan";
echo "Cześć $zmienna";          // Cześć Jan
echo 'Cześć $zmienna';          // Cześć $zmienna (nie interpoluje!)

// Funkcje stringowe:
strlen($tekst);                 // Długość: 11
strtoupper($tekst);             // HELLO WORLD
strtolower($tekst);             // hello world
str_replace("World", "PHP", $tekst);  // Hello PHP
substr($tekst, 0, 5);           // Hello (znaki 0-4)
strpos($tekst, "World");        // Pozycja: 6
explode(" ", $tekst);           // Tablica: ["Hello", "World"]
implode(" ", $tablica);         // String: "Hello World"
trim($tekst);                   // Usuń spacje z początku/końca
```

## 5. Warunki (IF, ELSE, ELSEIF)
Sterowanie przepływem programu.

```php
$wiek = 25;

if ($wiek >= 18) {
    echo "Jesteś pełnoletni";
} elseif ($wiek >= 13) {
    echo "Jesteś nastolatkiem";
} else {
    echo "Jesteś dzieckiem";
}

// Skrót (ternary operator):
$status = ($wiek >= 18) ? "Pełnoletni" : "Niepełnoletni";
```

## 6. Pętle
Powtarzanie kodu – bardzo ważne zagadnienie.

*   **Pętla `while`:**
    ```php
    $i = 0;
    while ($i < 5) {
        echo $i;
        $i++;
    }
    ```

*   **Pętla `do...while`** (wykonuje się przynajmniej raz):
    ```php
    $i = 0;
    do {
        echo $i;
        $i++;
    } while ($i < 5);
    ```

*   **Pętla `for`:**
    ```php
    for ($i = 0; $i < 5; $i++) {
        echo $i;
    }
    ```

*   **Pętla `foreach`** (dla tablic):
    ```php
    $tablica = ["Jan", "Maria", "Piotr"];
    foreach ($tablica as $osoba) {
        echo $osoba;
    }
    
    // Z indeksem:
    foreach ($tablica as $index => $osoba) {
        echo "$index: $osoba";
    }
    ```

*   **Break i Continue:**
    ```php
    for ($i = 0; $i < 10; $i++) {
        if ($i == 5) break;       // Wyjście z pętli
        if ($i == 3) continue;    // Pomiń bieżącą iterację
        echo $i;
    }
    ```

## 7. Tablice (Arrays)
Bardzo ważne zagadnienie na egzaminie.

```php
// Tablica indeksowana (numeryczna):
$owoce = ["Jabłko", "Gruszka", "Banan"];
echo $owoce[0];                 // Jabłko
$owoce[] = "Pomarańcza";        // Dodaj na koniec
array_push($owoce, "Kiwi");     // Dodaj element
array_pop($owoce);              // Usuń ostatni
count($owoce);                  // Ilość elementów

// Tablica asocjacyjna (z kluczami):
$osoba = [
    "imie" => "Jan",
    "nazwisko" => "Kowalski",
    "wiek" => 25
];
echo $osoba["imie"];            // Jan
$osoba["miasto"] = "Kraków";    // Dodaj klucz

// Funkcje do tablic:
in_array("Jan", $tablica);      // Czy element istnieje?
array_key_exists("imie", $osoba);  // Czy klucz istnieje?
array_keys($osoba);             // Lista kluczy
array_values($osoba);           // Lista wartości
array_merge($tab1, $tab2);      // Połącz dwie tablice
sort($tablica);                 // Sortuj rosnąco
rsort($tablica);                // Sortuj malejąco
```

## 8. Funkcje
Organizacja kodu – duże znaczenie na egzaminie.

```php
// Definicja funkcji:
function powitaj($imie) {
    return "Cześć $imie!";
}

echo powitaj("Jan");            // Cześć Jan!

// Funkcja z domyślnym argumentem:
function powitaj($imie = "Gość") {
    return "Cześć $imie!";
}

// Funkcja z wieloma argumentami:
function dodaj($a, $b) {
    return $a + $b;
}

echo dodaj(3, 5);               // 8

// Funkcja zwracająca tablicę:
function pobierz_dane() {
    return ["Jan", "Kowalski", 25];
}

list($imie, $nazwisko, $wiek) = pobierz_dane();
```

## 9. Połączenie z Bazą Danych
Bardzo ważny temat – prawie zawsze pojawia się na egzaminie.

```php
// Połączenie (MySQLi proceduralne):
$polaczenie = mysqli_connect("localhost", "root", "", "moja_baza");

// Sprawdzenie połączenia:
if (!$polaczenie) {
    die("Błąd połączenia: " . mysqli_connect_error());
}

// Zapytanie SELECT:
$wynik = mysqli_query($polaczenie, "SELECT * FROM studenci");

// Pobranie wyniku - wierszami:
while ($wiersz = mysqli_fetch_array($wynik)) {
    echo $wiersz["imie"] . " " . $wiersz["nazwisko"];
}

// Albo pobranie jednego wiersza:
$wiersz = mysqli_fetch_assoc($wynik);
echo $wiersz["imie"];

// Ilość wierszy:
$liczba_wierszy = mysqli_num_rows($wynik);

// Zapytanie INSERT:
$sql = "INSERT INTO studenci (imie, nazwisko) VALUES ('Jan', 'Kowalski')";
mysqli_query($polaczenie, $sql);

// Zapytanie UPDATE:
$sql = "UPDATE studenci SET imie='Janusz' WHERE id=1";
mysqli_query($polaczenie, $sql);

// Zapytanie DELETE:
$sql = "DELETE FROM studenci WHERE id=1";
mysqli_query($polaczenie, $sql);

// Zamknięcie połączenia:
mysqli_close($polaczenie);
```

> **Typowe pytanie:** "Jaka funkcja pobiera następny wiersz z wyniku zapytania?"
> **Odp:** `mysqli_fetch_array()` lub `mysqli_fetch_assoc()`.

## 10. Formularze i Metody GET/POST
Najczęstsze pytania egzaminacyjne.

**HTML (formularz):**
```html
<form action="obsluga.php" method="POST">
    Imię: <input type="text" name="imie"><br>
    Email: <input type="email" name="email"><br>
    <input type="submit" value="Wyślij">
</form>
```

**PHP (obsluga.php):**
```php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $imie = $_POST["imie"];
    $email = $_POST["email"];
    
    echo "Cześć $imie, twój email to $email";
}
```

| Właściwość | GET | POST |
|:-----------|:---|:-----|
| Widoczność danych | W URL (publiczna) | Ukryta (prywatna) |
| Limit rozmiaru | ~2000 znaków | Brak limitu |
| Zastosowanie | Filtry, wyszukiwanie | Hasła, dane sensytywne |
| Bezpieczeństwo | Słabe | Lepsze |

## 11. Walidacja i Bezpieczeństwo
Bardzo ważne na egzaminie.

```php
// Sprawdzenie, czy zmienna istnieje:
if (isset($_POST["imie"])) {
    $imie = $_POST["imie"];
}

// Sprawdzenie, czy nie jest pusta:
if (!empty($_POST["imie"])) {
    $imie = trim($_POST["imie"]);
}

// Usunięcie złośliwych znaków (XSS ochrona):
$imie = htmlspecialchars($_POST["imie"]);

// Walidacja emaila:
if (!filter_var($_POST["email"], FILTER_VALIDATE_EMAIL)) {
    echo "Błędny email!";
}

// Ochrona przed SQL Injection (przygotowane zapytania):
$stmt = $polaczenie->prepare("INSERT INTO studenci (imie) VALUES (?)");
$stmt->bind_param("s", $imie);
$stmt->execute();
```

## 12. Sesje
Przechowywanie danych dla użytkownika – czasem pojawia się.

```php
// Na początku strony:
session_start();

// Ustawienie zmiennej sesji:
$_SESSION["uzytkownik"] = "Jan";
$_SESSION["id"] = 123;

// Pobranie:
echo $_SESSION["uzytkownik"];   // Jan

// Usunięcie zmiennej:
unset($_SESSION["uzytkownik"]);

// Wyczyszczenie sesji:
session_destroy();
```

## 13. Ciasteczka (Cookies)
Rzadsze, ale mogą się pojawić.

```php
// Ustawienie ciasteczka:
setcookie("uzytkownik", "Jan", time() + 3600, "/");

// Pobranie:
echo $_COOKIE["uzytkownik"];    // Jan

// Usunięcie:
setcookie("uzytkownik", "", time() - 3600, "/");
```

## 14. Pliki
Operacje na plikach – czasem w pytaniach.

```php
// Czytanie pliku:
$zawartosc = file_get_contents("plik.txt");
$linie = file("plik.txt");     // Tablica linii

// Pisanie do pliku:
file_put_contents("plik.txt", "Nowa zawartość");

// Dołączanie do pliku:
file_put_contents("plik.txt", "Nowa linia\n", FILE_APPEND);

// Sprawdzenie, czy plik istnieje:
if (file_exists("plik.txt")) {
    // ...
}

// Usuwanie pliku:
unlink("plik.txt");

// Przesyłanie pliku:
if (isset($_FILES["plik"])) {
    $nazwa = $_FILES["plik"]["name"];
    $tmp = $_FILES["plik"]["tmp_name"];
    $blad = $_FILES["plik"]["error"];
    
    if ($blad == 0) {
        move_uploaded_file($tmp, "uploads/" . $nazwa);
    }
}
```

## 15. Przekierowania
Czasem pojawia się na egzaminie.

```php
// Przekierowanie na inną stronę:
header("Location: strona.php");
exit();

// Setowanie nagłówka:
header("Content-Type: text/html; charset=utf-8");
```

## 16. Funkcje Wbudowane (Built-in Functions)
PHP ma wiele użytecznych funkcji.

```php
// Matematyka:
abs(-5);                        // 5
round(3.7);                     // 4
ceil(3.2);                      // 4
floor(3.8);                     // 3
sqrt(16);                       // 4
pow(2, 3);                      // 8
rand(1, 100);                   // Losowa liczba

// Data i czas:
date("Y-m-d");                  // 2025-12-01
time();                         // Czas UNIX
strtotime("2025-12-01");        // UNIX timestamp daty

// Typ danych:
is_string($x);                  // Czy string?
is_int($x);                     // Czy int?
is_array($x);                   // Czy tablica?
gettype($x);                    // Zwróć typ

// Konwersja:
(int)"123";                     // Zamień na int
(string)456;                    // Zamień na string
```

## 17. Pętla Foreach z Bazą Danych
Najczęstszy kod na egzaminie.

```php
$polaczenie = mysqli_connect("localhost", "root", "", "moja_baza");
$wynik = mysqli_query($polaczenie, "SELECT * FROM studenci");

?>
<table>
    <tr>
        <th>ID</th>
        <th>Imię</th>
        <th>Nazwisko</th>
    </tr>
    <?php
    while ($wiersz = mysqli_fetch_assoc($wynik)) {
        ?>
        <tr>
            <td><?php echo $wiersz["id"]; ?></td>
            <td><?php echo $wiersz["imie"]; ?></td>
            <td><?php echo $wiersz["nazwisko"]; ?></td>
        </tr>
        <?php
    }
mysqli_close($polaczenie);
    ?>
</table>

mysqli_close($polaczenie);
```

## 18. Obsługa Błędów
Czasem pojawia się w praktyce.

```php
// Proste sprawdzenie:
if ($wynik === FALSE) {
    echo "Błąd zapytania: " . mysqli_error($polaczenie);
}

// Try-catch (zaawansowane):
try {
    // Kod, który może rzucić błąd
    if (empty($_POST["imie"])) {
        throw new Exception("Imię jest wymagane!");
    }
} catch (Exception $e) {
    echo "Błąd: " . $e->getMessage();
}
```

---

### 🔥 Szybki test wiedzy (Sprawdź się!)

1.  **Pytanie:** Gdzie jest wykonywany kod PHP?
    *   **Odp:** Na serwerze. Klient otrzymuje tylko HTML.

2.  **Pytanie:** Jaka jest różnica między `==` a `===` w PHP?
    *   **Odp:** `==` porównuje wartość, `===` porównuje wartość i typ (5 == "5" to true, ale 5 === "5" to false).

3.  **Pytanie:** Do czego służy funkcja `mysqli_connect()`?
    *   **Odp:** Do nawiązania połączenia z bazą danych.

4.  **Pytanie:** Jak przesłać dane z formularza metodą POST?
    *   **Odp:** `<form method="POST" action="...">` a potem `$_POST["nazwa"]`.

5.  **Pytanie:** Jaka pętla powtarza się dla każdego elementu tablicy?
    *   **Odp:** `foreach ($tablica as $element) { ... }`

6.  **Pytanie:** Jak usunąć spacje z początku i końca stringa?
    *   **Odp:** `trim($string)`

7.  **Pytanie:** Jaka funkcja pobiera wszystkie wiersze wyniku zapytania?
    *   **Odp:** `mysqli_fetch_array()` w pętli while lub `mysqli_fetch_assoc()`.

8.  **Pytanie:** Jak sprawdzić, czy zmienna POST istnieje?
    *   **Odp:** `isset($_POST["nazwa"])` lub `!empty($_POST["nazwa"])`

### Jak korzystać z bazy pytań?
Rozwiązując testy na zawodowe.edu.pl:
1.  **Czytaj kod PHP uważnie** – zwróć uwagę na zmienne `$_POST`, `$_GET`, `$_SESSION`
2.  **Testuj w praktyce** – twórz skrypty PHP i sprawdzaj wyniki
3.  **Zapamiętaj funkcje do baz** – `mysqli_connect()`, `mysqli_query()`, `mysqli_fetch_assoc()`
4.  **Ćwicz pętle** – szczególnie `foreach` z bazą danych
5.  **Zrozum przepływ** – formularz HTML → $_POST → PHP → MySQL → wynik
6.  **Zwróć uwagę na bezpieczeństwo** – walidacja i czyszczenie danych
