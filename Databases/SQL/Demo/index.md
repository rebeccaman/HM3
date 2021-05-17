# Index

*Purpose: speed test. Use index to speedup queries.*

Indexes are used to retrieve data from the database more quickly than otherwise. The users cannot see the indexes, they are just used to speed up searches/queries.

Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.

For example, if you want to reference all pages in a book that discusses a certain topic, you first refer to the index, which lists all the topics alphabetically and are then referred to one or more specific page numbers.

An index helps to speed up SELECT queries and WHERE clauses, but it slows down data input, with the UPDATE and the INSERT statements. Indexes can be created or dropped with no effect on the data.

Indexes can also be unique, like the UNIQUE constraint, in that the index prevents duplicate entries in the column or combination of columns on which there is an index.

The following guidelines indicate when the use of an index should be reconsidered.

- Indexes should not be used on small tables.
- Tables that have frequent, large batch updates or insert operations.
- Indexes should not be used on columns that contain a high number of NULL values.
- Columns that are frequently manipulated should not be indexed.

https://www.w3schools.com/sql/sql_create_index.asp
https://www.tutorialspoint.com/sql/sql-indexes.htm


## Exercise

Create these two tables and will with data (may take some time, like 30s):

	use master
	exec Happybits.Recreate 'Demo'
	use Demo

	CREATE TABLE Person(Id int not null, Name nvarchar(60), StreetAddress nvarchar(60), Height int, CompanyId int)
	CREATE TABLE Company(Id int not null, Name nvarchar(60))
	GO

	ALTER TABLE [dbo].[Person] ADD CONSTRAINT [PK_Person] PRIMARY KEY CLUSTERED ([Id] ASC)
	ALTER TABLE [dbo].[Company] ADD CONSTRAINT [PK_Company] PRIMARY KEY CLUSTERED ([Id] ASC)
	GO


	

	DECLARE @i int = 0

	WHILE @i < 300000 BEGIN

		INSERT INTO Person(Id, Name, StreetAddress, Height, CompanyId) 
		VALUES (
			@i, 
			CONVERT(nvarchar(60), newid()), 
			CONVERT(nvarchar(60), newid()), 
			140+rand()*60, 
			rand()*100) 

		SET @i = @i + 1
	END


## Exercise

We want to know how many people that has a name that starts with A

Run this script five times and note the difference. Calculate the median value of "elapsed time".

For example: 214ms (205 206 214 221 225)

	set statistics time on
		select *
		from 
		Person p 
		where p.Name like 'a%'
	set statistics time off

## Exercise

Change the query to speed up. Calculate the median value of "elapsed time".

For example: 31ms (30 31 31 31 31)

	set statistics time on
		select Count(*)
		from 
		Person p 
		where p.Name like 'a%'
	set statistics time off

## Exercise

Add an index.  Calculate the median value of "elapsed time".

Solution

	CREATE INDEX IX_Name ON Person(Name)
	GO

	For example 2ms: 3 2 2 2 2

	(More than 10 times faster than previous!)
