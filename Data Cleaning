%let path=/home/u62562597/UpWork;

/* import CSV data */
proc import datafile="&path/sales_data.csv"
    out=sales_data
    dbms=csv
    replace;
    guessingrows=500;
    getnames=yes;
run;

/* Exploratory data inspection */
proc contents data=sales_data; run;
proc print data=sales_data (obs=10); run;

/* Missing values check */
proc means data=sales_data n nmiss;
run;

proc freq data=sales_data;
    tables Product / missing;
run;

/* Delete Product or Unit_Price missing records */
data sales_data_no_missing;
    set sales_data;
    if missing(Product) or missing(Unit_Price) then delete;
run;

/* Delete duplicate rows */
proc sort data=sales_data_no_missing noduprecs out=sales_data_clean;
    by _all_;
run;

/* checked  cleaned data */
proc print data=sales_data_clean (obs=10); run;

proc means data=sales_data_clean;
    var Quantity Unit_Price Total_Sales;
run;
