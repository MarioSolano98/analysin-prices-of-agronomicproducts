# Agricultural Products Prices-Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection

## Problem Statement

This dashboard helps to understand the prices in agricultural products in El Salvador mayors markets. The data comes from the ministry of agriculture in daily reports and I bould a scrapper to download, process and consolidate the data. We can see the changes on products prices over the years organized on four main categories (Fruits, Grains, Vegetables and Agroindustrials) from diferents zones in the country.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Filter for the prodcutos that doesnt have a correlative indicative
- Step 3 : Enhance the information adding a table with units of different productos
- Step 4 : Enhance the information adding a table with the location of the markets
- Step 5 : Add a standar Calendar table
- Step 6 : Add a dedicated measures table

The measuires created where: 
       
        Precio Promedio = 
        /*
        Average Prices
        */
        AVERAGE('Reporte_Consolidado Precios de Productos'[Promedio Mayoristas])

        Precio Promedio Mes Anterior = 
        /*
        Average Price of the previus Month usint time intelligence
        */
        CALCULATE([Precio Promedio],PARALLELPERIOD('Tabla Calendario'[Fecha],-1,MONTH))
        
        
        
        Precio Promedio y Unidad de Medida = 
        /*
        Average Price and Measure Unit, display the avg price measure and the unit of measure as a string
        */
        CONCATENATE([Precio Promedio],FIRSTNONBLANK('Unidades de Productos'[Unidad])) 
        
        Primer Precio Promedio = 
              /*
              First Montly Average Price, this measure shows the average price for the first month of the context
              If we select a year as a filter this will show the average price of january
              */
              CALCULATE([Precio Promedio],
                  FILTER(
                      'Reporte_Consolidado Precios de Productos',
                      AND(
                      MONTH('Reporte_Consolidado Precios de Productos'[Fecha])=
                      MONTH(MIN('Reporte_Consolidado Precios de Productos'[Fecha])),
                      YEAR('Reporte_Consolidado Precios de Productos'[Fecha])=
                      YEAR(MIN('Reporte_Consolidado Precios de Productos'[Fecha]))
                      )
                      ))
        Ultimo Precio Promedio =
              /*
              Last Montly Average Price, this measure shows the average price for the last month of the context
              If we select a year as a filter this will show the average price of december
              */
              CALCULATE([Precio Promedio],
                  FILTER(
                      'Reporte_Consolidado Precios de Productos',
                      AND(
                      MONTH('Reporte_Consolidado Precios de Productos'[Fecha])=
                      MONTH(MAX('Reporte_Consolidado Precios de Productos'[Fecha])),
                      YEAR('Reporte_Consolidado Precios de Productos'[Fecha])=
                      YEAR(MAX('Reporte_Consolidado Precios de Productos'[Fecha]))
                      )
                     ))
       Cambios en Precios =
               /*
              Actual Montly Average Price Change, this measure shows the change bewtween the actual price and the price at the begining of the selected preiod
              */
               [Precio Promedio]-[Precio Promedio Mes Anterior]
               
       Cambios en Precios Periodo Selecionado =
              /*
              Changes in prices in the selected period
              If a year is selected the result will be the average price in december vs the average price in january
              */
              [Ultimo Precio Promedio]-[Primer Precio Promedio]
       
        
        Cambios en Precios Periodo Selecionado % =
               /*
              Porcentual changes in prices in the selected period
              */
               DIVIDE([Cambios en Precios Periodo Selecionado],[Primer Precio Promedio],0)

 
 # Report Snapshot (Power BI DESKTOP)
![general-categories](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/analizing-agriculturalproductos-prices-dashboard2.png)

![prodcuts](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/analizing-agriculturalproductos-prices-dashboard1.png)

# Visualizations Created

1 Percentual Grown bt Category
![prodcuts](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/Percentual%20Changes%20Line%20Chart.png)

2 Category Cards
![prodcuts](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/Category%20KPI%20card.png)

3. Markets and Zones
![prodcuts](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/Markets%20and%20Zones%20Map.png)

4. Productos with in categories
![prodcuts](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/Product%20within%20Subcategory%20Line%20Chart.png)


# Insights

A 
 



