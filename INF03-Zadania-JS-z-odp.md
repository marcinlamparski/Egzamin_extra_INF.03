# Zbiór zadań JavaScript dla egzaminu INF.03 - WERSJA Z ODPOWIEDZIAMI

## Instrukcja

Poniżej znajduje się **10 zadań** na poziomie trudności typowym dla egzaminu INF.03 zawodowego wraz z ich rozwiązaniami. Każde zadanie dotyczy umiejętności programowania w JavaScript, które są wymagane na egzaminie z kwalifikacji **INF.03** (Tworzenie aplikacji internetowych i baz danych).

---

## ZADANIE 1: Kalkulator BMI (Body Mass Index)

### Opis:
Stwórz aplikację obliczającą wskaźnik BMI (Body Mass Index) z formularzem, przyciskiem i wyświetlaniem wyniku z kolorowym kodowaniem kategorii.

### Wskazówki:
Przydatne funkcje i metody: `document.getElementById()`, `parseFloat()`, `addEventListener()`, `toFixed(2)`, `if...else if...else`

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Kalkulator BMI</title>
    <style>
        body { font-family: Arial, sans-serif; padding: 20px; }
        .container { max-width: 500px; margin: 0 auto; }
        input { display: block; margin: 10px 0; padding: 8px; width: 100%; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; }
        .result { margin-top: 20px; font-size: 18px; font-weight: bold; }
        .blue { color: blue; }
        .green { color: green; }
        .yellow { color: orange; }
        .red { color: red; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Kalkulator BMI</h1>
        <label>Waga (kg):</label>
        <input type="number" id="waga" placeholder="Wpisz wagę w kg">
        
        <label>Wzrost (cm):</label>
        <input type="number" id="wzrost" placeholder="Wpisz wzrost w cm">
        
        <button id="obliczBtn">Oblicz BMI</button>
        
        <div id="wynik" class="result"></div>
    </div>

    <script>
        document.getElementById('obliczBtn').addEventListener('click', function() {
            // Pobranie wartości z pól
            const waga = parseFloat(document.getElementById('waga').value);
            const wzrost = parseInt(document.getElementById('wzrost').value);
            const wynikDiv = document.getElementById('wynik');
            
            // Walidacja
            if (isNaN(waga) || isNaN(wzrost) || waga <= 0 || wzrost <= 0) {
                wynikDiv.textContent = 'Błąd: Wpisz prawidłowe wartości!';
                wynikDiv.className = 'result red';
                return;
            }
            
            // Obliczenie BMI
            const wzrostMetry = wzrost / 100;
            const bmi = (waga / (wzrostMetry * wzrostMetry)).toFixed(2);
            
            // Określenie kategorii
            let kategoria = '';
            let klasa = '';
            
            if (bmi < 18.5) {
                kategoria = `Niedowaga (BMI: ${bmi})`;
                klasa = 'blue';
            } else if (bmi < 25) {
                kategoria = `Waga prawidłowa (BMI: ${bmi})`;
                klasa = 'green';
            } else if (bmi < 30) {
                kategoria = `Nadwaga (BMI: ${bmi})`;
                klasa = 'yellow';
            } else {
                kategoria = `Otyłość (BMI: ${bmi})`;
                klasa = 'red';
            }
            
            // Wyświetlenie wyniku
            wynikDiv.textContent = kategoria;
            wynikDiv.className = 'result ' + klasa;
        });
    </script>
</body>
</html>
```

---

## ZADANIE 2: Walidacja formularza rejestracji

### Opis:
Stwórz formularz rejestracji z walidacją poszczególnych pól w czasie rzeczywistym (podczas pisania) z komunikatami o błędach.

### Wskazówki:
Przydatne funkcje i metody: `querySelector()`, `addEventListener('input')`, `length`, `.includes()`, `.match()`, wyrażenia regularne

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Formularz rejestracji</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .form-group { margin: 15px 0; }
        input { width: 100%; padding: 8px; border: 2px solid #ddd; box-sizing: border-box; }
        input.valid { border-color: green; }
        input.invalid { border-color: red; }
        .error { color: red; font-size: 12px; display: none; }
        .error.show { display: block; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; }
        button:disabled { background-color: #ccc; cursor: not-allowed; }
    </style>
</head>
<body>
    <h1>Formularz rejestracji</h1>
    <form id="formRejestracja">
        <div class="form-group">
            <label>Imię:</label>
            <input type="text" id="imie" placeholder="Minimum 3 znaki, tylko litery">
            <div class="error" id="imieError">Imię musi mieć minimum 3 znaki i zawierać tylko litery</div>
        </div>
        
        <div class="form-group">
            <label>E-mail:</label>
            <input type="email" id="email" placeholder="Prawidłowy format e-mail">
            <div class="error" id="emailError">Podaj prawidłowy adres e-mail</div>
        </div>
        
        <div class="form-group">
            <label>Hasło:</label>
            <input type="password" id="haslo" placeholder="Min. 8 znaków, cyfra, duża litera">
            <div class="error" id="hasloError">Hasło musi mieć min. 8 znaków, zawierać cyfrę i dużą literę</div>
        </div>
        
        <div class="form-group">
            <label>Powtórz hasło:</label>
            <input type="password" id="hasloPowtorz" placeholder="Powtórz hasło">
            <div class="error" id="hasloPowtorzError">Hasła nie są identyczne</div>
        </div>
        
        <button type="submit" id="rejestrujBtn" disabled>Zarejestruj</button>
    </form>

    <script>
        const imieInput = document.getElementById('imie');
        const emailInput = document.getElementById('email');
        const hasloInput = document.getElementById('haslo');
        const hasloPowtorzInput = document.getElementById('hasloPowtorz');
        const form = document.getElementById('formRejestracja');
        const rejestrujBtn = document.getElementById('rejestrujBtn');
        
        // Zmienne do śledzenia stanu walidacji
        let statusImie = false;
        let statusEmail = false;
        let statusHaslo = false;
        let statusHasloPowtorz = false;
        
        // Funkcja walidacji imienia
        function walidujImie() {
            const imie = imieInput.value.trim();
            const regexImie = /^[a-zA-Ząćęłńóśźż]+$/;
            
            if (imie.length >= 3 && regexImie.test(imie)) {
                imieInput.classList.remove('invalid');
                imieInput.classList.add('valid');
                document.getElementById('imieError').classList.remove('show');
                statusImie = true;
            } else {
                imieInput.classList.remove('valid');
                imieInput.classList.add('invalid');
                document.getElementById('imieError').classList.add('show');
                statusImie = false;
            }
            sprawdzFormularz();
        }
        
        // Funkcja walidacji e-maila
        function walidujEmail() {
            const email = emailInput.value.trim();
            const regexEmail = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            
            if (regexEmail.test(email)) {
                emailInput.classList.remove('invalid');
                emailInput.classList.add('valid');
                document.getElementById('emailError').classList.remove('show');
                statusEmail = true;
            } else {
                emailInput.classList.remove('valid');
                emailInput.classList.add('invalid');
                document.getElementById('emailError').classList.add('show');
                statusEmail = false;
            }
            sprawdzFormularz();
        }
        
        // Funkcja walidacji hasła
        function walidujHaslo() {
            const haslo = hasloInput.value;
            const regexHaslo = /^(?=.*[A-Z])(?=.*\d).{8,}$/;
            
            if (regexHaslo.test(haslo)) {
                hasloInput.classList.remove('invalid');
                hasloInput.classList.add('valid');
                document.getElementById('hasloError').classList.remove('show');
                statusHaslo = true;
            } else {
                hasloInput.classList.remove('valid');
                hasloInput.classList.add('invalid');
                document.getElementById('hasloError').classList.add('show');
                statusHaslo = false;
            }
            sprawdzPowtorzenieHasla();
            sprawdzFormularz();
        }
        
        // Funkcja walidacji powtórzenia hasła
        function walidujPowtorzenieHasla() {
            const haslo = hasloInput.value;
            const hasloPowtorz = hasloPowtorzInput.value;
            
            if (haslo === hasloPowtorz && haslo.length > 0) {
                hasloPowtorzInput.classList.remove('invalid');
                hasloPowtorzInput.classList.add('valid');
                document.getElementById('hasloPowtorzError').classList.remove('show');
                statusHasloPowtorz = true;
            } else {
                hasloPowtorzInput.classList.remove('valid');
                hasloPowtorzInput.classList.add('invalid');
                document.getElementById('hasloPowtorzError').classList.add('show');
                statusHasloPowtorz = false;
            }
            sprawdzFormularz();
        }
        
        function sprawdzPowtorzenieHasla() {
            const haslo = hasloInput.value;
            const hasloPowtorz = hasloPowtorzInput.value;
            
            if (hasloPowtorz.length > 0) {
                walidujPowtorzenieHasla();
            }
        }
        
        // Funkcja do sprawdzenia czy wszystkie pola są prawidłowe
        function sprawdzFormularz() {
            if (statusImie && statusEmail && statusHaslo && statusHasloPowtorz) {
                rejestrujBtn.disabled = false;
            } else {
                rejestrujBtn.disabled = true;
            }
        }
        
        // Dodanie nasłuchujących zdarzeń
        imieInput.addEventListener('input', walidujImie);
        emailInput.addEventListener('input', walidujEmail);
        hasloInput.addEventListener('input', walidujHaslo);
        hasloPowtorzInput.addEventListener('input', walidujPowtorzenieHasla);
        
        // Obsługa wysłania formularza
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            alert('Rejestracja udana! Witaj ' + imieInput.value);
        });
    </script>
</body>
</html>
```

---

## ZADANIE 3: Konwerter temperatur

### Opis:
Stwórz konwerter temperatur między trzema skalami z automatyczną aktualizacją wartości i ostrzeżeniami o temperaturze poniżej zera absolutnego.

### Wskazówki:
Przydatne funkcje i metody: `addEventListener('input')`, `parseFloat()`, `toFixed(2)`, operacje matematyczne

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Konwerter temperatur</title>
    <style>
        body { font-family: Arial; padding: 20px; }
        .container { max-width: 600px; margin: 0 auto; }
        .temp-group { margin: 20px 0; display: flex; gap: 20px; }
        input { width: 200px; padding: 10px; font-size: 14px; }
        .warning { color: red; font-weight: bold; margin-top: 10px; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; margin-top: 10px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Konwerter temperatur</h1>
        
        <div class="temp-group">
            <div>
                <label>Celsius (°C):</label><br>
                <input type="number" id="celsius" placeholder="Wpisz stopnie Celsjusza">
            </div>
            <div>
                <label>Fahrenheit (°F):</label><br>
                <input type="number" id="fahrenheit" placeholder="Wpisz stopnie Fahrenheita">
            </div>
            <div>
                <label>Kelvin (K):</label><br>
                <input type="number" id="kelvin" placeholder="Wpisz Kelviny">
            </div>
        </div>
        
        <button id="wyczyscBtn">Wyczyść wszystko</button>
        
        <div id="warning" class="warning"></div>
    </div>

    <script>
        const celsiusInput = document.getElementById('celsius');
        const fahrenheitInput = document.getElementById('fahrenheit');
        const kelvinInput = document.getElementById('kelvin');
        const warningDiv = document.getElementById('warning');
        const wyczyscBtn = document.getElementById('wyczyscBtn');
        
        const ZERO_ABSOLUTNE = -273.15;
        
        // Funkcja sprawdzająca czy temperatura jest prawidłowa
        function sprawdzTemperature(celsius) {
            if (celsius < ZERO_ABSOLUTNE) {
                warningDiv.textContent = '⚠️ Ostrzeżenie: Temperatura poniżej zera absolutnego!';
                return false;
            } else {
                warningDiv.textContent = '';
                return true;
            }
        }
        
        // Konwersja Celsius -> Fahrenheit i Kelvin
        celsiusInput.addEventListener('input', function() {
            const celsius = parseFloat(this.value);
            
            if (!isNaN(celsius)) {
                sprawdzTemperature(celsius);
                
                const fahrenheit = (celsius * 9/5) + 32;
                const kelvin = celsius + 273.15;
                
                fahrenheitInput.value = fahrenheit.toFixed(2);
                kelvinInput.value = kelvin.toFixed(2);
            } else {
                fahrenheitInput.value = '';
                kelvinInput.value = '';
                warningDiv.textContent = '';
            }
        });
        
        // Konwersja Fahrenheit -> Celsius i Kelvin
        fahrenheitInput.addEventListener('input', function() {
            const fahrenheit = parseFloat(this.value);
            
            if (!isNaN(fahrenheit)) {
                const celsius = (fahrenheit - 32) * 5/9;
                sprawdzTemperature(celsius);
                
                const kelvin = celsius + 273.15;
                
                celsiusInput.value = celsius.toFixed(2);
                kelvinInput.value = kelvin.toFixed(2);
            } else {
                celsiusInput.value = '';
                kelvinInput.value = '';
                warningDiv.textContent = '';
            }
        });
        
        // Konwersja Kelvin -> Celsius i Fahrenheit
        kelvinInput.addEventListener('input', function() {
            const kelvin = parseFloat(this.value);
            
            if (!isNaN(kelvin) && kelvin >= 0) {
                const celsius = kelvin - 273.15;
                sprawdzTemperature(celsius);
                
                const fahrenheit = (celsius * 9/5) + 32;
                
                celsiusInput.value = celsius.toFixed(2);
                fahrenheitInput.value = fahrenheit.toFixed(2);
            } else {
                celsiusInput.value = '';
                fahrenheitInput.value = '';
                if (kelvin < 0) {
                    warningDiv.textContent = '⚠️ Kelvin nie może być ujemny!';
                } else {
                    warningDiv.textContent = '';
                }
            }
        });
        
        // Wyczyść wszystko
        wyczyscBtn.addEventListener('click', function() {
            celsiusInput.value = '';
            fahrenheitInput.value = '';
            kelvinInput.value = '';
            warningDiv.textContent = '';
        });
    </script>
</body>
</html>
```

---

## ZADANIE 4: Generator kolorów losowych

### Opis:
Stwórz aplikację do generowania losowych kolorów z wyświetlaniem w formatach HEX i RGB, możliwością kopiowania oraz historią.

### Wskazówki:
Przydatne funkcje i metody: `Math.random()`, `Math.floor()`, `toString(16)`, `padStart()`, `navigator.clipboard.writeText()`, tablica, `forEach()`

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Generator kolorów</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 600px; margin: 0 auto; background: white; padding: 20px; border-radius: 8px; }
        .color-display { width: 100%; height: 200px; border-radius: 8px; margin: 20px 0; }
        .color-info { text-align: center; margin: 20px 0; }
        .color-code { font-size: 18px; font-weight: bold; font-family: monospace; }
        .button-group { display: flex; gap: 10px; margin: 20px 0; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; flex: 1; }
        button:hover { background-color: #0056b3; }
        .message { text-align: center; color: green; font-weight: bold; margin-top: 10px; }
        .history { margin-top: 30px; }
        .history h3 { margin-bottom: 10px; }
        .history-colors { display: flex; gap: 10px; flex-wrap: wrap; }
        .color-swatch { width: 60px; height: 60px; border-radius: 4px; cursor: pointer; border: 2px solid #ddd; }
        .color-swatch:hover { border-color: #007bff; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Generator kolorów losowych</h1>
        
        <div class="color-display" id="colorDisplay"></div>
        
        <div class="color-info">
            <p>HEX: <span class="color-code" id="hexCode">#000000</span></p>
            <p>RGB: <span class="color-code" id="rgbCode">rgb(0,0,0)</span></p>
        </div>
        
        <div class="button-group">
            <button id="generateBtn">Generuj nowy kolor</button>
            <button id="copyBtn">Kopiuj HEX</button>
        </div>
        
        <div id="copyMessage" class="message" style="display: none;">Skopiowano do schowka!</div>
        
        <div class="history">
            <h3>Historia (ostatnie 5 kolorów)</h3>
            <div id="historyColors" class="history-colors"></div>
            <button id="clearHistoryBtn">Wyczyść historię</button>
        </div>
    </div>

    <script>
        const colorDisplay = document.getElementById('colorDisplay');
        const hexCode = document.getElementById('hexCode');
        const rgbCode = document.getElementById('rgbCode');
        const generateBtn = document.getElementById('generateBtn');
        const copyBtn = document.getElementById('copyBtn');
        const copyMessage = document.getElementById('copyMessage');
        const historyColors = document.getElementById('historyColors');
        const clearHistoryBtn = document.getElementById('clearHistoryBtn');
        
        let historia = [];
        
        // Funkcja do generowania losowej liczby od 0 do 255
        function losowaCzesc() {
            return Math.floor(Math.random() * 256);
        }
        
        // Funkcja do generowania losowego koloru HEX
        function generujKolor() {
            const r = losowaCzesc();
            const g = losowaCzesc();
            const b = losowaCzesc();
            
            const hex = '#' + [r, g, b].map(x => {
                const wartosc = x.toString(16);
                return wartosc.length === 1 ? '0' + wartosc : wartosc;
            }).join('').toUpperCase();
            
            const rgb = `rgb(${r},${g},${b})`;
            
            // Wyświetlenie koloru
            colorDisplay.style.backgroundColor = hex;
            hexCode.textContent = hex;
            rgbCode.textContent = rgb;
            
            // Dodanie do historii
            if (!historia.includes(hex)) {
                historia.unshift(hex);
                if (historia.length > 5) {
                    historia.pop();
                }
                aktualizujHistorie();
            }
        }
        
        // Funkcja do aktualizacji wyświetlania historii
        function aktualizujHistorie() {
            historyColors.innerHTML = '';
            historia.forEach(kolor => {
                const swatch = document.createElement('div');
                swatch.className = 'color-swatch';
                swatch.style.backgroundColor = kolor;
                swatch.title = kolor;
                swatch.addEventListener('click', function() {
                    colorDisplay.style.backgroundColor = kolor;
                    hexCode.textContent = kolor;
                    // Konwersja HEX na RGB
                    const r = parseInt(kolor.slice(1, 3), 16);
                    const g = parseInt(kolor.slice(3, 5), 16);
                    const b = parseInt(kolor.slice(5, 7), 16);
                    rgbCode.textContent = `rgb(${r},${g},${b})`;
                });
                historyColors.appendChild(swatch);
            });
        }
        
        // Obsługa przycisków
        generateBtn.addEventListener('click', generujKolor);
        
        copyBtn.addEventListener('click', function() {
            const hex = hexCode.textContent;
            navigator.clipboard.writeText(hex).then(() => {
                copyMessage.style.display = 'block';
                setTimeout(() => {
                    copyMessage.style.display = 'none';
                }, 2000);
            });
        });
        
        clearHistoryBtn.addEventListener('click', function() {
            historia = [];
            aktualizujHistorie();
        });
        
        // Generuj początkowy kolor
        generujKolor();
    </script>
</body>
</html>
```

---

## ZADANIE 5: Kalkulator wydatków

### Opis:
Stwórz aplikację do zarządzania wydatkami z możliwością dodawania, usuwania, sortowania i kategoryzacji wydatków.

### Wskazówki:
Przydatne funkcje i metody: tablice, obiekty, `push()`, `filter()`, `reduce()`, `forEach()`, `sort()`, manipulacja DOM

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Kalkulator wydatków</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 800px; margin: 0 auto; background: white; padding: 20px; border-radius: 8px; }
        .form-group { margin: 15px 0; }
        input, select { padding: 8px; width: 100%; box-sizing: border-box; }
        .button-group { display: flex; gap: 10px; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        button:hover { background-color: #0056b3; }
        .summary { background-color: #f9f9f9; padding: 15px; margin: 20px 0; border-radius: 4px; }
        .summary-item { display: flex; justify-content: space-between; margin: 5px 0; }
        .summary-total { font-weight: bold; font-size: 16px; border-top: 2px solid #ddd; padding-top: 10px; }
        .expenses-list { margin-top: 20px; }
        .expense-item { background-color: #f9f9f9; padding: 10px; margin: 10px 0; border-radius: 4px; display: flex; justify-content: space-between; align-items: center; }
        .expense-info { flex: 1; }
        .expense-category { background-color: #007bff; color: white; padding: 3px 8px; border-radius: 3px; font-size: 12px; margin-right: 10px; }
        .expense-date { font-size: 12px; color: #666; }
        .remove-btn { background-color: red; padding: 5px 10px; cursor: pointer; }
        .sort-buttons { margin: 15px 0; display: flex; gap: 10px; flex-wrap: wrap; }
        .sort-buttons button { padding: 5px 10px; font-size: 12px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Kalkulator wydatków</h1>
        
        <div>
            <h3>Dodaj wydatek</h3>
            <div class="form-group">
                <label>Opis:</label>
                <input type="text" id="opis" placeholder="np. Obiad">
            </div>
            <div class="form-group">
                <label>Kwota (zł):</label>
                <input type="number" id="kwota" placeholder="0.00" step="0.01">
            </div>
            <div class="form-group">
                <label>Kategoria:</label>
                <select id="kategoria">
                    <option value="Jedzenie">Jedzenie</option>
                    <option value="Transport">Transport</option>
                    <option value="Rozrywka">Rozrywka</option>
                    <option value="Inne">Inne</option>
                </select>
            </div>
            <div class="button-group">
                <button id="dodajBtn">Dodaj wydatek</button>
                <button id="wyczyscListeBtn" style="background-color: red;">Wyczyść listę</button>
            </div>
        </div>
        
        <div class="summary">
            <div class="summary-item">
                <span>Łączne wydatki:</span>
                <span id="lacznie">0.00 zł</span>
            </div>
            <div id="poKategoriach"></div>
            <div class="summary-total" id="szczegoly"></div>
        </div>
        
        <h3>Sortowanie</h3>
        <div class="sort-buttons">
            <button id="sortDataBtn">Sortuj po dacie</button>
            <button id="sortKwotaRosnBtn">Sortuj po kwocie (rosnąco)</button>
            <button id="sortKwotaMalejBtn">Sortuj po kwocie (malejąco)</button>
        </div>
        
        <h3>Lista wydatków</h3>
        <div id="listaWydatkow" class="expenses-list"></div>
    </div>

    <script>
        let wydatki = [];
        let sortowan_typ = 'data';
        
        const opisInput = document.getElementById('opis');
        const kwotaInput = document.getElementById('kwota');
        const kategoriaSelect = document.getElementById('kategoria');
        const dodajBtn = document.getElementById('dodajBtn');
        const wyczyscListeBtn = document.getElementById('wyczyscListeBtn');
        const listaDiv = document.getElementById('listaWydatkow');
        const laczenieDiv = document.getElementById('lacznie');
        const szczegályDiv = document.getElementById('szczegoly');
        const poKategoriachDiv = document.getElementById('poKategoriach');
        
        // Funkcja dodawania wydatku
        function dodajWydatek() {
            const opis = opisInput.value.trim();
            const kwota = parseFloat(kwotaInput.value);
            const kategoria = kategoriaSelect.value;
            
            if (!opis || isNaN(kwota) || kwota <= 0) {
                alert('Wpisz prawidłowe dane!');
                return;
            }
            
            const wydatek = {
                id: Date.now(),
                opis: opis,
                kwota: kwota,
                kategoria: kategoria,
                data: new Date().toLocaleDateString('pl-PL')
            };
            
            wydatki.push(wydatek);
            
            opisInput.value = '';
            kwotaInput.value = '';
            
            aktulizujWyswietlanie();
        }
        
        // Funkcja usuwania wydatku
        function usunWydatek(id) {
            wydatki = wydatki.filter(w => w.id !== id);
            aktulizujWyswietlanie();
        }
        
        // Funkcja aktualizacji wyświetlania
        function aktulizujWyswietlanie() {
            // Sortowanie
            let sortowaneWydatki = [...wydatki];
            
            if (sortowan_typ === 'kwota-rosnaco') {
                sortowaneWydatki.sort((a, b) => a.kwota - b.kwota);
            } else if (sortowan_typ === 'kwota-malejaco') {
                sortowaneWydatki.sort((a, b) => b.kwota - a.kwota);
            }
            
            // Wyświetlanie listy
            listaDiv.innerHTML = '';
            sortowaneWydatki.forEach(wydatek => {
                const itemDiv = document.createElement('div');
                itemDiv.className = 'expense-item';
                itemDiv.innerHTML = `
                    <span class="expense-category">${wydatek.kategoria}</span>
                    <div class="expense-info">
                        <strong>${wydatek.opis}</strong>
                        <div class="expense-date">${wydatek.data}</div>
                    </div>
                    <span>${wydatek.kwota.toFixed(2)} zł</span>
                    <button class="remove-btn" onclick="window.usunWydatek(${wydatek.id})">Usuń</button>
                `;
                listaDiv.appendChild(itemDiv);
            });
            
            // Obliczanie sum
            const lacza = wydatki.reduce((suma, w) => suma + w.kwota, 0);
            laczenieDiv.textContent = lacza.toFixed(2) + ' zł';
            
            // Sumy po kategoriach
            poKategoriachDiv.innerHTML = '';
            const kategorie = {};
            wydatki.forEach(w => {
                if (!kategorie[w.kategoria]) {
                    kategorie[w.kategoria] = 0;
                }
                kategorie[w.kategoria] += w.kwota;
            });
            
            for (const [kat, suma] of Object.entries(kategorie)) {
                const item = document.createElement('div');
                item.className = 'summary-item';
                item.innerHTML = `<span>${kat}:</span><span>${suma.toFixed(2)} zł</span>`;
                poKategoriachDiv.appendChild(item);
            }
        }
        
        // Obsługa przycisków
        dodajBtn.addEventListener('click', dodajWydatek);
        
        wyczyscListeBtn.addEventListener('click', function() {
            if (confirm('Na pewno chcesz usunąć wszystkie wydatki?')) {
                wydatki = [];
                aktulizujWyswietlanie();
            }
        });
        
        document.getElementById('sortDataBtn').addEventListener('click', function() {
            sortowan_typ = 'data';
            aktulizujWyswietlanie();
        });
        
        document.getElementById('sortKwotaRosnBtn').addEventListener('click', function() {
            sortowan_typ = 'kwota-rosnaco';
            aktulizujWyswietlanie();
        });
        
        document.getElementById('sortKwotaMalejBtn').addEventListener('click', function() {
            sortowan_typ = 'kwota-malejaco';
            aktulizujWyswietlanie();
        });
        
        // Obsługa Enter w polu opisu
        opisInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') dodajWydatek();
        });
        
        // Udostępnienie funkcji usuwania w globalnym scope
        window.usunWydatek = usunWydatek;
    </script>
</body>
</html>
```

---

## ZADANIE 6: Licznik słów i znaków

### Opis:
Stwórz aplikację do analizy tekstu wyświetlającą statystyki: liczbę słów, znaków, linii oraz dodatkowe informacje.

### Wskazówki:
Przydatne funkcje i metody: `addEventListener('input')`, `trim()`, `split()`, `length`, `replace()`, `toLowerCase()`, `.match()`

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Licznik słów i znaków</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 900px; margin: 0 auto; background: white; padding: 20px; border-radius: 8px; }
        textarea { width: 100%; height: 250px; padding: 10px; font-family: Arial; font-size: 14px; }
        .stats { display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; margin: 20px 0; }
        .stat-box { background-color: #f9f9f9; padding: 15px; border-radius: 4px; text-align: center; border-left: 4px solid #007bff; }
        .stat-number { font-size: 24px; font-weight: bold; color: #007bff; }
        .stat-label { color: #666; margin-top: 5px; }
        .button-group { margin: 15px 0; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; margin-right: 10px; }
        button:hover { background-color: #0056b3; }
        .detailed-stats { background-color: #f9f9f9; padding: 15px; margin-top: 20px; border-radius: 4px; }
        .stat-item { display: flex; justify-content: space-between; padding: 8px 0; border-bottom: 1px solid #eee; }
        .search-group { margin: 15px 0; display: flex; gap: 10px; }
        input[type="text"] { flex: 1; padding: 10px; }
        .search-result { margin-top: 10px; padding: 10px; background-color: #e8f4f8; border-radius: 4px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Analizator tekstu</h1>
        
        <textarea id="tekst" placeholder="Wpisz tutaj tekst do analizy..."></textarea>
        
        <div class="button-group">
            <button id="wyczyscBtn">Wyczyść tekst</button>
        </div>
        
        <div class="stats">
            <div class="stat-box">
                <div class="stat-number" id="slowa">0</div>
                <div class="stat-label">Słów</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="znaki">0</div>
                <div class="stat-label">Znaków (razem)</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="znakiBezSpacji">0</div>
                <div class="stat-label">Znaków (bez spacji)</div>
            </div>
        </div>
        
        <div class="stats">
            <div class="stat-box">
                <div class="stat-number" id="linie">0</div>
                <div class="stat-label">Linii</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="czasCzytania">0</div>
                <div class="stat-label">Minut czytania</div>
            </div>
            <div class="stat-box">
                <div class="stat-number" id="najczestsze">-</div>
                <div class="stat-label">Najczęściej</div>
            </div>
        </div>
        
        <div class="detailed-stats">
            <h3>Szczegółowe statystyki</h3>
            <div class="stat-item">
                <span>Najdłuższe słowo:</span>
                <strong id="najdluzszeSlowo">-</strong>
            </div>
            <div class="stat-item">
                <span>Najkrótsze słowo:</span>
                <strong id="najkrotszeSlow">-</strong>
            </div>
            <div class="stat-item">
                <span>Średnia długość słowa:</span>
                <strong id="srednaSlowa">0</strong>
            </div>
        </div>
        
        <div class="search-group">
            <input type="text" id="szukajSlowa" placeholder="Szukaj słowa...">
            <button id="szukajBtn">Szukaj</button>
        </div>
        <div id="szukajWynik"></div>
    </div>

    <script>
        const tekstArea = document.getElementById('tekst');
        const slowaDiv = document.getElementById('slowa');
        const znakiDiv = document.getElementById('znaki');
        const znakiBezSpacjiDiv = document.getElementById('znakiBezSpacji');
        const linieDiv = document.getElementById('linie');
        const czasCzytaniaDiv = document.getElementById('czasCzytania');
        const najczestszaDiv = document.getElementById('najczestsze');
        const najdluzszeSlowo = document.getElementById('najdluzszeSlowo');
        const najkrotszeSlow = document.getElementById('najkrotszeSlow');
        const srednaSlowa = document.getElementById('srednaSlowa');
        const wyczyscBtn = document.getElementById('wyczyscBtn');
        const szukajSlowa = document.getElementById('szukajSlowa');
        const szukajBtn = document.getElementById('szukajBtn');
        const szukajWynik = document.getElementById('szukajWynik');
        
        function analizujTekst() {
            const tekst = tekstArea.value;
            
            // Liczba znaków
            const znaki = tekst.length;
            const znakiBezSpacji = tekst.replace(/\s/g, '').length;
            
            // Liczba słów
            const slowa = tekst.trim() === '' ? 0 : tekst.trim().split(/\s+/).length;
            
            // Liczba linii
            const linie = tekst.trim() === '' ? 0 : tekst.split('\n').length;
            
            // Czas czytania (200 słów/minutę)
            const czasCzytania = Math.ceil(slowa / 200);
            
            // Analiza słów
            const tablicaSlowa = tekst.toLowerCase().match(/\b\w+\b/g) || [];
            
            // Najczęściej występujące słowo
            const licznikSlowa = {};
            tablicaSlowa.forEach(slowo => {
                licznikSlowa[slowo] = (licznikSlowa[slowo] || 0) + 1;
            });
            
            let najczestsze = '-';
            let maxIlosc = 0;
            for (const [slowo, ilosc] of Object.entries(licznikSlowa)) {
                if (ilosc > maxIlosc) {
                    maxIlosc = ilosc;
                    najczestsze = slowo + ' (' + ilosc + ')';
                }
            }
            
            // Najdłuższe i najkrótsze słowo
            let najdlugie = '';
            let najkrotkie = tablicaSlowa[0] || '';
            
            tablicaSlowa.forEach(slowo => {
                if (slowo.length > najdlugie.length) {
                    najdlugie = slowo;
                }
                if (slowo.length < najkrotkie.length) {
                    najkrotkie = slowo;
                }
            });
            
            // Średnia długość słowa
            const srednia = tablicaSlowa.length > 0 
                ? (tablicaSlowa.reduce((suma, slowo) => suma + slowo.length, 0) / tablicaSlowa.length).toFixed(2) 
                : 0;
            
            // Aktualizacja wyświetlania
            slowaDiv.textContent = slowa;
            znakiDiv.textContent = znaki;
            znakiBezSpacjiDiv.textContent = znakiBezSpacji;
            linieDiv.textContent = linie;
            czasCzytaniaDiv.textContent = czasCzytania;
            najczestszaDiv.textContent = najczestsze;
            najdluzszeSlowo.textContent = najdlugie || '-';
            najkrotszeSlow.textContent = najkrotkie || '-';
            srednaSlowa.textContent = srednia;
        }
        
        // Obsługa zdarzeń
        tekstArea.addEventListener('input', analizujTekst);
        
        wyczyscBtn.addEventListener('click', function() {
            tekstArea.value = '';
            analizujTekst();
        });
        
        szukajBtn.addEventListener('click', function() {
            const szukane = szukajSlowa.value.toLowerCase().trim();
            
            if (!szukane) {
                szukajWynik.textContent = '';
                return;
            }
            
            const tekst = tekstArea.value.toLowerCase();
            const wyrazenia = new RegExp('\\b' + szukane + '\\b', 'g');
            const dopasowania = tekst.match(wyrazenia);
            const ilosc = dopasowania ? dopasowania.length : 0;
            
            if (ilosc > 0) {
                szukajWynik.innerHTML = `<div class="search-result">Znaleziono <strong>${ilosc}</strong> dopasowań słowa "${szukane}"</div>`;
            } else {
                szukajWynik.innerHTML = `<div class="search-result">Nie znaleziono słowa "${szukane}"</div>`;
            }
        });
        
        // Obsługa Enter w polu szukania
        szukajSlowa.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') szukajBtn.click();
        });
        
        // Inicjalna analiza
        analizujTekst();
    </script>
</body>
</html>
```

---

## ZADANIE 7: Gra "Zgadnij liczbę"

### Opis:
Stwórz interaktywną grę, w której gracz zgaduje liczbę losową z komunikatami o zbyt wysokiej/niskiej liczbie.

### Wskazówki:
Przydatne funkcje i metody: `Math.random()`, `Math.floor()`, warunki `if...else if...else`, liczniki, tablica do historii

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Gra - Zgadnij liczbę</title>
    <style>
        body { font-family: Arial; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; }
        .container { max-width: 500px; margin: 0 auto; background: white; padding: 30px; border-radius: 8px; }
        h1 { text-align: center; color: #333; }
        .difficulty { text-align: center; margin: 20px 0; }
        .difficulty button { padding: 8px 15px; margin: 0 5px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        .difficulty button.active { background-color: #28a745; }
        .game-info { text-align: center; background-color: #f9f9f9; padding: 15px; border-radius: 4px; margin: 20px 0; }
        .game-info p { margin: 5px 0; }
        input { width: 100%; padding: 10px; box-sizing: border-box; margin: 10px 0; font-size: 16px; }
        .buttons { display: flex; gap: 10px; margin: 20px 0; }
        .buttons button { flex: 1; padding: 10px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        .message { text-align: center; padding: 15px; margin: 15px 0; border-radius: 4px; font-weight: bold; }
        .success { background-color: #d4edda; color: #155724; }
        .error { background-color: #f8d7da; color: #721c24; }
        .info { background-color: #d1ecf1; color: #0c5460; }
        .history { background-color: #f9f9f9; padding: 15px; margin-top: 20px; border-radius: 4px; }
        .history h3 { margin-top: 0; }
        .game { display: none; }
        .game.active { display: block; }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎮 Zgadnij liczbę</h1>
        
        <div class="difficulty">
            <p>Wybierz poziom trudności:</p>
            <button id="latwoscBtn" class="active">Łatwy (1-50)</button>
            <button id="sredniBtn">Średni (1-100)</button>
            <button id="trudnyBtn">Trudny (1-1000)</button>
        </div>
        
        <div class="game active" id="game">
            <div class="game-info">
                <p>Liczba do zgadnięcia: <strong id="zakres">1-100</strong></p>
                <p>Liczba prób: <strong id="proby">0</strong></p>
            </div>
            
            <input type="number" id="liczba" placeholder="Wpisz swoją liczbę">
            
            <div class="buttons">
                <button id="sprawdzBtn">Sprawdź</button>
                <button id="nowaGraBtn" style="background-color: #28a745;">Nowa gra</button>
            </div>
            
            <div id="komunikat"></div>
            
            <div class="history">
                <h3>Historia ostatnich gier</h3>
                <div id="historiaGier"></div>
            </div>
        </div>
    </div>

    <script>
        let sekretnaLiczba;
        let proby = 0;
        let maxLiczba = 100;
        let historia = [];
        
        const liczbaInput = document.getElementById('liczba');
        const sprawdzBtn = document.getElementById('sprawdzBtn');
        const nowaGraBtn = document.getElementById('nowaGraBtn');
        const komunikatDiv = document.getElementById('komunikat');
        const probySzan = document.getElementById('proby');
        const zakresSpan = document.getElementById('zakres');
        const historiaDiv = document.getElementById('historiaGier');
        
        // Przyciski trudności
        const latwoscBtn = document.getElementById('latwoscBtn');
        const sredniBtn = document.getElementById('sredniBtn');
        const trudnyBtn = document.getElementById('trudnyBtn');
        
        function nowaGra(max) {
            maxLiczba = max;
            sekretnaLiczba = Math.floor(Math.random() * max) + 1;
            proby = 0;
            liczbaInput.value = '';
            komunikatDiv.innerHTML = '';
            liczbaInput.focus();
            
            if (max === 50) {
                zakresSpan.textContent = '1-50';
            } else if (max === 100) {
                zakresSpan.textContent = '1-100';
            } else {
                zakresSpan.textContent = '1-1000';
            }
            
            aktualizujProby();
        }
        
        function aktualizujProby() {
            probySzan.textContent = proby;
        }
        
        function sprawdzLiczbe() {
            const liczba = parseInt(liczbaInput.value);
            
            if (isNaN(liczba) || liczba < 1 || liczba > maxLiczba) {
                komunikatDiv.innerHTML = `<div class="message error">Wpisz liczbę od 1 do ${maxLiczba}!</div>`;
                return;
            }
            
            proby++;
            aktualizujProby();
            
            if (liczba === sekretnaLiczba) {
                komunikatDiv.innerHTML = `<div class="message success">🎉 Brawo! Wpadłeś! Liczba to ${sekretnaLiczba}. Zajęło Ci ${proby} prób.</div>`;
                
                // Dodaj do historii
                historia.unshift({
                    liczba: sekretnaLiczba,
                    proby: proby,
                    data: new Date().toLocaleTimeString('pl-PL')
                });
                if (historia.length > 5) historia.pop();
                
                aktualizujHistorie();
                liczbaInput.disabled = true;
                sprawdzBtn.disabled = true;
            } else if (liczba < sekretnaLiczba) {
                komunikatDiv.innerHTML = `<div class="message info">📈 Za nisko! Spróbuj ponownie.</div>`;
                liczbaInput.value = '';
            } else {
                komunikatDiv.innerHTML = `<div class="message info">📉 Za wysoko! Spróbuj ponownie.</div>`;
                liczbaInput.value = '';
            }
        }
        
        function aktualizujHistorie() {
            historiaDiv.innerHTML = '';
            historia.forEach((gra, index) => {
                const item = document.createElement('div');
                item.style.cssText = 'padding: 8px; margin: 5px 0; background-color: white; border-left: 3px solid #007bff; border-radius: 2px;';
                item.textContent = `Gra ${index + 1}: Liczba ${gra.liczba} - ${gra.proby} prób (${gra.data})`;
                historiaDiv.appendChild(item);
            });
        }
        
        // Obsługa przycisków trudności
        latwoscBtn.addEventListener('click', function() {
            latwoscBtn.classList.add('active');
            sredniBtn.classList.remove('active');
            trudnyBtn.classList.remove('active');
            liczbaInput.disabled = false;
            sprawdzBtn.disabled = false;
            nowaGra(50);
        });
        
        sredniBtn.addEventListener('click', function() {
            latwoscBtn.classList.remove('active');
            sredniBtn.classList.add('active');
            trudnyBtn.classList.remove('active');
            liczbaInput.disabled = false;
            sprawdzBtn.disabled = false;
            nowaGra(100);
        });
        
        trudnyBtn.addEventListener('click', function() {
            latwoscBtn.classList.remove('active');
            sredniBtn.classList.remove('active');
            trudnyBtn.classList.add('active');
            liczbaInput.disabled = false;
            sprawdzBtn.disabled = false;
            nowaGra(1000);
        });
        
        // Obsługa przycisków gry
        sprawdzBtn.addEventListener('click', sprawdzLiczbe);
        
        nowaGraBtn.addEventListener('click', function() {
            liczbaInput.disabled = false;
            sprawdzBtn.disabled = false;
            nowaGra(maxLiczba);
        });
        
        // Obsługa Enter
        liczbaInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') sprawdzLiczbe();
        });
        
        // Inicjalizacja gry
        nowaGra(100);
    </script>
</body>
</html>
```

---

## ZADANIE 8: Harmonogram zadań (TODO List)

### Opis:
Stwórz aplikację do zarządzania listą zadań z możliwością dodawania, usuwania, filtrowania i sortowania.

### Wskazówki:
Przydatne funkcje i metody: obiekty, tablice, `push()`, `filter()`, `map()`, `sort()`, manipulacja DOM, obiekty `Date`

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>TODO List</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 800px; margin: 0 auto; background: white; padding: 20px; border-radius: 8px; }
        .form-group { margin: 15px 0; }
        input, textarea { width: 100%; padding: 10px; box-sizing: border-box; }
        .buttons { display: flex; gap: 10px; margin: 15px 0; flex-wrap: wrap; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; }
        button:hover { background-color: #0056b3; }
        .stats { display: flex; gap: 20px; margin: 20px 0; }
        .stat { background-color: #f9f9f9; padding: 10px; border-radius: 4px; flex: 1; text-align: center; }
        .stat-number { font-size: 24px; font-weight: bold; color: #007bff; }
        .filters { display: flex; gap: 10px; margin: 15px 0; flex-wrap: wrap; }
        .filters button { padding: 8px 15px; font-size: 12px; }
        .filters button.active { background-color: #28a745; }
        .task-item { background-color: #f9f9f9; padding: 15px; margin: 10px 0; border-radius: 4px; display: flex; align-items: center; gap: 10px; }
        .task-item.completed { opacity: 0.6; }
        .task-item.completed .task-text { text-decoration: line-through; }
        .task-item input[type="checkbox"] { width: 20px; height: 20px; cursor: pointer; }
        .task-info { flex: 1; }
        .task-text { font-weight: bold; }
        .task-date { font-size: 12px; color: #666; }
        .task-overdue { color: red; font-weight: bold; }
        .delete-btn { background-color: red; padding: 5px 10px; }
        .empty-message { text-align: center; color: #999; padding: 20px; }
    </style>
</head>
<body>
    <div class="container">
        <h1>✓ Lista zadań (TODO List)</h1>
        
        <div>
            <h3>Dodaj nowe zadanie</h3>
            <div class="form-group">
                <label>Opis zadania:</label>
                <input type="text" id="opis" placeholder="Wpisz opis zadania...">
            </div>
            <div class="form-group">
                <label>Termin wykonania:</label>
                <input type="date" id="termin">
            </div>
            <button id="dodajBtn">Dodaj zadanie</button>
            <button id="wyczyscWszystkieBtn" style="background-color: red;">Wyczyść wykonane</button>
        </div>
        
        <div class="stats">
            <div class="stat">
                <div class="stat-number" id="wszystkich">0</div>
                <div>Wszystkich</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="wykonanych">0</div>
                <div>Wykonanych</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="niewykonanych">0</div>
                <div>Niewykonanych</div>
            </div>
        </div>
        
        <h3>Filtry i sortowanie</h3>
        <div class="filters">
            <button id="wszystkieBtn" class="active">Wszystkie</button>
            <button id="wykonaneBtn">Wykonane</button>
            <button id="niewykonaneBtn">Niewykonane</button>
            <button id="przeterminowaneBtn">Przeterminowane</button>
        </div>
        
        <h3>Zadania</h3>
        <div id="listaZadan"></div>
    </div>

    <script>
        let zadania = [];
        let aktualnyFiltr = 'wszystkie';
        
        const opisInput = document.getElementById('opis');
        const terminInput = document.getElementById('termin');
        const dodajBtn = document.getElementById('dodajBtn');
        const listaDiv = document.getElementById('listaZadan');
        const wszystkichSpan = document.getElementById('wszystkich');
        const wykonanychSpan = document.getElementById('wykonanych');
        const niewykonanychSpan = document.getElementById('niewykonanych');
        const wyczyscWszystkieBtn = document.getElementById('wyczyscWszystkieBtn');
        
        // Filtry
        const wszystkieBtn = document.getElementById('wszystkieBtn');
        const wykonaneBtn = document.getElementById('wykonaneBtn');
        const niewykonaneBtn = document.getElementById('niewykonaneBtn');
        const przeterminowaneBtn = document.getElementById('przeterminowaneBtn');
        
        function dodajZadanie() {
            const opis = opisInput.value.trim();
            const termin = terminInput.value;
            
            if (!opis) {
                alert('Wpisz opis zadania!');
                return;
            }
            
            const zadanie = {
                id: Date.now(),
                opis: opis,
                termin: termin || null,
                wykonane: false,
                dataDodania: new Date().toLocaleDateString('pl-PL')
            };
            
            zadania.push(zadanie);
            opisInput.value = '';
            terminInput.value = '';
            
            aktualizujWyswietlanie();
        }
        
        function usunZadanie(id) {
            zadania = zadania.filter(z => z.id !== id);
            aktualizujWyswietlanie();
        }
        
        function przywracacWykonanie(id) {
            const zadanie = zadania.find(z => z.id === id);
            if (zadanie) {
                zadanie.wykonane = !zadanie.wykonane;
                aktualizujWyswietlanie();
            }
        }
        
        function czy_przeterminowane(termin) {
            if (!termin) return false;
            const hoje = new Date();
            hoje.setHours(0, 0, 0, 0);
            const dataTerm = new Date(termin);
            return dataTerm < hoje;
        }
        
        function aktualizujWyswietlanie() {
            // Statystyki
            const wszystkich = zadania.length;
            const wykonanych = zadania.filter(z => z.wykonane).length;
            const niewykonanych = wszystkich - wykonanych;
            
            wszystkichSpan.textContent = wszystkich;
            wykonanychSpan.textContent = wykonanych;
            niewykonanychSpan.textContent = niewykonanych;
            
            // Filtrowanie
            let pokazywaZadania = [...zadania];
            
            if (aktualnyFiltr === 'wykonane') {
                pokazywaZadania = pokazywaZadania.filter(z => z.wykonane);
            } else if (aktualnyFiltr === 'niewykonane') {
                pokazywaZadania = pokazywaZadania.filter(z => !z.wykonane);
            } else if (aktualnyFiltr === 'przeterminowane') {
                pokazywaZadania = pokazywaZadania.filter(z => !z.wykonane && czy_przeterminowane(z.termin));
            }
            
            // Wyświetlanie
            listaDiv.innerHTML = '';
            
            if (pokazywaZadania.length === 0) {
                listaDiv.innerHTML = '<div class="empty-message">Brak zadań w tej kategorii</div>';
                return;
            }
            
            pokazywaZadania.forEach(zadanie => {
                const itemDiv = document.createElement('div');
                itemDiv.className = 'task-item' + (zadanie.wykonane ? ' completed' : '');
                
                const isPrzeterminowane = !zadanie.wykonane && czy_przeterminowane(zadanie.termin);
                const terminText = zadanie.termin ? new Date(zadanie.termin).toLocaleDateString('pl-PL') : 'Brak terminu';
                
                itemDiv.innerHTML = `
                    <input type="checkbox" ${zadanie.wykonane ? 'checked' : ''} onchange="window.przywracacWykonanie(${zadanie.id})">
                    <div class="task-info">
                        <div class="task-text">${zadanie.opis}</div>
                        <div class="task-date ${isPrzeterminowane ? 'task-overdue' : ''}">
                            Termin: ${terminText} ${isPrzeterminowane ? '(PRZETERMINOWANE!)' : ''}
                        </div>
                    </div>
                    <button class="delete-btn" onclick="window.usunZadanie(${zadanie.id})">Usuń</button>
                `;
                listaDiv.appendChild(itemDiv);
            });
        }
        
        // Obsługa przycisków
        dodajBtn.addEventListener('click', dodajZadanie);
        
        wyczyscWszystkieBtn.addEventListener('click', function() {
            zadania = zadania.filter(z => !z.wykonane);
            aktualnyFiltr = 'wszystkie';
            wszystkieBtn.classList.add('active');
            wykonaneBtn.classList.remove('active');
            niewykonaneBtn.classList.remove('active');
            przeterminowaneBtn.classList.remove('active');
            aktualizujWyswietlanie();
        });
        
        wszystkieBtn.addEventListener('click', function() {
            aktualnyFiltr = 'wszystkie';
            wszystkieBtn.classList.add('active');
            wykonaneBtn.classList.remove('active');
            niewykonaneBtn.classList.remove('active');
            przeterminowaneBtn.classList.remove('active');
            aktualizujWyswietlanie();
        });
        
        wykonaneBtn.addEventListener('click', function() {
            aktualnyFiltr = 'wykonane';
            wszystkieBtn.classList.remove('active');
            wykonaneBtn.classList.add('active');
            niewykonaneBtn.classList.remove('active');
            przeterminowaneBtn.classList.remove('active');
            aktualizujWyswietlanie();
        });
        
        niewykonaneBtn.addEventListener('click', function() {
            aktualnyFiltr = 'niewykonane';
            wszystkieBtn.classList.remove('active');
            wykonaneBtn.classList.remove('active');
            niewykonaneBtn.classList.add('active');
            przeterminowaneBtn.classList.remove('active');
            aktualizujWyswietlanie();
        });
        
        przeterminowaneBtn.addEventListener('click', function() {
            aktualnyFiltr = 'przeterminowane';
            wszystkieBtn.classList.remove('active');
            wykonaneBtn.classList.remove('active');
            niewykonaneBtn.classList.remove('active');
            przeterminowaneBtn.classList.add('active');
            aktualizujWyswietlanie();
        });
        
        // Obsługa Enter
        opisInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') dodajZadanie();
        });
        
        // Udostępnienie funkcji w globalnym scope
        window.usunZadanie = usunZadanie;
        window.przywracacWykonanie = przywracacWykonanie;
        
        aktualizujWyswietlanie();
    </script>
</body>
</html>
```

---

## ZADANIE 9: Kalkulator rat kredytowych

### Opis:
Stwórz kalkulator do obliczania rat kredytowych z harmonogramem amortyzacji.

### Wskazówki:
Przydatne funkcje i metody: `Math.pow()`, pętle `for`, tworzenie tabel HTML, `toFixed(2)`, operacje matematyczne

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Kalkulator rat kredytowych</title>
    <style>
        body { font-family: Arial; padding: 20px; background-color: #f0f0f0; }
        .container { max-width: 900px; margin: 0 auto; background: white; padding: 20px; border-radius: 8px; }
        .form-group { margin: 15px 0; }
        input { width: 100%; padding: 10px; box-sizing: border-box; margin: 5px 0; }
        label { font-weight: bold; }
        .button-group { margin: 20px 0; }
        button { padding: 10px 20px; background-color: #007bff; color: white; border: none; cursor: pointer; border-radius: 4px; margin-right: 10px; }
        button:hover { background-color: #0056b3; }
        .summary { display: grid; grid-template-columns: repeat(3, 1fr); gap: 15px; margin: 20px 0; }
        .summary-box { background-color: #f9f9f9; padding: 15px; border-radius: 4px; text-align: center; border-left: 4px solid #007bff; }
        .summary-value { font-size: 20px; font-weight: bold; color: #007bff; }
        .summary-label { color: #666; margin-top: 5px; }
        .schedule { margin-top: 30px; }
        table { width: 100%; border-collapse: collapse; }
        th { background-color: #007bff; color: white; padding: 10px; text-align: left; }
        td { padding: 10px; border-bottom: 1px solid #ddd; }
        tr:nth-child(even) { background-color: #f9f9f9; }
        .error { color: red; font-weight: bold; margin: 10px 0; }
    </style>
</head>
<body>
    <div class="container">
        <h1>Kalkulator rat kredytowych</h1>
        
        <div>
            <div class="form-group">
                <label>Kwota kredytu (zł):</label>
                <input type="number" id="kwotaKredytu" placeholder="np. 100000" min="1" step="1000">
            </div>
            
            <div class="form-group">
                <label>Oprocentowanie roczne (%):</label>
                <input type="number" id="oprocentowanie" placeholder="np. 5" min="0" max="100" step="0.1">
            </div>
            
            <div class="form-group">
                <label>Okres spłaty (liczba miesięcy):</label>
                <input type="number" id="okresSpluty" placeholder="np. 360" min="1" step="1">
            </div>
            
            <div class="button-group">
                <button id="obliczBtn">Oblicz ratę</button>
                <button id="drukujBtn" style="background-color: #28a745;">Drukuj harmonogram</button>
            </div>
        </div>
        
        <div id="blad"></div>
        
        <div class="summary" id="summary" style="display: none;">
            <div class="summary-box">
                <div class="summary-value" id="rataMiesięczna">0.00</div>
                <div class="summary-label">Rata miesięczna (zł)</div>
            </div>
            <div class="summary-box">
                <div class="summary-value" id="laczznaKwota">0.00</div>
                <div class="summary-label">Łączna kwota do spłaty (zł)</div>
            </div>
            <div class="summary-box">
                <div class="summary-value" id="odsetki">0.00</div>
                <div class="summary-label">Łączne odsetki (zł)</div>
            </div>
        </div>
        
        <div class="schedule" id="schedule"></div>
    </div>

    <script>
        const kwotaInput = document.getElementById('kwotaKredytu');
        const oprocentowanieInput = document.getElementById('oprocentowanie');
        const okresInput = document.getElementById('okresSpluty');
        const obliczBtn = document.getElementById('obliczBtn');
        const drukujBtn = document.getElementById('drukujBtn');
        const summaryDiv = document.getElementById('summary');
        const scheduleDiv = document.getElementById('schedule');
        const bladDiv = document.getElementById('blad');
        
        let harmonogram = [];
        
        function obliczRate() {
            bladDiv.textContent = '';
            
            const kwota = parseFloat(kwotaInput.value);
            const roczen = parseFloat(oprocentowanieInput.value);
            const miesiace = parseInt(okresInput.value);
            
            // Walidacja
            if (isNaN(kwota) || kwota <= 0) {
                bladDiv.textContent = 'Błąd: Wpisz prawidłową kwotę kredytu!';
                return;
            }
            if (isNaN(roczen) || roczen < 0) {
                bladDiv.textContent = 'Błąd: Wpisz prawidłowe oprocentowanie!';
                return;
            }
            if (isNaN(miesiace) || miesiace <= 0) {
                bladDiv.textContent = 'Błąd: Wpisz prawidłowy okres spłaty!';
                return;
            }
            
            // Obliczenie raty
            const r = roczen / 100 / 12; // Oprocentowanie miesięczne
            
            let rata;
            if (r === 0) {
                rata = kwota / miesiace;
            } else {
                rata = kwota * (r * Math.pow(1 + r, miesiace)) / (Math.pow(1 + r, miesiace) - 1);
            }
            
            // Generowanie harmonogramu
            harmonogram = [];
            let pozostalaKwota = kwota;
            let laczeOdsetki = 0;
            
            for (let i = 1; i <= miesiace; i++) {
                const odsetki = pozostalaKwota * r;
                const kapital = rata - odsetki;
                pozostalaKwota -= kapital;
                
                // Dostosowanie ostatniej raty
                let ostatecznaRata = rata;
                let ostateczneOdsetki = odsetki;
                let ostatecznyKapital = kapital;
                
                if (i === miesiace) {
                    ostatecznaRata = (rata - odsetki) + pozostalaKwota;
                    ostatecznyKapital = ostatecznaRata - ostateczneOdsetki;
                    pozostalaKwota = 0;
                }
                
                laczeOdsetki += ostateczneOdsetki;
                
                harmonogram.push({
                    numer: i,
                    rata: ostatecznaRata.toFixed(2),
                    odsetki: ostateczneOdsetki.toFixed(2),
                    kapital: ostatecznyKapital.toFixed(2),
                    pozostala: Math.max(0, pozostalaKwota).toFixed(2)
                });
            }
            
            // Wyświetlenie wyników
            document.getElementById('rataMiesięczna').textContent = rata.toFixed(2);
            document.getElementById('laczznaKwota').textContent = (kwota + laczeOdsetki).toFixed(2);
            document.getElementById('odsetki').textContent = laczeOdsetki.toFixed(2);
            summaryDiv.style.display = 'grid';
            
            wyswietlHarmonogram();
        }
        
        function wyswietlHarmonogram() {
            scheduleDiv.innerHTML = '';
            
            if (harmonogram.length === 0) return;
            
            const tabela = document.createElement('table');
            const naglowek = tabela.createTHead();
            const wierszNaglowka = naglowek.insertRow(0);
            
            const kolumny = ['Rata', 'Kwota raty', 'Odsetki', 'Kapitał', 'Pozostała do spłaty'];
            kolumny.forEach(kolumna => {
                const komórka = wierszNaglowka.insertCell();
                komórka.textContent = kolumna;
            });
            
            const cialo = tabela.createTBody();
            harmonogram.forEach(wiersz => {
                const nowyWiersz = cialo.insertRow();
                nowyWiersz.insertCell(0).textContent = wiersz.numer;
                nowyWiersz.insertCell(1).textContent = wiersz.rata + ' zł';
                nowyWiersz.insertCell(2).textContent = wiersz.odsetki + ' zł';
                nowyWiersz.insertCell(3).textContent = wiersz.kapital + ' zł';
                nowyWiersz.insertCell(4).textContent = wiersz.pozostala + ' zł';
            });
            
            const h3 = document.createElement('h3');
            h3.textContent = 'Harmonogram amortyzacji';
            scheduleDiv.appendChild(h3);
            scheduleDiv.appendChild(tabela);
        }
        
        obliczBtn.addEventListener('click', obliczRate);
        
        drukujBtn.addEventListener('click', function() {
            window.print();
        });
        
        // Obsługa Enter
        [kwotaInput, oprocentowanieInput, okresInput].forEach(input => {
            input.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') obliczRate();
            });
        });
    </script>
</body>
</html>
```

---

## ZADANIE 10: Aplikacja do nauki słówek (Flashcards)

### Opis:
Stwórz aplikację do nauki słówek z kartami (flashcards) z możliwością tasowania i śledzenia postępu.

### Wskazówki:
Przydatne funkcje i metody: tablice obiektów, zmienne do śledzenia bieżącej karty, `addEventListener()`, `.sort()`, `classList.toggle()`

### Kod HTML:
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Flashcards - Nauka słówek</title>
    <style>
        body { font-family: Arial; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; }
        .container { max-width: 600px; margin: 0 auto; }
        .card-container { perspective: 1000px; margin: 30px 0; }
        .card { background: white; padding: 40px; border-radius: 8px; box-shadow: 0 4px 8px rgba(0,0,0,0.2); min-height: 250px; display: flex; flex-direction: column; justify-content: center; align-items: center; cursor: pointer; transition: transform 0.6s; transform-style: preserve-3d; position: relative; }
        .card:hover { transform: rotateY(180deg); }
        .card-front, .card-back { position: absolute; width: 100%; height: 100%; display: flex; flex-direction: column; justify-content: center; align-items: center; }
        .card-front { backface-visibility: hidden; }
        .card-back { transform: rotateY(180deg); backface-visibility: hidden; background-color: #f0f0f0; }
        .card-question { font-size: 28px; font-weight: bold; color: #333; text-align: center; }
        .card-answer { font-size: 24px; font-weight: bold; color: #007bff; text-align: center; }
        .card-label { font-size: 12px; color: #999; margin-top: 20px; }
        .progress { text-align: center; color: white; margin: 20px 0; font-size: 18px; }
        .progress-bar { background-color: rgba(255,255,255,0.3); height: 20px; border-radius: 10px; overflow: hidden; margin: 10px 0; }
        .progress-fill { background-color: #28a745; height: 100%; width: 0%; transition: width 0.3s; }
        .buttons { display: flex; gap: 10px; margin: 20px 0; flex-wrap: wrap; justify-content: center; }
        button { padding: 10px 20px; background-color: white; color: #667eea; border: none; cursor: pointer; border-radius: 4px; font-weight: bold; transition: 0.3s; }
        button:hover { background-color: #f0f0f0; }
        button.active { background-color: #28a745; color: white; }
        .stats { background: white; padding: 15px; border-radius: 8px; text-align: center; margin-bottom: 20px; }
        .stat-item { display: inline-block; margin: 0 15px; }
        .stat-number { font-size: 24px; font-weight: bold; color: #007bff; }
        .stat-label { color: #666; font-size: 12px; }
        .card-simple { display: flex; flex-direction: column; justify-content: center; align-items: center; text-align: center; }
        .add-card-form { background: white; padding: 20px; border-radius: 8px; margin-top: 20px; }
        input, textarea { width: 100%; padding: 10px; margin: 10px 0; box-sizing: border-box; }
    </style>
</head>
<body>
    <div class="container">
        <h1 style="text-align: center; color: white;">📚 Nauka słówek (Flashcards)</h1>
        
        <div class="stats">
            <div class="stat-item">
                <div class="stat-number" id="biezacaKarta">1</div>
                <div class="stat-label">Karta</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="lacznie">0</div>
                <div class="stat-label">Razem</div>
            </div>
            <div class="stat-item">
                <div class="stat-number" id="zaliczone">0</div>
                <div class="stat-label">Zaliczone</div>
            </div>
        </div>
        
        <div class="progress">
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
        </div>
        
        <div class="card-container">
            <div class="card" id="karta">
                <div class="card-front">
                    <div class="card-simple">
                        <div class="card-question" id="pytanie">apple</div>
                        <div class="card-label">Kliknij aby zobaczyć odpowiedź</div>
                    </div>
                </div>
                <div class="card-back">
                    <div class="card-simple">
                        <div class="card-answer" id="odpowiedz">jabłko</div>
                        <div class="card-label">Odpowiedź</div>
                    </div>
                </div>
            </div>
        </div>
        
        <div class="buttons">
            <button id="poprzedniaBtn">← Poprzednia</button>
            <button id="czekujBtn">Czekaj</button>
            <button id="nastepnaBtn">Następna →</button>
            <button id="shuffle">🔀 Tasuj</button>
            <button id="reset">↺ Resetuj</button>
        </div>
        
        <div class="add-card-form">
            <h3>Dodaj nową kartę</h3>
            <input type="text" id="noweS" placeholder="Słowo/pytanie">
            <input type="text" id="nowaOdp" placeholder="Odpowiedź/tłumaczenie">
            <button id="dodajKarteBtn">Dodaj kartę</button>
        </div>
    </div>

    <script>
        let karty = [
            { question: "apple", answer: "jabłko" },
            { question: "book", answer: "książka" },
            { question: "computer", answer: "komputer" },
            { question: "door", answer: "drzwi" },
            { question: "elephant", answer: "słoń" },
            { question: "flower", answer: "kwiat" },
            { question: "guitar", answer: "gitara" },
            { question: "house", answer: "dom" },
            { question: "ice", answer: "lód" },
            { question: "jacket", answer: "kurtka" }
        ];
        
        let biezacaKarta = 0;
        let zaliczone = [];
        
        const kartaDiv = document.getElementById('karta');
        const pytanieDiv = document.getElementById('pytanie');
        const odpowiedzDiv = document.getElementById('odpowiedz');
        const poprzedniaBtn = document.getElementById('poprzedniaBtn');
        const nastepnaBtn = document.getElementById('nastepnaBtn');
        const czekujBtn = document.getElementById('czekujBtn');
        const shuffleBtn = document.getElementById('shuffle');
        const resetBtn = document.getElementById('reset');
        const biezacaKartaSpan = document.getElementById('biezacaKarta');
        const laczenieSpan = document.getElementById('lacznie');
        const zaliczoneSpan = document.getElementById('zaliczone');
        const progressFill = document.getElementById('progressFill');
        const noweSlowo = document.getElementById('noweS');
        const nowaOdp = document.getElementById('nowaOdp');
        const dodajKarteBtn = document.getElementById('dodajKarteBtn');
        
        function wyswietlKarte() {
            if (karty.length === 0) {
                pytanieDiv.textContent = 'Brak kart!';
                odpowiedzDiv.textContent = 'Dodaj nowe karty';
                return;
            }
            
            pytanieDiv.textContent = karty[biezacaKarta].question;
            odpowiedzDiv.textContent = karty[biezacaKarta].answer;
            
            // Reset obrotu karty
            kartaDiv.style.transform = 'rotateY(0deg)';
            
            // Aktualizacja liczników
            biezacaKartaSpan.textContent = biezacaKarta + 1;
            laczenieSpan.textContent = karty.length;
            zaliczoneSpan.textContent = zaliczone.length;
            
            // Aktualizacja paska postępu
            const procent = (zaliczone.length / karty.length) * 100;
            progressFill.style.width = procent + '%';
            
            // Aktualizacja przycisków
            poprzedniaBtn.disabled = biezacaKarta === 0;
            nastepnaBtn.disabled = biezacaKarta === karty.length - 1;
        }
        
        function poprzednia() {
            if (biezacaKarta > 0) {
                biezacaKarta--;
                wyswietlKarte();
            }
        }
        
        function nastepna() {
            if (biezacaKarta < karty.length - 1) {
                biezacaKarta++;
                wyswietlKarte();
            }
        }
        
        function zaliczKarte() {
            if (!zaliczone.includes(biezacaKarta)) {
                zaliczone.push(biezacaKarta);
            }
            wyswietlKarte();
        }
        
        function tasujKarty() {
            for (let i = karty.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [karty[i], karty[j]] = [karty[j], karty[i]];
            }
            biezacaKarta = 0;
            zaliczone = [];
            wyswietlKarte();
        }
        
        function resetuj() {
            biezacaKarta = 0;
            zaliczone = [];
            wyswietlKarte();
        }
        
        function dodajKarte() {
            const slowo = noweSlowo.value.trim();
            const odpowiedz = nowaOdp.value.trim();
            
            if (!slowo || !odpowiedz) {
                alert('Wpisz słowo i odpowiedź!');
                return;
            }
            
            karty.push({
                question: slowo,
                answer: odpowiedz
            });
            
            noweSlowo.value = '';
            nowaOdp.value = '';
            
            wyswietlKarte();
            alert('Dodano nową kartę!');
        }
        
        // Obsługa przycisków
        poprzedniaBtn.addEventListener('click', poprzednia);
        nastepnaBtn.addEventListener('click', nastepna);
        czekujBtn.addEventListener('click', zaliczKarte);
        shuffleBtn.addEventListener('click', tasujKarty);
        resetBtn.addEventListener('click', resetuj);
        dodajKarteBtn.addEventListener('click', dodajKarte);
        
        // Obsługa kliknięcia na kartę
        kartaDiv.addEventListener('click', function() {
            kartaDiv.style.transform = kartaDiv.style.transform === 'rotateY(180deg)' ? 'rotateY(0deg)' : 'rotateY(180deg)';
        });
        
        // Obsługa Enter w polach
        noweSlowo.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') dodajKarte();
        });
        
        nowaOdp.addEventListener('keypress', function(e) {
            if (e.key === 'Enter') dodajKarte();
        });
        
        // Inicjalizacja
        wyswietlKarte();
    </script>
</body>
</html>
```

---

## Podsumowanie

Wszystkie 10 zadań zawiera pełny kod HTML/CSS/JavaScript, który można natychmiast uruchomić w przeglądarce. Każde zadanie:

- ✅ Jest na poziomie trudności egzaminu INF.03
- ✅ Zawiera komentarze wyjaśniające kod
- ✅ Demonstruje ważne koncepty JavaScript
- ✅ Jest w pełni funkcjonalne i testowane
- ✅ Zawiera obsługę błędów i walidacji
- ✅ Ma estetyczne interfejsy użytkownika

Powodzenia w przygotowaniach do egzaminu INF.03!