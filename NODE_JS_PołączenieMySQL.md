# 🗄️ JavaScript i Bazy Danych MySQL

## Materiał dodatkowy - wykraczający poza podstawę programową

---

## 📋 Spis treści

1. [Wstęp - dlaczego Node.js?](#1-wstęp---dlaczego-nodejs)
2. [Instalacja środowiska](#2-instalacja-środowiska)
3. [Biblioteka mysql2](#3-biblioteka-mysql2)
4. [Nawiązywanie połączenia](#4-nawiązywanie-połączenia)
5. [Operacje CRUD](#5-operacje-crud)
6. [Prepared Statements - bezpieczeństwo](#6-prepared-statements---bezpieczeństwo)
7. [Pula połączeń (Connection Pool)](#7-pula-połączeń-connection-pool)
8. [Async/Await - nowoczesna składnia](#8-asyncawait---nowoczesna-składnia)
9. [Kompletny przykład - Mini API](#9-kompletny-przykład---mini-api)
10. [Podsumowanie](#10-podsumowanie)

---

## 1. Wstęp - dlaczego Node.js?

### ⚠️ JavaScript w przeglądarce NIE MOŻE łączyć się z bazą danych!

```
┌─────────────────┐         ┌─────────────────┐
│   PRZEGLĄDARKA  │    ❌    │     MySQL       │
│   (JavaScript)  │ ──────── │     Baza        │
│                 │  NIE!    │                 │
└─────────────────┘         └─────────────────┘
```

**Dlaczego?**
- Bezpieczeństwo - dane logowania byłyby widoczne dla użytkownika
- Przeglądarka nie ma dostępu do protokołów bazodanowych
- Każdy mógłby modyfikować bazę z poziomu konsoli

### ✅ Rozwiązanie: Node.js (JavaScript na serwerze)

```
┌─────────────┐       ┌─────────────┐       ┌─────────────┐
│ PRZEGLĄDARKA│       │   SERWER    │       │   MySQL     │
│             │ ────► │  (Node.js)  │ ────► │   Baza      │
│  Frontend   │  API  │  Backend    │  SQL  │             │
└─────────────┘       └─────────────┘       └─────────────┘
```

**Node.js** to środowisko uruchomieniowe JavaScript poza przeglądarką - pozwala pisać kod serwerowy w JS.

---

## 2. Instalacja środowiska

### Krok 1: Zainstaluj Node.js

Pobierz z oficjalnej strony: [https://nodejs.org](https://nodejs.org)

Wybierz wersję **LTS** (Long Term Support).

Sprawdź instalację w terminalu:
```bash
node --version
# np. v20.10.0

npm --version
# np. 10.2.3
```

### Krok 2: Utwórz projekt

```bash
# Utwórz folder projektu
mkdir moj-projekt-mysql
cd moj-projekt-mysql

# Zainicjuj projekt Node.js
npm init -y
```

To utworzy plik `package.json` - manifest projektu.

### Krok 3: Zainstaluj bibliotekę mysql2

```bash
npm install mysql2
```

**Dlaczego `mysql2` a nie `mysql`?**
- `mysql2` jest nowsza i szybsza
- Obsługuje Promises i async/await
- Kompatybilna z MySQL 8.0+
- Lepsza obsługa prepared statements

---

## 3. Biblioteka mysql2

### Struktura projektu

```
moj-projekt-mysql/
├── node_modules/      ← biblioteki (ignoruj w git!)
├── package.json       ← manifest projektu
├── package-lock.json  ← wersje bibliotek
└── app.js             ← Twój kod
```

### Importowanie biblioteki

```javascript
// Sposób 1: CommonJS (tradycyjny)
const mysql = require('mysql2');

// Sposób 2: ES Modules (nowoczesny - wymaga "type": "module" w package.json)
import mysql from 'mysql2';
```

W tej lekcji używamy składni **CommonJS** (require).

---

## 4. Nawiązywanie połączenia

### Podstawowe połączenie

```javascript
const mysql = require('mysql2');

// Konfiguracja połączenia
const connection = mysql.createConnection({
    host: 'localhost',       // adres serwera MySQL
    port: 3306,              // port (domyślnie 3306)
    user: 'root',            // nazwa użytkownika
    password: 'mojeHaslo',   // hasło
    database: 'szkola'       // nazwa bazy danych
});

// Nawiązanie połączenia
connection.connect(function(err) {
    if (err) {
        console.error('Błąd połączenia:', err.message);
        return;
    }
    console.log('Połączono z bazą danych MySQL!');
});
```

### Zamykanie połączenia

```javascript
// Po zakończeniu pracy z bazą
connection.end(function(err) {
    if (err) {
        console.error('Błąd zamykania:', err.message);
        return;
    }
    console.log('Połączenie zamknięte.');
});
```

### Obsługa błędów połączenia

```javascript
connection.connect(function(err) {
    if (err) {
        switch (err.code) {
            case 'ECONNREFUSED':
                console.error('MySQL nie działa lub zły port');
                break;
            case 'ER_ACCESS_DENIED_ERROR':
                console.error('Błędna nazwa użytkownika lub hasło');
                break;
            case 'ER_BAD_DB_ERROR':
                console.error('Baza danych nie istnieje');
                break;
            default:
                console.error('Błąd:', err.message);
        }
        return;
    }
    console.log('Połączono!');
});
```

---

## 5. Operacje CRUD

**CRUD** = Create, Read, Update, Delete

### Przykładowa tabela

```sql
CREATE TABLE uczniowie (
    id INT AUTO_INCREMENT PRIMARY KEY,
    imie VARCHAR(50) NOT NULL,
    nazwisko VARCHAR(50) NOT NULL,
    klasa VARCHAR(10),
    srednia DECIMAL(3,2),
    data_urodzenia DATE
);
```

### 5.1 CREATE - Dodawanie rekordów

```javascript
// Dodanie jednego rekordu
const sql = 'INSERT INTO uczniowie (imie, nazwisko, klasa, srednia) VALUES (?, ?, ?, ?)';
const dane = ['Jan', 'Kowalski', '3TI', 4.75];

connection.query(sql, dane, function(err, result) {
    if (err) {
        console.error('Błąd dodawania:', err.message);
        return;
    }
    console.log('Dodano ucznia, ID:', result.insertId);
    console.log('Zmodyfikowanych wierszy:', result.affectedRows);
});
```

### 5.2 READ - Pobieranie danych

```javascript
// Pobranie wszystkich rekordów
connection.query('SELECT * FROM uczniowie', function(err, results) {
    if (err) {
        console.error('Błąd:', err.message);
        return;
    }
    
    console.log('Liczba uczniów:', results.length);
    
    // results to tablica obiektów
    results.forEach(function(uczen) {
        console.log(uczen.id, uczen.imie, uczen.nazwisko);
    });
});
```

```javascript
// Pobranie z warunkiem WHERE
const sql = 'SELECT * FROM uczniowie WHERE klasa = ?';

connection.query(sql, ['3TI'], function(err, results) {
    if (err) {
        console.error('Błąd:', err.message);
        return;
    }
    console.log('Uczniowie z 3TI:', results);
});
```

```javascript
// Pobranie jednego rekordu
const sql = 'SELECT * FROM uczniowie WHERE id = ?';

connection.query(sql, [5], function(err, results) {
    if (err) {
        console.error('Błąd:', err.message);
        return;
    }
    
    if (results.length === 0) {
        console.log('Nie znaleziono ucznia');
        return;
    }
    
    const uczen = results[0];  // pierwszy (jedyny) wynik
    console.log('Znaleziono:', uczen.imie, uczen.nazwisko);
});
```

### 5.3 UPDATE - Aktualizacja danych

```javascript
const sql = 'UPDATE uczniowie SET srednia = ? WHERE id = ?';
const dane = [5.00, 3];  // nowa średnia, ID ucznia

connection.query(sql, dane, function(err, result) {
    if (err) {
        console.error('Błąd aktualizacji:', err.message);
        return;
    }
    
    if (result.affectedRows === 0) {
        console.log('Nie znaleziono ucznia o podanym ID');
        return;
    }
    
    console.log('Zaktualizowano rekordów:', result.affectedRows);
    console.log('Zmienionych wartości:', result.changedRows);
});
```

### 5.4 DELETE - Usuwanie danych

```javascript
const sql = 'DELETE FROM uczniowie WHERE id = ?';

connection.query(sql, [10], function(err, result) {
    if (err) {
        console.error('Błąd usuwania:', err.message);
        return;
    }
    
    if (result.affectedRows === 0) {
        console.log('Nie znaleziono ucznia do usunięcia');
        return;
    }
    
    console.log('Usunięto rekordów:', result.affectedRows);
});
```

---

## 6. Prepared Statements - bezpieczeństwo

### ⚠️ NIGDY nie składaj zapytań SQL ze stringów!

```javascript
// ❌ BARDZO ŹLE - podatne na SQL Injection!
const id = req.query.id;  // np. "1; DROP TABLE uczniowie;--"
const sql = 'SELECT * FROM uczniowie WHERE id = ' + id;
connection.query(sql);  // KATASTROFA!
```

### ✅ ZAWSZE używaj prepared statements (placeholderów `?`)

```javascript
// ✅ DOBRZE - bezpieczne
const sql = 'SELECT * FROM uczniowie WHERE id = ?';
connection.query(sql, [id]);  // id jest automatycznie escapowane
```

### Jak to działa?

```javascript
// Placeholder ? jest zastępowany przez bezpiecznie sformatowaną wartość
const sql = 'SELECT * FROM uczniowie WHERE klasa = ? AND srednia > ?';
const parametry = ['3TI', 4.0];

// MySQL otrzyma:
// SELECT * FROM uczniowie WHERE klasa = '3TI' AND srednia > 4.0
```

### Wiele placeholderów

```javascript
const sql = `
    INSERT INTO uczniowie (imie, nazwisko, klasa, srednia, data_urodzenia) 
    VALUES (?, ?, ?, ?, ?)
`;
const dane = ['Anna', 'Nowak', '2TI', 4.85, '2007-03-15'];

connection.query(sql, dane, function(err, result) {
    // ...
});
```

### Named placeholders (alternatywa)

```javascript
const sql = 'SELECT * FROM uczniowie WHERE klasa = :klasa AND srednia > :min';
const dane = { klasa: '3TI', min: 4.0 };

connection.query(sql, dane, function(err, results) {
    // ...
});
```

---

## 7. Pula połączeń (Connection Pool)

### Problem z pojedynczym połączeniem

Jedno połączenie = jedna operacja na raz. Przy wielu użytkownikach to wąskie gardło.

### Rozwiązanie: Connection Pool

Pula utrzymuje wiele połączeń gotowych do użycia.

```javascript
const mysql = require('mysql2');

// Utworzenie puli połączeń
const pool = mysql.createPool({
    host: 'localhost',
    user: 'root',
    password: 'mojeHaslo',
    database: 'szkola',
    
    // Konfiguracja puli
    waitForConnections: true,  // czekaj jeśli wszystkie zajęte
    connectionLimit: 10,       // max 10 połączeń
    queueLimit: 0              // brak limitu kolejki (0 = bez limitu)
});

// Użycie - automatyczne pobieranie i zwalnianie połączenia
pool.query('SELECT * FROM uczniowie', function(err, results) {
    if (err) {
        console.error('Błąd:', err.message);
        return;
    }
    console.log(results);
    // Połączenie automatycznie wraca do puli
});
```

### Ręczne zarządzanie połączeniem z puli

```javascript
pool.getConnection(function(err, connection) {
    if (err) {
        console.error('Błąd pobierania połączenia:', err.message);
        return;
    }
    
    // Użyj połączenia
    connection.query('SELECT * FROM uczniowie', function(err, results) {
        // WAŻNE: Zwolnij połączenie po użyciu!
        connection.release();
        
        if (err) {
            console.error('Błąd:', err.message);
            return;
        }
        console.log(results);
    });
});
```

---

## 8. Async/Await - nowoczesna składnia

Callbacki mogą być nieczytelne. Async/await to elegantsze rozwiązanie.

### Włączenie obsługi Promise

```javascript
const mysql = require('mysql2/promise');  // ← /promise na końcu!
```

### Połączenie z async/await

```javascript
const mysql = require('mysql2/promise');

async function main() {
    // Nawiązanie połączenia
    const connection = await mysql.createConnection({
        host: 'localhost',
        user: 'root',
        password: 'mojeHaslo',
        database: 'szkola'
    });
    
    console.log('Połączono z bazą!');
    
    try {
        // Zapytanie SELECT
        const [rows, fields] = await connection.query('SELECT * FROM uczniowie');
        console.log('Uczniowie:', rows);
        
        // Zapytanie INSERT
        const [result] = await connection.query(
            'INSERT INTO uczniowie (imie, nazwisko, klasa) VALUES (?, ?, ?)',
            ['Piotr', 'Wiśniewski', '1TI']
        );
        console.log('Nowe ID:', result.insertId);
        
    } catch (error) {
        console.error('Błąd zapytania:', error.message);
    } finally {
        // Zawsze zamknij połączenie
        await connection.end();
        console.log('Połączenie zamknięte.');
    }
}

// Uruchomienie
main();
```

### Pula połączeń z async/await

```javascript
const mysql = require('mysql2/promise');

// Utworzenie puli
const pool = mysql.createPool({
    host: 'localhost',
    user: 'root',
    password: 'mojeHaslo',
    database: 'szkola',
    connectionLimit: 10
});

async function pobierzUczniow() {
    try {
        const [rows] = await pool.query('SELECT * FROM uczniowie');
        return rows;
    } catch (error) {
        console.error('Błąd:', error.message);
        throw error;
    }
}

async function dodajUcznia(imie, nazwisko, klasa) {
    try {
        const [result] = await pool.query(
            'INSERT INTO uczniowie (imie, nazwisko, klasa) VALUES (?, ?, ?)',
            [imie, nazwisko, klasa]
        );
        return result.insertId;
    } catch (error) {
        console.error('Błąd dodawania:', error.message);
        throw error;
    }
}

// Użycie
async function main() {
    const uczniowie = await pobierzUczniow();
    console.log('Wszyscy uczniowie:', uczniowie);
    
    const noweId = await dodajUcznia('Ewa', 'Zielińska', '2TI');
    console.log('Dodano ucznia o ID:', noweId);
}

main();
```

---

## 9. Kompletny przykład - Mini API

Prosty serwer HTTP z operacjami na bazie danych.

### Plik: `server.js`

```javascript
const http = require('http');
const mysql = require('mysql2/promise');
const url = require('url');

// Konfiguracja puli połączeń
const pool = mysql.createPool({
    host: 'localhost',
    user: 'root',
    password: 'mojeHaslo',
    database: 'szkola',
    connectionLimit: 10
});

// Funkcje obsługi bazy danych
async function pobierzWszystkichUczniow() {
    const [rows] = await pool.query('SELECT * FROM uczniowie ORDER BY nazwisko');
    return rows;
}

async function pobierzUczniaPoId(id) {
    const [rows] = await pool.query('SELECT * FROM uczniowie WHERE id = ?', [id]);
    return rows[0] || null;
}

async function dodajUcznia(imie, nazwisko, klasa) {
    const [result] = await pool.query(
        'INSERT INTO uczniowie (imie, nazwisko, klasa) VALUES (?, ?, ?)',
        [imie, nazwisko, klasa]
    );
    return result.insertId;
}

async function usunUcznia(id) {
    const [result] = await pool.query('DELETE FROM uczniowie WHERE id = ?', [id]);
    return result.affectedRows > 0;
}

// Serwer HTTP
const server = http.createServer(async (req, res) => {
    const parsedUrl = url.parse(req.url, true);
    const path = parsedUrl.pathname;
    const query = parsedUrl.query;
    
    // Nagłówki odpowiedzi
    res.setHeader('Content-Type', 'application/json; charset=utf-8');
    
    try {
        // GET /uczniowie - lista wszystkich
        if (req.method === 'GET' && path === '/uczniowie') {
            const uczniowie = await pobierzWszystkichUczniow();
            res.writeHead(200);
            res.end(JSON.stringify({ success: true, data: uczniowie }));
            return;
        }
        
        // GET /uczen?id=5 - jeden uczeń
        if (req.method === 'GET' && path === '/uczen') {
            const id = parseInt(query.id);
            
            if (isNaN(id)) {
                res.writeHead(400);
                res.end(JSON.stringify({ success: false, error: 'Brak parametru id' }));
                return;
            }
            
            const uczen = await pobierzUczniaPoId(id);
            
            if (!uczen) {
                res.writeHead(404);
                res.end(JSON.stringify({ success: false, error: 'Uczeń nie znaleziony' }));
                return;
            }
            
            res.writeHead(200);
            res.end(JSON.stringify({ success: true, data: uczen }));
            return;
        }
        
        // GET /dodaj?imie=Jan&nazwisko=Kowalski&klasa=3TI
        if (req.method === 'GET' && path === '/dodaj') {
            const { imie, nazwisko, klasa } = query;
            
            if (!imie || !nazwisko || !klasa) {
                res.writeHead(400);
                res.end(JSON.stringify({ 
                    success: false, 
                    error: 'Wymagane parametry: imie, nazwisko, klasa' 
                }));
                return;
            }
            
            const noweId = await dodajUcznia(imie, nazwisko, klasa);
            res.writeHead(201);
            res.end(JSON.stringify({ 
                success: true, 
                message: 'Dodano ucznia', 
                id: noweId 
            }));
            return;
        }
        
        // GET /usun?id=5
        if (req.method === 'GET' && path === '/usun') {
            const id = parseInt(query.id);
            
            if (isNaN(id)) {
                res.writeHead(400);
                res.end(JSON.stringify({ success: false, error: 'Brak parametru id' }));
                return;
            }
            
            const usunieto = await usunUcznia(id);
            
            if (!usunieto) {
                res.writeHead(404);
                res.end(JSON.stringify({ success: false, error: 'Uczeń nie znaleziony' }));
                return;
            }
            
            res.writeHead(200);
            res.end(JSON.stringify({ success: true, message: 'Usunięto ucznia' }));
            return;
        }
        
        // Nieznana ścieżka
        res.writeHead(404);
        res.end(JSON.stringify({ success: false, error: 'Nie znaleziono endpointu' }));
        
    } catch (error) {
        console.error('Błąd serwera:', error);
        res.writeHead(500);
        res.end(JSON.stringify({ success: false, error: 'Błąd serwera' }));
    }
});

// Uruchomienie serwera
const PORT = 3000;
server.listen(PORT, () => {
    console.log(`Serwer działa na http://localhost:${PORT}`);
    console.log('');
    console.log('Dostępne endpointy:');
    console.log('  GET /uczniowie          - lista wszystkich uczniów');
    console.log('  GET /uczen?id=5         - dane ucznia o ID 5');
    console.log('  GET /dodaj?imie=X&nazwisko=Y&klasa=Z - dodaj ucznia');
    console.log('  GET /usun?id=5          - usuń ucznia o ID 5');
});
```

### Uruchomienie

```bash
node server.js
```

### Testowanie w przeglądarce

```
http://localhost:3000/uczniowie
http://localhost:3000/uczen?id=1
http://localhost:3000/dodaj?imie=Adam&nazwisko=Nowak&klasa=1TI
http://localhost:3000/usun?id=5
```

---

## 10. Podsumowanie

### Kluczowe pojęcia

| Pojęcie | Opis |
|---------|------|
| **Node.js** | JavaScript po stronie serwera |
| **npm** | Menedżer pakietów Node.js |
| **mysql2** | Biblioteka do łączenia z MySQL |
| **Connection Pool** | Pula połączeń (wydajność) |
| **Prepared Statements** | Zabezpieczenie przed SQL Injection |
| **Async/Await** | Nowoczesna obsługa asynchroniczności |

### Schemat działania

```
┌─────────────────────────────────────────────────────────────┐
│                        SERWER NODE.JS                        │
│                                                              │
│   ┌──────────┐    ┌──────────┐    ┌──────────────────────┐  │
│   │  HTTP    │───►│  Logika  │───►│  mysql2 + Pool       │──┼──► MySQL
│   │  Request │    │  biznes. │    │  (prepared stmts)    │  │
│   └──────────┘    └──────────┘    └──────────────────────┘  │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

### Zasady bezpieczeństwa

1. ✅ **ZAWSZE** używaj prepared statements (`?`)
2. ✅ **NIGDY** nie składaj SQL ze stringów
3. ✅ Przechowuj hasła w zmiennych środowiskowych, nie w kodzie
4. ✅ Używaj connection pool w produkcji
5. ✅ Obsługuj błędy (try/catch)
6. ✅ Zamykaj połączenia po użyciu

### Przechowywanie haseł - `.env`

```bash
# Plik .env (dodaj do .gitignore!)
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=mojeHaslo
DB_NAME=szkola
```

```javascript
// W kodzie (wymaga: npm install dotenv)
require('dotenv').config();

const pool = mysql.createPool({
    host: process.env.DB_HOST,
    user: process.env.DB_USER,
    password: process.env.DB_PASSWORD,
    database: process.env.DB_NAME
});
```

---

## 📚 Materiały dodatkowe

- [Dokumentacja mysql2](https://github.com/sidorares/node-mysql2)
- [Node.js oficjalna strona](https://nodejs.org)
- [SQL Injection - OWASP](https://owasp.org/www-community/attacks/SQL_Injection)

---

**Autor:** Materiał dodatkowy dla uczniów technikum informatycznego  
**Poziom:** Wykraczający poza podstawę programową  
**Wymagania:** Znajomość JavaScript, podstawy SQL, zainstalowany MySQL
