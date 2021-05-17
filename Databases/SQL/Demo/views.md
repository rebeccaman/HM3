# Views

*Purpose: show the usage of "views"*

In SQL, a view is a virtual table based on the result-set of an SQL statement.

A view contains rows and columns, just like a real table. The fields in a view are fields from one or more real tables in the database.

You can add SQL functions, WHERE, and JOIN statements to a view and present the data as if the data were coming from one single table.

A view always shows up-to-date data! The database engine recreates the data, using the view's SQL statement, every time a user queries a view.

https://www.w3schools.com/sql/sql_view.asp

Execute this

	use master
	exec Happybits.Recreate 'Demo'
	use Demo

	CREATE TABLE [RoomSize](
		[Id] [int] NOT NULL,
		[RoomType] [nvarchar](50) NOT NULL,
		[NumberOfBeds] [int] NOT NULL,
		[ExtraBeds] [int] NULL,
		[Price] [int] NOT NULL
	)

	INSERT [RoomSize] VALUES (1, 'Single room', 1, 0, 700)
	INSERT [RoomSize] VALUES (2, 'Single room + 1', 1, 1, 720)
	INSERT [RoomSize] VALUES (3, 'Double room', 2, 0, 900)
	INSERT [RoomSize] VALUES (4, 'Double room + 1', 2, 1, 920)
	INSERT [RoomSize] VALUES (5, 'Double room + 2', 2, 2, 940)
	INSERT [RoomSize] VALUES (6, 'Suite', 4, 0, 1200)
	INSERT [RoomSize] VALUES (7, 'Precidential suite', 2, 4, 1500)
	INSERT [RoomSize] VALUES (8, 'Bridal suite', 2, 0, 2000)

Look at the RoomSize-table

	select * from RoomSize

## Exercise

Create a view with name "[Rooms With Extra Beds]" that gets all rooms with one or more extra beds.

Solution

	create View [Rooms With Extra Beds]
	as
		select * 
		from RoomSize
		where ExtraBeds>=1

Use the view

	select * 
	from 
	[Rooms With Extra Beds]


Detail: if you want to run the script at once you have to write "go" above "create View"

## Exercise

Use the last view but only show rooms cheaper than 925

This is an example that you can continue to filter on a view

Solution

	select * from [Rooms With Extra Beds]
	where Price<=925

## Exercise

Create a view "Cheap Rooms With Extra Beds" that show rooms with extra beds that are cheaper than 925.

Solution

	create View [Cheap Rooms With Extra Beds]
	as

		select * from [Rooms With Extra Beds]
		where Price<=925

	-- So it's possible to use views inside of views