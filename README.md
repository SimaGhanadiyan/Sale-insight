This repository contains DAX (Data Analysis Expressions) functions that can be used for sales analysis in Power BI or other Microsoft Power Platform tools. These functions are designed to provide insights into factors such as the number of invoices, average sales amount, and sales per store.

1.(Number of Invoices)
This function calculates the total number of unique invoices in the 'HF' table:
تعداد_فاکتور = COUNTROWS(VALUES('HF'[شماره فاکتور]))


2.(Number of Invoices per Store)
This function calculates the number of invoices for each store, considering all other filters:

تعداد_فاکتور_هرفروشگاه = 
CALCULATE(
    COUNTROWS('HF'),
    ALLEXCEPT('HF', 'HF'[شماره فروشگاه])
)

3.(Total Invoice Lines)
This function calculates the total number of lines across all invoices:

تعداد_کل_خطوط_فاکتور = COUNTX(VALUES('HF'[شماره فاکتور]), 1)

4.(Number of Customers per Store)
This function calculates the number of customers for each store and day:

تعداد_مشتری_هرفروشگاه = 
SUMX(
    GROUPBY(
        'HF',
        'HF'[شماره فروشگاه],
        'HF'[روز]
    ),
    COUNTROWS('HF')
)

5.(Total Sales)
This function calculates the total sales amount from the 'HF' table:

میانگین مبلغ کل فاکتورها = DIVIDE(SUMX(HF, [مبلغ فروش]), COUNTROWS(HF))

6. (Average Total Invoice Amount)
This function calculates the average total amount of all invoices:

میانگین مبلغ کل فاکتورها = DIVIDE(SUMX(HF, [مبلغ فروش]), COUNTROWS(HF))

7.(Average Invoice Lines)
This function calculates the average number of lines per invoice:

میانگین_خطوط_فاکتور = AVERAGEX(VALUES('HF'[شماره فاکتور]), COUNTX('HF', 1))

8. (Sales per Store per Day)
This function calculates the total sales amount for each store on each day:


میزان_فروش_هر_فروشگاه_درروز = CALCULATE(
    SUM('HF'[مبلغ خالص فروش]),
    GROUPBY(
        'HF',
        'HF'[شماره فروشگاه],
        'HF'[روز]
    )
)

