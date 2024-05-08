# E-commerce  Website Management Project

This project aims to design and implement an e-commerce website exclusively for clothing. Our e-commerce management system is all about – making life simpler for businesses and customers .
From keeping track of products to making sure orders are delivered on time, our system has got it covered. 
It involves creating a database to support the functionality of the website, including tables .


## **1. Problem Statement:**

Designing and implementing a scalable Online Shopping Database Management System to streamline the operations of an e-commerce platform. 
The primary goal is to develop a comprehensive database system of online shopping, including product description, customer database, seller details, managing Wishlist of customer and keeping track of order status.

## **2. ER Diagram:**

![image](https://github.com/smritisinghh07/E-COMMERCE-DATABASE-SYSTEM/assets/126103324/ab9f7c75-9634-4ecf-95ac-1ed7e437795a)


## **3. ER to Table:**

![image](https://github.com/smritisinghh07/E-COMMERCE-DATABASE-SYSTEM/assets/126103324/914d4a86-3917-40c3-944f-7002461092fc)

## **4. Functional requirement**

1. A new user can register on the website.
2. A customer can see details of the product present in the cart
3. A customer can view his order history.
4. Customer can filter the product based on the product details.
5. A customer can add or delete a product from the cart.
6. A seller can unregister/ stop selling his product.
7. A seller/ customer can update his details.
8. Admin can view the products purchased on particular date.
9. Admin can view number of products sold on a particular date.
10.A customer can view the total price of product present in the cart unpurchased.
11. Admin can view details of customer who have not purchased anything.
12.Admin can view total profit earned from the website.

## **5. Implementation**

You can directly copy and paste all the commands from the text given here into the SQL console to create and insert values into your table.

## **6. Main SQL Source Code**

```**Customer Table**

create table customer(
    customer_id number(10) primary key,
    customer_name varchar(20) not null,
    date_of_birth date,
    email_id varchar(30)
);

**Phone Number Table**

create table phone_number(
    phone_number number(10),
    customer_id references customer(customer_id)
);

**Address Table**

CREATE TABLE address(
    address_id NUMBER(6),
    city VARCHAR2(20),
    s_state VARCHAR2(20),
    pincode NUMBER(6) NOT NULL,
    address_line1 VARCHAR2(30),
    address_line2 VARCHAR2(30),
    customer_id NUMBER(10) REFERENCES customer(customer_id)
);

**Seller Table**

create table seller(
    seller_id number(5) primary key,
    seller_name varchar2(20),
    seller_phone_no number(10),
    house_no number(5),
    area varchar2(20),
    city varchar2(30),
    pincode number(6) not null
);

**Product Table**

CREATE TABLE product(
    product_id NUMBER(10) PRIMARY KEY,
    product_name VARCHAR2(30),
    price NUMBER(10) NOT NULL,
    quantity NUMBER(3),
    commission NUMBER(10),
gender varchar2(6) check (gender in('male','female')),
    sizes varchar2(5) check  (sizes in ('XS','S','M','L','XL','XXL','3XL','4XL','5XL')),
    color varchar2(20) check (color in ('black','white','blue','red','yellow','pink','green','beige','golden','silver','lavender','purple',
    'orange','multi','brown')),
    brand varchar2(30),
    stock number(5),
    seller_id NUMBER(10) REFERENCES seller(seller_id)
);

**Cart Table**

CREATE TABLE cart(
    cart_id NUMBER(10) PRIMARY KEY,
    customer_id NUMBER(10) REFERENCES customer(customer_id),
    product_id NUMBER(10) REFERENCES product(product_id)
);

**Order Table**

CREATE TABLE orders(
    order_id NUMBER(10),
    order_status VARCHAR2(30) CHECK (order_status IN ('order placed', 'shipped', 'out for delivery', 'delivered')),
    shipping_date DATE,
    customer_id NUMBER(10) REFERENCES customer(customer_id),
    cart_id NUMBER(10) REFERENCES cart(cart_id)
);

**User login**

create table user_login(
    email varchar2(30) unique,
    password varchar2(16) not null,
    customer_id references customer(customer_id)
); 

**Order Item Table**

CREATE TABLE order_item(
    order_item_id NUMBER(12) PRIMARY KEY,
    price NUMBER(10) NOT NULL,
    quantity NUMBER(3) NOT NULL,
    cart_id NUMBER(10) REFERENCES cart(cart_id)
);

**Wishlist**

create table wishlist(
    wishlist_id number(10) primary key,
    customer_id references customer(customer_id),
    product_id references product(product_id)
);

**Payment**

create table payment(
    payment_id number(10) primary key,
    methods varchar2(15) check (methods in('UPI', 'credit card','debit card','cash on delivery','wallet')),
    customer_id references customer(customer_id),
    product_id references product(product_id),
    order_item_id references order_item(order_item_id),
    payment_date date
);

**customer values**

INSERT INTO customer VALUES (1, 'Rajesh Kumar', TO_DATE('1985-04-12', 'YYYY-MM-DD'), 'rajesh.kumar@gmail.com');
INSERT INTO customer VALUES (2, 'Priya Singh', TO_DATE('1990-07-21', 'YYYY-MM-DD'), 'priya.singh@gmail.com');
INSERT INTO customer VALUES (3, 'Amit Patel', TO_DATE('1982-09-05', 'YYYY-MM-DD'), 'amit.patel@gmail.com');
INSERT INTO customer VALUES (4, 'Divya Sharma', TO_DATE('1995-03-18', 'YYYY-MM-DD'), 'divya.sharma@gmail.com');
INSERT INTO customer VALUES (5, 'Sanjay Gupta', TO_DATE('1988-11-30', 'YYYY-MM-DD'), 'sanjay.gupta@gmail.com');
INSERT INTO customer VALUES (6, 'Sneha Verma', TO_DATE('1993-06-24', 'YYYY-MM-DD'), 'sneha.verma@gmail.com');
INSERT INTO customer VALUES (7, 'Ritu Mehta', TO_DATE('1980-02-14', 'YYYY-MM-DD'), 'ritu.mehta@gmail.com');
INSERT INTO customer VALUES (8, 'Anil Yadav', TO_DATE('1977-08-09', 'YYYY-MM-DD'), 'anil.yadav@gmail.com');
INSERT INTO customer VALUES (9, 'Pooja Malhotra', TO_DATE('1998-05-20', 'YYYY-MM-DD'), 'pooja.malhotra@gmail.com');
INSERT INTO customer VALUES (10, 'Kiran Reddy', TO_DATE('1984-10-17', 'YYYY-MM-DD'), 'kiran.reddy@gmail.com');
INSERT INTO customer VALUES (11, 'Manoj Tiwari', TO_DATE('1986-12-03', 'YYYY-MM-DD'), 'manoj.tiwari@gmail.com');
INSERT INTO customer VALUES (12, 'Neha Kapoor', TO_DATE('1991-09-28', 'YYYY-MM-DD'), 'neha.kapoor@gmail.com');
INSERT INTO customer VALUES (13, 'Vivek Joshi', TO_DATE('1979-07-10', 'YYYY-MM-DD'), 'vivek.joshi@gmail.com');
INSERT INTO customer VALUES (14, 'Anjali Singh', TO_DATE('1983-05-15', 'YYYY-MM-DD'), 'anjali.singh@gmail.com');
INSERT INTO customer VALUES (15, 'Suresh Sharma', TO_DATE('1978-08-22', 'YYYY-MM-DD'), 'suresh.sharma@gmail.com');
INSERT INTO customer VALUES (16, 'Deepika Patel', TO_DATE('1996-02-19', 'YYYY-MM-DD'), 'deepika.patel@gmail.com');
INSERT INTO customer VALUES (17, 'Rahul Gupta', TO_DATE('1981-01-07', 'YYYY-MM-DD'), 'rahul.gupta@gmail.com');
INSERT INTO customer VALUES (18, 'Riya Malhotra', TO_DATE('1994-04-23', 'YYYY-MM-DD'), 'riya.malhotra@gmail.com');
INSERT INTO customer VALUES (19, 'Alok Singh', TO_DATE('1975-11-09', 'YYYY-MM-DD'), 'alok.singh@gmail.com');
INSERT INTO customer VALUES (20, 'Aditi Verma', TO_DATE('1992-06-06', 'YYYY-MM-DD'), 'aditi.verma@gmail.com');
INSERT INTO customer VALUES (21, 'Suman Yadav', TO_DATE('1987-03-30', 'YYYY-MM-DD'), 'suman.yadav@gmail.com');
INSERT INTO customer VALUES (22, 'Ravi Kumar', TO_DATE('1984-10-02', 'YYYY-MM-DD'), 'ravi.kumar@gmail.com');
INSERT INTO customer VALUES (23, 'Preeti Sharma', TO_DATE('1976-09-14', 'YYYY-MM-DD'), 'preeti.sharma@gmail.com');
INSERT INTO customer VALUES (24, 'Akash Gupta', TO_DATE('1993-08-07', 'YYYY-MM-DD'), 'akash.gupta@gmail.com');
INSERT INTO customer VALUES (25, 'Ananya Singh', TO_DATE('1988-07-28', 'YYYY-MM-DD'), 'ananya.singh@gmail.com');
INSERT INTO customer VALUES (26, 'Vikas Malhotra', TO_DATE('1980-04-11', 'YYYY-MM-DD'), 'vikas.malhotra@gmail.com');
INSERT INTO customer VALUES (27, 'Juhi Patel', TO_DATE('1997-12-16', 'YYYY-MM-DD'), 'juhi.patel@gmail.com');
INSERT INTO customer VALUES (28, 'Rajeshwari Singh', TO_DATE('1979-03-25', 'YYYY-MM-DD'), 'rajeshwari.singh@gmail.com');
INSERT INTO customer VALUES (29, 'Kunal Sharma', TO_DATE('1982-11-20', 'YYYY-MM-DD'), 'kunal.sharma@gmail.com');
INSERT INTO customer VALUES (30, 'Shreya Gupta', TO_DATE('1995-10-08', 'YYYY-MM-DD'), 'shreya.gupta@gmail.com');

**phone number values**

INSERT INTO phone_number VALUES (9876543210, 1);
INSERT INTO phone_number VALUES (1234567890, 2);
INSERT INTO phone_number VALUES (2345678901, 3);
INSERT INTO phone_number VALUES (3456789012, 4);
INSERT INTO phone_number VALUES (4567890123, 5);
INSERT INTO phone_number VALUES (5678901234, 6);
INSERT INTO phone_number VALUES (6789012345, 7);
INSERT INTO phone_number VALUES (7890123456, 8);
INSERT INTO phone_number VALUES (8901234567, 9);
INSERT INTO phone_number VALUES (9012345678, 10);
INSERT INTO phone_number VALUES (1357924680, 11);
INSERT INTO phone_number VALUES (2468013579, 12);
INSERT INTO phone_number VALUES (3579246801, 13);
INSERT INTO phone_number VALUES (4680135792, 14);
INSERT INTO phone_number VALUES (5792468013, 15);
INSERT INTO phone_number VALUES (6901357924, 16);
INSERT INTO phone_number VALUES (8013579246, 17);
INSERT INTO phone_number VALUES (9124680135, 18);
INSERT INTO phone_number VALUES (2468013579, 19);
INSERT INTO phone_number VALUES (3579246801, 20);
INSERT INTO phone_number VALUES (4680135792, 21);
INSERT INTO phone_number VALUES (5792468013, 22);
INSERT INTO phone_number VALUES (6901357924, 23);
INSERT INTO phone_number VALUES (8013579246, 24);
INSERT INTO phone_number VALUES (9124680135, 25);
INSERT INTO phone_number VALUES (1234567890, 26);
INSERT INTO phone_number VALUES (2345678901, 27);
INSERT INTO phone_number VALUES (3456789012, 28);
INSERT INTO phone_number VALUES (4567890123, 29);
INSERT INTO phone_number VALUES (5678901234, 30);
INSERT INTO phone_number VALUES (6789012345, 1);
INSERT INTO phone_number VALUES (7890123456, 2);
INSERT INTO phone_number VALUES (8901234567, 3);
INSERT INTO phone_number VALUES (9012345678, 4);
INSERT INTO phone_number VALUES (5432109876, 5);
INSERT INTO phone_number VALUES (6543210987, 6);
INSERT INTO phone_number VALUES (7654321098, 7);
INSERT INTO phone_number VALUES (8765432109, 8);
INSERT INTO phone_number VALUES (9876543210, 9);
INSERT INTO phone_number VALUES (8901234567, 10);

**address values**

INSERT INTO address VALUES (2000, 'Mumbai', 'Maharashtra', 400001, '123, ABC Street', 'Near XYZ Park', 1);
INSERT INTO address VALUES (2001, 'Delhi', 'Delhi', 110001, '456, XYZ Road', 'Opposite ABC Mall', 2);
INSERT INTO address VALUES (2002, 'Kolkata', 'West Bengal', 700001, '789, PQR Avenue', 'Adjacent to LMN Hospital', 3);
INSERT INTO address VALUES (2003, 'Chennai', 'Tamil Nadu', 600001, '1011, LMN Lane', 'Behind PQR Market', 4);
INSERT INTO address VALUES (2004, 'Bangalore', 'Karnataka', 560001, '1213, RST Road', 'Next to EFG Garden', 5);
INSERT INTO address VALUES (2005, 'Hyderabad', 'Telangana', 500001, '1415, UVW Street', 'Near GHI School', 6);
INSERT INTO address VALUES (2006, 'Pune', 'Maharashtra', 411001, '1617, HIJ Avenue', 'Beside UVW Park', 7);
INSERT INTO address VALUES (2007, 'Ahmedabad', 'Gujarat', 380001, '1819, EFG Lane', 'Opposite HIJ Mall', 8);
INSERT INTO address VALUES (2008, 'Jaipur', 'Rajasthan', 302001, '2021, STU Road', 'Adjacent to VWX Hospital', 9);
INSERT INTO address VALUES (2009, 'Lucknow', 'Uttar Pradesh', 226001, '2223, WXY Avenue', 'Near RST Market', 10);
INSERT INTO address VALUES (2010, 'Patna', 'Bihar', 800001, '2425, OPQ Street', 'Next to STU Garden', 11);
INSERT INTO address VALUES (2011, 'Noida', 'Uttar Pradesh', 201301, '2627, XYZ Road', 'Opposite ABC Mall', 12);
INSERT INTO address VALUES (2012, 'Gurgaon', 'Haryana', 122001, '2829, PQR Avenue', 'Adjacent to LMN Hospital', 13);
INSERT INTO address VALUES (2013, 'Chandigarh', 'Punjab', 160001, '3031, LMN Lane', 'Behind PQR Market', 14);
INSERT INTO address VALUES (2014, 'Indore', 'Madhya Pradesh', 452001, '3233, RST Road', 'Next to EFG Garden', 15);
INSERT INTO address VALUES (2015, 'Bhopal', 'Madhya Pradesh', 462001, '3435, UVW Street', 'Near GHI School', 16);
INSERT INTO address VALUES (2016, 'Kanpur', 'Uttar Pradesh', 208001, '3637, HIJ Avenue', 'Beside UVW Park', 17);
INSERT INTO address VALUES (2017, 'Nagpur', 'Maharashtra', 440001, '3839, EFG Lane', 'Opposite HIJ Mall', 18);
INSERT INTO address VALUES (2018, 'Visakhapatnam', 'Andhra Pradesh', 530001, '4041, STU Road', 'Adjacent to VWX Hospital', 19);
INSERT INTO address VALUES (2019, 'Thane', 'Maharashtra', 400601, '4243, WXY Avenue', 'Near RST Market', 20);
INSERT INTO address VALUES (2020, 'Agra', 'Uttar Pradesh', 282001, '4445, OPQ Street', 'Next to STU Garden', 21);
INSERT INTO address VALUES (2021, 'Varanasi', 'Uttar Pradesh', 221001, '4647, XYZ Road', 'Opposite ABC Mall', 22);
INSERT INTO address VALUES (2022, 'Srinagar', 'Jammu and Kashmir', 190001, '4849, PQR Avenue', 'Adjacent to LMN Hospital', 23);
INSERT INTO address VALUES (2023, 'Ghaziabad', 'Uttar Pradesh', 201001, '5051, LMN Lane', 'Behind PQR Market', 24);
INSERT INTO address VALUES (2024, 'Amritsar', 'Punjab', 143001, '5253, RST Road', 'Next to EFG Garden', 25);
INSERT INTO address VALUES (2025, 'Allahabad', 'Uttar Pradesh', 211001, '5455, UVW Street', 'Near GHI School', 26);
INSERT INTO address VALUES (2026, 'Ranchi', 'Jharkhand', 834001, '5657, HIJ Avenue', 'Beside UVW Park', 27);
INSERT INTO address VALUES (2027, 'Howrah', 'West Bengal', 711101, '5859, EFG Lane', 'Opposite HIJ Mall', 28);
INSERT INTO address VALUES (2028, 'Coimbatore', 'Tamil Nadu', 641001, '6061, STU Road', 'Adjacent to VWX Hospital', 29);
INSERT INTO address VALUES (2029, 'Vadodara', 'Gujarat', 390001, '6263, WXY Avenue', 'Near RST Market', 30);
INSERT INTO address VALUES (2030, 'Rajkot', 'Gujarat', 360001, '6465, OPQ Street', 'Next to STU Garden', 1);
INSERT INTO address VALUES (2031, 'Kochi', 'Kerala', 682001, '6667, XYZ Road', 'Opposite ABC Mall', 2);
INSERT INTO address VALUES (2032, 'Thiruvananthapuram', 'Kerala', 695001, '6869, PQR Avenue', 'Adjacent to LMN Hospital', 3);
INSERT INTO address VALUES (2033, 'Kollam', 'Kerala', 691001, '7071, LMN Lane', 'Behind PQR Market', 4);
INSERT INTO address VALUES (2034, 'Kozhikode', 'Kerala', 673001, '7273, RST Road', 'Next to EFG Garden', 5);
INSERT INTO address VALUES (2035, 'Thrissur', 'Kerala', 680001, '7475, UVW Street', 'Near GHI School', 6);
INSERT INTO address VALUES (2036, 'Alappuzha', 'Kerala', 688001, '7677, HIJ Avenue', 'Beside UVW Park', 7);
INSERT INTO address VALUES (2037, 'Palakkad', 'Kerala', 678001, '7879, EFG Lane', 'Opposite HIJ Mall', 8);
INSERT INTO address VALUES (2038, 'Malappuram', 'Kerala', 676001, '8081, STU Road', 'Adjacent to VWX Hospital', 9);
INSERT INTO address VALUES (2039, 'Kannur', 'Kerala', 670001, '8283, WXY Avenue', 'Near RST Market', 10);

**seller values**

INSERT INTO seller VALUES (1001, 'Fashion Hub', 9876543210, 123, 'Main Street', 'Mumbai', 400001);
INSERT INTO seller VALUES (1002, 'Trendy Wear', 8765432109, 456, 'Fashion Avenue', 'Delhi', 110001);
INSERT INTO seller VALUES (1003, 'Chic Styles', 7654321098, 789, 'Fashion Plaza', 'Bangalore', 560001);
INSERT INTO seller VALUES (1004, 'Glamour Attire', 6543210987, 234, 'Fashion Park', 'Chennai', 600001);
INSERT INTO seller VALUES (1005, 'Urban Trends', 5432109876, 567, 'Fashion Street', 'Kolkata', 700001);
INSERT INTO seller VALUES (1006, 'Casual Closet', 4321098765, 890, 'Fashion Lane', 'Hyderabad', 500001);
INSERT INTO seller VALUES (1007, 'Dress Code', 3210987654, 901, 'Fashion Road', 'Pune', 411001);
INSERT INTO seller VALUES (1008, 'Style Statement', 2109876543, 234, 'Fashion Avenue', 'Ahmedabad', 380001);
INSERT INTO seller VALUES (1009, 'Designer Dreams', 1098765432, 567, 'Fashion Street', 'Jaipur', 302001);
INSERT INTO seller VALUES (1010, 'Trend Setters', 1234567890, 890, 'Fashion Lane', 'Lucknow', 226001);
INSERT INTO seller VALUES (1011, 'Fashion Forward', 2345678901, 901, 'Fashion Road', 'Chandigarh', 160001);
INSERT INTO seller VALUES (1012, 'Elite Elegance', 3456789012, 123, 'Fashion Street', 'Nagpur', 440001);
INSERT INTO seller VALUES (1013, 'Vogue Vault', 4567890123, 456, 'Fashion Park', 'Indore', 452001);
INSERT INTO seller VALUES (1014, 'Stylish Creations', 5678901234, 789, 'Fashion Plaza', 'Bhopal', 462001);
INSERT INTO seller VALUES (1015, 'Trendy Threads', 6789012345, 890, 'Fashion Lane', 'Visakhapatnam', 530001);

**product values**

INSERT INTO product VALUES (5001, 'mens t-shirt', 999, 50, 150, 'male','M', 'black', 'adidas', 100, 1001);
INSERT INTO product VALUES (5002, 'womens jeans', 1499, 30, 200,'female', 'L', 'blue', 'levis', 80, 1002);
INSERT INTO product VALUES (5003, 'mens polo shirt', 899, 40, 120,'male', 'XL', 'green', 'puma', 120, 1003);
INSERT INTO product VALUES (5004, 'womens dress', 1999, 25, 250, 'female','M', 'red', 'zara', 60, 1004);
INSERT INTO product VALUES (5005, 'mens sneakers', 2999, 20, 300,'male', 'L', 'white', 'nike', 50, 1005);
INSERT INTO product VALUES (5006, 'womens sandals', 799, 35, 100,'female', 'S', 'brown', 'bata', 90, 1006);
INSERT INTO product VALUES (5007, 'mens formal shirt', 1299, 45, 180, 'male','XXL', 'blue', 'van heusen', 70, 1007);
INSERT INTO product VALUES (5008, 'womens leggings', 599, 40, 80, 'female','M', 'black', 'H&M', 110, 1008);
INSERT INTO product VALUES (5009, 'mens shorts', 699, 55, 90, 'male','XL', 'grey', 'HRX', 95, 1009);
INSERT INTO product VALUES (5010, 'womens skirt', 899, 30, 120, 'L', 'pink', 'forever 21', 75, 1010);
INSERT INTO product VALUES (5011, 'mens hoodie', 1499, 25, 200,'male', 'M', 'grey', 'gap', 85, 1011);
INSERT INTO product VALUES (5012, 'womens sweater', 1199, 35, 150,'female', 'S', 'white', 'zara', 65, 1012);
INSERT INTO product VALUES (5013, 'mens jacket', 2499, 20, 250, 'male','L', 'black', 'roadster', 55, 1013);
INSERT INTO product VALUES (5014, 'womens coat', 2999, 15, 300, 'female','M', 'brown', 'H&M', 40, 1014);
INSERT INTO product VALUES (5015, 'mens jeans', 1799, 40, 170,'male', 'XL', 'blue', 'levis', 75, 1015);
INSERT INTO product VALUES (5016, 'womens top', 699, 50, 90,'female', 'L', 'yellow', 'forever 21', 85, 1001);
INSERT INTO product VALUES (5017, 'mens chinos', 1299, 45, 120,'male', 'XXL', 'beige', 'allen solly', 60, 1002);
INSERT INTO product VALUES (5018, 'womens blouse', 899, 30, 100,'female', 'M', 'purple', 'van heusen', 70, 1003);
INSERT INTO product VALUES (5019, 'mens sweatshirt', 999, 35, 150, 'male','XL', 'navy', 'gap', 80, 1004);
INSERT INTO product VALUES (5020, 'womens jumpsuit', 1599, 25, 200,'female', 'S', 'black', 'H&M', 45, 1005);
INSERT INTO product VALUES (5021, 'mens polo t-shirt', 799, 40, 100,'male', 'L', 'green', 'puma', 90, 1006);
INSERT INTO product VALUES (5022, 'womens cardigan', 1199, 30, 120,'female', 'M', 'blue', 'zara', 55, 1007);
INSERT INTO product VALUES (5023, 'mens formal trouser', 1299, 35, 150,'male', 'XXL', 'grey', 'van heusen', 70, 1008);
INSERT INTO product VALUES (5024, 'womens scarf', 499, 50, 80, 'female','L', 'pink', 'H&M', 100, 1009);
INSERT INTO product VALUES (5025, 'mens shirt', 999, 45, 120,'male', 'XL', 'white', 'levis', 65, 1010);
INSERT INTO product VALUES (5026, 'womens hoodie', 1499, 25, 200,'female', 'M', 'black', 'gap', 55, 1011);
INSERT INTO product VALUES (5027, 'mens vest', 599, 50, 80,'male', 'L', 'blue', 'nike', 85, 1012);
INSERT INTO product VALUES (5028, 'womens jacket', 1999, 20, 250, 'female','S', 'brown', 'zara', 45, 1013);
INSERT INTO product VALUES (5029, 'mens sweatpants', 1099, 30, 100, 'male','XL', 'black', 'HRX', 70, 1014);
INSERT INTO product VALUES (5030, 'womens leg warmers', 299, 60, 50,'female', 'M', 'grey', 'H&M', 110, 1015);
INSERT INTO product VALUES (5031, 'mens cap', 499, 55, 80, 'male','L', 'navy', 'puma', 75, 1001);
INSERT INTO product VALUES (5032, 'womens sunglasses', 799, 40, 100, 'female','S', 'black', 'ray-ban', 90, 1002);
INSERT INTO product VALUES (5033, 'mens belt', 599, 50, 80, 'male','L', 'brown', 'levis', 85, 1003);
INSERT INTO product VALUES (5034, 'womens earrings', 299, 60, 50, 'female','M', 'silver', 'zara', 110, 1004);
INSERT INTO product VALUES (5035, 'mens watch', 1999, 25, 200,'male', 'L', 'black', 'casio', 50, 1005);
INSERT INTO product VALUES (5036, 'womens shrug', 999, 35, 150, 'female','S', 'gold', 'tanishq', 80, 1006);
INSERT INTO product VALUES (5037, 'mens coat', 1299, 40, 100, 'male','XL', 'brown', 'hidesign', 120, 1007);
INSERT INTO product VALUES (5038, 'womens leggings', 1499, 30, 120,'female', 'M', 'red', 'baggit', 60, 1008);
INSERT INTO product VALUES (5039, 'mens turtle neck', 1999, 20, 250,'male', 'XXL', 'black', 'wildcraft', 55, 1009);
INSERT INTO product VALUES (5040, 'womens sweater', 999, 45, 120,'female', 'L', 'blue', 'lavie', 65, 1010);

**cart values**

INSERT INTO cart VALUES (10001, 1, 5001);
INSERT INTO cart VALUES (20002, 2, 5002);
INSERT INTO cart VALUES (30003, 3, 5003);
INSERT INTO cart VALUES (40004, 4, 5004);
INSERT INTO cart VALUES (50005, 5, 5005);
INSERT INTO cart VALUES (60006, 6, 5006);
INSERT INTO cart VALUES (70007, 7, 5007);
INSERT INTO cart VALUES (80008, 8, 5008);
INSERT INTO cart VALUES (90009, 9, 5009);
INSERT INTO cart VALUES (10010, 10, 5010);
INSERT INTO cart VALUES (11011, 11, 5011);
INSERT INTO cart VALUES (12012, 12, 5012);
INSERT INTO cart VALUES (13013, 13, 5013);
INSERT INTO cart VALUES (14014, 14, 5014);
INSERT INTO cart VALUES (15015, 15, 5015);
INSERT INTO cart VALUES (16016, 16, 5016);
INSERT INTO cart VALUES (17017, 17, 5017);
INSERT INTO cart VALUES (18018, 18, 5018);
INSERT INTO cart VALUES (19019, 19, 5019);
INSERT INTO cart VALUES (20020, 20, 5020);
INSERT INTO cart VALUES (21021, 21, 5021);
INSERT INTO cart VALUES (22022, 22, 5022);
INSERT INTO cart VALUES (23023, 23, 5023);
INSERT INTO cart VALUES (24024, 24, 5024);
INSERT INTO cart VALUES (25025, 25, 5025);
INSERT INTO cart VALUES (26001, 26, 5003);
INSERT INTO cart VALUES (27002, 27, 5007);
INSERT INTO cart VALUES (28003, 28, 5015);
INSERT INTO cart VALUES (29004, 29, 5020);
INSERT INTO cart VALUES (30005, 30, 5023);

**order values**

INSERT INTO orders VALUES (1000101, 'order placed', TO_DATE('2024-05-04', 'YYYY-MM-DD'), 1, 10001);
INSERT INTO orders VALUES (2000202, 'shipped', TO_DATE('2024-05-05', 'YYYY-MM-DD'), 2, 20002);
INSERT INTO orders VALUES (3000303, 'out for delivery', TO_DATE('2024-05-06', 'YYYY-MM-DD'), 3, 30003);
INSERT INTO orders VALUES (4000404, 'delivered', TO_DATE('2024-05-07', 'YYYY-MM-DD'), 4, 40004);
INSERT INTO orders VALUES (5000505, 'order placed', TO_DATE('2024-05-08', 'YYYY-MM-DD'), 5, 50005);
INSERT INTO orders VALUES (6000606, 'shipped', TO_DATE('2024-05-09', 'YYYY-MM-DD'), 6, 60006);
INSERT INTO orders VALUES (7000707, 'out for delivery', TO_DATE('2024-05-10', 'YYYY-MM-DD'), 7, 70007);
INSERT INTO orders VALUES (8000808, 'delivered', TO_DATE('2024-05-11', 'YYYY-MM-DD'), 8, 80008);
INSERT INTO orders VALUES (9000909, 'order placed', TO_DATE('2024-05-12', 'YYYY-MM-DD'), 9, 90009);
INSERT INTO orders VALUES (10010010, 'shipped', TO_DATE('2024-05-13', 'YYYY-MM-DD'), 10, 10010);
INSERT INTO orders VALUES (11001111, 'out for delivery', TO_DATE('2024-05-14', 'YYYY-MM-DD'), 11, 11011);
INSERT INTO orders VALUES (12001212, 'delivered', TO_DATE('2024-05-15', 'YYYY-MM-DD'), 12, 12012);
INSERT INTO orders VALUES (13001313, 'order placed', TO_DATE('2024-05-16', 'YYYY-MM-DD'), 13, 13013);
INSERT INTO orders VALUES (14001414, 'shipped', TO_DATE('2024-05-17', 'YYYY-MM-DD'), 14, 14014);
INSERT INTO orders VALUES (15001515, 'out for delivery', TO_DATE('2024-05-18', 'YYYY-MM-DD'), 15, 15015);
INSERT INTO orders VALUES (16001616, 'delivered', TO_DATE('2024-05-19', 'YYYY-MM-DD'), 16, 16016);
INSERT INTO orders VALUES (17001717, 'order placed', TO_DATE('2024-05-20', 'YYYY-MM-DD'), 17, 17017);
INSERT INTO orders VALUES (18001818, 'shipped', TO_DATE('2024-05-21', 'YYYY-MM-DD'), 18, 18018);
INSERT INTO orders VALUES (19001919, 'out for delivery', TO_DATE('2024-05-22', 'YYYY-MM-DD'), 19, 19019);
INSERT INTO orders VALUES (20002020, 'delivered', TO_DATE('2024-05-23', 'YYYY-MM-DD'), 20, 20020);
INSERT INTO orders VALUES (21002121, 'order placed', TO_DATE('2024-05-24', 'YYYY-MM-DD'), 21, 21021);
INSERT INTO orders VALUES (22002222, 'shipped', TO_DATE('2024-05-25', 'YYYY-MM-DD'), 22, 22022);
INSERT INTO orders VALUES (23002323, 'out for delivery', TO_DATE('2024-05-26', 'YYYY-MM-DD'), 23, 23023);
INSERT INTO orders VALUES (24002424, 'delivered', TO_DATE('2024-05-27', 'YYYY-MM-DD'), 24, 24024);
INSERT INTO orders VALUES (25002525, 'order placed', TO_DATE('2024-05-28', 'YYYY-MM-DD'), 25, 25025);
INSERT INTO orders VALUES (2600126, 'shipped', TO_DATE('2024-05-29', 'YYYY-MM-DD'), 26, 26001);
INSERT INTO orders VALUES (27002727, 'out for delivery', TO_DATE('2024-05-30', 'YYYY-MM-DD'), 27, 27002);
INSERT INTO orders VALUES (28002828, 'delivered', TO_DATE('2024-05-31', 'YYYY-MM-DD'), 28, 28003);
INSERT INTO orders VALUES (29002929, 'order placed', TO_DATE('2024-06-01', 'YYYY-MM-DD'), 29, 29004);
INSERT INTO orders VALUES (30003030, 'shipped', TO_DATE('2024-06-02', 'YYYY-MM-DD'), 30, 30005);
INSERT INTO orders VALUES (31003131, 'out for delivery', TO_DATE('2024-06-03', 'YYYY-MM-DD'), 1, 10001);
INSERT INTO orders VALUES (32003232, 'delivered', TO_DATE('2024-06-04', 'YYYY-MM-DD'), 2, 20002);
INSERT INTO orders VALUES (33003333, 'order placed', TO_DATE('2024-06-05', 'YYYY-MM-DD'), 3, 30003);
INSERT INTO orders VALUES (34003434, 'shipped', TO_DATE('2024-06-06', 'YYYY-MM-DD'), 4, 40004);
INSERT INTO orders VALUES (35003535, 'out for delivery', TO_DATE('2024-06-07', 'YYYY-MM-DD'), 5, 50005);
INSERT INTO orders VALUES (36003636, 'delivered', TO_DATE('2024-06-08', 'YYYY-MM-DD'), 6, 60006);
INSERT INTO orders VALUES (37003737, 'order placed', TO_DATE('2024-06-09', 'YYYY-MM-DD'), 7, 70007);
INSERT INTO orders VALUES (38003838, 'shipped', TO_DATE('2024-06-10', 'YYYY-MM-DD'), 8, 80008);
INSERT INTO orders VALUES (39003939, 'out for delivery', TO_DATE('2024-06-11', 'YYYY-MM-DD'), 9, 90009);
INSERT INTO orders VALUES (40004040, 'delivered', TO_DATE('2024-06-12', 'YYYY-MM-DD'), 10, 10010);

**user_login values**

INSERT INTO user_login VALUES ('rajesh.kumar@gmail.com', 'rajesh001', 1);
INSERT INTO user_login VALUES ('priya.singh@gmail.com', 'priya002', 2);
INSERT INTO user_login VALUES ('amit.patel@gmail.com', 'amit003', 3);
INSERT INTO user_login VALUES ('divya.sharma@gmail.com', 'divya004', 4);
INSERT INTO user_login VALUES ('sanjay.gupta@gmail.com', 'sanjay005', 5);
INSERT INTO user_login VALUES ('sneha.verma@gmail.com', 'sneha006', 6);
INSERT INTO user_login VALUES ('ritu.mehta@gmail.com', 'ritu007', 7);
INSERT INTO user_login VALUES ('anil.yadav@gmail.com', 'anil008', 8);
INSERT INTO user_login VALUES ('pooja.malhotra@gmail.com', 'pooja009', 9);
INSERT INTO user_login VALUES ('kiran.reddy@gmail.com', 'kiran010', 10);
INSERT INTO user_login VALUES ('manoj.tiwari@gmail.com', 'manoj011', 11);
INSERT INTO user_login VALUES ('neha.kapoor@gmail.com', 'neha012', 12);
INSERT INTO user_login VALUES ('vivek.joshi@gmail.com', 'vivek013', 13);
INSERT INTO user_login VALUES ('anjali.singh@gmail.com', 'anjali014', 14);
INSERT INTO user_login VALUES ('suresh.sharma@gmail.com', 'suresh015', 15);
INSERT INTO user_login VALUES ('deepika.patel@gmail.com', 'deepika016', 16);
INSERT INTO user_login VALUES ('rahul.gupta@gmail.com', 'rahul017', 17);
INSERT INTO user_login VALUES ('riya.malhotra@gmail.com', 'riya018', 18);
INSERT INTO user_login VALUES ('alok.singh@gmail.com', 'alok019', 19);
INSERT INTO user_login VALUES ('aditi.verma@gmail.com', 'aditi020', 20);
INSERT INTO user_login VALUES ('suman.yadav@gmail.com', 'suman021', 21);
INSERT INTO user_login VALUES ('ravi.kumar@gmail.com', 'ravi022', 22);
INSERT INTO user_login VALUES ('preeti.sharma@gmail.com', 'preeti023', 23);
INSERT INTO user_login VALUES ('akash.gupta@gmail.com', 'akash024', 24);
INSERT INTO user_login VALUES ('ananya.singh@gmail.com', 'ananya025', 25);
INSERT INTO user_login VALUES ('vikas.malhotra@gmail.com', 'vikas026', 26);
INSERT INTO user_login VALUES ('juhi.patel@gmail.com', 'juhi027', 27);
INSERT INTO user_login VALUES ('rajeshwari.singh@gmail.com', 'rajeshwari028', 28);
INSERT INTO user_login VALUES ('kunal.sharma@gmail.com', 'kunal029', 29);
INSERT INTO user_login VALUES ('shreya.gupta@gmail.com', 'shreya030', 30);

**order item values**

INSERT INTO order_item VALUES (900101, 1000, 2, 10001);
INSERT INTO order_item VALUES (900102, 750, 3, 20002);
INSERT INTO order_item VALUES (900201, 1200, 1, 30003);
INSERT INTO order_item VALUES (900301, 500, 2, 40004);
INSERT INTO order_item VALUES (900302, 800, 1, 50005);
INSERT INTO order_item VALUES (900401, 1500, 1, 60006);
INSERT INTO order_item VALUES (900501, 2000, 2, 70007);
INSERT INTO order_item VALUES (900601, 600, 1, 80008);
INSERT INTO order_item VALUES (900602, 900, 3, 90009);
INSERT INTO order_item VALUES (900701, 300, 2, 10010);
INSERT INTO order_item VALUES (900801, 400, 1, 11011);
INSERT INTO order_item VALUES (900901, 1100, 1, 12012);
INSERT INTO order_item VALUES (901001, 750, 2, 13013);
INSERT INTO order_item VALUES (901002, 800, 1, 14014);
INSERT INTO order_item VALUES (901101, 2000, 1, 15015);
INSERT INTO order_item VALUES (901201, 500, 3, 16016);
INSERT INTO order_item VALUES (901202, 900, 2, 17017);
INSERT INTO order_item VALUES (901301, 1200, 1, 18018);
INSERT INTO order_item VALUES (901401, 700, 2, 19019);
INSERT INTO order_item VALUES (901501, 1500, 1, 20020);
INSERT INTO order_item VALUES (901502, 800, 3, 21021);
INSERT INTO order_item VALUES (901601, 600, 1, 22022);
INSERT INTO order_item VALUES (901701, 500, 2, 23023);
INSERT INTO order_item VALUES (901801, 900, 1, 24024);
INSERT INTO order_item VALUES (901901, 2000, 1, 25025);
INSERT INTO order_item VALUES (901902, 1100, 2, 26001);
INSERT INTO order_item VALUES (902001, 750, 1, 27002);
INSERT INTO order_item VALUES (902101, 800, 2, 28003);
INSERT INTO order_item VALUES (902201, 1200, 1, 29004);
INSERT INTO order_item VALUES (902301, 700, 1, 30005);
INSERT INTO order_item VALUES (902401, 1500, 2, 22022);
INSERT INTO order_item VALUES (902501, 800, 1, 30005);
INSERT INTO order_item VALUES (902502, 600, 1, 25025);
INSERT INTO order_item VALUES (902601, 500, 3, 20002);
INSERT INTO order_item VALUES (902701, 900, 1, 40004);
INSERT INTO order_item VALUES (902801, 2000, 2, 70007);
INSERT INTO order_item VALUES (902901, 1100, 1, 21021);
INSERT INTO order_item VALUES (903001, 750, 1, 26001);
INSERT INTO order_item VALUES (903101, 800, 3, 17017);
INSERT INTO order_item VALUES (903201, 1200, 1, 19019);
INSERT INTO order_item VALUES (903301, 700, 1, 20020);
INSERT INTO order_item VALUES (903401, 1500, 2, 30003);
INSERT INTO order_item VALUES (903501, 800, 1, 50005);
INSERT INTO order_item VALUES (903601, 600, 1, 60006);
INSERT INTO order_item VALUES (903701, 500, 3, 17017);

**wishlist values**

INSERT INTO wishlist VALUES (111, 1, 5001);
INSERT INTO wishlist VALUES (112, 2, 5003);
INSERT INTO wishlist VALUES (113, 3, 5005);
INSERT INTO wishlist VALUES (114, 4, 5007);
INSERT INTO wishlist VALUES (115, 5, 5009);
INSERT INTO wishlist VALUES (116, 6, 5011);
INSERT INTO wishlist VALUES (117, 7, 5013);
INSERT INTO wishlist VALUES (118, 8, 5015);
INSERT INTO wishlist VALUES (119, 9, 5017);
INSERT INTO wishlist VALUES (120, 10, 5019);
INSERT INTO wishlist VALUES (121, 11, 5021);
INSERT INTO wishlist VALUES (122, 12, 5023);
INSERT INTO wishlist VALUES (123, 13, 5025);
INSERT INTO wishlist VALUES (124, 14, 5027);
INSERT INTO wishlist VALUES (125, 15, 5029);
INSERT INTO wishlist VALUES (126, 16, 5031);
INSERT INTO wishlist VALUES (127, 17, 5033);
INSERT INTO wishlist VALUES (128, 18, 5035);
INSERT INTO wishlist VALUES (129, 19, 5037);
INSERT INTO wishlist VALUES (130, 20, 5039);

**payment values**
    
INSERT INTO payment VALUES (1563, 'UPI', 1, 5001, 900101, TO_DATE('2023-09-05', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1564, 'credit card', 2, 5002, 903601, TO_DATE('2023-09-08', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1565, 'debit card', 3, 5003, 900102, TO_DATE('2023-09-12', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1566, 'cash on delivery', 4, 5004, 900201, TO_DATE('2023-09-15', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1567, 'wallet', 5, 5005, 900301, TO_DATE('2023-09-20', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1568, 'UPI', 6, 5006, 900302, TO_DATE('2023-09-25', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1569, 'credit card', 7, 5007, 900401, TO_DATE('2023-09-28', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1570, 'debit card', 8, 5008, 900501, TO_DATE('2023-10-02', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1571, 'cash on delivery', 9, 5009, 900601, TO_DATE('2023-10-05', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1572, 'wallet', 10, 5010, 900901, TO_DATE('2023-10-08', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1573, 'UPI', 11, 5011, 901001, TO_DATE('2023-10-12', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1574, 'credit card', 12, 5012, 901002, TO_DATE('2023-10-15', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1575, 'debit card', 13, 5013, 901101, TO_DATE('2023-10-18', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1576, 'cash on delivery', 14, 5014, 901201, TO_DATE('2023-10-22', 'YYYY-MM-DD'));
INSERT INTO payment VALUES (1577, 'wallet', 15, 5015, 901202, TO_DATE('2023-10-25', 'YYYY-MM-DD'));

```

# Contributors
## Smriti Singh
##Ridhhi Sekhri
## Kashika Chopra
