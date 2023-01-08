![[SQL Cheatsheet.pdf]]

## Database Commands
```SQL
CREATE DATABASE DBAnimals;

DROP DATABASE DBAnimals;
```

## Table Commands
```SQL
--Creates a new table with 4 columns
CREATE TABLE TBAnimals (
	CommonName    VARCHAR(255),
	Kingdom       VARCHAR(255),
	Phylum        VARCHAR(255),
	Species       VARCHAR(255),
)

--Creates a new table duplicated from tbAnimals with only 2 columns
CREATE TABLE TBAnimalsDuplicate As
	SELECT CommonName, Species
	FROM tbAnimals

--Deletes a table
DROP TABLE TBAnimalsDuplicates;

--Clears all data within a table
TRUNCATE TABLE TBAnimals; 

ALTER TABLE TBAnimals
	ADD Genus NVARCHAR(255) --Adds a column
	DROP COLUMN Phylum
	RENAME COLUMN Species to SpeciesName --Renames a column
	ALTER COLUMN CommonName NVARCHAR(255) --Modifies datatype
```

## Constraints
```SQL
CREATE TABLE TBAnimals (
	ID            INT           NOT NULL, 
	CommonName    VARCHAR(255)  NOT NULL,
	Kingdom       VARCHAR(255)  UNIQUE,
	Phylum        VARCHAR(255),
	Species       VARCHAR(255),
	QuantityAtZoo INT           DEFAULT = 0,
	DateCreated   DATE          DEFAULT GETDATE(),
	AvgWeight     INT           DEFAULT = 0,
)

ALTER TABLE TBAnimals
	ADD PRIMARY KEY (ID) --Makes ID a primary key
	ADD CONSTRAINT PK_Animal PRIMARY KEY (Species, ID)
	DROP PRIMARY KEY
```

## Frequent Commands
```SQL
SELECT * FROM TBAnimals

SELECT DISTINCT Kindom FROM TBAnimals --Selects a list of all unique Kingdom values

INSERT INTO TBAnimals (commonName, kingdom, phylum)
VALUES ('Panther Chameleon', 'Animalia', 'Chordata')

UPDATE TBAnimals
SET species = 'F. pardalis'
WHERE commonName = 'Panther Chameleon'

DELETE FROM TBAnimals WHERE species = 'F. pardalis'

SELECT Species, ID FROM TBAnimals ORDER BY ID ASC
```

## Simple Maths
```SQL
SELECT COUNT(Species)
FROM TBAnimals
WHERE Species IS NOT NULL

SELECT AVG(Species)

SELECT SUM(AvgWeight)
```

## LIKE Operator
```SQL
WHERE CustomerName LIKE 'a%'
--Finds any values that start with "a"

WHERE CustomerName LIKE '%a'
--Finds any values that end with "a"

WHERE CustomerName LIKE '%or%'
--Finds any values that have "or" in any position

WHERE CustomerName LIKE '_r%'
--Finds any values that have "r" in the second position

WHERE CustomerName LIKE 'a_%'
--Finds any values that start with "a" and are at least 2 characters in length

WHERE CustomerName LIKE 'a__%'
--Finds any values that start with "a" and are at least 3 characters in length

WHERE ContactName LIKE 'a%o'
--Finds any values that start with "a" and ends with "o"
```