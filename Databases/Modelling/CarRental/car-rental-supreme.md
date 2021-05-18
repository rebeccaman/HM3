# SQL - Modeling car rental

## Task

Car rental company **Car Rental Supreme** wants to create a computer system to keep track of its customers, reservations and cars. Right now they use paper and pencil and it gets very messy. To build the computer system, a database model must first be developed.

You have had a meeting with Car Rental Supreme where they told you about their needs and you have taken notes. Based on these notes, you should design a database. Here are your notes:

A customer should be able to book a car for a period of time.

It is not certain that the customer will be the person driving the car, so the driver must also be saved in the booking.

    Basic information (first name, last name, social security number, address) should be saved for customers and also car drivers.

    Customers who often rent from the company should be able to receive a discount. There should be three level: Standard, Premium and Gold. Premium should give 10% discount and Gold should give 25% discount.

    The car rental company currently has three car brands: Scoda, Volvo, BMW

    Cars now have these different colors: Red, White, Black

    There are three sizes of cars: Minicar, Normal, SUV. If a customer rents a Minicar, he should receive a 50% discount. An SUV costs 2.5 times more than a Normal.

    Payment is made by invoice. The invoice must include such description and address. The system should keep track of whether an invoice is paid or not.
 
Create the  tables and columns you think are needed.

Add appropriate primary keys and relations to the tables.

Everything is about database modeling, creating tables and relationships. You do not need to do any calculations for eg discounts or any other functionality. Only make sure up may adjust the discount in the database. The entire task is solved in **SQL Management Studio**.

Fill the database with appropriate test values.

## Extra

1. CRS (Car Rental Supreme) has a number of parking lots. They want to keep track of where the cars are parked.

2. Some parking lots are small and the SUVs do not fit. Update the database model for this scenario.

3. Now things are going well for the company and they have started several offices. CRS wants to keep track of which office has which cars etc.

4. CRS is expanding and is now available throughout Sweden. There are three offices in the Gothenburg area, two in Stockholm and one in Malmö. Update the database model.

5. Things are going well in Gothenburg and they now have five offices. CRS has decided that their companies should be divided into regions. These are available right now:
- Gothenburg North
- Gothenburg South
- Stockholm
- Malmö

6. Most cars are rented out of one office, but some cars are shared by several offices. Update the database model.

7. Think about what additional information a car hire company may need to handle.
Add a few tables with associated columns and any relationships. Motivate your choice. Report to your teacher.