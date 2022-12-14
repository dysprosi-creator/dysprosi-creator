- 👋 Hi, I’m @dysprosi-creator
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
dysprosi-creator/dysprosi-creator is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
-- DROP TABLE Sale;
-- DROP TABLE Customer;
-- DROP TABLE Pizza_item;
-- DROP VIEW datas;

-- CREATE TABLE Customer(cust_id int PRIMARY KEY, cust_name varchar(100));
-- CREATE TABLE Pizza_item(item_id int PRIMARY KEY, item_name varchar(100),price int);
-- CREATE TABLE Sale(bill_no int PRIMARY KEY, bill_date date, qty_sold int,cust_id int REFERENCES Customer(cust_id), item_id int REFERENCES Pizza_item(item_id));

-- INSERT INTO Customer VALUES(1,'Jayant Khanna');
-- INSERT INTO Customer VALUES(2,'Jai Anand');
-- INSERT INTO Customer VALUES(3,'Ananya Khanna');
-- INSERT INTO Customer VALUES(4,'KUMUD Khanna');
-- INSERT INTO Customer VALUES(5,'Chhavi Khanna');

-- INSERT INTO Pizza_item VALUES(1,'Chicago Pizza',5000);
-- INSERT INTO Pizza_item VALUES(2,'My Pizza',1000);
-- INSERT INTO Pizza_item VALUES(3,'Your Pizza',1500);
-- INSERT INTO Pizza_item VALUES(4,'Pizza',1200);
-- INSERT INTO Pizza_item VALUES(5,'Pattee',20);

-- INSERT INTO Sale VALUES(1,'24-July-2002',2,1,1);
-- INSERT INTO Sale VALUES(2,'24-July-2002',2,1,2);
-- INSERT INTO Sale VALUES(3,'24-July-2002',2,1,3);
-- INSERT INTO Sale VALUES(4,'24-July-2002',2,1,4);
-- INSERT INTO Sale VALUES(5,'24-July-2002',2,1,5);

-- --1
 SELECT * FROM Pizza_item WHERE price = (SELECT Min(price) FROM Pizza_item);

-- --2
 SELECT * FROM Pizza_item WHERE price > (SELECT AVG(price) FROM Pizza_item);

-- --3
SELECT s.* FROM Pizza_item p , Sale s WHERE p.price > 1200 AND p.item_id = s.item_id;

-- --4
 UPDATE Pizza_item SET price = 2000 WHERE item_name = 'Chicago Pizza';
 SELECT * FROM Pizza_item WHERE item_name = 'Chicago Pizza';

-- --5
SELECT AVG(qty_sold) as avgqty_sold FROM Sale group by item_id order by avgqty_sold desc;

-- --6 
  select * from Customer where cust_id in (select s.cust_id  from sale s left join Pizza_item p on s.item_id=p.item_id where p.price = (select min(price) from Pizza_item where price > (select min(price) from Pizza_item)));

-- --7
SELECT c.cust_name FROM Customer c, Sale s WHERE s.qty_sold = 2 AND s.cust_id = c.cust_id GROUP BY(c.cust_name); 

-- --8 
-- CREATE VIEW datas AS SELECT c.cust_name, p.item_name, s.bill_no FROM Customer c, Pizza_item p, Sale s WHERE s.item_id = p.item_id AND c.cust_id = s.cust_id;
 SELECT * FROM datas;

-- --9
SELECT * FROM Customer LEFT JOIN Sale on Customer.cust_id=Sale.cust_id;

-- --10
delete from pizza_item where item_id not in (select item_id from sale);
