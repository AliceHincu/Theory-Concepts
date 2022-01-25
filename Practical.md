# L13
A musical instruments manufacturer relies on a relational database to support its activities. You are asked to design a part of the database schema and answer some questions the management is interested in using the specified database language. The manufacturer produces instruments of different categories. A category has: name (e.g., string, percussion, woodwind, etc), description, and several subcategories. A subcategory belongs to a category and has a name (e.g., violin, piano, contrabass, etc). An instrument currently in stock belongs to a subcategory and has: serial number, date of manufacture, color, and price. A customer has: name, score, and type (e.g., music academy, orchestra, etc). The company takes orders directly from customers, online or by phone. An order is placed by a customer and has: 2 dates – the date when the order was made and the date when it was honored (null for unfulfilled orders), a field indicating whether it’s been placed online or by phone, and, for each subcategory of instruments in the order, the number of ordered instruments of each color (e.g., an order for 7 red violins, 3 white violins, 2 white pianos, and a yellow contrabass).

![image](https://user-images.githubusercontent.com/53339016/151051008-a2e270dd-ffe6-45d8-a902-6f0fc0fcf774.png)


# Written2019
The website of the Romanian Society of Ornithology is powered by a relational database that contains data about registered birdwatchers, the observations they collect, and natural areas managed by the society. You are asked to design a part of the database schema and answer some questions using the specified database language. A birdwatcher has: id, first name, last name. A bird species has: latin name, common name, short description, estimated population, genus. A species belongs to a genus; a genus belongs to a family and can correspond to several species; a family can be associated with several genera. Both a genus and a family have only a name. E.g., the white stork species (common name) belongs to the Ciconia genus, which in turn belongs to the Ciconiidae family. A natural area has: id, name; it can be host to several species; a species can live in several natural areas. A birdwatcher’s observation has: date, species, and number of observed birds.

### --- 1
![image](https://user-images.githubusercontent.com/53339016/151050654-c816d129-f23e-402d-81a0-c36ba46e8a52.png)

### --- 2
2. Write a query for each of the tasks below, using the specified language:
 
a. For every birdwatcher with at least 10 observations, find his/her: first name, last name, total number of observations, and total number of observations of species of the Aquila genus – in SQL, without views. <br>
b. For every species with an estimated population of less than 1000 birds and that lives in at least one natural area, find its: common name, latin name, and estimated population – in the relational algebra.

### --- 2a
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

### --- 2b
For every species with an estimated population of less than 1000 birds and that lives in at least one natural area, find its: common name, latin name, and estimated population – in the relational algebra.

To help us we have this relations: BirdSpecies-NatASpec-NaturalArea (for the inner joins)

```sql
SELECT B.CommonName, B.LatinName, B.Population
FROM BirdSpecies B 
          INNER JOIN NatASpec ON B.Id = NatASpec.SpecId
          INNER JOIN NaturalArea NA ON NatASpec.NatId -- now it respects the "at least one natural area" 
WHERE B.Population < 1000
```

# Written 2020 ex 1
The website astronomyforbeginners.ro is powered by a relational database that contains data about astronomical objects and phenomena. You are asked to design a part of the database schema and answer some questions using the specified database language. A natural satellite has a name and orbits a planet. A planet has a name and belongs to a planetary system, which has formed around a star and can have several planets. A planet can have several natural satellites. A star has a name, age, and metallicity (real number); it belongs to a galaxy and can have a planetary system. A galaxy has a name, diameter, category (elliptical, spiral, irregular), mass, and belongs to a group of galaxies or to a cluster of galaxies. A galaxy can contain a large number of stars. A group of galaxies has a name, diameter, and mass. A cluster of galaxies has a name, mass, and a type - integer number between 1 and 3 as defined by the Bautz-Morgan classification. Groups and clusters of galaxies can contain large numbers of galaxies. E.g., the Sun is a star in the Milky Way galaxy, which in turn belongs to a galaxy group called Local Group. The Earth is part of the Sun’s planetary system, and has one natural satellite, the Moon. 

### --- 1a
a. Draw a database diagram (tables, constraints) for the above data. The schema must be 3NF. 

![image](https://user-images.githubusercontent.com/53339016/151050809-d434ae9c-1d59-42b0-9205-9035c8945989.png)

### --- 1b
b. Write a SQL statement that creates a table with a primary key and a foreign key.

```sql
CREATE TABLE NaturalSatellite (
   Id INT IDENTITY PRIMARY KEY,
   Name VARCHAR(10),
   PlanetId INT REFERENCES Planet(Id)
)
```

### --- 2a
a. Find the name and age of every star in the Milky Way galaxy with a planetary system that has:
* at least 5 planets OR
* at least one natural satellite (as stated above, such a satellite belongs to a planet in the planetary system).
– in SQL, without views (StarName, StarAge).

To help us with joins: Galaxy - Star - PlanetarySystem - Planet - NaturalSatelitte

**STEP 1: Get the PlanetarySystems that have at least 5 planets.**

```sql
SELECT PS.Id
FROM PlanetarySystem.Id 
       INNER JOIN Planet P ON PS.Id = P.Id
GROUP BY P.Id
HAVING COUNT(DISTINCT P.Id) >= 5
```

**STEP 2: Get the PlanetarySystems that have at least one satelitte.**

```sql
SELECT PS.Id
FROM PlanetarySystem PS
       INNER JOIN Planet P on PS.Id = P.Id
       INNER JOIN NaturalSatelitte ON P.Id = NS.PlanetId
```

**STEP 3: Combine**

```sql
SELECT S.SName, S.Age
FROM PlanetarySystem PS, Star S, Galaxy G
WHERE PS IN ((Step1Query) UNION (Step2Query)) AND S.GalaxyId = G.Id AND S.Id = PS.StarId AND G.Name='Milky Way'
```
### --- 2b
b. Find all galaxies in clusters of type 2 – in the relational algebra (cluster name, galaxy name).

```sql
SELECT CG.Name, G.Name
FROM ClusterOfG CG INNER JOIN Galaxy G ON G.ClusterId = CG.Id
WHERE CG.Type = 2
```
