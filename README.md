# BI
Clothing Marketing which is analyzed in two parts Within-campaign and Outside-campaign.

👩‍💻 Created using Microsoft Power BI.


💻 Overview : Shows total products, total revenue, total quantity sold and total transactions.
💰 Revenue : Revenue shown over different months, campaign name, by categories and also MOM growth 📈 shown in KPI card.
👔 Product : Analysis is for product sold out in campaign, category and sub-category wise product, % contribution of each product in total revenue etc.
🕵‍♀️ RCA : Showing revenue distribution among the campaign-category-product name. 

Some of the DAX I used in my report are,

Calendar Table = ADDCOLUMNS(CALENDAR(MIN(Fact_transactions[purchase_date]),MAX(Fact_transactions[purchase_date])),
                          "Month Num",MONTH([Date]),
                          "Month Name",FORMAT([Date],"mmm"),
                          "Year",YEAR([Date]),
                          "Quarter","Q "&QUARTER([Date]),
                          "Day1", DAY([Date]))

**PM_Qnty** = CALCULATE([Total Quantity],DATEADD('Calendar Table'[Date],-1,MONTH))

**MOM Quantity** = 
    var mom = CALCULATE([Total Revenue],DATEADD('Calendar Table'[Date],-1,MONTH))
RETURN
    DIVIDE(mom-[Total Revenue],mom,"null")
    
**Total Products** = DISTINCTCOUNT(Fact_transactions[product_id])
**Total Revenue** = SUM(Fact_transactions[RevenueT])
**Avg Qnty Sold** = AVERAGE(Fact_transactions[quantity])
