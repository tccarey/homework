```SQL
1.1: 
SELECT Accel FROM evCars

1.2 – 1.3:  

SELECT Accel, RTRIM(Accel, '  sec') 
FROM evCars

1.4: 
UPDATE evCars 
SET Accel = RTRIM(Accel, ' sec')

1.5: 
SELECT Accel FROM evCars

1.6:
ALTER TABLE evCars
RENAME Accel TO AccelSec

2.1:
SELECT TopSpeed, Range, efficiency, FastCharge
FROM evCars
LIMIT 10
SELECT TopSpeed FROM evCars

2.2:
RTRIM(TopSpeed, ‘ km/h’)

2.3:
SELECT TopSpeed, RTRIM(TopSpeed, ‘ km/h’)
FROM evCars

2.4:
UPDATE evCars
SET TopSpeed = RTRIM(TopSpeed, ‘ km/h’)

2.5:
SELECT TopSpeed FROM evCars

2.6 convert to MPH:
SELECT TopSpeed, ROUND(TopSpeed * 0.621371, 1) as TopSpeedMPH
FROM evCars

create update statement: 

UPDATE evCars
SET TopSpeed = ROUND(TopSpeed * 0.621371, 1)
;
SELECT TopSpeed FROM evCars

2.7 rename column:
ALTER TABLE evCars
RENAME TopSpeed TO topSpeedMPH

2.8: 
Select * FROM evCars

3.1: 
SELECT Range FROM evCars

3.2:
RTRIM(Range, ‘ km’)

3.3:
SELECT Range, RTRIM(Range, ' km')
FROM evCars
3.4:
UPDATE evCars
SET Range = RTRIM(Range, ‘ km’)

3.5:
Select Range from evCars

3.6: 
SELECT Range, ROUND(Range * 0.621371, 1) as RangeMiles
FROM evCars; 

UPDATE evCars
SET Range = ROUND(Range * 0.621371, 1)

Select Range from evCars

3.7:
ALTER TABLE evCars
RENAME Range TO rangeMiles

3.8:
SELECT * FROM evCars

4.1: 
SELECT Efficiency, FastCharge
FROM evCars
- 103 rows

4.2:
RTRIM(Efficiency, ‘ Wh/km’)
RTRIM(FastCharge, ‘ km/h’)

4.3:
SELECT Efficiency, RTRIM(Efficiency, ‘ Wh/km’), FastCharge,
RTRIM(FastCharge, ‘ km/h’)
FROM evCars

4.4:
UPDATE evCars
SET Efficiency = RTRIM(Efficiency, 'Wh/km'), 
FastCharge = RTRIM(FastCharge, ' km/h')

4.5: 
SELECT Efficiency, FastCharge 
FROM evCars

4.6: 
SELECT FastCharge, ROUND(FastCharge * 0.621371, 1) as OneHourFastChargeMiles
FROM evCars;

UPDATE evCars
SET FastCharge = ROUND(FastCharge * 0.621371, 1)

SELECT FastCharge
FROM evCars

4.7: 
ALTER TABLE evCars
RENAME FastCharge TO OneHourFastChargeMiles

ALTER TABLE evCars
RENAME Efficiency TO efficiencyWHperKM

4.8: SELECT * FROM evCars

5.1: rapic charge
SELECT RapidCharge, Count(*)
FROM evCars
GROUP BY RapidCharge

5.2: --if car has rapid charge ability
SELECT RapidCharge, 
CASE WHEN RapidCharge = 'Rapid charging possible' THEN 'YES' 
ELSE 'NO'
END as new_rapidcharge
FROM evCars

5.3: 
--if RapidCharge = 'Rapid charging  possible' then change to YES
--if RapidCharge = 'Rapid charging not possible' then NO
SELECT RapidCharge, 
CASE WHEN RapidCharge = 'Rapid charging possible' THEN 'YES' 
ELSE 'NO'
END as new_rapidcharge
FROM evCars

5.4: --update statements
--NO
UPDATE evCars
SET  RapidCharge = 'NO'
WHERE RapidCharge = 'Rapid charging not possible'

--YES
UPDATE evCars
SET  RapidCharge = 'YES'
WHERE RapidCharge = 'Rapid charging possible'

6.1: --Powertrain AWD 41, FWD 37, RWD 25
SELECT PowerTrain, Count(*)
FROM evCars
GROUP BY PowerTrain

6.2: 
-- If the PowerTrain equals _All Wheel Drive_ then I want you to change the value to 'AWD'
-- If the PowerTrain equals _Rear Wheel Drive_ then I want you to change the value to 'RWD'
-- If the PowerTrain equals _Front Wheel Drive_ then I want you to change the value to 'FWD'

SELECT PowerTrain, 
CASE WHEN PowerTrain = 'All Wheel Drive' THEN 'AWD' 
WHEN PowerTrain = 'Front Wheel Drive' THEN 'FWD'
ELSE 'RWD'
END as new_powertrain
FROM evCars

6.3: --update statements
UPDATE evCars
SET  PowerTrain = 'AWD'
WHERE PowerTrain = 'All Wheel Drive'

UPDATE evCars
SET  PowerTrain = 'FWD'
WHERE PowerTrain = 'Front Wheel Drive'

UPDATE evCars
SET  PowerTrain = 'RWD'
WHERE PowerTrain = 'Rear Wheel Drive'

SELECT PowerTrain FROM evCars

7.1: --euro to us dollar
SELECT PriceEuro, ROUND(PriceEuro * 1.09, 2) as PriceUSD
FROM evCars

7.2: --update statement
UPDATE evCars
SET PriceEuro = ROUND(PriceEuro * 1.09, 2)


7.3: --rename column
ALTER TABLE evCars
RENAME PriceEuro TO PriceUSD


'''