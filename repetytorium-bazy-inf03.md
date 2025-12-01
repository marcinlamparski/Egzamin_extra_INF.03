# 📘 Repetytorium Bazy Danych – Egzamin Zawodowy INF.03
**Cel:** Szybka powtórka zagadnień SQL i baz danych, które najczęściej występują w pytaniach testowych.

## 1. Pojęcia Fundamentalne
Egzamin zawsze zaczyna się od teorii. Musisz znać definicje podstawowych pojęć.

*   **Baza danych:** Zorganizowana kolekcja powiązanych danych przechowywana w systemie komputerowym.
*   **Tabela:** Struktura składająca się z wierszy (rekordów) i kolumn (atrybutów).
*   **Rekord (wiersz):** Pojedynczy wpis w tabeli (jeden rząd).
*   **Pole (kolumna):** Atrybut przechowujący określony typ danych (np. imię, wiek).
*   **Encja:** Rzecz lub pojęcie, które chcemy przechowywać w bazie (np. Student, Kurs).
*   **Atrybut:** Charakterystyka encji (np. atrybut encji Student to imię, nazwisko).
*   **Związek (relacja):** Powiązanie między encjami (np. Student _bierze_ Kurs).

> **Typowe pytanie:** "Co to jest encja w bazie danych?"
> **Odp:** To rzeczywisty obiekt lub pojęcie, które przechowujemy w bazie (np. Student, Produkt, Pracownik).

## 2. Typy Baz Danych
CKE pyta o różne rodzaje systemów baz danych.

| Typ | Opis | Przykład |
|:---|:---|:---|
| **Relacyjne** | Dane w tabelach powiązanych ze sobą za pomocą kluczy | MySQL, PostgreSQL, MS SQL Server |
| **Nierelacyjne (NoSQL)** | Dane przechowywane w formacie dokumentów (JSON) | MongoDB |
| **Dokumentowe** | Bazy przechowujące dokumenty | MongoDB, Firebase |
| **Grafowe** | Bazy przechowujące węzły i krawędzie | Neo4j |

Na egzaminie **bazy relacyjne (SQL)** to 99% pytań.

## 3. Diagramy E/R (Entity-Relationship)
Egzamin testuje umiejętność czytania i interpretacji diagramów.

*   **Encja:** Prostokąt z nazwą
*   **Atrybut:** Elipsa połączona z encją
*   **Związek:** Romb z opisem typu relacji
*   **Liczebność związku:**
    *   `1:1` – jeden do jednego (1 Student ma 1 Numer Albumu)
    *   `1:N` – jeden do wielu (1 Kurs ma wielu Studentów)
    *   `N:N` – wiele do wielu (wielu Studentów bierze wiele Kursów)

## 4. Normalizacja Baz Danych
Bardzo ważny temat na egzaminie. Normalizacja eliminuje redundancję danych.

*   **Pierwsza Postać Normalna (1PN/1NF):**
    *   Każde pole zawiera tylko **jedną wartość** (nie tablice)
    *   Każdy rekord jest **unikalny**
    *   Przykład błędu: `Imiona: Jan, Maria, Piotr` ← To wielowartościowe pole!

*   **Druga Postać Normalna (2PN/2NF):**
    *   Wszystkie atrybuty **nie-kluczowe** są **w pełni zależne** od klucza głównego
    *   Jeśli masz klucz złożony (np. `StudentID + KursID`), każdy atrybut musi zależeć od całego klucza, nie tylko jego części

*   **Trzecia Postać Normalna (3PN/3NF):**
    *   Nie ma **zależności przejściowych** (atrybuty nie zależą od innych atrybutów niż klucz)
    *   Przykład błędu: Tabela `Pracownicy` zawiera `DepartamentID` i `NazwaDepartamentu` – druga zależy od pierwszej, a nie od klucza głównego

> **Typowe pytanie:** "Jakie są cechy pierwszej postaci normalnej?"
> **Odp:** Każde pole zawiera tylko jedną wartość, każdy rekord jest unikalny.

## 5. Klucze w Bazach Danych
Pytania o klucze pojawiają się prawie na każdym egzaminie.

| Typ Klucza | Opis | Przykład |
|:-----------|:-----|:---------|
| **Klucz Główny (Primary Key)** | Jednoznacznie identyfikuje rekord; nie może być NULL | `StudentID INT PRIMARY KEY` |
| **Klucz Obcy (Foreign Key)** | Łączy tabelę z inną tabelą | `KursID INT FOREIGN KEY REFERENCES Kursy(KursID)` |
| **Klucz Kandydat** | Może być kluczem głównym, ale nie jest | `PESEL VARCHAR(11) UNIQUE` |
| **Klucz Złożony** | Klucz z więcej niż jednej kolumny | `PRIMARY KEY (StudentID, KursID)` |

## 6. Typy Danych w SQL
Egzamin sprawdza, czy wiesz, jakie typy stosować w określonych sytuacjach.

| Typ | Opis | Przykład |
|:---|:---|:---|
| **INT** | Liczba całkowita (-2,147,483,648 do 2,147,483,647) | `wiek INT` |
| **BIGINT** | Duża liczba całkowita | `populacja BIGINT` |
| **FLOAT** | Liczba zmiennoprzecinkowa | `cena FLOAT` |
| **DECIMAL(10,2)** | Liczba dziesiętna (dokładna) – 10 cyfr, 2 po przecinku | `kurs DECIMAL(10,2)` |
| **DOUBLE** | Duża liczba zmiennoprzecinkowa | `wspolrzedna DOUBLE` |
| **VARCHAR(n)** | Tekst o zmiennej długości do n znaków | `imie VARCHAR(50)` |
| **CHAR(n)** | Tekst o stałej długości n znaków | `kod_kraju CHAR(2)` |
| **TEXT** | Duży tekst | `opis TEXT` |
| **DATE** | Data (YYYY-MM-DD) | `data_urodzenia DATE` |
| **TIME** | Czas (HH:MM:SS) | `godzina_pracy TIME` |
| **DATETIME** | Data i czas | `data_rejestracji DATETIME` |
| **BOOLEAN** | Wartość logiczna (TRUE/FALSE) | `aktywny BOOLEAN` |
| **ENUM** | Wybór z listy | `plec ENUM('M', 'K')` |

> **Typowe pytanie:** "Jaki typ danych wybrać do przechowywania ceny z dokładnością do groszy?"
> **Odp:** `DECIMAL(10,2)` (dokładny) lub `FLOAT` (przybliżony, ale wystarczający)

## 7. Polecenia SQL – DDL (Data Definition Language)
Rozkazy do tworzenia i modyfikacji struktury bazy.

*   **CREATE DATABASE:**
    ```sql
    CREATE DATABASE IF NOT EXISTS moja_baza CHARACTER SET utf8mb4;
    ```

*   **CREATE TABLE:**
    ```sql
    CREATE TABLE IF NOT EXISTS Studenci (
        StudentID INT PRIMARY KEY AUTO_INCREMENT,
        Imie VARCHAR(50) NOT NULL,
        Nazwisko VARCHAR(50) NOT NULL,
        DataUrodzenia DATE,
        PESEL VARCHAR(11) UNIQUE
    );
    ```

*   **ALTER TABLE** (modyfikacja tabeli):
    ```sql
    ALTER TABLE Studenci ADD COLUMN Email VARCHAR(100);
    ALTER TABLE Studenci DROP COLUMN Email;
    ALTER TABLE Studenci MODIFY COLUMN Imie VARCHAR(100);
    ```

*   **DROP TABLE:**
    ```sql
    DROP TABLE IF EXISTS Studenci;
    ```

*   **TRUNCATE TABLE** (usuwanie danych, zachowuje strukturę):
    ```sql
    TRUNCATE TABLE Studenci;
    ```

## 8. Polecenia SQL – DML (Data Manipulation Language)
Rozkazy do pracy z danymi w tabelach.

*   **SELECT** (pobieranie danych):
    ```sql
    SELECT * FROM Studenci;
    SELECT Imie, Nazwisko FROM Studenci;
    ```

*   **INSERT** (dodawanie danych):
    ```sql
    INSERT INTO Studenci (Imie, Nazwisko, DataUrodzenia)
    VALUES ('Jan', 'Kowalski', '2005-05-15');
    ```

*   **UPDATE** (zmiana danych):
    ```sql
    UPDATE Studenci SET Imie = 'Janusz' WHERE StudentID = 1;
    ```

*   **DELETE** (usuwanie danych):
    ```sql
    DELETE FROM Studenci WHERE StudentID = 1;
    ```

## 9. WHERE i Operatory Logiczne
Filtrowanie danych – najczęstsze pytania.

```sql
SELECT * FROM Studenci WHERE wiek > 18;
SELECT * FROM Studenci WHERE imie = 'Jan';
SELECT * FROM Studenci WHERE wiek >= 18 AND imie = 'Jan';
SELECT * FROM Studenci WHERE wiek < 20 OR imie = 'Maria';
SELECT * FROM Studenci WHERE NOT imie = 'Jan';
```

*   **Operatory porównania:** `=`, `!=` (lub `<>`), `>`, `<`, `>=`, `<=`
*   **Operatory logiczne:** `AND`, `OR`, `NOT`
*   **BETWEEN:**
    ```sql
    SELECT * FROM Studenci WHERE wiek BETWEEN 18 AND 25;
    ```

*   **IN:**
    ```sql
    SELECT * FROM Studenci WHERE imie IN ('Jan', 'Maria', 'Piotr');
    ```

*   **LIKE** (wyszukiwanie wzorców):
    ```sql
    SELECT * FROM Studenci WHERE Imie LIKE 'J%';      -- zaczynające się na 'J'
    SELECT * FROM Studenci WHERE Imie LIKE '%a';      -- kończące się na 'a'
    SELECT * FROM Studenci WHERE Imie LIKE '%o%';     -- zawierające 'o'
    SELECT * FROM Studenci WHERE Imie LIKE 'J_n';     -- 'J' + jeden dowolny znak + 'n'
    ```

## 10. ORDER BY i LIMIT
Sortowanie i ograniczanie wyników.

```sql
SELECT * FROM Studenci ORDER BY Imie ASC;        -- A-Z
SELECT * FROM Studenci ORDER BY Imie DESC;       -- Z-A
SELECT * FROM Studenci ORDER BY Wiek DESC LIMIT 5;  -- 5 najstarszych
SELECT * FROM Studenci LIMIT 10 OFFSET 5;        -- przesunięcie o 5, 10 wyników
```

## 11. Funkcje Agregujące
Pytania o funkcje `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` prawie zawsze pojawiają się.

```sql
SELECT COUNT(*) FROM Studenci;                   -- ilość rekordów
SELECT COUNT(Email) FROM Studenci;               -- ile studentów ma email
SELECT SUM(Ocena) FROM Oceny;                    -- suma ocen
SELECT AVG(Ocena) FROM Oceny;                    -- średnia ocena
SELECT MIN(Ocena) FROM Oceny;                    -- najniższa ocena
SELECT MAX(Ocena) FROM Oceny;                    -- najwyższa ocena
```

## 12. GROUP BY i HAVING
Grupowanie i filtrowanie grup.

```sql
SELECT Kierunek, COUNT(*) as IloscStudentow
FROM Studenci
GROUP BY Kierunek;

SELECT Kierunek, AVG(Ocena) as SrednaOcena
FROM Studenci
GROUP BY Kierunek
HAVING AVG(Ocena) > 3.0;
```

> **Typowe pytanie:** "Na czym polega różnica między WHERE a HAVING?"
> **Odp:** WHERE filtruje **przed** grupowaniem, HAVING filtruje **po** grupowaniu.

## 13. JOIN – Łączenie Tabel (BARDZO WAŻNE!)
Jeden z najtrudniejszych tematów, ale bardzo częsty na egzaminie.

*   **INNER JOIN** (część wspólna):
    ```sql
    SELECT s.Imie, k.Nazwa
    FROM Studenci s
    INNER JOIN Kursy k ON s.StudentID = k.StudentID;
    ```
    Zwraca tylko te rekordy, które istnieją w **obu** tabelach.

*   **LEFT JOIN** (wszystko z lewej tabeli + połączenia):
    ```sql
    SELECT s.Imie, k.Nazwa
    FROM Studenci s
    LEFT JOIN Kursy k ON s.StudentID = k.StudentID;
    ```
    Zwraca **wszystkich** studentów, nawet jeśli nie mają kursu (wtedy NULL).

*   **RIGHT JOIN** (wszystko z prawej tabeli + połączenia):
    ```sql
    SELECT s.Imie, k.Nazwa
    FROM Studenci s
    RIGHT JOIN Kursy k ON s.StudentID = k.StudentID;
    ```
    Zwraca **wszystkie** kursy, nawet jeśli nikt się nie zarejestrował.

*   **FULL OUTER JOIN** (suma obu tabel):
    ```sql
    SELECT s.Imie, k.Nazwa
    FROM Studenci s
    FULL OUTER JOIN Kursy k ON s.StudentID = k.StudentID;
    ```
    (Nie wszystkie bazy obsługują FULL OUTER JOIN)

| Typ | Co zwraca |
|:---|:---|
| INNER JOIN | Tylko dopasowania |
| LEFT JOIN | Wszystko z lewej + dopasowania |
| RIGHT JOIN | Wszystko z prawej + dopasowania |
| FULL OUTER JOIN | Wszystko z obu + duplikaty usunięte |

## 14. Relacje N:N (Wiele-do-Wielu)
Egzamin pyta o obsługę relacji wiele-do-wielu.

Tabela `Studenci`:
```
StudentID | Imie
1         | Jan
2         | Maria
```

Tabela `Kursy`:
```
KursID | Nazwa
1      | Python
2      | HTML
```

Tabela `StudentyKursy` (tabela łącznikowa):
```
StudentID | KursID
1         | 1
1         | 2
2         | 1
```

Zapytanie:
```sql
SELECT s.Imie, k.Nazwa
FROM Studenci s
INNER JOIN StudentyKursy sk ON s.StudentID = sk.StudentID
INNER JOIN Kursy k ON sk.KursID = k.KursID;
```

## 15. Aliasy
Aliasy skracają nazwy tabel i kolumn – często pojawia się w pytaniach.

```sql
SELECT s.Imie AS "Imię Studenta", k.Nazwa AS "Nazwa Kursu"
FROM Studenci s
INNER JOIN Kursy k ON s.StudentID = k.StudentID;
```

## 16. DISTINCT
Usuwanie duplikatów – łatwe pytanie, ale częste.

```sql
SELECT DISTINCT Kierunek FROM Studenci;  -- lista unikalnych kierunków
```

## 17. Funkcje Tekstowe
Czasem pojawiają się pytania o operacje na tekście.

```sql
SELECT UPPER(Imie) FROM Studenci;        -- wielkie litery
SELECT LOWER(Imie) FROM Studenci;        -- małe litery
SELECT LENGTH(Imie) FROM Studenci;       -- długość tekstu
SELECT CONCAT(Imie, ' ', Nazwisko) FROM Studenci;  -- łączenie
SELECT SUBSTRING(Imie, 1, 3) FROM Studenci;  -- pierwsze 3 znaki
SELECT TRIM(Imie) FROM Studenci;         -- usunięcie spacji
SELECT REPLACE(Imie, 'a', 'o') FROM Studenci;  -- zamiana znaków
```

## 18. Funkcje Matematyczne
Rzadsze, ale mogą się pojawić.

```sql
SELECT ROUND(3.14159, 2);        -- zaokrąglenie: 3.14
SELECT FLOOR(3.9);               -- zaokrąglenie w dół: 3
SELECT CEIL(3.1);                -- zaokrąglenie w górę: 4
SELECT ABS(-5);                  -- wartość bezwzględna: 5
SELECT POWER(2, 3);              -- potęga: 8
SELECT SQRT(16);                 -- pierwiastek: 4
```

## 19. Funkcje Daty i Czasu
Ważne dla zapytań z datami.

```sql
SELECT NOW();                    -- bieżąca data i czas
SELECT DATE(NOW());              -- tylko data
SELECT TIME(NOW());              -- tylko czas
SELECT YEAR(DataUrodzenia) FROM Studenci;      -- rok
SELECT MONTH(DataUrodzenia) FROM Studenci;     -- miesiąc
SELECT DAY(DataUrodzenia) FROM Studenci;       -- dzień
SELECT DATEDIFF('2025-12-31', '2025-01-01');   -- różnica w dniach
SELECT DATE_ADD(NOW(), INTERVAL 1 DAY);        -- dodaj 1 dzień
```

## 20. Podzapytania (Subqueries)
Zaawansowany temat, czasem pojawia się.

```sql
-- Wszyscy studenci z kierunku 'Informatyka'
SELECT * FROM Studenci WHERE Kierunek = (
    SELECT Kierunek FROM Studenci WHERE Imie = 'Jan'
);

-- Studenci lepsi od średniej
SELECT * FROM Studenci WHERE Ocena > (
    SELECT AVG(Ocena) FROM Studenci
);
```

## 21. CASE (Instrukcja Warunkowa)
Zaawansowana, ale czasem pytana.

```sql
SELECT Imie,
    CASE
        WHEN Ocena >= 5 THEN 'Bardzo Dobry'
        WHEN Ocena >= 4 THEN 'Dobry'
        WHEN Ocena >= 3 THEN 'Dostateczny'
        ELSE 'Niedostateczny'
    END AS Ocena_Opisowa
FROM Studenci;
```

## 22. Wyzwalacze (TRIGGERS)
Zaawansowany temat, rzadko pytany na poziomie teoretycznym.

Wyzwalacz to reguła, która automatycznie wykonuje się po określonym zdarzeniu.

```sql
CREATE TRIGGER zanim_usuniesz_studenta
BEFORE DELETE ON Studenci
FOR EACH ROW
BEGIN
    INSERT INTO Archiwum_Studenci VALUES (OLD.StudentID, OLD.Imie, NOW());
END;
```

## 23. Transakcje (TRANSACTIONS)
Gwarantuje, że wszystkie operacje się wykonają albo żadna.

```sql
START TRANSACTION;
UPDATE Konta SET Saldo = Saldo - 100 WHERE KontoID = 1;
UPDATE Konta SET Saldo = Saldo + 100 WHERE KontoID = 2;
COMMIT;  -- zatwierdzenie

-- Lub wycofanie:
ROLLBACK;
```

## 24. Widoki (VIEWS)
Wirtualna tabela utworzona na podstawie zapytania.

```sql
CREATE VIEW Studenci_2025 AS
SELECT * FROM Studenci WHERE ROK_AKADEMICKI = 2025;

SELECT * FROM Studenci_2025;
```

## 25. Indeksy
Przyspieszają wyszukiwanie, ale spowalniają wstawianie.

```sql
CREATE INDEX idx_imie ON Studenci(Imie);
DROP INDEX idx_imie ON Studenci;
```

## 26. Uprawnieniaużytkowników
Administracja bazą – czasem pojawia się.

```sql
CREATE USER 'uzytkownik'@'localhost' IDENTIFIED BY 'haslo';
GRANT SELECT, INSERT ON moja_baza.* TO 'uzytkownik'@'localhost';
REVOKE DELETE ON moja_baza.* FROM 'uzytkownik'@'localhost';
```

## 27. Backup i Restore
Administracja – czasem pytane.

```sql
-- Backup całej bazy (z linii poleceń):
mysqldump -u root -p moja_baza > backup.sql

-- Restore (z linii poleceń):
mysql -u root -p moja_baza < backup.sql
```

---

### 🔥 Szybki test wiedzy (Sprawdź się!)

1.  **Pytanie:** Co to jest klucz główny (Primary Key)?
    *   **Odp:** Kolumna, która jednoznacznie identyfikuje każdy rekord w tabeli.

2.  **Pytanie:** Na czym polega różnica między INNER JOIN a LEFT JOIN?
    *   **Odp:** INNER zwraca tylko dopasowania, LEFT zwraca wszystko z lewej tabeli + dopasowania.

3.  **Pytanie:** Jaki typ danych wybrać do przechowywania daty?
    *   **Odp:** `DATE` (YYYY-MM-DD).

4.  **Pytanie:** Jak usunąć duplikaty z wyników zapytania?
    *   **Odp:** `SELECT DISTINCT ...`

5.  **Pytanie:** Czy NULL jest równy 0 lub pusty string?
    *   **Odp:** Nie! NULL to brak wartości. Porównanie z NULL wymaga `IS NULL` lub `IS NOT NULL`.

6.  **Pytanie:** Co to jest normalizacja bazy danych?
    *   **Odp:** Proces organizowania danych w tabelach w celu eliminacji redundancji (powtórzeń).

7.  **Pytanie:** Jaka jest różnica między WHERE a HAVING?
    *   **Odp:** WHERE filtruje **przed** grupowaniem, HAVING filtruje **po** grupowaniu.

8.  **Pytanie:** Jak połączyć trzy tabele za pomocą JOIN?
    *   **Odp:** 
    ```sql
    SELECT * FROM T1
    INNER JOIN T2 ON T1.id = T2.id
    INNER JOIN T3 ON T2.id = T3.id;
    ```

### Jak korzystać z bazy pytań?
Rozwiązując testy na zawodowe.edu.pl:
1.  **Czytaj uważnie zapytania** – zwróć uwagę na JOIN i filtry WHERE
2.  **Testuj w praktyce** – twórz bazy w phpMyAdmin i eksperymentuj
3.  **Zapamiętaj klauzule** – SELECT, FROM, WHERE, GROUP BY, ORDER BY, HAVING
4.  **Zapamiętaj typy relacji** – 1:1, 1:N, N:N
5.  **Ćwicz normalizację** – rozpoznaj błędy w strukturze bazy
