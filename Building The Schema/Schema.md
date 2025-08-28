## Here we are building the schema for a real estate broker containing entity tables, their primary and foreign key constraints, and attribute data types.

Tables: Employers, Employees, Contractors, Contracts, Styles, Properties, Buyers, Sales.

````sql
-- Table for Employers
CREATE TABLE Employers (
    Company_Code NUMBER PRIMARY KEY,
    Emplr_Name VARCHAR2(100),
    Emplr_Email VARCHAR2(100),
    Emplr_Phone VARCHAR2(15),
    Emplr_ADDR VARCHAR2(200),
    Emplr_City VARCHAR2(100),
    Emplr_St VARCHAR2(50),
    Emplr_PostCode VARCHAR2(20)
);

-- Table for Employees
CREATE TABLE Employees (
    Emp_ID NUMBER PRIMARY KEY,
    Company_Code NUMBER,
    Emp_Type VARCHAR2(50),
    Emp_LNAME VARCHAR2(100),
    Emp_FNAME VARCHAR2(100),
    Emp_Email VARCHAR2(100),
    Emp_Phone VARCHAR2(15),
    Emp_ADDR VARCHAR2(200),
    Emp_City VARCHAR2(100),
    Emp_St VARCHAR2(50),
    Emp_PostCode VARCHAR2(20),
    FOREIGN KEY (Company_Code) REFERENCES Employers(Company_Code)
);

-- Table for Contractors
CREATE TABLE Contractors (
    Contr_AGTID NUMBER PRIMARY KEY,
    Company_Code NUMBER,
    Contr_Name VARCHAR2(100),
    Contr_Type VARCHAR2(50),
    Contr_POC_LNAME VARCHAR2(100),
    Contr_POC_FNAME VARCHAR2(100),
    Contr_Phone VARCHAR2(15),
    Contr_ADDR VARCHAR2(200),
    Contr_City VARCHAR2(100),
    Contr_St VARCHAR2(50),
    Contr_PostCode VARCHAR2(20),
    FOREIGN KEY (Company_Code) REFERENCES Employers(Company_Code)
);

-- Table for Contracts
CREATE TABLE Contracts (
    Agreement_ID NUMBER PRIMARY KEY,
    Contr_AGTID NUMBER,
    Contract_Type VARCHAR2(50),
    Parcel_No NUMBER,
    Agreement_Descr CLOB,
    Agr_Price_Negot NUMBER,
    FOREIGN KEY (Contr_AGTID) REFERENCES Contractors(Contr_AGTID)
    FOREIGN KEY (Parcel_No) REFERENCES Properties(Parcel_No)
);

-- Table for Styles
CREATE TABLE Styles (
    Arch_Style_Code NUMBER PRIMARY KEY,
    Arch_Style_Short_Desc VARCHAR2(100),
    Arch_Style_Ext_Desc CLOB
);

-- Table for Properties
CREATE TABLE Properties (
    Parcel_No NUMBER PRIMARY KEY,
    Arch_Style_Code NUMBER,
    Prop_ADDR VARCHAR2(200),
    Prop_City VARCHAR2(100),
    Prop_St VARCHAR2(50),
    Prop_PostCode VARCHAR2(20),
    Num_Rooms NUMBER,
    Sq_fr NUMBER,
    Market_Value NUMBER,
    FOREIGN KEY (Arch_Style_Code) REFERENCES Styles(Arch_Style_Code)
);

-- Table for Buyers
CREATE TABLE Buyers (
    Buyer_Acc_Num NUMBER PRIMARY KEY,
    Contr_AGTID NUMBER,
    Buyer_FNAME VARCHAR2(100),
    Buyer_LNAME VARCHAR2(100),
    Buyer_ADDR VARCHAR2(200),
    Buyer_City VARCHAR2(100),
    Buyer_St VARCHAR2(50),
    Buyer_PostCode VARCHAR2(20),
    Buyer_Email VARCHAR2(100),
    Buyer_Phone VARCHAR2(15),
    Buyer_Occupation VARCHAR2(100),
    Buyer_Employer VARCHAR2(100),
    Buyer_Salary NUMBER,
    Buyer_Credit_Score NUMBER,
    FOREIGN KEY (Contr_AGTID) REFERENCES Contractors(Contr_AGTID)
);

-- Table for Sales
CREATE TABLE Sales (
    Sale_ID NUMBER PRIMARY KEY,
    Parcel_No NUMBER,
    Company_Code NUMBER,
    Purchase_Date DATE,
    Purchase_Amt NUMBER,
    Contr_AGTID NUMBER,
    Buyer_Acc_Num NUMBER,
    FOREIGN KEY (Parcel_No) REFERENCES Properties(Parcel_No),
    FOREIGN KEY (Company_Code) REFERENCES Employers(Company_Code),
    FOREIGN KEY (Contr_AGTID) REFERENCES Contractors(Contr_AGTID),
    FOREIGN KEY (Buyer_Acc_Num) REFERENCES Buyers(Buyer_Acc_Num)
);
````
