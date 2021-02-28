<h2>Description</h2>
<p>This repository contains a small hands-on project on how Relational Database Management on ecommerce platform.</p>
<h2>App Function List</h2>
<ul>
    <li>Customer can choose product by category</li>
    <li>Customer can see his/her cart list</li>
    <li>Customer can check/uncheck which item they would like to proceed to the payment process</li>
    <li>Customer can see purchase history and status</li>
    <li>Customer can search a product by its name and sort by the ratings</li>
</ul>
<h2>Database Design</h2>
<img src="https://github.com/Trisna2828/Ecommerce-Relational-Database/blob/main/database_ecommerce.JPG" alt="" width="100%" height="auto">
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
            CONSTRAINT fk_Product_seller
                FOREIGN KEY Seller_id 
                REFERENCES Seller(Seller_id) 
                ON DELETE CASCADE,
            CONSTRAINT fk_Product_category
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
            CONSTRAINT fk_Customer_cart
                FOREIGN KEY Cart_id 
                REFERENCES Cart(Cart_id) 
                ON UPDATE CASCADE,
            CONSTRAINT fk_Customer_purchase
                FOREIGN KEY Purchase_id
                REFERENCES Purchase(Purchase_id)
                ON UPDATE CASCADE
        );

        CREATE TABLE Cart_item
        (
            CONSTRAINT fk_Cartitem_cart
                FOREIGN KEY Cart_id 
                REFERENCES Cart(Cart_id) 
                ON DELETE CASCADE,
            CONSTRAINT fk_Cartitem_product
                FOREIGN KEY Product_id 
                REFERENCES Product(Product_id) 
                ON DELETE CASCADE,
            CONSTRAINT fk_Cartitem_seller
                FOREIGN KEY Seller_id 
                REFERENCES Seller(Seller_id) 
                ON DELETE CASCADE,
            Quantity smallint,
            Price decimal(10,2) NOT NULL,
            Total_price decimal(10,2) NOT NULL,
            To_purchase_status BOOLEAN
        );

        CREATE TABLE Delivery_Status
        (
            Delivery_id int(1) PRIMARY KEY,
            Status VARCHAR(10)
        );

        CREATE TABLE Purchase_list
        (
            CONSTRAINT fk_Purchaselist_purchase
                FOREIGN KEY Purchase_id 
                REFERENCES Purchase(Purchase_id),
            CONSTRAINT fk_Purchaselist_cart
                FOREIGN KEY Cart_id 
                REFERENCES Cart(Cart_id) 
                ON DELETE CASCADE,
            Date_payment datetime DEFAULT(get(date)),
            CONSTRAINT fk_Purchaselist_delivery
                FOREIGN KEY Delivery_id
                REFERENCES Delivery_Status(Delivery_id) 
        )
    </code>
</pre>
<h2>Insert Data</h2>
<h2>SQL Queries on Each Function</h2>
<p>When Customer want to choose a product  by category (Groceries (GCR) for example)</p>
<pre>
    <code>
        SELECT Product_id, Product_name, Product_rating, Price, Product_category.Category_name, Seller.Seller_name
        FROM Product
        JOIN Product_category
        ON Product.Category_id = Product_category.Category_id 
        JOIN Seller
        ON Product.Seller_id = Seller.Seller_id
        WHERE Category_id = 'GCR'
    </code>
</pre>
<h2>Triggers</h2>
<h2>SQL/T-SQL Functions</h2>
