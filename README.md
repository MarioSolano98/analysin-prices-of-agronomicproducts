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
       
        Precio Promedio = AVERAGE('Reporte_Consolidado Precios de Productos'[Promedio Mayoristas])

        Precio Promedio Mes Anterior = 
        CALCULATE([Precio Promedio],PARALLELPERIOD('Tabla Calendario'[Fecha],-1,MONTH))
        
        
        
        Precio Promedio y Medida = 
        CONCATENATE([Precio Promedio],FIRSTNONBLANK('Unidades de Productos'[Unidad])) 
           Primer Precio Promedio = CALCULATE([Precio Promedio],
           FILTER(
               'Reporte_Consolidado Precios de Productos',
               AND(
               MONTH('Reporte_Consolidado Precios de Productos'[Fecha])=
               MONTH(MIN('Reporte_Consolidado Precios de Productos'[Fecha])),
               YEAR('Reporte_Consolidado Precios de Productos'[Fecha])=
               YEAR(MIN('Reporte_Consolidado Precios de Productos'[Fecha]))
               )
               ))

           Ultimo Precio Promedio = CALCULATE([Precio Promedio],
           FILTER(
               'Reporte_Consolidado Precios de Productos',
               AND(
               MONTH('Reporte_Consolidado Precios de Productos'[Fecha])=
               MONTH(MAX('Reporte_Consolidado Precios de Productos'[Fecha])),
               YEAR('Reporte_Consolidado Precios de Productos'[Fecha])=
               YEAR(MAX('Reporte_Consolidado Precios de Productos'[Fecha]))
               )
           ))

           Cambios en Precios Periodo Selecionado = 
        [Ultimo Precio Promedio]-[Primer Precio Promedio]
        
        Cambios en Precios =
        [Precio Promedio]-[Precio Promedio Mes Anterior]
        
        Cambios en Precios Periodo Selecionado % = 
        DIVIDE([Cambios en Precios Periodo Selecionado],[Primer Precio Promedio],0)


# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

 
 # Report Snapshot (Power BI DESKTOP)
![dashboard_snapo](https://github.com/MarioSolano98/analyzing-prices-of-agronomicproducts/blob/main/analizing-agriculturalproductos-prices-dashboard1.png)
 

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings


  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Grown
  

 ### Some other insights

 



