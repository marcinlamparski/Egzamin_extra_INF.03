# 📘 Repetytorium JavaScript – Egzamin Zawodowy INF.03
**Cel:** Szybka powtórka zagadnień JavaScript, które najczęściej występują w pytaniach testowych.

## 1. Podstawy JavaScript
JavaScript to język wykonywany **po stronie klienta** (w przeglądarce), przeciwnie do PHP (serwer).

*   **Gdzie umieścić kod JavaScript:**
    *   W tagu `<script>` w HTML: `<script> ... </script>`
    *   W atrybucie `onclick`: `<button onclick="funkcja()">Kliknij</button>`
    *   W zewnętrznym pliku: `<script src="skrypt.js"></script>`

*   **Komentarze:**
    *   Jednoliniowy: `// komentarz`
    *   Wieloliniowy: `/* komentarz */`

*   **Instrukcja `console.log()`:**
    *   Wypisuje wartość do konsoli przeglądarki (F12)
    *   Przydatna do debugowania

> **Typowe pytanie:** "Gdzie jest wykonywany kod JavaScript – na kliencie czy na serwerze?"
> **Odp:** Po stronie klienta (w przeglądarce).

## 2. Zmienne i Typy Danych
Fundamenty każdego języka programowania.

*   **Deklaracja zmiennych:**
    *   `var imie = "Jan";` – stara metoda (unikać)
    *   `let imie = "Jan";` – nowa metoda (zalecana)
    *   `const PI = 3.14;` – stała (nie można zmienić)

*   **Typy danych:**
    *   `string` – tekst `"Hello"` lub `'Hello'`
    *   `number` – liczba `123` lub `3.14`
    *   `boolean` – `true` lub `false`
    *   `undefined` – zmienna bez wartości
    *   `null` – brak wartości (przypisane)
    *   `object` – obiekt `{}`
    *   `array` – tablica `[]`

```javascript
typeof "Jan";               // "string"
typeof 25;                  // "number"
typeof true;                // "boolean"
typeof undefined;           // "undefined"
```

## 3. Operatory
Podstawowe operacje.

| Operator | Opis | Przykład |
|:---------|:-----|:---------|
| `+` | Dodawanie / konkatenacja | `5 + 3` = 8, `"Hej " + "Ty"` = "Hej Ty" |
| `-` | Odejmowanie | `5 - 3` = 2 |
| `*` | Mnożenie | `5 * 3` = 15 |
| `/` | Dzielenie | `6 / 2` = 3 |
| `%` | Reszta z dzielenia | `7 % 3` = 1 |
| `**` | Potęga | `2 ** 3` = 8 |
| `=` | Przypisanie | `x = 5` |
| `==` | Porównanie wartości | `5 == "5"` = true |
| `===` | Porównanie wartości i typu | `5 === "5"` = false |
| `!=` | Różne | `5 != 3` = true |
| `!==` | Różne (typ i wartość) | `5 !== "5"` = true |
| `>`, `<`, `>=`, `<=` | Porównanie | `5 > 3` = true |
| `&&` | Logiczne AND | `true && true` = true |
| `\|\|` | Logiczne OR | `true \|\| false` = true |
| `!` | Logiczne NOT | `!true` = false |
| `++` | Inkrementacja | `x++` lub `++x` |
| `--` | Dekrementacja | `x--` lub `--x` |
| `+=` | Dodaj do zmiennej | `x += 5` |
| `-=` | Odejmij od zmiennej | `x -= 3` |
| `.=` lub `+=` | Konkatenacja | `tekst += " dodatkowy"` |

## 4. Łańcuchy Znaków (Strings)
Praca z tekstem – bardzo ważne na egzaminie.

```javascript
let tekst = "Hello World";

// Funkcje stringowe:
tekst.length;                           // 11
tekst.toUpperCase();                    // HELLO WORLD
tekst.toLowerCase();                    // hello world
tekst.indexOf("World");                 // 6 (pozycja)
tekst.substring(0, 5);                  // Hello (od 0 do 4)
tekst.slice(6);                         // World (od 6 do końca)
tekst.replace("World", "JavaScript");   // Hello JavaScript
tekst.split(" ");                       // ["Hello", "World"]
tekst.trim();                           // Usuń spacje z początku/końca
tekst.charAt(0);                        // H (znak na pozycji 0)
tekst.charCodeAt(0);                    // 72 (kod ASCII)

// Szablony (template literals):
let imie = "Jan";
let wiek = 25;
console.log(`Mam na imię ${imie} i mam ${wiek} lat`);
```

## 5. Warunki (IF, ELSE, ELSE IF)
Sterowanie przepływem programu.

```javascript
let wiek = 25;

if (wiek >= 18) {
    console.log("Jesteś pełnoletni");
} else if (wiek >= 13) {
    console.log("Jesteś nastolatkiem");
} else {
    console.log("Jesteś dzieckiem");
}

// Skrót (ternary operator):
let status = (wiek >= 18) ? "Pełnoletni" : "Niepełnoletni";

// Switch:
switch (wiek) {
    case 18:
        console.log("Właśnie osiągnęła pełnoletniość!");
        break;
    case 25:
        console.log("Masz 25 lat");
        break;
    default:
        console.log("Inny wiek");
}
```

## 6. Pętle
Powtarzanie kodu – zawsze pojawia się na egzaminie.

*   **Pętla `while`:**
    ```javascript
    let i = 0;
    while (i < 5) {
        console.log(i);
        i++;
    }
    ```

*   **Pętla `do...while`** (wykonuje się przynajmniej raz):
    ```javascript
    let i = 0;
    do {
        console.log(i);
        i++;
    } while (i < 5);
    ```

*   **Pętla `for`:**
    ```javascript
    for (let i = 0; i < 5; i++) {
        console.log(i);
    }
    ```

*   **Pętla `for...of`** (dla tablic):
    ```javascript
    let tablica = ["Jan", "Maria", "Piotr"];
    for (let osoba of tablica) {
        console.log(osoba);
    }
    ```

*   **Pętla `for...in`** (dla obiektów):
    ```javascript
    let osoba = {imie: "Jan", nazwisko: "Kowalski", wiek: 25};
    for (let klucz in osoba) {
        console.log(klucz + ": " + osoba[klucz]);
    }
    ```

*   **Break i Continue:**
    ```javascript
    for (let i = 0; i < 10; i++) {
        if (i == 5) break;       // Wyjście z pętli
        if (i == 3) continue;    // Pomiń bieżącą iterację
        console.log(i);
    }
    ```

## 7. Tablice (Arrays)
Bardzo ważne zagadnienie.

```javascript
// Tworzenie:
let tablica = [1, 2, 3, 4, 5];
let tablica2 = new Array(1, 2, 3);

// Dostęp do elementów:
console.log(tablica[0]);        // 1
console.log(tablica.length);    // 5

// Modyfikacja:
tablica[0] = 10;                // Zmień pierwszy element
tablica.push(6);                // Dodaj na koniec: [1,2,3,4,5,6]
tablica.pop();                  // Usuń ostatni: [1,2,3,4,5]
tablica.shift();                // Usuń pierwszy: [2,3,4,5]
tablica.unshift(0);             // Dodaj na początek: [0,2,3,4,5]

// Funkcje tablicowe:
tablica.indexOf(3);             // 2 (pozycja)
tablica.includes(3);            // true (czy istnieje)
tablica.slice(1, 3);            // [2, 3] (od 1 do 2)
tablica.splice(1, 1, "X");      // Usuń 1 element od pozycji 1 i wstaw "X"
tablica.join(", ");             // "0, 2, 3, 4, 5" (połącz w string)
tablica.reverse();              // [5, 4, 3, 2, 0] (odwróć)
tablica.sort();                 // Sortuj

// Iteracja po tablicy:
tablica.forEach(function(element) {
    console.log(element);
});

// Map (transformacja tablicy):
let kwadrata = tablica.map(x => x * x);

// Filter (filtrowanie):
let parzyste = tablica.filter(x => x % 2 == 0);

// Reduce (złożenie):
let suma = tablica.reduce((a, b) => a + b, 0);
```

## 8. Obiekty
Struktury danych zawierające klucz-wartość.

```javascript
// Tworzenie obiektu:
let osoba = {
    imie: "Jan",
    nazwisko: "Kowalski",
    wiek: 25,
    greet: function() {
        return "Cześć, jestem " + this.imie;
    }
};

// Dostęp:
console.log(osoba.imie);        // Jan
console.log(osoba["nazwisko"]); // Kowalski

// Modyfikacja:
osoba.wiek = 26;
osoba.miasto = "Kraków";        // Dodaj nowe pole

// Usunięcie:
delete osoba.wiek;

// Metody:
console.log(osoba.greet());     // Cześć, jestem Jan
```

## 9. Funkcje
Organizacja kodu.

```javascript
// Deklaracja funkcji:
function dodaj(a, b) {
    return a + b;
}

console.log(dodaj(3, 5));       // 8

// Funkcja anonimowa:
let mnozenie = function(a, b) {
    return a * b;
};

console.log(mnozenie(4, 5));    // 20

// Arrow function (strzałkowa - nowoczesna):
let potegowanie = (a, b) => a ** b;
console.log(potegowanie(2, 3)); // 8

// Domyślne argumenty:
function powitaj(imie = "Gość") {
    return "Cześć " + imie;
}

console.log(powitaj());         // Cześć Gość
console.log(powitaj("Jan"));    // Cześć Jan

// Zwrócenie wielu wartości:
function pobierz_dane() {
    return [25, "Jan", "Kowalski"];
}

let [wiek, imie, nazwisko] = pobierz_dane();
```

## 10. DOM (Document Object Model) – BARDZO WAŻNE!
Manipulacja elementami HTML – jedno z najczęstszych pytań.

```javascript
// Pobranie elementu:
document.getElementById("moj_id");           // Po ID
document.getElementsByClassName("klasa");   // Po klasie
document.querySelector(".klasa");           // Selektor CSS
document.querySelectorAll("p");              // Wszystkie <p>

// Zmiana zawartości:
document.getElementById("id").innerHTML = "Nowa zawartość";
document.getElementById("id").innerText = "Nowy tekst";

// Zmiana atrybutów:
document.getElementById("id").setAttribute("src", "obraz.jpg");
document.getElementById("id").getAttribute("class");

// Zmiana stylów:
document.getElementById("id").style.color = "red";
document.getElementById("id").style.fontSize = "20px";
document.getElementById("id").style.display = "none";  // Ukrycie

// Dodawanie/usuwanie klasy CSS:
document.getElementById("id").classList.add("aktywny");
document.getElementById("id").classList.remove("aktywny");
document.getElementById("id").classList.toggle("aktywny");

// Tworzenie i usuwanie elementów:
let div = document.createElement("div");
div.innerHTML = "Nowy element";
document.body.appendChild(div);  // Dodaj do body
div.remove();                    // Usuń element

// Przechodzenie po drzewie DOM:
element.parentElement;           // Rodzic
element.children;                // Dzieci (tablica)
element.firstChild;              // Pierwsze dziecko
element.lastChild;               // Ostatnie dziecko
```

## 11. Zdarzenia (Events)
Bardzo ważne dla interaktywności.

```javascript
// W HTML:
<button onclick="funkcja()">Kliknij</button>

// W JavaScript:
document.getElementById("przycisk").addEventListener("click", function() {
    console.log("Kliknięto!");
});

// Popularne zdarzenia:
// - click: kliknięcie
// - dblclick: dwukrotne kliknięcie
// - mouseover: najechanie myszą
// - mouseout: zjechanie myszą
// - mousemove: ruch myszy
// - keydown: wciśnięcie klawisza
// - keyup: zwolnienie klawisza
// - change: zmiana wartości (input, select)
// - submit: wysłanie formularza
// - load: wczytanie strony
// - resize: zmiana rozmiaru okna

// Exempli gratia:
document.getElementById("input").addEventListener("change", function(event) {
    console.log(event.target.value);  // Wartość pola input
});
```

## 12. Formularze
Walidacja i obsługa formularzy.

```html
<form id="moj_formularz">
    Imię: <input type="text" id="imie" required><br>
    Email: <input type="email" id="email" required><br>
    <input type="submit" value="Wyślij">
</form>
```

```javascript
document.getElementById("moj_formularz").addEventListener("submit", function(event) {
    event.preventDefault();  // Zapobiegaj domyślnej akcji
    
    let imie = document.getElementById("imie").value;
    let email = document.getElementById("email").value;
    
    if (imie == "" || email == "") {
        alert("Wypełnij wszystkie pola!");
        return;
    }
    
    console.log("Formularz wysłany: " + imie + " (" + email + ")");
    // Tutaj wysyłamy dane...
});

// Pobieranie wartości pola:
let wartość = document.getElementById("input").value;

// Czyszczenie pola:
document.getElementById("input").value = "";

// Ustawienie wartości domyślnej:
document.getElementById("input").value = "wartość domyślna";
```

## 13. AJAX (XMLHttpRequest)
Wysyłanie danych bez przeładowania strony – czasem pojawia się.

```javascript
// Fetch API (nowoczesne):
fetch("plik.php", {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({imie: "Jan", wiek: 25})
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error(error));

// XMLHttpRequest (stare):
let xhr = new XMLHttpRequest();
xhr.open("GET", "plik.php", true);
xhr.onload = function() {
    if (xhr.status === 200) {
        console.log(xhr.responseText);
    }
};
xhr.send();
```

## 14. JSON
Wymiana danych w formacie tekstowym.

```javascript
// Zamiana obiektu na JSON:
let osoba = {imie: "Jan", wiek: 25};
let json_string = JSON.stringify(osoba);
// {"imie":"Jan","wiek":25}

// Zamiana JSON na obiekt:
let json_text = '{"imie":"Jan","wiek":25}';
let obiekt = JSON.parse(json_text);
console.log(obiekt.imie);  // Jan
```

## 15. Walidacja Formularzy (HTML5)
HTML5 ma wbudowaną walidację.

```html
<form>
    <input type="email" required>
    <input type="number" min="0" max="100">
    <input type="text" minlength="3" maxlength="50">
    <input type="password" required>
    <button type="submit">Wyślij</button>
</form>
```

JavaScript walidacja:
```javascript
let input = document.getElementById("email");

// Sprawdzenie validity:
if (input.validity.valid) {
    console.log("Email jest poprawny");
} else if (input.validity.typeMismatch) {
    console.log("To nie jest email");
} else if (input.validity.valueMissing) {
    console.log("Pole jest wymagane");
}

// Własna wiadomość:
input.setCustomValidity("Błędna wartość!");
```

## 16. Timing Events
Opóźnianie i powtarzanie – czasem pojawia się.

```javascript
// setTimeout - wykonaj po określonym czasie:
setTimeout(function() {
    console.log("Wykonane po 2 sekundach");
}, 2000);

// setInterval - wykonuj co określony czas:
let licznik = 0;
let interval = setInterval(function() {
    licznik++;
    console.log("Iteracja: " + licznik);
    if (licznik == 5) {
        clearInterval(interval);  // Zatrzymaj
    }
}, 1000);

// clearTimeout - anuluj timeout:
let timeout = setTimeout(() => console.log("Timeout"), 5000);
clearTimeout(timeout);  // Anuluj
```

## 17. String Methods (Metody Stringowe)
Dodatkowe operacje na tekstach.

```javascript
let tekst = "Hello World";

tekst.includes("World");        // true
tekst.startsWith("Hello");      // true
tekst.endsWith("World");        // true
tekst.repeat(2);                // Hello WorldHello World
tekst.padStart(15, "-");        // ----Hello World
tekst.padEnd(15, "-");          // Hello World----
```

## 18. Liczby i Math
Operacje matematyczne.

```javascript
// Funkcje Math:
Math.abs(-5);                   // 5
Math.round(3.7);                // 4
Math.floor(3.8);                // 3
Math.ceil(3.2);                 // 4
Math.max(1, 5, 3);              // 5
Math.min(1, 5, 3);              // 1
Math.sqrt(16);                  // 4
Math.pow(2, 3);                 // 8
Math.random();                  // 0-1

// Losowa liczba 1-10:
let losowa = Math.floor(Math.random() * 10) + 1;

// Konwersja na liczbę:
Number("123");                  // 123
parseInt("123.45");             // 123
parseFloat("123.45");           // 123.45
```

## 19. localStorage i sessionStorage
Przechowywanie danych w przeglądarce – rzadko, ale może się pojawić.

```javascript
// Zapisanie:
localStorage.setItem("uzytkownik", "Jan");

// Pobranie:
let uzytkownik = localStorage.getItem("uzytkownik");

// Usunięcie:
localStorage.removeItem("uzytkownik");

// Wyczyszczenie wszystkiego:
localStorage.clear();

// SessionStorage (chwilowe, usuwa się po zamknięciu przeglądarki):
sessionStorage.setItem("temp", "wartość");
```

## 20. Klasy (Class) – Zaawansowane
Nowoczesne podejście do programowania obiektowego.

```javascript
class Pracownik {
    constructor(imie, stanowisko) {
        this.imie = imie;
        this.stanowisko = stanowisko;
    }
    
    przedstawSie() {
        return `Jestem ${this.imie} i pracuję jako ${this.stanowisko}`;
    }
}

let pracownik = new Pracownik("Jan", "Programista");
console.log(pracownik.przedstawSie());
```

---

### 🔥 Szybki test wiedzy (Sprawdź się!)

1.  **Pytanie:** Gdzie jest wykonywany kod JavaScript?
    *   **Odp:** Po stronie klienta (w przeglądarce).

2.  **Pytanie:** Jaka jest różnica między `let` a `var`?
    *   **Odp:** `let` ma zasięg blokowy, `var` ma zasięg funkcyjny. `let` jest zalecane.

3.  **Pytanie:** Jak pobrać element HTML o ID "moj_id"?
    *   **Odp:** `document.getElementById("moj_id")`

4.  **Pytanie:** Jak zmienić tekst elementu?
    *   **Odp:** `element.innerHTML = "nowy tekst"` lub `element.innerText = "nowy tekst"`

5.  **Pytanie:** Jaka pętla iteruje po każdym elemencie tablicy?
    *   **Odp:** `for...of` lub `forEach()`

6.  **Pytanie:** Jak dodać listener do zdarzenia kliknięcia?
    *   **Odp:** `element.addEventListener("click", function() { ... })`

7.  **Pytanie:** Jakie są różne sposoby deklaracji funkcji?
    *   **Odp:** `function nazwa() {}`, `let nazwa = function() {}`, `let nazwa = () => {}`

8.  **Pytanie:** Jak sprawdzić, czy string zawiera określoną wartość?
    *   **Odp:** `string.includes("wartość")`

### Jak korzystać z bazy pytań?
Rozwiązując testy na zawodowe.edu.pl:
1.  **Zwróć uwagę na manipulację DOM** – to najczęstsza kategoria pytań
2.  **Testuj kod w przeglądarce** – F12 → Console
3.  **Zapamiętaj zdarzenia** – click, change, submit, keydown
4.  **Ćwicz pętle i tablice** – najczęściej pytane struktury
5.  **Rozumiej przepływ** – HTML → zdarzenie → JavaScript → zmiana DOM
6.  **Praktykuj formularze** – pobieranie wartości, walidacja, wysyłanie
