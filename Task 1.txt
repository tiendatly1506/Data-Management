CREATE DATABASE IF NOT EXISTS BigM_157;
USE BigM_157;

CREATE TABLE IF NOT EXISTS CUSTOMER (
    Cust_Number      INT PRIMARY KEY AUTO_INCREMENT,
    Cust_FName       VARCHAR(30),
    Cust_LName       VARCHAR(30),
    Cust_Phone       CHAR(10),
    Cust_StrtNumber  VARCHAR(4),
    Cust_StrtName    VARCHAR(40),
    Cust_City        VARCHAR(20),
    Cust_State       CHAR(3),
    Cust_PostCode    CHAR(4)
);

CREATE TABLE IF NOT EXISTS DEPARTMENT (
    Dept_ID          INT PRIMARY KEY AUTO_INCREMENT,
    Dept_Name        VARCHAR(40)
);

CREATE TABLE IF NOT EXISTS PRODUCT (
    Prod_Num         INT PRIMARY KEY AUTO_INCREMENT,
    Prod_Desc        VARCHAR(50),
    Prod_Size        VARCHAR(10),
    Prod_Price       DECIMAL(4,2)
);


CREATE TABLE IF NOT EXISTS STORE (
    Str_Num          INT PRIMARY KEY AUTO_INCREMENT,
    Str_Name         VARCHAR(50),
    Str_Phone        CHAR(10),
    Str_Fax          CHAR(10),
    Str_Email        VARCHAR(40),
    StoreManagerID   INT,
    SupStore_Num     INT,
    FOREIGN KEY (SupStore_Num) REFERENCES STORE(Str_Num)
);

CREATE TABLE IF NOT EXISTS STOREDEPARTMENT (
    StrDept_ID       INT PRIMARY KEY AUTO_INCREMENT,
    StrDept_Phone    CHAR(10),
    StrDept_Email    VARCHAR(40),
    DeptSupervisorID INT,
    Str_Num          INT,
    Dept_ID          INT,
    FOREIGN KEY (Str_Num) REFERENCES STORE(Str_Num),
    FOREIGN KEY (Dept_ID) REFERENCES DEPARTMENT(Dept_ID)
);


CREATE TABLE IF NOT EXISTS EMPLOYEE (
    Emp_ID           INT PRIMARY KEY AUTO_INCREMENT,
    Emp_FName        VARCHAR(30),
    Emp_LName        VARCHAR(30),
    Emp_Phone        CHAR(10),
    Emp_DoB          DATE,
    Emp_StartDate    DATE,
    Emp_TaxFNum      CHAR(15),
    Emp_HourlySalary DECIMAL(10,2),
    StrDept_ID       INT,
    SupvisorID       INT,
    FOREIGN KEY (StrDept_ID) REFERENCES STOREDEPARTMENT(StrDept_ID),
    FOREIGN KEY (SupvisorID) REFERENCES EMPLOYEE(Emp_ID)
);


CREATE TABLE IF NOT EXISTS PAYSLIP (
    Pay_ID           INT PRIMARY KEY AUTO_INCREMENT,
    Pay_date         DATE,
    Pay_num_of_hours DECIMAL(4,2),
    Pay_amount_gross DECIMAL(6,2),
    Emp_ID           INT,
    Str_Num          INT,
    FOREIGN KEY (Emp_ID) REFERENCES EMPLOYEE(Emp_ID),
    FOREIGN KEY (Str_Num) REFERENCES STORE(Str_Num)
);

CREATE TABLE IF NOT EXISTS INVENTORY (
    ProductNum       INT,
    Str_Num          INT,
    Inv_QtyOnHand    INT,
    Inv_QtyOrdered   INT,
    PRIMARY KEY (ProductNum, Str_Num),
    FOREIGN KEY (ProductNum) REFERENCES PRODUCT(Prod_Num),
    FOREIGN KEY (Str_Num) REFERENCES STORE(Str_Num)
);

CREATE TABLE IF NOT EXISTS CUSTOMERORDER (
    CustOrd_ID       INT PRIMARY KEY AUTO_INCREMENT,
    CustOrd_Date     DATE,
    Cust_Number      INT,
    Str_Num          INT,
    FOREIGN KEY (Cust_Number) REFERENCES CUSTOMER(Cust_Number),
    FOREIGN KEY (Str_Num) REFERENCES STORE(Str_Num)
);
	
CREATE TABLE IF NOT EXISTS ORDERLINE (
    CustOrd_ID       INT,
    Prod_Num         INT,
    OrdLn_DateReady  DATE,
    OrdLn_DatePicked DATE,
    OrdLn_Qnty       INT,
    PRIMARY KEY (CustOrd_ID, Prod_Num),
    FOREIGN KEY (CustOrd_ID) REFERENCES CUSTOMERORDER(CustOrd_ID),
    FOREIGN KEY (Prod_Num) REFERENCES PRODUCT(Prod_Num)
);
