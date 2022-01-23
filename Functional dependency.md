# Functional dependency
**Functional Dependency** (FD) is a constraint that determines the relation of one attribute to another attribute in a Database Management System (DBMS). Functional Dependency helps to maintain  the quality of data in the database. It plays a vital role to find the difference between good and bad database design. If the relation contains such a functional dependency, the following problems can arise (some of them need to be solved through additional programming efforts - executing a SQL command is not enough):
* **we are wasting space** (we are stating the fact that the salary for the reputation as many times as there are pirates with that reputation)
* **we have update/insertion/deletion anomalies** (see the beginning of the normalization readme).

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
2. If "alpha" is a set of attributes, so we need to determine the closure of a set of attributes under a set of functional dependencies which is {alpha}+ ![image](https://user-images.githubusercontent.com/53339016/150689270-8cfdc594-25ec-4fa7-9d07-1a473786ac80.png). Basically the attributes that are functionally dependent on attributes in alpha(under F).
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
* **Decomposition**: If X → YZ, then X → Y and X → Z.
* **Pseudo-transitivity**:  If X → Y and YZ → W, then XZ → W.

### Problem
* Relational schema R[ABCDEF]
* Set of functional dependencies S = {A -> B, A -> C, CD -> E, CD -> F, D -> E}
We have to show that the following FDs are in {S+}: A -> BC, CD -> EF, AD -> E, AD -> F

#### A->BC (we apply union)
![image](https://user-images.githubusercontent.com/53339016/150689862-0352b223-04d3-4515-809b-f7ffa3010e77.png)

#### CD->EF (we apply union)
![image](https://user-images.githubusercontent.com/53339016/150689886-41183517-add1-4375-851e-1758cfebfd4e.png)

#### AD->E (we apply augmentation and then tranzitivity)
![image](https://user-images.githubusercontent.com/53339016/150689942-38096ba7-bd22-44e8-9853-0da7f829587f.png)

#### AD->F(or we can just apply pseudo-transitivity)
![image](https://user-images.githubusercontent.com/53339016/150689980-a1684fff-859a-4d97-83b7-9864966ffacc.png)

## Step2: The Closure Of alpha under F: alpha+
Compute the closure of a set of attributes under a set of functional dependencies:

![image](https://user-images.githubusercontent.com/53339016/150690224-10f19e53-58fc-4d45-8cea-a3052acdd79b.png)

### Problem
* Relational schema R[ABCDEF]
* Set of functional dependencies S = {A -> B, A -> C, CD -> E, CD -> F, D -> E}
* alpha = {A, D}
We have to compute {alpha+}

![image](https://user-images.githubusercontent.com/53339016/150690436-323c6d77-1394-48f4-91df-53478fe8d4e7.png)

The closure changed. Before it was {A,D} and now it's {A,B,C,D,E,F}, so we have to iterate over all dependencies one more time. So after we iterate, we'll the that the closure hasn't change with respect to the previous iteration, at which moment we can stop.

{aplha+} = {A,B,C,D,E,F} and they are dependent on alpha.

## Step3: Minimal cover
F, G - two sets of functional dependencies; **F and G are equivalent (notation F ≡ G) if {F+} = {G+}**

Let F be a set of functional dependencies; **a minimal cover for F is a set of functional dependencies FM that satisfies the following conditions**:
1. FM ≡ F
2. the right side of every dependency in FM has a single attribute;
3. the left side of every dependency in FM is irreducible (i.e., no attribute can be removed from the determinant of a dependency in FM without changing FM's closure);
4. no dependency f in FM is redundant (no dependency can be discarded without changing FM’s closure).

### Problem
* Relational schema R[ABCD]
* Set of functional dependencies S = {A -> BC, B -> C, A -> B, AB -> C, AC -> D}
* alpha = {A, D}
Compute a minimal cover

* In the first dependency, the dependent is not a single attribute. We decompose it and we will have:
   * S = {A -> B, A -> C, B -> C, A -> B, AB -> C, AC -> D}
* A->B appears twice so we eliminate it:
   * S = {A -> B, A -> C, B -> C, AB -> C, AC -> D} 
* The right side of every dependency in FM has a single attribute. We go to the left side. 
* A->C, by augmentation: AA->AC which can be reduce as A->AC. We also know that AC->D. By transitivity, A->AC and AC->D means A->D
   * S = {A -> B, A -> C, B -> C, AB -> C, A -> D}
* A->C, by augmentation: AB->CB. From decomposition, AB->C. So the dependency is redundant.
   *  S = {A -> B, A -> C, B -> C, A -> D}
* Now the left side of every dependency in FM is irreducible. We have to check now that no dependency f in FM is redundant
* A->B, B->C, so A->C..... A->C is redundant.
   * S = {A -> B, B -> C, A -> D}   

The minimal cover is {A -> B, B -> C, A -> D}  , which means its closure is the same as the original S.
