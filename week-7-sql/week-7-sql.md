# [Lecture 7](https://cs50.harvard.edu/x/weeks/6)

- SQL - Structured Query Langugage, a declarative programming language, where in general problem is declared and language figures out solution

### Flat-file Databases
- A normal csv file has data stored in it with normal text - a *flat-file database* with values separated by commas
- tsv - tab separated values, psv - pipe separated vvlues are alike csv which use a character which will not appear in data to separate values
- Each row in a csv can be considered a dictionary with headers and indices serving as keys for a value

### Relational Database
- Relations are defind along with data among data
- Associates various fields/keys with each other which we saw in flat-file database
- SQL is the language to work with such database

### SQL Operations
- C - Create - `CREATE`, `INSERT`
- R- Read - `SELECT`
- U - Update - `UPDATE`
- D - Delete - `DELETE`, `DROP`
- SQL deals with tables defined with `CREATE TABLE table(column type, ...);`

### SQLite
- Lightweighr version of SQL
- Does not have the scalability that of servers
-`sqlite3 FILE` would get us started by creating a start database. `.db` extension states database by convention
- In commands `.command` are specific to SQLite
- To load data from `csv` file:
    1. `.mode csv` - Setmode for SQLite to `csv`
    2. `.import file.csv file/table` - import information from `file.csv` to `.db` file created/opened when entering SQLite
    3. `.quit` - exit SQLite
- Syntax and Operations 
    - `.schema` returns the design of imported or created database file with one or more tables
    - `SELECT column-name FROM table-name;` returns one particular column or if mentioned the columns separated by commas in the table
    - Functions are built-in like - `COUNT()` - returns count of input arguments from `SELECT`ed table
    - `*` denotes all, `'` single quote before any symbol acts as escape character, `%` deontes zero or more characters among piece of values to look
    - `NULL` represents absence of data

### Schema
- Managing data in terms of unique id values instead of the data-value itself helps with algorithms  for searching
- Data can be associated easily to have normalized representations of information
- SQL supports one-to-one relations, a row in one table relates with some other row in another table

### Types
- Defined per column for what kind of data it holds:
    - `BLOB` - Binary Large Objects for binary data
    - `INTEGER` - Numbers
    - `NUMERIC` - Date, Time, etc.
    - `REAL` - Floats
    - `TEXT` - Text values
    - No more Data Types in SQLite, other SQL providers may have more
- `NOT NULL` - ensures absence of data is avoided
- `UNIQUE` - ensures that a column has distinct values avoiding duplications
- `PRIMARY KEY` - Unique identifier for each row in a table
- `FOREIGN KEY` - If the `PRIMARY KEY` referenced in table other than parent

### Indexes
- Too much data may even slow down SQL queries as it is mostly linear operation
- Database or usage of SQL can be optimized for certain common queries using indexes
- Very oftenly created using a B-Tree, unlike inary tree it can have more than two children

### SQL Injection Attacks
- When using alongside other programming languages like python, SQL allows dynamically injection of variable values in queries
- Sometimes these queries can tricked to do malicious activities with sufficient knowledge of SQL
- Thus either using the standard library or using `?` placeholder in query and variable sequence outside query instead of injecting variable in the query directly avoids this

### Race Conditions
- Too much concurrent usage cuases a race condition if not handled well
- Thus while accessing a database value it is enssential to lock it before anyone else inspects it only to run into a worse result
- Transactions are used to access data, make changes and do commit those changes if everything's right otherwise abort to safekeep data

# [Problem Set 7](https://cs50.harvard.edu/x/psets/7/)

### [songs](https://cs50.harvard.edu/x/psets/7/songs/)
```
-- 1. List the names of all songs in the database
SELECT name 
FROM songs;

-- 2. List the names of all songs in increasing order of tempo
SELECT name 
FROM songs 
ORDER BY tempo;

-- 3. List the names of the top 5 longest songs, in descending order of length
SELECT name 
FROM songs 
ORDER BY duration_ms DESC 
LIMIT 5;

-- 4. List the names of any songs that have danceability, energy, and valence greater than 0.75
SELECT name 
FROM songs 
WHERE danceability > 0.75 
  AND energy > 0.75 
  AND valence > 0.75;

-- 5. Returns the average energy of all the songs
SELECT AVG(energy) 
FROM songs;

-- 6. List the names of songs by Post Malone (using a subquery to find the artist_id)
SELECT name 
FROM songs 
WHERE artist_id = (
    SELECT id 
    FROM artists 
    WHERE name = 'Post Malone'
);

-- 7. Returns the average energy of songs by Drake
SELECT AVG(energy) 
FROM songs 
WHERE artist_id = (
    SELECT id 
    FROM artists 
    WHERE name = 'Drake'
);

-- 8. List the names of songs that feature other artists (containing "feat.")
SELECT name 
FROM songs 
WHERE name LIKE '%feat.%';
```

### [movies](https://cs50.harvard.edu/x/psets/7/movies/)
```
-- 1. List the titles of all movies released in 2008
SELECT title 
FROM movies 
WHERE year = 2008;

-- 2. Determine the birth year of Emma Stone
SELECT birth 
FROM people 
WHERE name = 'Emma Stone';

-- 3. List the titles of all movies with a release date on or after 2018, in alphabetical order
SELECT title 
FROM movies 
WHERE year >= 2018 
ORDER BY title;

-- 4. Determine the number of movies with an IMDb rating of 10.0
SELECT COUNT(*) 
FROM ratings 
WHERE rating = 10.0;

-- 5. List the titles and release years of all Harry Potter movies, in chronological order
SELECT title, year 
FROM movies 
WHERE title LIKE 'Harry Potter%' 
ORDER BY year;

-- 6. Determine the average rating of all movies released in 2012
SELECT AVG(rating) 
FROM ratings 
WHERE movie_id IN (
    SELECT id 
    FROM movies 
    WHERE year = 2012
);

-- 7. List all movies released in 2010 and their ratings, in descending order by rating
-- For movies with the same rating, order them alphabetically by title
SELECT title, rating 
FROM movies 
JOIN ratings ON movies.id = ratings.movie_id 
WHERE year = 2010 
ORDER BY rating DESC, title ASC;

-- 8. List the names of all people who starred in Toy Story
SELECT name 
FROM people 
WHERE id IN (
    SELECT person_id 
    FROM stars 
    WHERE movie_id IN (
        SELECT id 
        FROM movies 
        WHERE title = 'Toy Story'
    )
);

-- 9. List the names of all people who starred in a movie released in 2004, ordered by birth year
SELECT name 
FROM people 
WHERE id IN (
    SELECT person_id 
    FROM stars 
    WHERE movie_id IN (
        SELECT id 
        FROM movies 
        WHERE year = 2004
    )
) 
ORDER BY birth;

-- 10. List the names of all people who have directed a movie that received a rating of at least 9.0
SELECT name 
FROM people 
WHERE id IN (
    SELECT person_id 
    FROM directors 
    WHERE movie_id IN (
        SELECT movie_id 
        FROM ratings 
        WHERE rating >= 9.0
    )
);

-- 11. List the titles of the five highest rated movies (in order) that Chadwick Boseman starred in
SELECT title 
FROM movies 
JOIN ratings ON movies.id = ratings.movie_id 
JOIN stars ON movies.id = stars.movie_id 
JOIN people ON stars.person_id = people.id 
WHERE people.name = 'Chadwick Boseman' 
ORDER BY rating DESC 
LIMIT 5;

-- 12. List the titles of all movies in which both Jennifer Lawrence and Bradley Cooper starred
SELECT title 
FROM movies 
JOIN stars s1 ON movies.id = s1.movie_id 
JOIN people p1 ON s1.person_id = p1.id 
JOIN stars s2 ON movies.id = s2.movie_id 
JOIN people p2 ON s2.person_id = p2.id 
WHERE p1.name = 'Jennifer Lawrence' 
  AND p2.name = 'Bradley Cooper';

-- 13. List the names of all people who starred in a movie in which Kevin Bacon also starred
SELECT name 
FROM people 
WHERE id IN (
    SELECT person_id 
    FROM stars 
    WHERE movie_id IN (
        SELECT movie_id 
        FROM stars 
        WHERE person_id = (
            SELECT id 
            FROM people 
            WHERE name = 'Kevin Bacon' 
            AND birth = 1958
        )
    )
) 
AND name != 'Kevin Bacon';
```

### [fiftyville](https://cs50.harvard.edu/x/psets/7/fiftyville/)
```
-- Keep a log of any SQL queries you execute as you solve the mystery.

-- First, I checked the crime scene reports for the incident on July 28, 2025 on Humphrey Street.
SELECT * FROM crime_scene_reports
WHERE day = 28 AND month = 7 AND year = 2025 AND street = 'Humphrey Street';

-- I found report 295 mentioned a CS50 duck theft at 10:15am and noted three witnesses.
-- I then looked for interviews from that day to hear the witness testimonies.
SELECT * FROM interviews
WHERE day = 28 AND month = 7 AND year = 2025;

-- Witness Ruth mentioned the thief drove away in a car within 10 minutes of the theft.
-- Witness Eugene mentioned seeing the thief at an ATM on Leggett Street earlier that morning.
-- Witness Raymond mentioned the thief made a call of less than a minute as they left the bakery.
-- Raymond also noted they were taking the earliest flight out of Fiftyville on July 29.

-- I checked the ATM transactions for withdrawals on Leggett Street that morning.
SELECT * FROM atm_transactions
WHERE day = 28 AND month = 7 AND year = 2025
AND atm_location = 'Leggett Street' AND transaction_type = 'withdraw';

-- I checked the bakery security logs for cars exiting between 10:15 and 10:25.
SELECT * FROM bakery_security_logs
WHERE day = 28 AND month = 7 AND year = 2025
AND hour = 10 AND minute >= 15 AND minute <= 25 AND activity = 'exit';

-- I checked phone calls from that day lasting less than 60 seconds.
SELECT * FROM phone_calls
WHERE day = 28 AND month = 7 AND year = 2025 AND duration < 60;

-- I looked for the earliest flight on July 29th.
SELECT flights.id, full_name, city, hour, minute FROM flights
JOIN airports ON flights.destination_airport_id = airports.id
WHERE year = 2025 AND month = 7 AND day = 29
ORDER BY hour, minute LIMIT 1;

-- Finally, I combined all clues to find the person who matches the ATM, car, phone, and flight records.
SELECT name FROM people
JOIN bank_accounts ON people.id = bank_accounts.person_id
JOIN atm_transactions ON bank_accounts.account_number = atm_transactions.account_number
WHERE atm_transactions.year = 2025 AND atm_transactions.month = 7 AND atm_transactions.day = 28
AND atm_transactions.atm_location = 'Leggett Street' AND atm_transactions.transaction_type = 'withdraw'
AND people.license_plate IN (
    SELECT license_plate FROM bakery_security_logs
    WHERE year = 2025 AND month = 7 AND day = 28
    AND hour = 10 AND minute >= 15 AND minute <= 25 AND activity = 'exit'
)
AND people.phone_number IN (
    SELECT caller FROM phone_calls
    WHERE year = 2025 AND month = 7 AND day = 28 AND duration < 60
)
AND people.passport_number IN (
    SELECT passport_number FROM passengers
    WHERE flight_id = (
        SELECT id FROM flights
        WHERE year = 2025 AND month = 7 AND day = 29
        ORDER BY hour, minute LIMIT 1
    )
);

-- After finding Bruce, I searched for his accomplice (the receiver of the phone call).
SELECT name FROM people
WHERE phone_number = (
    SELECT receiver FROM phone_calls
    WHERE year = 2025 AND month = 7 AND day = 28 AND duration < 60
    AND caller = (SELECT phone_number FROM people WHERE name = 'Bruce')
);

```