# Zbiór zadań JavaScript dla egzaminu INF.03 - WERSJA ŁATWA (Z ODPOWIEDZIAMI)

## Instrukcja

Poniżej znajduje się **10 zadań** na łatwiejszym poziomie trudności wraz z **pełnymi kodami do skopiowania**. Każdy kod jest gotowy do uruchomienia w przeglądarce.

---

## ZADANIE 1: Powitanie - Pierwsze JavaScript

### Opis:
Stwórz stronę, która wyświetli powitanie z wpisanym imieniem.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Powitanie</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .container { max-width: 400px; margin: 0 auto; }
        input { padding: 10px; width: 100%; box-sizing: border-box; margin: 10px 0; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        #wynik { margin-top: 20px; font-size: 18px; font-weight: bold; color: #28a745; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Witaj!</h1>
        <p>Wpisz swoje imię:</p>
        <input type="text" id="imie" placeholder="Wpisz swoje imię">
        <button id="powitajBtn">Powitaj</button>
        <div id="wynik"></div>
    </div>

    <script>
        // Pobierz przycisk
        const powitajBtn = document.getElementById('powitajBtn');
        
        // Dodaj nasłuchiwacza zdarzenia kliknięcia
        powitajBtn.addEventListener('click', function() {
            // Pobierz wartość z pola tekstowego
            const imie = document.getElementById('imie').value;
            
            // Wyświetl powitanie
            document.getElementById('wynik').textContent = 'Cześć ' + imie + '!';
        });
        
        // Bonus: Obsługa klawisza Enter
        document.getElementById('imie').addEventListener('keypress', function(event) {
            if (event.key === 'Enter') {
                powitajBtn.click();
            }
        });
    </script>
</body>
</html>
```

---

## ZADANIE 2: Kalkulator dodawania - Dwie liczby

### Opis:
Stwórz prosty kalkulator, który dodaje dwie liczby.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Kalkulator dodawania</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .container { max-width: 400px; margin: 0 auto; background-color: #f9f9f9; padding: 20px; border-radius: 8px; }
        input { padding: 10px; width: 100%; box-sizing: border-box; margin: 10px 0; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; width: 100%; }
        #wynik { margin-top: 20px; font-size: 20px; font-weight: bold; text-align: center; color: #28a745; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Kalkulator dodawania</h1>
        <p>Wpisz dwie liczby:</p>
        <input type="number" id="liczba1" placeholder="Pierwsza liczba">
        <input type="number" id="liczba2" placeholder="Druga liczba">
        <button id="dodajBtn">Dodaj</button>
        <div id="wynik"></div>
    </div>

    <script>
        // Pobierz przycisk
        const dodajBtn = document.getElementById('dodajBtn');
        
        // Dodaj nasłuchiwacza
        dodajBtn.addEventListener('click', function() {
            // Pobierz wartości z pól
            const liczba1 = parseInt(document.getElementById('liczba1').value);
            const liczba2 = parseInt(document.getElementById('liczba2').value);
            
            // Sprawdź czy pola nie są puste
            if (isNaN(liczba1) || isNaN(liczba2)) {
                document.getElementById('wynik').textContent = 'Wpisz obie liczby!';
                document.getElementById('wynik').style.color = 'red';
                return;
            }
            
            // Oblicz sumę
            const suma = liczba1 + liczba2;
            
            // Wyświetl wynik
            document.getElementById('wynik').textContent = 'Wynik: ' + suma;
            document.getElementById('wynik').style.color = '#28a745';
        });
        
        // Bonus: Enter
        document.getElementById('liczba1').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') dodajBtn.click();
        });
        document.getElementById('liczba2').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') dodajBtn.click();
        });
    </script>
</body>
</html>
```

---

## ZADANIE 3: Zmiana koloru tła

### Opis:
Stwórz przyciski, które zmieniają kolor tła strony.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Zmiana koloru tła</title>
    <style>
        body { font-family: Arial; padding: 20px; transition: background-color 0.3s; }
        .container { max-width: 500px; margin: 0 auto; }
        .button-group { display: flex; gap: 10px; flex-wrap: wrap; }
        button { padding: 12px 20px; border: none; cursor: pointer; border-radius: 4px; font-weight: bold; color: white; }
        #czerwonyBtn { background-color: red; }
        #zielonyBtn { background-color: green; }
        #niebieskyBtn { background-color: blue; }
        #zoltyBtn { background-color: gold; color: black; }
        #resetBtn { background-color: gray; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Zmiana koloru tła</h1>
        <p>Kliknij przycisk aby zmienić kolor tła:</p>
        <div class="button-group">
            <button id="czerwonyBtn">Czerwony</button>
            <button id="zielonyBtn">Zielony</button>
            <button id="niebieskyBtn">Niebieski</button>
            <button id="zoltyBtn">Żółty</button>
            <button id="resetBtn">Reset</button>
        </div>
    </div>

    <script>
        // Przycisk czerwony
        document.getElementById('czerwonyBtn').addEventListener('click', function() {
            document.body.style.backgroundColor = 'red';
        });
        
        // Przycisk zielony
        document.getElementById('zielonyBtn').addEventListener('click', function() {
            document.body.style.backgroundColor = 'green';
        });
        
        // Przycisk niebieski
        document.getElementById('niebieskyBtn').addEventListener('click', function() {
            document.body.style.backgroundColor = 'blue';
        });
        
        // Przycisk żółty
        document.getElementById('zoltyBtn').addEventListener('click', function() {
            document.body.style.backgroundColor = 'gold';
        });
        
        // Przycisk reset
        document.getElementById('resetBtn').addEventListener('click', function() {
            document.body.style.backgroundColor = 'white';
        });
    </script>
</body>
</html>
```

---

## ZADANIE 4: Lista zakupów - Dodawanie elementów

### Opis:
Stwórz aplikację do listy zakupów. Użytkownik wpisuje przedmiot i klika przycisk.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Lista zakupów</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 500px; margin: 0 auto; background-color: white; padding: 20px; border-radius: 8px; }
        input { padding: 10px; width: 100%; box-sizing: border-box; margin: 10px 0; }
        button { padding: 10px 20px; background-color: #28a745; color: white; border: none; cursor: pointer; border-radius: 4px; width: 100%; }
        #lista { list-style: none; padding: 0; margin-top: 20px; }
        #lista li { background-color: #f9f9f9; padding: 10px; margin: 5px 0; border-left: 4px solid #28a745; border-radius: 4px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>🛒 Lista zakupów</h1>
        <p>Wpisz przedmiot do kupienia:</p>
        <input type="text" id="przedmiot" placeholder="np. Mleko, Chleb, Masło...">
        <button id="dodajBtn">Dodaj do listy</button>
        <ul id="lista"></ul>
    </div>

    <script>
        // Pobierz przycisk
        const dodajBtn = document.getElementById('dodajBtn');
        
        // Dodaj nasłuchiwacza
        dodajBtn.addEventListener('click', function() {
            // Pobierz wartość z pola
            const przedmiot = document.getElementById('przedmiot').value;
            
            // Sprawdź czy pole nie jest puste
            if (przedmiot === '') {
                alert('Wpisz przedmiot!');
                return;
            }
            
            // Utwórz nowy element listy
            const li = document.createElement('li');
            li.textContent = przedmiot;
            
            // Dodaj do listy na stronie
            document.getElementById('lista').appendChild(li);
            
            // Wyczyść pole tekstowe
            document.getElementById('przedmiot').value = '';
            
            // Ustaw fokus na pole (żeby użytkownik mógł od razu pisać)
            document.getElementById('przedmiot').focus();
        });
        
        // Bonus: Enter
        document.getElementById('przedmiot').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                dodajBtn.click();
            }
        });
    </script>
</body>
</html>
```

---

## ZADANIE 5: Licznik kliknięć

### Opis:
Stwórz prostą aplikację, która liczy ile razy użytkownik kliknął przycisk.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Licznik kliknięć</title>
    <style>
        body { font-family: Arial; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; }
        .container { max-width: 400px; margin: 0 auto; background-color: white; padding: 30px; border-radius: 8px; text-align: center; }
        #liczba { font-size: 48px; font-weight: bold; color: #667eea; margin: 20px 0; }
        #klikBtn { padding: 15px 30px; background-color: #667eea; color: white; border: none; cursor: pointer; border-radius: 4px; font-size: 16px; margin: 10px 0; }
        #resetBtn { padding: 10px 20px; background-color: #dc3545; color: white; border: none; cursor: pointer; border-radius: 4px; }
        #klikBtn:hover { background-color: #764ba2; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Licznik kliknięć</h1>
        <div id="liczba">0</div>
        <p>Kliknij przycisk aby licznik wzrósł:</p>
        <button id="klikBtn">Kliknij mnie</button>
        <br>
        <button id="resetBtn">Resetuj</button>
    </div>

    <script>
        // Utwórz zmienną licznika na początku (poza funkcjami!)
        let licznikKlikniecia = 0;
        
        // Pobierz przycisk klikania
        const klikBtn = document.getElementById('klikBtn');
        
        // Dodaj nasłuchiwacza do przycisku
        klikBtn.addEventListener('click', function() {
            // Zwiększ licznik o 1
            licznikKlikniecia = licznikKlikniecia + 1;
            
            // Wyświetl nową wartość
            document.getElementById('liczba').textContent = licznikKlikniecia;
        });
        
        // Pobierz przycisk resetowania
        const resetBtn = document.getElementById('resetBtn');
        
        // Dodaj nasłuchiwacza do przycisku resetowania
        resetBtn.addEventListener('click', function() {
            // Zresetuj licznik
            licznikKlikniecia = 0;
            
            // Wyświetl 0
            document.getElementById('liczba').textContent = '0';
        });
    </script>
</body>
</html>
```

---

## ZADANIE 6: Pokazywanie i ukrywanie elementu

### Opis:
Stwórz dwa przyciski - jeden pokazuje element, drugi go ukrywa.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Pokazywanie/Ukrywanie</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .container { max-width: 500px; margin: 0 auto; }
        .button-group { margin: 20px 0; }
        button { padding: 10px 20px; margin: 5px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        #tajny { 
            background-color: #fff3cd; 
            padding: 20px; 
            border-radius: 4px; 
            margin-top: 20px; 
            display: none; /* Na początku ukryty */
            border-left: 4px solid #ffc107;
        }
        .visible { display: block !important; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Pokazuj/Ukrywaj</h1>
        <div class="button-group">
            <button id="pokazBtn">Pokaż</button>
            <button id="ukryjBtn">Ukryj</button>
        </div>
        
        <div id="tajny">
            <h3>🎉 To jest ukryty element!</h3>
            <p>Udało Ci się go znaleźć! To jest tajny tekst, który pojawił się po kliknięciu przycisku.</p>
        </div>
    </div>

    <script>
        // Pobierz przyciski
        const pokazBtn = document.getElementById('pokazBtn');
        const ukryjBtn = document.getElementById('ukryjBtn');
        const tajny = document.getElementById('tajny');
        
        // Przycisk "Pokaż"
        pokazBtn.addEventListener('click', function() {
            tajny.style.display = 'block';
        });
        
        // Przycisk "Ukryj"
        ukryjBtn.addEventListener('click', function() {
            tajny.style.display = 'none';
        });
    </script>
</body>
</html>
```

---

## ZADANIE 7: Zmiana rozmiaru czcionki

### Opis:
Stwórz dwa przyciski, które zmieniają rozmiar tekstu.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Zmiana rozmiaru czcionki</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .container { max-width: 500px; margin: 0 auto; }
        .button-group { margin: 20px 0; }
        button { padding: 10px 20px; margin: 5px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        #tekst { 
            background-color: #f0f0f0; 
            padding: 20px; 
            border-radius: 4px; 
            margin-top: 20px; 
            font-size: 16px; 
            transition: font-size 0.3s;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Zmiana rozmiaru czcionki</h1>
        <div class="button-group">
            <button id="powiekszBtn">Powiększ tekst</button>
            <button id="pomniejszBtn">Pomniejsz tekst</button>
        </div>
        
        <div id="tekst">
            To jest tekst, który możesz powiększać i pomniejszać. Kliknij przyciski aby zmienić jego rozmiar!
        </div>
    </div>

    <script>
        // Utwórz zmienną na rozmiar (start od 16 pikseli)
        let rozmiarTekstu = 16;
        
        // Pobierz elementy
        const powiekszBtn = document.getElementById('powiekszBtn');
        const pomniejszBtn = document.getElementById('pomniejszBtn');
        const tekst = document.getElementById('tekst');
        
        // Przycisk powiększenia
        powiekszBtn.addEventListener('click', function() {
            // Zwiększ rozmiar o 2 piksele
            rozmiarTekstu = rozmiarTekstu + 2;
            
            // Ustaw nowy rozmiar
            tekst.style.fontSize = rozmiarTekstu + 'px';
        });
        
        // Przycisk pomniejszenia
        pomniejszBtn.addEventListener('click', function() {
            // Zmniejsz rozmiar o 2 piksele (ale minimum 12)
            if (rozmiarTekstu > 12) {
                rozmiarTekstu = rozmiarTekstu - 2;
                tekst.style.fontSize = rozmiarTekstu + 'px';
            }
        });
    </script>
</body>
</html>
```

---

## ZADANIE 8: Weryfikacja czy pole jest wypełnione

### Opis:
Stwórz formularz, który sprawdza czy użytkownik coś wpisał.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Weryfikacja pola</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 500px; margin: 0 auto; background-color: white; padding: 20px; border-radius: 8px; }
        input { padding: 10px; width: 100%; box-sizing: border-box; margin: 10px 0; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; width: 100%; }
        #wiadomosc { margin-top: 20px; padding: 15px; border-radius: 4px; text-align: center; font-weight: bold; display: none; }
        .blad { background-color: #f8d7da; color: #721c24; }
        .ok { background-color: #d4edda; color: #155724; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Formularz weryfikacji</h1>
        <p>Wpisz coś w polu poniżej:</p>
        <input type="text" id="pole" placeholder="Wpisz dowolny tekst">
        <button id="wyslijBtn">Wyślij</button>
        <div id="wiadomosc"></div>
    </div>

    <script>
        // Pobierz elementy
        const wyslijBtn = document.getElementById('wyslijBtn');
        const pole = document.getElementById('pole');
        const wiadomosc = document.getElementById('wiadomosc');
        
        // Dodaj nasłuchiwacza
        wyslijBtn.addEventListener('click', function() {
            // Pobierz wartość z pola
            const tekst = pole.value;
            
            // Sprawdź czy pole jest puste
            if (tekst === '') {
                // Pokaż błąd
                wiadomosc.textContent = '❌ Błąd: Wpisz coś w polu!';
                wiadomosc.className = 'blad';
                wiadomosc.style.display = 'block';
            } else {
                // Pokaż OK
                wiadomosc.textContent = '✅ OK! Tekst "' + tekst + '" został zapisany';
                wiadomosc.className = 'ok';
                wiadomosc.style.display = 'block';
                
                // Wyczyść pole
                pole.value = '';
            }
        });
        
        // Bonus: Enter
        pole.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                wyslijBtn.click();
            }
        });
    </script>
</body>
</html>
```

---

## ZADANIE 9: Pętla - Wypisanie liczb od 1 do 10

### Opis:
Stwórz program, który wypisze wszystkie liczby od 1 do 10.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Pętla - Liczby</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 500px; margin: 0 auto; background-color: white; padding: 20px; border-radius: 8px; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; width: 100%; }
        #wynik { margin-top: 20px; background-color: #f9f9f9; padding: 20px; border-radius: 4px; }
        .liczba { display: inline-block; background-color: #007bff; color: white; padding: 10px 15px; margin: 5px; border-radius: 4px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Wypisz liczby od 1 do 10</h1>
        <p>Kliknij przycisk aby wyświetlić liczby:</p>
        <button id="wyspliszBtn">Wypisz liczby</button>
        <div id="wynik"></div>
    </div>

    <script>
        // Pobierz przycisk
        const wyspliszBtn = document.getElementById('wyspliszBtn');
        
        // Dodaj nasłuchiwacza
        wyspliszBtn.addEventListener('click', function() {
            // Utwórz zmienną na wynik
            let wynik = '';
            
            // Pętla od 1 do 10
            for (let i = 1; i <= 10; i++) {
                // Dodaj liczba do wyniku
                wynik = wynik + '<span class="liczba">' + i + '</span>';
            }
            
            // Wyświetl wynik
            document.getElementById('wynik').innerHTML = wynik;
        });
    </script>
</body>
</html>
```

---

## ZADANIE 10: Tablica - Lista imion

### Opis:
Stwórz program, który przechowuje listę imion w tablicy i wyświetla je wszystkie.

### Pełny kod HTML/CSS/JavaScript:

```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Tablica - Imiona</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 500px; margin: 0 auto; background-color: white; padding: 20px; border-radius: 8px; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; width: 100%; }
        #lista { margin-top: 20px; }
        .imie { background-color: #f9f9f9; padding: 10px; margin: 5px 0; border-left: 4px solid #007bff; border-radius: 4px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Lista imion</h1>
        <p>Kliknij przycisk aby wyświetlić listę imion:</p>
        <button id="pokazBtn">Pokaż imiona</button>
        <div id="lista"></div>
    </div>

    <script>
        // Utwórz tablicę z imionami
        const imiona = ['Anna', 'Bartosz', 'Cześć', 'Dominika', 'Ewa', 'Filip', 'Grzegorz', 'Hanna'];
        
        // Pobierz przycisk
        const pokazBtn = document.getElementById('pokazBtn');
        
        // Dodaj nasłuchiwacza
        pokazBtn.addEventListener('click', function() {
            // Utwórz zmienną na wynik
            let wynik = '<h3>Imiona w mojej klasie:</h3>';
            
            // Pętla przez całą tablicę
            for (let i = 0; i < imiona.length; i++) {
                // Dodaj każde imię do wyniku
                // (i + 1) żeby numeracja była od 1 zamiast od 0
                wynik = wynik + '<div class="imie">' + (i + 1) + '. ' + imiona[i] + '</div>';
            }
            
            // Wyświetl wynik
            document.getElementById('lista').innerHTML = wynik;
        });
    </script>
</body>
</html>
```

---

## Podsumowanie

Wszystkie zadania są **gotowe do skopiowania i uruchomienia**. Po prostu:

1. Skopiuj kod HTML
2. Wklej go do nowego pliku (np. `zadanie1.html`)
3. Zapisz plik
4. Otwórz go w przeglądarce
5. Gra!

### Główne koncepty JavaScript w zadaniach:

| Zadanie | Koncepty |
|---------|----------|
| 1 | getElementById, addEventListener, value, textContent |
| 2 | parseInt, walidacja, operacje matematyczne |
| 3 | style.backgroundColor, document.body |
| 4 | createElement, appendChild, focus |
| 5 | zmienne, event listeners, reset |
| 6 | style.display, show/hide |
| 7 | zmienne licznikowe, style.fontSize |
| 8 | sprawdzanie warunku, className |
| 9 | pętla for, innerHTML |
| 10 | tablice, length, for loop |

Powodzenia! 🚀