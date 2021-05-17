
# Subqueries

*Purpose: show example of "sub queries": a query within a query*

A Subquery or Inner query or a Nested query is a query within another SQL query and embedded within the WHERE clause.

A subquery is used to return data that will be used in the main query as a condition to further restrict the data to be retrieved.

Subqueries can be used with the SELECT, INSERT, UPDATE, and DELETE statements along with the operators like =, <, >, >=, <=, IN, BETWEEN, etc.

## Reference

https://www.tutorialspoint.com/sql/sql-sub-queries.htm

## Exercise

Execute this

	use master
	exec Happybits.Recreate 'Demo'
	use Demo

	CREATE TABLE Products (
	Code INTEGER PRIMARY KEY NOT NULL,
	Name TEXT NOT NULL
	);
	CREATE TABLE Companies (
	Code VARCHAR(40) 
	PRIMARY KEY NOT NULL,  
	Name TEXT NOT NULL 
	);
	CREATE TABLE Provides (
	Piece INTEGER, 
	FOREIGN KEY (Piece) REFERENCES Products(Code),
	Provider VARCHAR(40), 
	FOREIGN KEY (Provider) REFERENCES Companies(Code),  
	Price INTEGER NOT NULL,
	PRIMARY KEY(Piece, Provider) 
	);
	
	CREATE TABLE NewProducts (
		Produktnamn TEXT NOT NULL,
		Kod INTEGER
	);
	
	
	INSERT INTO Companies(Code, Name) VALUES('CLA','Clarke Enterprises');
	INSERT INTO Companies(Code, Name) VALUES('SUS','Susan Calvin Corp.');
	INSERT INTO Companies(Code, Name) VALUES('SKE','Skellington Supplies');

	INSERT INTO Products(Code, Name) VALUES(1,'Sprocket');
	INSERT INTO Products(Code, Name) VALUES(2,'Screw');
	INSERT INTO Products(Code, Name) VALUES(3,'Nut');
	INSERT INTO Products(Code, Name) VALUES(4,'Bolt');

	INSERT INTO Provides(Piece, Provider, Price) VALUES(1,'CLA',10);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(1,'SUS',15);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(2,'CLA',20);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(2,'SUS',50);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(2,'SKE',14);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(3,'SUS',50);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(3,'SKE',45);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(4,'CLA',5);
	INSERT INTO Provides(Piece, Provider, Price) VALUES(4,'SUS',7);

	INSERT INTO NewProducts(Produktnamn, Kod) VALUES('Hammer', 5);
	INSERT INTO NewProducts(Produktnamn, Kod) VALUES('Nail', 6);
	INSERT INTO NewProducts(Produktnamn, Kod) VALUES('Wrench', 7);
	INSERT INTO NewProducts(Produktnamn, Kod) VALUES('Apple', 100);
	INSERT INTO NewProducts(Produktnamn, Kod) VALUES('Banana', 200);


Get all data from all tables

	select * from Companies  
	select * from Products   
	select * from Provides   -- what products a company sells

...and try to figure out the relations between the tables


## Exercise

Get the highest prices of the products

Solution

	select Max(Price) from Provides


## Exercise

Get the Code of the Piece's which have the highest price

Expected:

	2
	3

Hint: 

	select ...... = (......)


Solution

	select Piece from Provides where Price =
		(select Max(Price) from Provides)


-- Alternative without subquery

	select top 1 with ties Piece
	from Provides 
	order by Price desc 

## Exercise

Get the names of the products from the query above

Expected

	Nut
	Screw

Hint: 

	select ...... in (.......)

Solution:

	select Name from Products where Code in (

		select Piece from Provides where Price =
			(select Max(Price) from Provides)
	)

	-- Alternative without subquery

	select top 1 with ties Name
	from Provides join Products on Provides.Piece = Products.Code
	order by Price desc 

	-- Alternative (Natnael)

	select provides.Piece, Products.Name, provides.Price from Provides
	left join Products on Provides.Piece = Products.Code
	where Price = (select Max(price) from Provides)
	order by provides.Price desc


Subqueries can also be used with INSERT statement

## Exercise

Add the products from NewProducts to Products which have a "Kod" lower than 100

	select * from Products   

should give:

	1	Sprocket
	2	Screw
	3	Nut
	4	Bolt
	5	Hammer
	6	Nail
	7	Wrench

(Apple and Banana should not be included)

Hint: use this pattern:

	insert into Products
		select ...

Solution

	insert into Products
		select Kod, Produktnamn
		from NewProducts
		where Kod < 100

	select * from Products    

	Alternative:

	insert into Products(Name, Code) 

		select *
		from NewProducts
		where Kod < 100