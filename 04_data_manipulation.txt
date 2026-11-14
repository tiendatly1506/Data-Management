INSERT INTO customer (Cust_FName, Cust_LName, Cust_Phone, Cust_StrtNumber, Cust_StrtName, Cust_City, Cust_State, Cust_PostCode) 
VALUES ('Daniel', 'Ortega', '0431245668', '30', 'Taylor Place', 'Brisbane', 'Queensland', '4156');

INSERT INTO customerorder (CustOrd_Date, Cust_Number, Str_Num)
VALUES ('2026-09-06', 11, 7);

INSERT INTO orderline (CustOrd_ID, Prod_Num, OrdLn_DateReady, OrdLn_DatePicked, OrdLn_Qnty) VALUES (10, 1, '2026-09-08', NULL, 2);

UPDATE orderline SET OrdLn_DatePicked = '2026-09-10' WHERE CustOrd_ID = 10 AND Prod_Num = 1;
