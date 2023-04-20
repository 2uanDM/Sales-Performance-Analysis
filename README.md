# Sales Performance Analysis

In this project, I have used the dataset `sale_data.xlxs` to process, build and visualize to show the business's sales performance. This report includes 3 pages and meets all the criteria about the status of the sales department:

- Understand the company's sales performance by sales channel, sales team, stores and items.
- Identify the areas with the highest and lowest sales and find out why?
- Identify the product with the highest and lowest sales and find out why?

## Dataset description

In the file `sale_data.xlxs`, there are 5 tables:

- **Sales table**: This table contains all the transactions by day, sales channel, stores and items
- **Regions**: This table contains information about all the states of the US and respective regions
- **Sales team**: This table contains information about sales team
- **Product**: This table contains information about the launched products
- **Store Locations**: This table contains information about the stores of this retail chain's stores.

<span style="color:red">Problem with this dataset:</span>

- The names are not synchronized, the format is not consistent and the meaning is unclear.
- The FACT table here is the "Sales table", meaning that this table will contains many records. To optimize memory problems, we should change some foreign keys' types from `text` to `int`.

  For example, in the "Sales Channel" attribute, the use of `text` type to store thousands, millions of records will take a lot more memory than using an `int` ID for each sales channel.

- In the FACT table "Sales table", the current number of rows is more than 1 million lines, while only about 20 thousand lines have complete data about orders. Furthermore, some attributes in the table "Sales table" can be omitted, such as "Currency" since all values are in `USD`

## Data processing (clean and transform)

In this part, I will make use of `Power Query` inside `Power BI` to clean and tranform data

1. Sales Table -> FactSales

   - Format and rename data types
   - Replace the “Sales Channel” attribute with “Sales Channel Index” and create another “DimSalesChannel” table
   - Delete the “Currency” attribute

2. Sales team -> DimSalesTeams

   - Choose a random name to fill in the missing value of sales team with index 20

3. Store Locations -> DimStoreLocation

   - Although this is a DIM table that includes stores' information, the amount of attributes in this table is extremely large. That is why I decided to create more DIM tables from this one to benefit for the visualization procress later <br><br>

    <p align="center"> 
    
    | Separated tables | Primary Key | Remaining attributes                                                              |
   | ---------------- | ----------- | --------------------------------------------------------------------------------- |
   | DimPopulation    | StoreID     | Population <br> Households <br> Median <br> Income <br> Land Area <br> Water Area |
   | DimState         | Sate Code   | State <br> Region                                                                 |
   | DimCounty        | County ID   | County Name                                                                       |
   | DimStoreTypes    | Type ID     | Type Name                                                                         |
    </p>
    <p align = "center"> <u>Table 1</u>: DimStoreLocation table </p>

   After separating and changing attributes from `text` to `whole number` ID respectively, DimStoreLocations will be like this:

   ![image](./img/dimstorelocation.png)
