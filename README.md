# Snowflake



CREATE OR REPLACE TABLE RAW_DB.RAW.RAW_CUSTOMER (
    CUSTOMER_ID        NUMBER,
    FIRST_NAME         STRING,
    LAST_NAME          STRING,
    EMAIL              STRING,
    PHONE              STRING,
    ADDRESS            STRING,
    CREATED_AT         STRING,
    LAST_UPDATED       STRING,
    IS_DELETED         STRING
);

CREATE OR REPLACE TABLE RAW.RAW_PRODUCT (
    PRODUCT_ID        NUMBER,
    PRODUCT_NAME      STRING,
    CATEGORY          STRING,
    PRICE             STRING,
    CREATED_AT        STRING,
    LAST_UPDATED      STRING,
    IS_DELETED        STRING
);


INSERT INTO RAW.RAW_PRODUCT VALUES
(101, ' iphone 14 ', 'Mobile', '$799', '2023-01-01', '2023-01-05', '0'),
(102, ' Samsung TV ', 'Electronics', '$1200', '2023-01-05', '2023-01-10', '0'),
(103, ' Dell Laptop ', NULL, '$999', '2023-01-10', '2023-01-15', '1');


INSERT INTO RAW.RAW_CUSTOMER VALUES
(1, 'John ', ' Doe', 'John.Doe@Gmail.com', '(123)-456 7890', ' 12 Street Road ', '2023-01-01', '2023-03-01', '0'),
(2, 'Anna', 'Smith ', 'Anna.Smith@Yahoo.com', '123 456 9999', '45 Lake View', '2023-02-10', '2023-03-10', '0'),
(3, 'Mike ', ' Jordan', ' Mike.Jordan@outlook.com ', '999-888-7777', ' 78 Hill Road ', '2023-01-15', '2023-03-20', '1');

------



CREATE OR REPLACE TABLE RAW.RAW_SALES (
    SALES_ID          NUMBER,
    CUSTOMER_ID       NUMBER,
    PRODUCT_ID        NUMBER,
    QUANTITY          STRING,
    AMOUNT            STRING,
    CREATED_AT        STRING,
    LAST_UPDATED      STRING,
    IS_DELETED        STRING
);


INSERT INTO RAW.RAW_SALES VALUES
(5001, 1, 101, ' 2 ', '799', '2023-03-01', '2023-03-02', '0'),
(5002, 2, 102, '1', '1200', '2023-03-10', '2023-03-10', '0'),
(5003, 3, 103, '3 ', '999', '2023-03-20', '2023-03-22', '1');

META DATA TABLE:

CREATE OR REPLACE TABLE CONTROL_TABLE (
    CONTROL_ID           NUMBER AUTOINCREMENT,
    SOURCE_TABLE         STRING,
    TARGET_TABLE         STRING,
    WATERMARK_COLUMN     STRING,
    WATERMARK_VALUE      TIMESTAMP_NTZ,
    SELECT_SQL           STRING,
    IS_SCD2              BOOLEAN,
    ACTIVE_FLAG_COLUMN   STRING,
    LOAD_FREQUENCY       STRING,
    STATUS               STRING,
    LAST_RUN             TIMESTAMP_NTZ
);


CREATE OR REPLACE TABLE CONTROL_TABLE (
    CONTROL_ID          NUMBER AUTOINCREMENT,
    SOURCE_TABLE        STRING,
    TARGET_TABLE        STRING,
    TABLE_TYPE          STRING,       -- DIM or FACT
    SCD_TYPE            NUMBER,       -- 0 = FACT, 1 = SCD1, 2 = SCD2
    WATERMARK_COLUMN    STRING,       -- Usually LAST_UPDATED or MODIFIED_DATE
    LAST_WATERMARK      TIMESTAMP,    -- Last processed point
    TRANSFORMATION_SQL  STRING,       -- SELECT with cleaning logic
    ACTIVE_FLAG         BOOLEAN DEFAULT TRUE,
    CREATED_AT          TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UPDATED_AT          TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


ONTROL_TABLE;
