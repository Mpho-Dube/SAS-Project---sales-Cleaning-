%let path=/home/u62562597/UpWork;
/* sales_data_clean have been in the WORK libraries */

/* Statistics: Summarize total sales by region */
proc sql;
    create table sales_by_region as
    select Region,
           sum(Total_Sales) as Total_Sales format=dollar12.2
    from sales_data_clean
    group by Region;
quit;

/* Statistics: Summary of quantity and sales revenue by product */
proc sql;
    create table sales_by_product as
    select Product,
           sum(Quantity) as Total_Units,
           sum(Total_Sales) as Total_Sales format=dollar12.2
    from sales_data_clean
    group by Product;
quit;

/* Chart 1: Bar Chart of Total Sales by Region */
proc sgplot data=sales_by_region;
    vbar Region / response=Total_Sales datalabel;
    title "Total Sales by Region";
run;

/* Chart 2: Bar Chart of Product Sales Quantity */
proc sgplot data=sales_by_product;
    vbar Product / response=Total_Units datalabel;
    title "Total Units Sold by Product";
run;

/* Chart 3: Product Sales Pie Chart */
proc template;
    define statgraph piechart;
        begingraph;
            layout region;
                piechart category=Product response=Total_Sales /
                    datalabelcontent=all;
            endlayout;
        endgraph;
    end;
run;

proc sgrender data=sales_by_product template=piechart;
    title "Sales Distribution by Product";
run;

/* Output report as PDF */
ods pdf file="&path/sales_report.pdf";  
title "Sales Report Summary";

/* Insert report content */
proc print data=sales_by_region noobs; title2 "Total Sales by Region"; run;
proc print data=sales_by_product noobs; title2 "Sales by Product"; run;

proc sgplot data=sales_by_region; vbar Region / response=Total_Sales datalabel; run;
proc sgplot data=sales_by_product; vbar Product / response=Total_Units datalabel; run;
proc sgrender data=sales_by_product template=piechart; run;

ods pdf close;
