# Functional dependency
**Functional Dependency** (FD) is a constraint that determines the relation of one attribute to another attribute in a Database Management System (DBMS). Functional Dependency helps to maintain  the quality of data in the database. It plays a vital role to find the difference between good and bad database design. If the relation contains such a functional dependency, the following problems can arise (some of them need to be solved through additional programming efforts - executing a SQL command is not enough):
* **we are wasting space** (we are stating the fact that the salary for the reputation as many times as there are pirates with that reputation)
* **we have update/insertion/deletion anomalies** (see the beginning of this readme).

A functional dependency is denoted by an arrow “→”. The functional dependency of X on Y is represented by X → Y. 
![image](https://user-images.githubusercontent.com/53339016/150660698-4cf1fc2d-d80c-4b8c-b269-0e8b39a4112f.png)

(P.S: {the determinant} -> {the dependent})

**{Reputation} -> {Salary} It's a functional dependence**. (Reputation determines salary). 


# Functional dependency properties
* **Property 1**: If K is a key of a relationship R[A1, A2, ..., An], **then K -> V**, oricare V a subset of {A1, A2, ..., An}
   * ex: {the key} -> {any attribute/set of attributes}
* **Property 2(Reflexivity)**: If Y is a subset of X, then X→Y holds by reflexivity rule
   * ![image](https://user-images.githubusercontent.com/53339016/150660935-c1b3296e-14c0-4719-b7ca-bd19a964a9b9.png) 
   * ex: {LastName, FirstName} -> {LastName}, 
   * {LastName, FirstName} -> {FirstName}, 
   * {LastName, FirstName} -> {LastName, FirstName}
* **Property 3**: If alpha -> beta(alpha determines beta), then for every gama that it's a superset of alpha (so alpha is a subset of gama), gama->beta(gama determines beta as well)
   * ![image](https://user-images.githubusercontent.com/53339016/150661083-42786986-9978-4ca5-9ceb-52a93d0b1a8c.png)
* **Property 4(Transitivity)**: If alpha → beta and beta → gamma are both valid dependencies, then alpha→gamma is also valid by the Transitivity rule.
   * ![image](https://user-images.githubusercontent.com/53339016/150678172-c8d543d9-3eb3-4807-bad5-7b4a12e2be35.png)
* **Property 5(Augmentation)**: If X → Y is a valid dependency, then XZ → YZ is also valid by the augmentation rule
   * ![image](https://user-images.githubusercontent.com/53339016/150678479-0c2b7e11-7b4e-468e-a707-2b59060ba30a.png)

# The closure of a set of dependencies
Given a particular set of functional dependencies, F, find some other set of dependencies, T, that's ideally much smaller than F and that has the property that every functional dependency in F is implied by the functional dependencies in T.

So if DBMS enforces {Friend} -> {Workplace} and {Workplace} -> {AvgSalary}, then automatically we will have {Friend} -> {AvgSalary} enforced.

(blue = F, yellow = T)

![image](https://user-images.githubusercontent.com/53339016/150688959-238233bf-ba0b-4fce-8627-28d29bdf3f6b.png)


**Computing the closure of a set of dependencies**: 
1. If “F” is a functional dependency then closure of functional dependency can be denoted using **“{F}+”**. ![image](https://user-images.githubusercontent.com/53339016/150689084-15b270c9-4953-4641-89a5-0e9b16b6844f.png). So the closure F+ of F is a set consisting of all the dependencies that are implied by F.
2. If "alpha" is a set of attributes, so we need to determine the closure of a set of attributes under a set of functional dependencies which is {alpha}+ ![image](https://user-images.githubusercontent.com/53339016/150689270-8cfdc594-25ec-4fa7-9d07-1a473786ac80.png)
3. We'll compute the **minimal cover** for a set of dependencies. 

## Step1: The Closure Of Functional Dependency: F+
The Closure Of Functional Dependency means **the complete set of all possible attributes that can be functionally derived from given functional dependency using the inference rules known as Armstrong’s Rules.**

Armstrong axioms consist of the following three rules:
* **Reflexivity**: If Y ⊆ X, then X → Y.
* **Augmentation**: If X → Y , then XZ → YZ.
* **Transitivity**: If X → Y and Y → Z, then X → Z.

The rules are both **SOUND** and **COMPLETE**.
* Complete = they compute the entire closure, all the dependencies in the closure
* Sound = you don't get any dependencies that are not in the closure

From these rules we can derive(to simplify the task of computing):
* **Union**: If X → Y and X → Z, then X → YZ.
* **Decomposition**: If X → YZ and X → Y, then X → Z.
* **Pseudo-transitivity**:  If X → Y and YZ → W, then XZ → W.



There are three steps to calculate closure of functional dependency. These are:
Step-1 : Add the attributes which are present on Left Hand Side in the original functional dependency.

Step-2 : Now, add the attributes present on the Right Hand Side of the functional dependency.

Step-3 : With the help of attributes present on Right Hand Side, check the other attributes that can be derived from the other given functional dependencies. Repeat this process until all the possible attributes which can be derived are added in the closure.
