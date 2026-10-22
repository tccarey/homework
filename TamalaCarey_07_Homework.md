# SECTION 07 HW 
<br>

## Directions 
1. You will need to open up the SavvyCoders_SQL_EVtables.db for the first part of the HW.
2. If you need to change databases you will be instructed to do so. 
3. Please answer all of the questions in a markdown file. Here is the sample format: 
 

<br>

# 7.1 HW Questions 


1. Using EVregistry, Write a query to select the `ModelYear`, `Make`, and `Model` off all of the vehicles in the registry.
```SQL
SELECT ModelYear, Make, Model
FROM EVRegistry 
```

2. Using the EVRegistry table, Write a query that lists all of the unique types of EV's. your reult set should have one column, `ElectricVehicleType`. 
```SQL
SELECT DISTINCT ElectricVehicleType
FROM EVRegistry
```
3. Using the EVRegistry, Write a query that shows all of the information on Battery Electric Vehicles (BEV) that are in the registry. 
```SQL
SELECT * 
FROM EVRegistry
WHERE ElectricVehicleType = 'Battery Electric Vehicle (BEV)'
```
4. Using the EVRegistry, wirte a query that returns the `Make` and `Model` of all of the EV's that have a BaseMSRP between 20000 and 35000?  
```SQL
SELECT Make, Model
FROM EVRegistry
WHERE BaseMSRP BETWEEN  >= 20000 AND <= 35000
--AND BaseMSRP <= 35000
```

# 7.2 HW Questions 

1. Using EVRegistry, write a query to find a record  where the `City` attribute is NULL. Return all of the available columns. 
```SQL
SELECT *
FROM EVRegistry
WHERE City IS NULL
```
2. Write a query to find the `make`, `model`, and `ElectricVehicleType` where the VIN number has  that ends in '3E1EA1J'.
```SQL
SELECT Make, Model, ElectricVehicleType
FROM EVRegistry
WHERE VIN LIKE '%3E1EA1J'
```
3. Select the `ModelYear`, `make`, `model`, `ElectricVehicleType`, and `range` of the Tesla vehicles or cheverolet vehicles in the registry. Order the result set by Make and Model year in from newest to oldest. 
```SQL
SELECT ModelYear, Make, Model, ElectricVehicleType, ElectricRange
FROM EVRegistry
WHERE Make IN ('TESLA', 'CHEVROLET')
ORDER BY Make, ModelYear DESC
```
4. Using EVCharging, Write a query to find out how many many times those stations were used. Order them by the most used to the least used and limit the output to 5 records. 
```SQL
SELECT StationID, Count(*) as numUses
FROM EVCharging
GROUP BY StationID 
ORDER BY COUNT(*) DESC
LIMIT 5
```
5.  Using EVCharging, For the folks who charged longer than 0.5 hours, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. 
```SQL
SELECT userId, MIN(chargeTimeHrs) as 'minhours', MAX(chargeTimeHrs) as 'maxHours'
FROM EVCharging
WHERE chargeTimeHrs > 0.5 
GROUP BY userId
ORDER BY 2,3
```


# Before moving on with the rest of the questions please set up the new database
1. in SQLlite close any open DB
2. file----> Open Database
3. Choose SavvyCoders_SQL_chargeDB.db from the resource repository from this section in the curriculum
4. Make sure that you have 5 tables: 
    - dimDay 
    - dimFacility
    - dimUser
    - factCharge
    - EVCharging


# 7.3 HW Questions

1. Using EVCharging, Which day of the week has the highest average charging time? Round the answer to 2 decimal points.
```SQL
SELECT Weekday, ROUND(avg(chargeTimeHrs),2) as 'AverageChargingTime'
FROM EVcharging
GROUP BY weekday
ORDER BY AverageChargingTime DESC
LIMIT 1
```

2. Using, EV charging, Find the total power consumed from charging EV's by each User. Return the `userId` and name the calculated column, `totalPower`. Round the answer to 2 deciaml points and list the out put in highest to lowest order. Limit the order to the top 15 users. 
```SQL
SELECT userId, ROUND(SUM(kwhTotal),2) as 'totalPower'
FROM EVcharging
GROUP BY userId
ORDER BY totalPower DESC
LIMIT 15
```

3. Using dimfacility and factCharge, write a query to find out which type of facility (GROUP BY) has the most amount of charging stations. Return `type Facility` and name the calculated column `numStation`. Order the result set from highest to lowest number of charging stations.  
```SQL
select df.typeFacility, count(fc.stationId) as numStation 
from factCharge fc
inner join dimFacility df on fc.facilityID = df.FacilityKey
GROUP BY df.typeFacility
ORDER BY numStation DESC
```

4. In your own words, Briefly explain Primary Keys and Foreign Keys. 
```SQL

--a primary key is a unique key that allows you to access a table or data of that table. 
--a foreign key are other fields that allow you to connect to another table in SQL. it can be a primary key of another table. 

```

5. Using EV Charging, For the folks who charged longer than one hour, show the min and max of the charging time for each user. Your output columns should be `userid`, `minTime`, and `maxTime`. Order this result set by the last two columns respectively. HINT: USE `HAVING`
```SQL
SELECT userId, MIN(chargeTimeHrs) as 'minhours', MAX(chargeTimeHrs) as 'maxHours'
FROM EVCharging
GROUP BY userId
HAVING MIN(chargeTimeHrs) > 1 
ORDER BY 2,3
```
## When done with homework

When all the week #3 homework has been completed, do the following...

- Make sure your homework file is well named
- Add the homework to your Homework folder
- Use  `git add .`, `git commit -m "message"`, and `git push` to upload your homework changes to GitHub in the cloud
- Create a JIRA ticket with your homework repo url, to indicate that your Homework is ready for review
