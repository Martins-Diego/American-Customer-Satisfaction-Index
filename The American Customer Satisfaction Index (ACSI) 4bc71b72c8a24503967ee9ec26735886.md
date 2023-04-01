# The American Customer Satisfaction Index (ACSI)

In today's highly competitive business landscape, understanding customer satisfaction is crucial for the success of any organization. It is a key driver of customer loyalty, brand reputation, and overall business performance, prompting organizations across various industries to invest heavily in measuring and improving customer satisfaction.

One organization that has emerged as a leader in this field is The American Customer Satisfaction Index (ACSI), which annually collects survey data from some 400,000 consumers across the United States for over 50 consumer industries and more than 400 companies.

To contribute to the growing body of knowledge on customer satisfaction and help businesses improve their customer satisfaction levels, this project analyzes a sample of survey data collected by the ACSI in 2015. The goal was to explore customers perceptions of their experiences with individual companies in the Processed Food, Commercial Airlines, Internet Service Providers, and Commercial Banks Industries, identifying trends and patterns that can inform decisions to gain a competitive advantage and ultimately drive business success. 

## High-Level Processed Data Overview

![ASCI DASHBOARD_page-0001.jpg](The%20American%20Customer%20Satisfaction%20Index%20(ACSI)%204bc71b72c8a24503967ee9ec26735886/ASCI_DASHBOARD_page-0001.jpg)

## Data Collection

- [https://data.mendeley.com/datasets/64xkbj2ry5/2](https://data.mendeley.com/datasets/64xkbj2ry5/2)

Found the secure private file path to allocate de dataset

```sql
SHOW VARIABLES LIKE "secure_file_priv"
```

After analyzing the dataset structure, we proceeded to create the data table

```sql
CREATE TABLE DATA(
		INDUSTRY VARCHAR(50) NOT NULL, --Industry Code
    YEAR_DATA YEAR, --Year in which data was collected
    SATIS VARCHAR(50), --Overall Customer Satisfaction
    CONFIRM VARCHAR(50), --Confirmation to Expectations
    IDEAL VARCHAR(50), --Close to ideal product/service
    OVERALLX VARCHAR(50), --Expectation about overall quality
    CUSTOMX VARCHAR(50), --Expectations about customization
    WRONGX VARCHAR(50), --Expectation about reliability
    OVERALLQ VARCHAR(50), --Overall Quality
    CUSTOMQ VARCHAR(50), --Meeting personal requirement (Customization)
    WRONGQ VARCHAR(50), --Things went wrong (Reliability)
    PQ VARCHAR(50), --Price given Quality
    QP VARCHAR(50), --Quality given Price
    COMP VARCHAR(50), --Customer complaints
    HANDLE VARCHAR(50), --Complaint handling
    REPUR VARCHAR(50), --Repurchase Intention
    HIGHPTOL VARCHAR(50), --Raising % price
    LOWPTOL VARCHAR(50), --Lowering % price
    AGE VARCHAR(50), --Age
    EDUCAT VARCHAR(50), --Education
    HISPANIC VARCHAR(50), --Hispanic
    RACE_1 VARCHAR(50), --Race_1
    RACE_2 VARCHAR(50), --Race_2
    RACE_3 VARCHAR(50), --Race_3
    RACE_4 VARCHAR(50), --Race_4
    RACE_5 VARCHAR(50), --Race_5
    INCOME VARCHAR(50), --Income
    GENDER VARCHAR(50), --Gender
    ZIPCODE VARCHAR(50) --Zip code
);
```

Loaded the data

```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/ACSI Data 2015.csv' INTO TABLE DATA
FIELDS TERMINATED BY ','
IGNORE 1 LINES;
```

## Data Wrangling

Data dictionaries were created to ensure accuracy and completeness of data

```sql
CREATE TABLE INDUSTRY(
	INDUSTRY_CODE INT PRIMARY KEY,
    INDUSTRY_NAME VARCHAR(50)
);
INSERT INTO INDUSTRY(INDUSTRY_CODE,INDUSTRY_NAME) 
VALUES (1001, 'Processed Food'),(3003, 'Commercial Airlines'),(3013, 'Internet Service Providers'), (5001, 'Commercial Banks');

CREATE TABLE SATISFACTION(
	SATISFACTION_ID INT PRIMARY KEY,
    SATISFACTION_LABEL VARCHAR(50)
);
INSERT INTO SATISFACTION(SATISFACTION_ID, SATISFACTION_LABEL) 
VALUES (1, 'Very Dissatisfied'),(2, 'Dissatisfied'),(3, 'Somewhat Dissatisfied'), (4, 'Slightly Dissatisfied'),(5, 'Neither Satisfied nor Dissatisfied'),
(6, 'Slightly Satisfied'),(7, 'Somewhat Satisfied'),(8, 'Moderately Satisfied'),(9, 'Satisfied'),(10, 'Very Satisfied');

CREATE TABLE CONFIRMATION(
	CONFIRMATION_ID INT PRIMARY KEY,
    CONFIRMATION_LABEL VARCHAR(50)
);
INSERT INTO CONFIRMATION(CONFIRMATION_ID, CONFIRMATION_LABEL)
VALUES (1, 'Falls short of expectations'),(2, 'Below expectations'),(3, 'Somewhat below expectations'),(4, 'Approaching expectations'),(5, 'Meets expectations'),
(6, 'Somewhat exceeds expectations'),(7, 'Exceeds expectations moderately'),(8, 'Exceeds expectations significantly'),(9, 'Exceeds expectations greatly'),(10, 'Far exceeds expectations');

CREATE TABLE IDEAL(
	IDEAL_ID INT PRIMARY KEY,
    IDEAL_LABEL VARCHAR(50)
);
INSERT INTO IDEAL(IDEAL_ID, IDEAL_LABEL)
VALUES (1, 'Not very close to ideal'),(2, 'Far from ideal'),(3, 'Somewhat far from ideal'),(4, 'Not quite close to ideal'),(5, 'Somewhat close to ideal'),
(6, 'Fairly close to ideal'),(7, 'Close to ideal'),(8, 'Very close to ideal'),(9, 'Nearly ideal'),(10, 'Ideal');

-- MULTIPLE
CREATE TABLE EXPECTATIONS(
	EXPECTATIONS_ID INT PRIMARY KEY,
    EXPECTATIONS_LABEL VARCHAR(50)
);
INSERT INTO EXPECTATIONS(EXPECTATIONS_ID, EXPECTATIONS_LABEL)
VALUES (1, 'Not very high'),(2, 'Somewhat low'),(3, 'Below average'),(4, 'Slightly low'),(5, 'Average'),
(6, 'Above average'),(7, 'Moderately high'),(8, 'High'),(9, 'Very high'),(10, 'Extremely high');

CREATE TABLE QUALITY(
	QUALITY_ID INT PRIMARY KEY,
    QUALITY_LABEL VARCHAR(50)
);
INSERT INTO QUALITY(QUALITY_ID, QUALITY_LABEL)
VALUES (1, 'Not very good'),(2, 'Below average'),(3, 'Somewhat below average'),(4, 'Slightly below average'),(5, 'Average'),
(6, 'Slightly above average'),(7, 'Somewhat good'),(8, 'Good'),(9, 'Very good'),(10, 'Exceptional');

CREATE TABLE PRICE(
	PRICE_ID INT PRIMARY KEY,
    PRICE_LABEL VARCHAR(50)
);
INSERT INTO PRICE(PRICE_ID, PRICE_LABEL)
VALUES (1, 'Not very good price given quality'),(2, 'Below average price given quality'),(3, 'Somewhat below average price given quality'),(4, 'Slightly below average price given quality'),(5, 'Average price given quality'),
(6, 'Slightly above average price given quality'),(7, 'Somewhat good price given quality'),(8, 'Good price given quality'),(9, 'Very good price given quality'),(10, 'Exceptional price given quality');

CREATE TABLE QUALITY_PRICE(
	QP_ID INT PRIMARY KEY,
    QP_LABEL VARCHAR(50)
);
INSERT INTO QUALITY_PRICE(QP_ID, QP_LABEL)
VALUES (1, 'Not very good quality given price'),(2, 'Below average quality given price'),(3, 'Somewhat below average quality given price'),(4, 'Slightly below average quality given price'),(5, 'Average quality given price'),
(6, 'Slightly above average quality given price'),(7, 'Somewhat good quality given price'),(8, 'Good quality given price'),(9, 'Very good quality given price'),(10, 'Exceptional quality given price');

-- CUSTOMER AND HISPANIC
CREATE TABLE CUSTOMER(
	CUSTOMER_ID INT PRIMARY KEY,
	CUSTOMER_LABEL VARCHAR(50)
);
INSERT INTO CUSTOMER(CUSTOMER_ID,CUSTOMER_LABEL)
VALUES (1, 'Yes'), (0, 'No');

CREATE TABLE COMPLAINT(
	COMPLAINT_ID INT PRIMARY KEY,
    COMPLAINT_LABEL VARCHAR(50)
);
INSERT INTO COMPLAINT(COMPLAINT_ID, COMPLAINT_LABEL)
VALUES (1, 'Not very well'),(2, 'Below average'),(3, 'Somewhat below average'),(4, 'Slightly below average'),(5, 'Average'),
(6, 'Slightly above average'),(7, 'Somewhat well'),(8, 'Well'),(9, 'Very well'),(10, 'Exceptionally well');

CREATE TABLE PURCHASE(
	PURCHASE_ID INT PRIMARY KEY,
	PURCHASE_LABEL VARCHAR(50)
);
INSERT INTO PURCHASE(PURCHASE_ID, PURCHASE_LABEL)
VALUES (1, 'Not very likely'),(2, 'Unlikely'),(3, 'Somewhat unlikely'),(4, 'Slightly unlikely'),(5, 'Neutral'),
(6, 'Slightly likely'),(7, 'Somewhat likely'),(8, 'Likely'),(9, 'Very likely'),(10, 'Extremely likely');

CREATE TABLE EDUCATION(
	EDUCATION_ID INT PRIMARY KEY,
    EDUCATION_LABEL VARCHAR(50)
);
INSERT INTO EDUCATION(EDUCATION_ID, EDUCATION_LABEL)
VALUES (1,'Less than high school'), (2,'High school'), (3,'Some college or associate degree'), (4,'College graduate'), (5,'Post-graduate');

CREATE TABLE RACE(
	RACE_ID INT PRIMARY KEY,
    RACE_LABEL VARCHAR(50)
);
INSERT INTO RACE(RACE_ID, RACE_LABEL)
VALUES (1,'White'), (2,'African-American'), (3,'American Indian'), (4,'Asian'), (5,'Native Hawaiian'), (6,'Other Race');

CREATE TABLE INCOME(
	INCOME_ID INT PRIMARY KEY,
    INCOME_LABEL VARCHAR(50)
);
INSERT INTO INCOME(INCOME_ID, INCOME_LABEL)
VALUES (1, 'Under 20K'), (2, '20K-30K'), (3, '30K-40K'), (4, '40K-60K'), (5, '60K-80K'),(6, '80K-100K'),(7, '100K or more');

CREATE TABLE GENDER(
	GENDER_ID INT PRIMARY KEY,
    GENDER_LABEL VARCHAR(50)
);
INSERT INTO GENDER(GENDER_ID, GENDER_LABEL)
VALUES (1, 'Male'), (2, 'Female');
```

## Data Modeling

These data dictionaries were used to correctly map the relationships between the raw data and their respective labels

```sql
SELECT I.INDUSTRY_NAME AS INDUSTRY, D.YEAR_DATA AS YEAR_DATA, S.SATISFACTION_LABEL AS SATIS, C.CONFIRMATION_LABEL AS CONFIRM, ID.IDEAL_LABEL AS IDEAL, 
O.EXPECTATIONS_LABEL AS OVERALLX, CUST.EXPECTATIONS_LABEL AS CUSTOMX, WRO.EXPECTATIONS_LABEL AS WRONGX, OL.QUALITY_LABEL AS OVERALLQ, MP.QUALITY_LABEL AS CUSTOMQ, 
RELI.QUALITY_LABEL AS WRONGQ, P.PRICE_LABEL AS PQ, QP.QP_LABEL AS QP, CC.CUSTOMER_LABEL AS COMP, COM.COMPLAINT_LABEL AS HANDLE, PURCH.PURCHASE_LABEL AS REPUR, 
D.HIGHPTOL AS HIGHPTOL, D.LOWPTOL AS LOWPTOL, D.AGE AS AGE, EDU.EDUCATION_LABEL AS EDUCAT, HISP.CUSTOMER_LABEL AS HISPANIC, 
R1.RACE_LABEL AS RACE_1, R2.RACE_LABEL AS RACE_2, R3.RACE_LABEL AS RACE_3, R4.RACE_LABEL AS RACE_4, R5.RACE_LABEL AS RACE_5, 
INC.INCOME_LABEL AS INCOME, GEN.GENDER_LABEL AS GENDER, D.ZIPCODE AS ZIPCODE
FROM DATA D
LEFT JOIN INDUSTRY I ON D.INDUSTRY = I.INDUSTRY_CODE
LEFT JOIN SATISFACTION S ON D.SATIS = S.SATISFACTION_ID
LEFT JOIN CONFIRMATION C ON D.CONFIRM = C.CONFIRMATION_ID
LEFT JOIN IDEAL ID ON D.IDEAL = ID.IDEAL_ID
LEFT JOIN EXPECTATIONS O ON D.OVERALLX = O.EXPECTATIONS_ID
LEFT JOIN EXPECTATIONS CUST ON D.CUSTOMX = CUST.EXPECTATIONS_ID
LEFT JOIN EXPECTATIONS WRO ON D.WRONGX = WRO.EXPECTATIONS_ID
LEFT JOIN QUALITY OL ON D.OVERALLQ = OL.QUALITY_ID
LEFT JOIN QUALITY MP ON D.CUSTOMQ = MP.QUALITY_ID
LEFT JOIN QUALITY RELI ON D.WRONGQ = RELI.QUALITY_ID
LEFT JOIN PRICE P ON D.PQ = P.PRICE_ID
LEFT JOIN QUALITY_PRICE QP ON D.QP = QP.QP_ID
LEFT JOIN CUSTOMER CC ON D.COMP = CC.CUSTOMER_ID
LEFT JOIN COMPLAINT COM ON D.HANDLE = COM.COMPLAINT_ID
LEFT JOIN PURCHASE PURCH ON D.REPUR = PURCH.PURCHASE_ID
LEFT JOIN EDUCATION EDU ON D.EDUCAT = EDU.EDUCATION_ID
LEFT JOIN CUSTOMER HISP ON D.HISPANIC = HISP.CUSTOMER_ID
LEFT JOIN RACE R1 ON D.RACE_1 = R1.RACE_ID
LEFT JOIN RACE R2 ON D.RACE_2 = R2.RACE_ID
LEFT JOIN RACE R3 ON D.RACE_3 = R3.RACE_ID
LEFT JOIN RACE R4 ON D.RACE_4 = R4.RACE_ID
LEFT JOIN RACE R5 ON D.RACE_5 = R5.RACE_ID
LEFT JOIN INCOME INC ON D.INCOME = INC.INCOME_ID
LEFT JOIN GENDER GEN ON D.GENDER = GEN.GENDER_ID;
```

Resulting Model

![image.png](The%20American%20Customer%20Satisfaction%20Index%20(ACSI)%204bc71b72c8a24503967ee9ec26735886/image.png)