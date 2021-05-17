# Sets

*Purpose: shows UNION, INTERSECT and EXCEPT*

Details:

- Set operators gives unique values (no duplicates)
- The datatypes must be comparable (e.g "text" is not comparable)

https://docs.microsoft.com/en-us/sql/t-sql/language-elements/set-operators-except-and-intersect-transact-sql?view=sql-server-ver15

Execute

	use master
	exec Happybits.Recreate 'Demo'
	use Demo

	CREATE TABLE BicycleParts (
		Produktnamn varchar(50),
		Kod INTEGER
	);

	CREATE TABLE Pieces (
		Code INTEGER,
		Name varchar(50) 
	);
	
	INSERT INTO BicycleParts(Produktnamn, Kod) VALUES('Sprocket', 5);      -- kugghjul
	INSERT INTO BicycleParts(Produktnamn, Kod) VALUES('Wheel', 6);         -- hjul
	INSERT INTO BicycleParts(Produktnamn, Kod) VALUES('Saddle', 7);        -- sadel
	INSERT INTO BicycleParts(Produktnamn, Kod) VALUES('Bike spokes', 8);   -- ekrar

	INSERT INTO Pieces(Code, Name) VALUES(100,'Apple'); 
	INSERT INTO Pieces(Code, Name) VALUES(6,'Wheel'); 
	INSERT INTO Pieces(Code, Name) VALUES(7,'Saddle'); 
	INSERT INTO Pieces(Code, Name) VALUES(200,'Banana'); 


List the content of the tables:

	SELECT * FROM BicycleParts
	SELECT * FROM Pieces

## Exercise

Why do you think the following won't work?

	SELECT * FROM BicycleParts
	UNION
	SELECT * FROM Pieces

Solution:

	The datatypes don't match

	Error message:

		Conversion failed when converting the varchar value 'Sprocket' to data type int.

## Exercise

Combine the two tables with "UNION"

Expected:

	Apple
	Banan
	Bike spokes
	Saddle
	Sprocket
	Wheel

Solution

	SELECT Produktnamn from BicycleParts
	UNION
	SELECT Name from Pieces



## Exercise

Get the codes from the both tables

Expected

	5
	6
	7
	8
	100
	200

Solution

	SELECT Kod from BicycleParts
	UNION
	SELECT Code from Pieces

## Exercise 

Get the productnames that are in BicycleParts but not in Piecese (use EXCEPT)

Expected:

	Bike spokes
	Sprocket

Solution

	SELECT Produktnamn from BicycleParts
	EXCEPT
	SELECT Name from Pieces

## Exercise

Exercise: Get the names that are in the both tables (use INTERSECT)

Result:

	Saddle
	Wheel

Solution

	SELECT Produktnamn from BicycleParts
	INTERSECT
	SELECT Name from Pieces


## Exercise (hard)

Create a new table **Products** with all products:

	Code Name
	5	 Sprocket
	6	 Wheel
	7	 Saddle
	8	 Bike spokes
	100	 Apple
	200	 Banana

Hint: use "UNION" select ... into ...

Solution

	SELECT * 
	INTO Products
	FROM(
	
	SELECT Code, Name from Pieces
	UNION
	SELECT Kod, Produktnamn from BicycleParts
	) P               
	
	-- Note the "P" at the end