  # SQL Movies DataBase Assignment
-------------------------------------------------------------------------
 `mysql> create database movies_db;`
 `Query OK, 1 row affected (0.03 sec)`

`mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| c16_db_two         |
| information_schema |
| movies_db          |
| mysql              |
| performance_schema |
| polls_db           |
| sakila             |
| sys                |
| world              |
+--------------------+
9 rows in set (0.00 sec)`

`mysql> use movies_db;
Database changed
mysql> create table Movies (
    -> movieid INT UNSIGNED NOT NULL AUTO_INCREMENT,
    -> Title VARCHAR(300) NOT NULL DEFAULT '',
    -> Runtime INT UNSIGNED NOT NULL DEFAULT 0,
    -> Genre VARCHAR(50) NOT NULL DEFAULT '',
    -> IMDB_Score DECIMAL(3,1),
    -> Rating VARCHAR(10) NOT NULL DEFAULT 'NR',
    -> PRIMARY KEY (movieid));
Query OK, 0 rows affected (0.06 sec)
mysql> show tables;
+---------------------+
| Tables_in_movies_db |
+---------------------+
| movies              |
+---------------------+
1 row in set (0.01 sec)
mysql> desc Movies;
+------------+--------------+------+-----+---------+----------------+
| Field      | Type         | Null | Key | Default | Extra          |
+------------+--------------+------+-----+---------+----------------+
| movieid    | int unsigned | NO   | PRI | NULL    | auto_increment |
| Title      | varchar(300) | NO   |     |         |                |
| Runtime    | int unsigned | NO   |     | 0       |                |
| Genre      | varchar(50)  | NO   |     |         |                |
| IMDB_Score | decimal(3,1) | YES  |     | NULL    |                |
| Rating     | varchar(10)  | NO   |     | NR      |                |
+------------+--------------+------+-----+---------+----------------+
6 rows in set (0.02 sec)`
`mysql> INSERT INTO Movies (Title, Runtime, Genre, IMDB_Score, Rating) VALUES
    -> ('Howard the Duck', 110, 'Sci-Fi', 4.6, 'PG'),
    -> ('Lavalantula', 83, 'Horror', 4.7, 'TV-14'),
    -> ('Starship Troopers', 129, 'Sci-Fi', 7.2, 'PG-13'),
    -> ('Waltz With Bashir', 90, 'Documentary', 8.0, 'R'),
    -> ('Spaceballs', 96, 'Comedy', 7.1, 'PG'),
    -> ('Monsters Inc.', 92, 'Animation', 8.1, 'G');
Query OK, 6 rows affected (0.03 sec)
Records: 6  Duplicates: 0  Warnings: 0
mysql> select * from Movies;
+---------+-------------------+---------+-------------+------------+--------+
| movieid | Title             | Runtime | Genre       | IMDB_Score | Rating |
+---------+-------------------+---------+-------------+------------+--------+
|       1 | Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
|       2 | Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
|       3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
|       4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|       5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|       6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
+---------+-------------------+---------+-------------+------------+--------+
6 rows in set (0.00 sec)`
### Add two more movies of your choosing to the table.
`mysql> INSERT INTO Movies (Title, Runtime, Genre, IMDB_Score, Rating) VALUES
    -> ('The Godfather', 175, 'Drama', 9.2, 'R'),
    -> ('Shark Tale', 90, 'Animation', 6.0, 'PG');
Query OK, 2 rows affected (0.01 sec)
Records: 2  Duplicates: 0  Warnings: 0`
`mysql> select * from Movies;
+---------+-------------------+---------+-------------+------------+--------+
| movieid | Title             | Runtime | Genre       | IMDB_Score | Rating |
+---------+-------------------+---------+-------------+------------+--------+
|       1 | Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
|       2 | Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
|       3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
|       4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|       5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|       6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
|       7 | The Godfather     |     175 | Drama       |        9.2 | R      |
|       8 | Shark Tale        |      90 | Animation   |        6.0 | PG     |
+---------+-------------------+---------+-------------+------------+--------+
8 rows in set (0.00 sec)`
### Create a query to find all movies in the Sci-Fi genre.
`mysql> SELECT * FROM Movies WHERE Genre = 'Sci-Fi';
+---------+-------------------+---------+--------+------------+--------+
| movieid | Title             | Runtime | Genre  | IMDB_Score | Rating |
+---------+-------------------+---------+--------+------------+--------+
|       1 | Howard the Duck   |     110 | Sci-Fi |        4.6 | PG     |
|       3 | Starship Troopers |     129 | Sci-Fi |        7.2 | PG-13  |
+---------+-------------------+---------+--------+------------+--------+
2 rows in set (0.01 sec)`
### Create a query to find all films that scored at least a 6.5 on IMDB.
`mysql> SELECT * FROM Movies WHERE IMDB_Score >= 6.5;
+---------+-------------------+---------+-------------+------------+--------+
| movieid | Title             | Runtime | Genre       | IMDB_Score | Rating |
+---------+-------------------+---------+-------------+------------+--------+
|       3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | PG-13  |
|       4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|       5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|       6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
|       7 | The Godfather     |     175 | Drama       |        9.2 | R      |
+---------+-------------------+---------+-------------+------------+--------+
5 rows in set (0.01 sec)`
### For parents who have young kids, but who don't want to sit through long children's movies, create a query to find all of the movies rated G or PG that are less than 100 minutes long.
`mysql> SELECT * FROM Movies WHERE (Rating = 'G' OR Rating = 'PG') AND Runtime < 100;
+---------+---------------+---------+-----------+------------+--------+
| movieid | Title         | Runtime | Genre     | IMDB_Score | Rating |
+---------+---------------+---------+-----------+------------+--------+
|       5 | Spaceballs    |      96 | Comedy    |        7.1 | PG     |
|       6 | Monsters Inc. |      92 | Animation |        8.1 | G      |
|       8 | Shark Tale    |      90 | Animation |        6.0 | PG     |
+---------+---------------+---------+-----------+------------+--------+
3 rows in set (0.00 sec)`
### Create a query to show the average runtimes of movies scoring below a 7.5 on imdb, grouped by their respective genres.
`mysql> SELECT Genre, AVG(Runtime) AS Average_Runtime
    -> FROM Movies
    -> WHERE IMDB_Score < 7.5
    -> GROUP BY Genre;
+-----------+-----------------+
| Genre     | Average_Runtime |
+-----------+-----------------+
| Sci-Fi    |        119.5000 |
| Horror    |         83.0000 |
| Comedy    |         96.0000 |
| Animation |         90.0000 |
+-----------+-----------------+
4 rows in set (0.01 sec)`
### There's been a data entry mistake; Starship Troopers is actually rated R, not PG-13. Create a query that finds the movie by its title and changes its rating to R.
`mysql> UPDATE Movies
    -> SET Rating = 'R' WHERE Title = 'Starship Troopers';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0
mysql> SELECT * FROM Movies;
+---------+-------------------+---------+-------------+------------+--------+
| movieid | Title             | Runtime | Genre       | IMDB_Score | Rating |
+---------+-------------------+---------+-------------+------------+--------+
|       1 | Howard the Duck   |     110 | Sci-Fi      |        4.6 | PG     |
|       2 | Lavalantula       |      83 | Horror      |        4.7 | TV-14  |
|       3 | Starship Troopers |     129 | Sci-Fi      |        7.2 | R      |
|       4 | Waltz With Bashir |      90 | Documentary |        8.0 | R      |
|       5 | Spaceballs        |      96 | Comedy      |        7.1 | PG     |
|       6 | Monsters Inc.     |      92 | Animation   |        8.1 | G      |
|       7 | The Godfather     |     175 | Drama       |        9.2 | R      |
|       8 | Shark Tale        |      90 | Animation   |        6.0 | PG     |
+---------+-------------------+---------+-------------+------------+--------+
8 rows in set (0.00 sec)`
### Show the ID number and rating of all of the Horror and Documentary movies in the database.
`mysql> SELECT movieid, Rating FROM Movies WHERE Genre IN ('Horror', 'Documen
tary');
+---------+--------+
| movieid | Rating |
+---------+--------+
|       2 | TV-14  |
|       4 | R      |
+---------+--------+
2 rows in set (0.00 sec)`
### This time let's find the average, maximum, and minimum IMDB score for movies of each rating.
`mysql> SELECT Rating, AVG(IMDB_Score) AS Avg_Score, MAX(IMDB_Score) AS Max_Score, MIN(IMDB_Score) AS Min_Score
    -> FROM Movies
    -> GROUP BY Rating;
+--------+-----------+-----------+-----------+
| Rating | Avg_Score | Max_Score | Min_Score |
+--------+-----------+-----------+-----------+
| PG     |   5.90000 |       7.1 |       4.6 |
| TV-14  |   4.70000 |       4.7 |       4.7 |
| R      |   8.13333 |       9.2 |       7.2 |
| G      |   8.10000 |       8.1 |       8.1 |
+--------+-----------+-----------+-----------+
4 rows in set (0.01 sec)`
### That last query isn't very informative for ratings that only have 1 entry. Use a HAVING COUNT(*) > 1 clause to only show ratings with multiple movies showing.
`mysql> SELECT Rating, AVG(IMDB_Score) AS Avg_Score, MAX(IMDB_Score) AS Max_Score, MIN(IMDB_Score) AS Min_Score
    -> FROM Movies
    -> GROUP BY Rating
    -> HAVING COUNT(*) > 1;
+--------+-----------+-----------+-----------+
| Rating | Avg_Score | Max_Score | Min_Score |
+--------+-----------+-----------+-----------+
| PG     |   5.90000 |       7.1 |       4.6 |
| R      |   8.13333 |       9.2 |       7.2 |
+--------+-----------+-----------+-----------+
2 rows in set (0.00 sec)`
### Make the movie list more child-friendly. Delete all entries that have a rating of R.
`mysql> DELETE FROM Movies WHERE Rating = 'R';
Query OK, 3 rows affected (0.01 sec)
mysql> SELECT * FROM Movies;
+---------+-----------------+---------+-----------+------------+--------+
| movieid | Title           | Runtime | Genre     | IMDB_Score | Rating |
+---------+-----------------+---------+-----------+------------+--------+
|       1 | Howard the Duck |     110 | Sci-Fi    |        4.6 | PG     |
|       2 | Lavalantula     |      83 | Horror    |        4.7 | TV-14  |
|       5 | Spaceballs      |      96 | Comedy    |        7.1 | PG     |
|       6 | Monsters Inc.   |      92 | Animation |        8.1 | G      |
|       8 | Shark Tale      |      90 | Animation |        6.0 | PG     |
+---------+-----------------+---------+-----------+------------+--------+
5 rows in set (0.00 sec)`
### Delete the Movies Table.
`mysql> DROP TABLE Movies;
Query OK, 0 rows affected (0.03 sec)
mysql> SHOW TABLES;
Empty set (0.00 sec)`
### Delete the Database.
`mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| c16_db_two         |
| information_schema |
| movies_db          |
| mysql              |
| performance_schema |
| polls_db           |
| sakila             |
| sys                |
| world              |
+--------------------+
9 rows in set (0.00 sec)
mysql> DROP DATABASE movies_db;
Query OK, 0 rows affected (0.04 sec)
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| c16_db_two         |
| information_schema |
| mysql              |
| performance_schema |
| polls_db           |
| sakila             |
| sys                |
| world              |
+--------------------+
8 rows in set (0.00 sec)`
