# 🐛 DEBUGOWANIE JAVASCRIPT - ŚCIĄGA BŁĘDÓW

## Przewodnik po błędach w konsoli przeglądarki

---

## 🔧 JAK OTWORZYĆ KONSOLĘ?

| Przeglądarka | Skrót | Alternatywa |
|--------------|-------|-------------|
| Chrome | `F12` lub `Ctrl+Shift+J` | Prawy klik → Zbadaj → Console |
| Firefox | `F12` lub `Ctrl+Shift+K` | Prawy klik → Zbadaj element → Konsola |
| Edge | `F12` lub `Ctrl+Shift+J` | Prawy klik → Zbadaj → Console |

---

## 📍 JAK CZYTAĆ BŁĄD W KONSOLI?

```
❌ Uncaught TypeError: Cannot read properties of null (reading 'innerHTML')
    at script.js:15:23
```

| Część błędu | Co oznacza |
|-------------|------------|
| `Uncaught` | Błąd nie został obsłużony (przechwycony) |
| `TypeError` | Typ błędu (zobacz listę poniżej) |
| `Cannot read properties of null` | Opis problemu |
| `(reading 'innerHTML')` | Której właściwości dotyczy |
| `at script.js:15:23` | **Plik, linia 15, znak 23** ← TU SZUKAJ! |

---

# 🔴 NAJCZĘSTSZE BŁĘDY

---

## 1. Cannot read properties of null

### Jak wygląda w konsoli:
```
❌ Uncaught TypeError: Cannot read properties of null (reading 'innerHTML')
❌ Uncaught TypeError: Cannot read properties of null (reading 'style')
❌ Uncaught TypeError: Cannot read properties of null (reading 'classList')
❌ Uncaught TypeError: Cannot read properties of null (reading 'addEventListener')
```

### Co to znaczy?
Próbujesz użyć czegoś (innerHTML, style, itp.) na elemencie, który **nie istnieje** (jest `null`).

### Możliwe przyczyny:

#### ❌ Przyczyna 1: Literówka w ID
```javascript
// W HTML: <p id="demo"></p>
// W JS:
document.getElementById('Demo').innerHTML = 'tekst';  // ❌ 'Demo' zamiast 'demo'
document.getElementById('dmo').innerHTML = 'tekst';   // ❌ literówka 'dmo'
```
✅ **Rozwiązanie:** Sprawdź czy ID w JS jest IDENTYCZNE jak w HTML (wielkość liter ma znaczenie!)

#### ❌ Przyczyna 2: Element nie istnieje w HTML
```javascript
// Próbujesz znaleźć element, którego nie ma w HTML
document.getElementById('mojElement').innerHTML = 'tekst';  // ❌ nie ma takiego ID w HTML
```
✅ **Rozwiązanie:** Sprawdź czy element z tym ID istnieje w pliku HTML

#### ❌ Przyczyna 3: Skrypt ładuje się przed HTML
```html
<head>
    <script src="script.js"></script>  <!-- ❌ Skrypt przed body! -->
</head>
<body>
    <p id="demo">Tekst</p>
</body>
```
✅ **Rozwiązanie:** Przenieś `<script>` na koniec `<body>`:
```html
<body>
    <p id="demo">Tekst</p>
    <script src="script.js"></script>  <!-- ✅ Na końcu body -->
</body>
```

#### ❌ Przyczyna 4: Brak kropki/hasha w querySelector
```javascript
document.querySelector('demo').innerHTML = 'tekst';   // ❌ brak #
document.querySelector('mojaKlasa').innerHTML = 'tekst';  // ❌ brak .
```
✅ **Rozwiązanie:**
```javascript
document.querySelector('#demo').innerHTML = 'tekst';      // ✅ z #
document.querySelector('.mojaKlasa').innerHTML = 'tekst'; // ✅ z .
```

---

## 2. Cannot read properties of undefined

### Jak wygląda w konsoli:
```
❌ Uncaught TypeError: Cannot read properties of undefined (reading 'innerHTML')
❌ Uncaught TypeError: Cannot read properties of undefined (reading 'style')
```

### Co to znaczy?
Zmienna istnieje, ale nie ma przypisanej wartości (jest `undefined`).

### Możliwe przyczyny:

#### ❌ Przyczyna 1: Zmienna zadeklarowana, ale nie przypisana
```javascript
let element;
element.innerHTML = 'tekst';  // ❌ element jest undefined
```
✅ **Rozwiązanie:**
```javascript
let element = document.getElementById('demo');
element.innerHTML = 'tekst';  // ✅
```

#### ❌ Przyczyna 2: Błędny indeks tablicy
```javascript
const lista = document.querySelectorAll('.item');  // np. 3 elementy [0,1,2]
lista[5].innerHTML = 'tekst';  // ❌ nie ma elementu o indeksie 5
```
✅ **Rozwiązanie:** Sprawdź ile elementów masz: `console.log(lista.length)`

#### ❌ Przyczyna 3: parentElement na elemencie bez rodzica
```javascript
const body = document.body;
body.parentElement.parentElement.innerHTML = 'tekst';  // ❌ za dużo parentElement
```
✅ **Rozwiązanie:** Sprawdź strukturę HTML - ile poziomów w górę możesz iść

---

## 3. X is not defined

### Jak wygląda w konsoli:
```
❌ Uncaught ReferenceError: mojaZmienna is not defined
❌ Uncaught ReferenceError: documnet is not defined
❌ Uncaught ReferenceError: getElementByld is not defined
```

### Co to znaczy?
Używasz nazwy, która **nie istnieje** - nie ma takiej zmiennej ani funkcji.

### Możliwe przyczyny:

#### ❌ Przyczyna 1: Literówka w nazwie zmiennej
```javascript
let licznik = 0;
liczik = liczik + 1;  // ❌ 'liczik' zamiast 'licznik'
```
✅ **Rozwiązanie:** Popraw literówkę

#### ❌ Przyczyna 2: Literówka w nazwie metody
```javascript
documnet.getElementById('demo');  // ❌ 'documnet' zamiast 'document'
document.getElementByld('demo');  // ❌ 'ld' zamiast 'Id'
document.queryselector('.demo');  // ❌ małe 's' zamiast 'S'
```
✅ **Rozwiązanie:**
```javascript
document.getElementById('demo');    // ✅
document.querySelector('.demo');    // ✅ duże 'S'
```

#### ❌ Przyczyna 3: Zmienna użyta przed deklaracją
```javascript
console.log(wynik);  // ❌ zmienna jeszcze nie istnieje
let wynik = 10;
```
✅ **Rozwiązanie:** Najpierw deklaracja, potem użycie

#### ❌ Przyczyna 4: Zmienna w innym zakresie (scope)
```javascript
function test() {
    let lokalnaZmienna = 5;
}
console.log(lokalnaZmienna);  // ❌ zmienna istnieje tylko w funkcji
```
✅ **Rozwiązanie:** Zadeklaruj zmienną w odpowiednim miejscu

---

## 4. X is not a function

### Jak wygląda w konsoli:
```
❌ Uncaught TypeError: document.getElementByID is not a function
❌ Uncaught TypeError: element.addEventlistener is not a function
❌ Uncaught TypeError: lista.foreach is not a function
```

### Co to znaczy?
Próbujesz wywołać coś jako funkcję, ale to **nie jest funkcja** (najczęściej literówka).

### Możliwe przyczyny:

#### ❌ Przyczyna 1: Błędna wielkość liter w nazwie metody
```javascript
document.getElementByID('demo');      // ❌ 'ID' zamiast 'Id'
document.getelementbyid('demo');      // ❌ wszystko małe
element.addEventlistener('click');    // ❌ małe 'l' w Listener
lista.foreach(function() {});         // ❌ małe 'e' w forEach
element.classlist.add('klasa');       // ❌ małe 'l' w classList
```
✅ **Rozwiązanie:**
```javascript
document.getElementById('demo');         // ✅ 'Id' nie 'ID'
element.addEventListener('click');       // ✅ 'L' w Listener
lista.forEach(function() {});            // ✅ 'E' w forEach
element.classList.add('klasa');          // ✅ 'L' w classList
```

#### ❌ Przyczyna 2: Brak nawiasów przy metodzie
```javascript
element.innerHTML();  // ❌ innerHTML to właściwość, nie funkcja!
```
✅ **Rozwiązanie:**
```javascript
element.innerHTML = 'tekst';  // ✅ bez nawiasów, to właściwość
```

#### ❌ Przyczyna 3: Pomyłka między właściwością a metodą
```javascript
element.style().color = 'red';  // ❌ style to właściwość
element.classList = 'nowa';     // ❌ classList to obiekt z metodami
```
✅ **Rozwiązanie:**
```javascript
element.style.color = 'red';        // ✅ style bez nawiasów
element.classList.add('nowa');      // ✅ classList z metodą add()
```

---

## 5. Unexpected token / Unexpected identifier

### Jak wygląda w konsoli:
```
❌ Uncaught SyntaxError: Unexpected token '}'
❌ Uncaught SyntaxError: Unexpected token ')'
❌ Uncaught SyntaxError: Unexpected identifier
❌ Uncaught SyntaxError: Unexpected string
```

### Co to znaczy?
Błąd składni - JavaScript nie rozumie Twojego kodu.

### Możliwe przyczyny:

#### ❌ Przyczyna 1: Brak przecinka między argumentami
```javascript
element.addEventListener('click' function() {});  // ❌ brak przecinka
```
✅ **Rozwiązanie:**
```javascript
element.addEventListener('click', function() {});  // ✅ z przecinkiem
```

#### ❌ Przyczyna 2: Brak cudzysłowu
```javascript
element.innerHTML = tekst;           // ❌ tekst bez cudzysłowów (szuka zmiennej)
element.style.color = red;           // ❌ red bez cudzysłowów
```
✅ **Rozwiązanie:**
```javascript
element.innerHTML = 'tekst';         // ✅ w cudzysłowach
element.style.color = 'red';         // ✅ w cudzysłowach
```

#### ❌ Przyczyna 3: Brak nawiasu zamykającego
```javascript
lista.forEach(function(el) {
    el.style.color = 'red';
}   // ❌ brak ); na końcu
```
✅ **Rozwiązanie:**
```javascript
lista.forEach(function(el) {
    el.style.color = 'red';
});  // ✅ }); zamyka forEach
```

#### ❌ Przyczyna 4: Dodatkowy przecinek
```javascript
const dane = [1, 2, 3,];  // OK w tablicy
element.style.color = 'red',;  // ❌ dodatkowy przecinek
```

---

## 6. Unexpected end of input

### Jak wygląda w konsoli:
```
❌ Uncaught SyntaxError: Unexpected end of input
```

### Co to znaczy?
Kod się "urwał" - brakuje czegoś na końcu.

### Możliwe przyczyny:

#### ❌ Przyczyna 1: Brak zamykającego nawiasu klamrowego
```javascript
function test() {
    console.log('test');
// ❌ brak }
```
✅ **Rozwiązanie:**
```javascript
function test() {
    console.log('test');
}  // ✅
```

#### ❌ Przyczyna 2: Brak zamykającego nawiasu w forEach
```javascript
lista.forEach(function(el) {
    el.style.color = 'red';
// ❌ brak });
```
✅ **Rozwiązanie:**
```javascript
lista.forEach(function(el) {
    el.style.color = 'red';
});  // ✅
```

#### ❌ Przyczyna 3: Niezamknięty string
```javascript
element.innerHTML = 'tekst bez zamknięcia
```
✅ **Rozwiązanie:**
```javascript
element.innerHTML = 'tekst z zamknięciem';  // ✅
```

---

## 7. Cannot set properties of null

### Jak wygląda w konsoli:
```
❌ Uncaught TypeError: Cannot set properties of null (setting 'innerHTML')
❌ Uncaught TypeError: Cannot set properties of null (setting 'className')
```

### Co to znaczy?
To samo co "Cannot read" - element nie istnieje, a próbujesz mu coś **przypisać**.

### Przyczyny:
Takie same jak w błędzie #1 (literówka w ID, element nie istnieje, skrypt przed HTML).

---

## 8. forEach is not a function (dla pojedynczego elementu)

### Jak wygląda w konsoli:
```
❌ Uncaught TypeError: element.forEach is not a function
```

### Co to znaczy?
Próbujesz użyć `forEach` na **pojedynczym elemencie** zamiast na liście.

### Przyczyna:
```javascript
const element = document.getElementById('demo');  // pojedynczy element
element.forEach(function() {});  // ❌ getElementById zwraca JEDEN element

const element2 = document.querySelector('.demo');  // też pojedynczy!
element2.forEach(function() {});  // ❌ querySelector zwraca JEDEN element
```
✅ **Rozwiązanie:**
```javascript
// Użyj querySelectorAll dla wielu elementów:
const elementy = document.querySelectorAll('.demo');  // lista elementów
elementy.forEach(function(el) {});  // ✅ teraz działa
```

---

# 📊 TABELA SZYBKIEGO WYSZUKIWANIA

| Błąd w konsoli | Najczęstsza przyczyna | Szybka naprawa |
|----------------|----------------------|----------------|
| `Cannot read properties of null` | Element nie istnieje | Sprawdź ID/klasę, literówki |
| `Cannot read properties of undefined` | Zmienna bez wartości | Przypisz wartość do zmiennej |
| `X is not defined` | Literówka w nazwie | Sprawdź pisownię |
| `X is not a function` | Zła wielkość liter | getElementById, querySelector, forEach |
| `Unexpected token` | Brak przecinka/cudzysłowu | Sprawdź składnię |
| `Unexpected end of input` | Brak } lub ); | Policz nawiasy |
| `forEach is not a function` | Użyto na pojedynczym elemencie | Użyj querySelectorAll |

---

# 🔍 TECHNIKI DEBUGOWANIA

## 1. console.log() - Twój najlepszy przyjaciel

```javascript
const element = document.getElementById('demo');
console.log(element);  // Sprawdź co znalazłeś (null = nie znaleziono!)

const lista = document.querySelectorAll('.item');
console.log(lista);         // Zobacz listę
console.log(lista.length);  // Ile elementów?

const wartosc = input.value;
console.log(wartosc);  // Co jest w inpucie?
console.log(typeof wartosc);  // Jaki typ? (string, number...)
```

## 2. Sprawdź krok po kroku

```javascript
// Zamiast pisać wszystko w jednej linii:
document.getElementById('demo').innerHTML = 'tekst';

// Rozłóż na kroki:
const element = document.getElementById('demo');
console.log('Znaleziony element:', element);  // Sprawdź

if (element !== null) {
    element.innerHTML = 'tekst';
} else {
    console.log('BŁĄD: Element nie znaleziony!');
}
```

## 3. Licz nawiasy!

```javascript
lista.forEach(function(element) {  // 1x ( 1x {
    element.addEventListener('click', function() {  // 2x ( 2x {
        this.classList.add('active');
    });  // zamyka addEventListener: 1x } 1x )
});  // zamyka forEach: 1x } 1x )
```

**Zasada:** Ile otworzyłeś, tyle musisz zamknąć!

---

# ✅ CHECKLIST PRZED ODDANIEM

- [ ] Otworzyłem konsolę (F12) - **czy są błędy na czerwono?**
- [ ] Sprawdziłem literówki w ID i klasach
- [ ] Sprawdziłem wielkość liter w metodach (getElementById, querySelector, forEach, addEventListener, classList)
- [ ] Używam `.` przed klasą i `#` przed ID w querySelector
- [ ] NIE używam `.` w classList.add()
- [ ] Policzyłem nawiasy - każdy otwarty ma zamknięty
- [ ] Skrypt jest NA KOŃCU body (przed `</body>`)
- [ ] Wartości tekstowe są w cudzysłowach

---

# 🆘 NADAL NIE DZIAŁA?

1. **Skopiuj CAŁY błąd** z konsoli
2. **Znajdź linię** wskazaną w błędzie (np. `script.js:15`)
3. **Przeczytaj kod** w tej linii i linii powyżej
4. **Porównaj** z przykładami z lekcji
5. **Poproś o pomoc** nauczyciela pokazując błąd i kod

---

**Pamiętaj: Każdy programista popełnia błędy. Różnica polega na umiejętności ich znajdowania i naprawiania! 🐛→🦋**
