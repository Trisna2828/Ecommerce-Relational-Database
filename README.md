<h2>Description</h2>
<h2>App Function List</h2>
<h2>Database Design</h2>
<h2>Create Table</h2>
<pre>
    <code>
        CREATE TABLE Seller
        (
            Seller_id VARCHAR(8) NOT NULL UNIQUE,
            Seller_name VARCHAR(15) NOT NULL,
            Seller_rating decimal(1,2),
            PRIMARY KEY (Seller_id)
        );

        CREATE TABLE Product_category
        (
            Category_id VARCHAR(3) NOT NULL UNIQUE,
            Category_name VARCHAR(15) NOT NULL,
            PRIMARY KEY (Category_id)
        );

        CREATE TABLE Product
        (
            Product_id VARCHAR(8) NOT NULL UNIQUE,
            Product_name VARCHAR(30) NOT NULL,
            Stock_amount smallint NOT NULL,
            Sold_amount smallint,
            Product_rating decimal(1,2),
            Price decimal(10,2),
            PRIMARY KEY (Product_id),
            CONSTRAINT fk_seller
                FOREIGN KEY Seller_id 
                REFERENCES Seller(Seller_id) 
                ON DELETE CASCADE,
            CONSTRAINT fk_product_category
                FOREIGN KEY Category_id
                REFERENCES Product_category(Category_id)
                ON UPDATE CASCADE
        );

        CREATE TABLE Cart 
        (
            Cart_id VARCHAR(8) PRIMARY KEY
        );

        CREATE TABLE Purchase
        (
            Purchase_id VARCHAR(8) PRIMARY KEY
        );

        CREATE TABLE Customer
        (
            Customer_id VARCHAR(8) NOT NULL UNIQUE,
            firstname VARCHAR(10) NOT NULL,
            lastname VARCHAR(10),
            user_password VARCHAR(16) NOT NULL,
            username VARCHAR(10) NOT NULL,
            user_address VARCHAR(50);
            email VARCHAR(30) NOT NULL,
            CONSTRAINT fk_cart
                FOREIGN KEY Cart_id 
                REFERENCES Cart(Cart_id) 
                ON UPDATE CASCADE,
            CONSTRAINT fk_purchase
                FOREIGN KEY Purchase_id
                REFERENCES Purchase(Purchase_id)
                ON UPDATE CASCADE
        );

        
    </code>
</pre>
<h2>SQL Queries on Each Function</h2>
<h2>C</h2>
<h2>C</h2>
