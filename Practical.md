# L13
A musical instruments manufacturer relies on a relational database to support its activities. You are asked to design a part of the database schema and answer some questions the management is interested in using the specified database language. The manufacturer produces instruments of different categories. A category has: name (e.g., string, percussion, woodwind, etc), description, and several subcategories. A subcategory belongs to a category and has a name (e.g., violin, piano, contrabass, etc). An instrument currently in stock belongs to a subcategory and has: serial number, date of manufacture, color, and price. A customer has: name, score, and type (e.g., music academy, orchestra, etc). The company takes orders directly from customers, online or by phone. An order is placed by a customer and has: 2 dates – the date when the order was made and the date when it was honored (null for unfulfilled orders), a field indicating whether it’s been placed online or by phone, and, for each subcategory of instruments in the order, the number of ordered instruments of each color (e.g., an order for 7 red violins, 3 white violins, 2 white pianos, and a yellow contrabass).

# Written2019
2. Write a query for each of the tasks below, using the specified language:
 
a. For every birdwatcher with at least 10 observations, find his/her: first name, last name, total number of observations, and total number of observations of species of the Aquila genus – in SQL, without views. <br>
b. For every species with an estimated population of less than 1000 birds and that lives in at least one natural area, find its: common name, latin name, and estimated population – in the relational algebra.

### 2a
For every birdwatcher with at least 10 observations, find his/her: first name, last name, total number of observations, and total number of observations of species of the Aquila genus – in SQL, without views.

**First Step is to get the number of observations of species of the Aquila genus of a birdwatcher.** To help us we have this relations: Genus - BirdSpecies - Observation - Birdwatcher (for the inner joins)

```sql
SELECT B.Id, COUNT(*) as AquilaCount
FROM Birdwatcher B 
        INNER JOIN Observations O on B.Id = O.BirdwatcherId 
        INNER JOIN BirdSpecies BS on BS.Id = O.SpeciesId
        INNER JOIN Genus G on G.Id = BS.GenusId -- we finally reached genus from birdwatcher
WHERE G.Name = 'Aquila'
GROUP BY B.Id
```

**Second Step is to get the number of observations**.  To help us we have this relations: Observation - Birdwatcher (for the inner joins)

```sql
SELECT B.Id, B.FName, B.LName -- we need the names for the final query
FROM Birdwatcher B 
        INNER JOIN Observations O on B.Id = O.BirdwatcherId 
GROUP BY B.Id, B.FName, B.LName
HAVING COUNT(DISTINCT B.Id) >= 10 --- if we do it here it will also apply generally since we have to inner join the ids.
```

**Third Step is to combine. We put in the condition the B.Id because they need to respect both conditions.**

```sql
SELECT T1.Id, T1.FName, T1.Lname, T2.AquilaCount
FROM (QueryStep1) T1 INNER JOIN (QueryStep2) T2 ON T1.Id = T2.Id
```

### 2b
For every species with an estimated population of less than 1000 birds and that lives in at least one natural area, find its: common name, latin name, and estimated population – in the relational algebra.

To help us we have this relations: BirdSpecies-NatASpec-NaturalArea (for the inner joins)

```sql
SELECT B.CommonName, B.LatinName, B.Population
FROM BirdSpecies B 
          INNER JOIN NatASpec ON B.Id = NatASpec.SpecId
          INNER JOIN NaturalArea NA ON NatASpec.NatId -- now it respects the "at least one natural area" 
WHERE B.Population < 1000
```
