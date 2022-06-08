# Description of Business
The He & She Coffee is a business of fostering a sustainable economy ecosystem for the in-campus community. Through a lifestyle business concept, He & She Coffee helps to build strong students’ backgrounds and personalities. The main purpose of the He & She Coffee shop is to serve every customer with delightfully delicious coffee. Currently, there are more than 10 operating outlets around the country. To give back to the community, He & She Coffee staff and employees are recruited from the students  community. The mission of He & She Coffee is to provide a place for the student’s connections with leading local and global companies and help university students to bridge the gap between their university experience and their professional career.

# Business Rules
Each outlet have more than 1 employees
Each employee may only work at one outlet at a time
Each employee will only have 1 position
Each manager will be appointed to supervise more than 1 outlet
Each outlet will only have 1 manager
Each outlet will have 1 or more products
Each product may exists in 1 or more outlets
the only customer info that will be stored is the name, which will be linked to their order
1 customer can make 1 or more orders
Each order is either dine-in or take-away, cannot be both
Each order may have 1 or more order items
Each order item may have quantities different than each other, and it will only be tied to 1 order
Customers are required to make payments after making orders
Only cash, card and e-wallet payment methods are accepted

# Business Objectives
To develop a centralized point of sales system for He & She Coffee
To generate the daily, monthly and yearly sales report
To calculate the ins and outs of the stock everyday and set up restock schedule
To ease the management of He & She Coffee through searching for information required for managing it
To increase the productivity of He & She Coffee employees
2.0 User Requirements
Maintaining data and record
To maintain data on orders
To maintain data on employees
To maintain data on remaining stock quantity
To maintain data on payments
To maintain data on products
Searching data and record
To perform searches on orders
To perform searches on employees
To perform searches on products
To perform searches on sales
Generating report
To generate daily, monthly, yearly sales report
To generate sales report per product


# Data Model
Entity name: job

Attribute
Constraints
Remarks
job_type
Not null
Max length 50
salary
Not null
In RM, 2 decimal places, per month


Cardinalities: 
One-to-many relationship with employees entity

Entity name: category

Attribute
Constraints
Remarks
category_id
Primary key
-
name
Not null
Max length 50


	Cardinalities:
One-to-many relationship products entity

Entity name: product

Attribute
Constraints
Remarks
product_id
Primary key
-
category_id
Foreign key (references id of product_category entity)
-
name
Not null
Max length 50
unit_price
Not null, default 0
Stored in RM, two 
decimal points

	
	Cardinalities:
One-to-one relationship with line_order entity
One-to-one relationship category entity
Many-to-many relationship stock

Entity name: employee

Attribute
Constraints
Remarks
employee_id
Primary key
-
name
Not null
Max length 50
phone_number
Not null


position_name
Foreign key (references id of position)
-
type
Not null
full/part time
outlet_id
Foreign key (references id of outlet)



	
	Cardinalities:
 Many-to-one relationship with outlet entity

Entity name: manager

Attribute
Constraints
Remarks
manager_id
Primary key
-
name
Not null
Max length 50
phone_number
Not null



	
	Cardinalities:
One-to-many relationship outlet entity
One-to many relationship employee entity


Entity name: outlet

Attribute
Constraints
Remarks
outlet_id
Primary key
-
name
Not null
Max length 50
address_1
Not null
Max length 50
address_2
-
Max length 50
city
Not null
Max length 50
zipcode
Not null
Max length 50
state
Not null
Max length 50
manager_id
Foreign key (references id of manager entity)
-


	Cardinalities:
One-to-many relationship with employee entity
Many-to-one relationship with manager entity
One-to-many relationship with stock entity
One-to-many relationship with order entity

Entity name: stock

Attribute
Constraints
Remarks
outlet_id
Primary Key
Foreign key (references id of outlets entity)
-
product_id
Primary Key
Foreign key (references id of products entity)
-
stock_quantity
Not null, default 0
-


	Cardinalities:
Many-to-one relationship with outlets entity
Many-to-many relationship with products
Entity name: order

Attribute
Constraints
Remarks
order_id
Primary key
-
outlet_id
Foreign key (references id of outlet entity)
-
customer_name
Not null
Max length 50
created_at
Not null, default to current timestamp
Timestamp, displayed as dd/mm/yyyy hh:mm
type
Not null
Dine-in, takeaway


Cardinalities:
Many-to-one relationship with outlets entity
One-to-many relationship with line_order entity
One-to-one relationship with payment entity

Entity name: line_order

Attribute
Constraints
Remarks
order_id
Primary key, Foreign key (references id of orders entity)
-
product_id
Primary key, Foreign key (references id of products entity)
-
quantity
Not null, default 0
-
subtotal
Not null, default 0.00
In RM, 2 decimal places


Cardinalities:
Many-to-one relationships with order entity
Many-to-many relationship with product entity


Entity name: payment

Attribute
Constraints
Remarks
payment_ id
Primary key
-
order_id
Foreign key (references id of orders entity)
-
employee_id
Foreign key (references id of employee entity)
-
payment_amount
Not null
-
payment_date
Not null, default to current timestamp
Timestamp, displayed as dd/mm/yyyy hh:mm
payment_method
Not null
Cash, e-wallet, card
status
Not null
Paid


	Cardinalities:
One-to-one relationships with order entity
One-to-many relationships with employee entity
