# Relational Algebra

- A mathematical way to formulate queries on relations / tables
- Has numeral **operators** for query formulation
    - **Selection, Projection, Union, Intersection**

# Selection $\sigma$ (row-wise operator)

![b82fb40c47c00848555634cf422324d1.png](../../_resources/b82fb40c47c00848555634cf422324d1.png)

- Query: "Find me the student named Alice"
    - $\sigma_{\text{Name = 'Alice'}}\text{Students}$
    - database will look at every single **row** to check for 'Alice' in Name and returns results:
        ![cd9fdd434a1e3dde96942140fcaefa97.png](../../_resources/cd9fdd434a1e3dde96942140fcaefa97.png)
- Conditional Operations (AND / OR) can also be used in selection
- Example 2:
    ![ab64fba9af452aa3cde8c78349416837.png](../../_resources/ab64fba9af452aa3cde8c78349416837.png)

# Projection $\Pi$ (column-wise operator)

![b82fb40c47c00848555634cf422324d1.png](../../_resources/b82fb40c47c00848555634cf422324d1.png)

- Query: "Find the IDs and Names of all students"
    - $\Pi_{\text {ID,Name}} \text{Students}$
    - database will look at every single **column** to get desired columns
        ![78b655e82dc0c53b6b5db40a9aee3f46.png](../../_resources/78b655e82dc0c53b6b5db40a9aee3f46.png)
    - creates a subtable containing the queried columns

# Combination of Operators

![b82fb40c47c00848555634cf422324d1.png](../../_resources/b82fb40c47c00848555634cf422324d1.png)

- Query: "Find the IDs and Names of all students in SCSE"
    - $\Pi_{\text{ID, Name}}(\sigma_{\text{School = 'SCSE'}} \text{Students})$
        ![1045bb94fd812307743b119a210cc174.png](../../_resources/1045bb94fd812307743b119a210cc174.png)
- **Order of operation matters**, if we do projection first, the intermediate subtable will not contain a School attribute

# Union $\cup$ Operator

![31cc57c025246b135bdd30217c0b5c7e.png](../../_resources/31cc57c025246b135bdd30217c0b5c7e.png)

- Query: "Find people who are either students or volunteers"
    - $\text{Students} \cup \text{Volunteer}$
        ![90fecf340b667158757ccb3ee099ddb8.png](../../_resources/90fecf340b667158757ccb3ee099ddb8.png)
    - **duplicates are automatically removed** (same like union of sets in set theory)

## Combining Projection and Union

- Query: "Find the names of people who are either students or volunteers"
    - $\Pi_{\text{Name}}(\text{Students} \cup \text{Volunteer})$
    - ($\Pi_{\text{Name}}\text{Students}) \cup (\Pi_{\text{Name}}\text{Volunteer})$
    - both methods work in this case
        ![15131555a87183092a79b6147dad7aee.png](../../_resources/15131555a87183092a79b6147dad7aee.png)
- **The two sides of a union must have the same schema (i.e. same set of attributes)**
    - if Volunteer Schema does not contain Age, then the union operator will not work
    - we can instead use a projection to get the name of students and perform the union operation on the subtable with the Volunteer Schema

# Intersection $\cap$ Operator

![31cc57c025246b135bdd30217c0b5c7e.png](../../_resources/31cc57c025246b135bdd30217c0b5c7e.png)

- Query: "Find people who are both students and volunteers"
    - $\text{Students} \cap \text{Volunteer}$
        ![05c0b97504062cf0a41e4f2526f8cf4d.png](../../_resources/05c0b97504062cf0a41e4f2526f8cf4d.png)
    - **similar to union operator, identical / duplicates are removed**

## Combining Projection and Intersection

![e49ee8c10e60da4f7b7e1ecf66c6c740.png](../../_resources/e49ee8c10e60da4f7b7e1ecf66c6c740.png)

- Query: "Find people who are both students and volunteers"
    - $(\Pi_{\text{Name}}\text{Students}) \cap \text{Volunteer}$
    - we get an intermediate table which has the same schema with Volunteer and intersect both tables
- **similar to union, two sides of an intersection must have the same schema**

# Difference $-$ Operator

![31cc57c025246b135bdd30217c0b5c7e.png](../../_resources/31cc57c025246b135bdd30217c0b5c7e.png)

- Query: "Find people who are students but not volunteers"
    - $\text{Students} - \text{Volunteer}$
        ![ef4d82c00e1b00bf1e2a3f9c17e623df.png](../../_resources/ef4d82c00e1b00bf1e2a3f9c17e623df.png)
    - **Duplicate rows are automatically removed**
    - returns what the LHS have that the RHS doesn't have
- **Both sides of a difference operation must have the same schema**
    - can use a projection of the main attribute

# Natural Join $\bowtie$ Operator

- Combines two tables into one table
    ![19d97b57155f634efba36f0846562398.png](../../_resources/19d97b57155f634efba36f0846562398.png)
- Query: "Find the NRIC, Name, and Phone of each student"
    - $\text{Students} \bowtie \text{Phones}$
        ![266ccd1a612354074689ff4a9d1473dd.png](../../_resources/266ccd1a612354074689ff4a9d1473dd.png)
    - for every NRIC in Students, we try to find corresponding NRIC in Phones and combine all attributes in Students and Phones (with duplicate attributes automatically removed) (tuples that do not have a match will not be in results)
- **Join is performed based on the common attributes (column) of the two relational schema**
- **Each common attribute (column) appears only once in the result**
- Example 2:
    ![58146cdf9bb6400b9c9620b7631588fc.png](../../_resources/58146cdf9bb6400b9c9620b7631588fc.png)![387452c60994d5b4919536ebf78279cc.png](../../_resources/387452c60994d5b4919536ebf78279cc.png)
- Example 3:
    ![ed064e507c67c62d7bd05f5febc2468c.png](../../_resources/ed064e507c67c62d7bd05f5febc2468c.png)

# Theta Join $\bowtie_{condition}$ Operator

![ed2f6a3f852146152e059eb5b133bf42.png](../../_resources/ed2f6a3f852146152e059eb5b133bf42.png)
(note there are no common attributes)

- Query: "For those students who have made donations, find their names, schools, and amounts of their donations"
    - $\text{Students} \bowtie_\text{SName=Name}\text{Donations}$
        ![2100111e376ea5e6c0fd503f588b5411.png](../../_resources/2100111e376ea5e6c0fd503f588b5411.png)
- **'Duplicate' attributes (columns) will not be removed from the results unlike in Natural Join**
    - Project attributes that we need from the results table
- Join condition can also be an inequality:
    ![b332118f5dadb47509c833337693038b.png](../../_resources/b332118f5dadb47509c833337693038b.png)
- Query: "Find students who scored higher in Quiz 2 than Quiz 1"
    - $\text{Quiz1}\bowtie_{\text{Quiz1.Name = Quiz2.Name AND Quiz1.Score < Quiz2.Score}}\text{Quiz2}$
        ![162f0190c562b657d429c5d1de9e0859.png](../../_resources/162f0190c562b657d429c5d1de9e0859.png)
        (note that duplicated attributes are not removed)
    - **We need to prefix table name (Quiz1.Score / Quiz2. Name) to eliminate ambiguity whenever there are ambiguous attribute names (Score and Name in this case)**

# Cartesian Product $\times$ Operator

- Theta join without a condition
    ![d7849db0189f426811e2e65be8dd122d.png](../../_resources/d7849db0189f426811e2e65be8dd122d.png)
- Query: "Create a table that provides all possible student-course combinations"
    - $\text{Students} \times \text{Course}$
        ![6f1d7ac44d42d8118cc95f2e89d82494.png](../../_resources/6f1d7ac44d42d8118cc95f2e89d82494.png)
    - each record in the first table will be merged with all the records in the second table

# Assignment $:=$ Operator

![83fed2aac5e22372ad3b61e2e6746835.png](../../_resources/83fed2aac5e22372ad3b61e2e6746835.png)

- Query / Concept: "Make another copy of the table and give it a new name"
    - $\text{Evaluation1} := \text{Quiz1}$
    - $\text{Over85} := \sigma_\text{Score > 85}\text{Quiz1}$
- **all attributes are copied**
- useful for breaking down steps
    - ($\Pi_{\text{Name}}\text{Students}) \cup (\Pi_{\text{Name}}\text{Volunteer})\newline =\text{R1} \cup \text{R2}$
    - $\text{R1} := \Pi_{\text{Name}}\text{Students}$
    - $\text{R2} := \Pi_{\text{Name}}\text{Volunteer}$

# Rename $\rho$ Operator

![3c8506027239c4a154e60ca89d459566.png](../../_resources/3c8506027239c4a154e60ca89d459566.png)

- Query / Concept: "Change the name of table"
    - $\rho_\text{Evaluation1}\text{Quiz1} \to$ $\text{Quiz1}$ has name changed to $\text {Evaulation1}$
    - $\rho_\text{Eval1(SName, QScore)}\text{Quiz1} \to$ change $\text{Quiz1}$'s name as well as attribute names

![c6dea01429042707e014c08afa649b85.png](../../_resources/c6dea01429042707e014c08afa649b85.png)

![b1fc312aed6d6b89c3470cfed0aee921.png](../../_resources/b1fc312aed6d6b89c3470cfed0aee921.png)

- **$<>$ means not equals to**

# Duplicate Elimination $\delta$ Operator

![f41adeed8c7ad12bf8b1a3406fec11c1.png](../../_resources/f41adeed8c7ad12bf8b1a3406fec11c1.png)

- Query: Find the list of products sold on 2017.01.01
    - $\text{R1} := \Pi_\text{Product}(\sigma_\text{Date='2017.01.01'}\text{Purchase})$
    - $\text{R2} := \delta(\text{R1})$

# Extended Projection $\Pi$ Operator

- **similar to ordinary projection but allows the creation of new attributes via arithmetic**
    ![385520235c8d338b7401fe615b3ef6fe.png](../../_resources/385520235c8d338b7401fe615b3ef6fe.png)
- Query: "For each student, find his/her total score in Quiz 1 and 2"
    - $\Pi_{\text{Name, Quiz1+Quiz2} \to \text{Total}}\text{Scores}$
    - $\to$ gives the arithmetic performed with the RHS giving an attribute name to the result

# Grouping and Aggregation $\gamma$ Operator

![9ed5cb07a47996a2a3a6a5bfc047e362.png](../../_resources/9ed5cb07a47996a2a3a6a5bfc047e362.png)
**Aggregation only**

- Query: "Find the highest score in Quiz1"
    - $\gamma_{\text{MAX(Score)}\to\text{MaxScore}}\text{Quiz1}$
    - Attribute name on RHS of $\to$ can be arbitrary
- Aggregate Functions:
    - MAX(...) - returns maximum entry in column
    - MIN(...) - returns minimum entry in column
    - AVG(...) - returns average of column
    - SUM(...) - returns total sum of column
    - COUNT(...) - returns number of entries (tuples)
- **Aggregate Functions can only be used with the aggregation operation $\gamma$**
    ![2c146e71d375a0eb43a4bc12cc777268.png](../../_resources/2c146e71d375a0eb43a4bc12cc777268.png)

![86c1ba47891485d9efbab25274152876.png](../../_resources/86c1ba47891485d9efbab25274152876.png)
**Aggregation + Grouping**

- Query: "Find the average GPA in each school"
    - $\gamma_{\text{School, AVG(GPA)}\to\text{AvgGPA}}\text{Quiz1}$
    - Grouping of records occur before the aggregate functions (can have more than 1 grouping operations)
        ![1398a771e01ee97d22910305d4b0637e.png](../../_resources/1398a771e01ee97d22910305d4b0637e.png)

# Division $\div$ Operator

![78be89bdb4272e8544801b9ad284cdbc.png](../../_resources/78be89bdb4272e8544801b9ad284cdbc.png)

- Query: "Find each person that owns **all** Apple products"
    - $\text{Owns} \div \text{AppleP}$
    - $R_1(A,B) \div R_2(B)$ returns a table that contains only attribute A $\therefore$ above query returns $\text{Name}$
        - The table will only contain each A value in $R_1$ that is associated with **every** B value in $R_2$
        - **A values can contain multiple attributes but this also means values of each attribute in the combination must be the same**
            - e.g. for a table $R_1(A, B)$ where $A_i = \{X_i, Y_i, B_a\} \text{ and }\newline A_j = \{X_i, Y_j, B_b\}, A = \{X_i, Y_i\}$ will not be in $\text{Results}$

![44c82ea2426a305a62950f34bee5f35d.png](../../_resources/44c82ea2426a305a62950f34bee5f35d.png)

- Query: "Find each person that owns all Apple products"
    - $\text{Owns}$ does not contain $\text{Price}_\text{AppleP}$ so we have to do a projection of $\text{AppleP}$
    - $\text{Owns}\div (\Pi_\text{Produdct}\text{AppleP})$

# Left Outerjoin $\mathring\bowtie_{L\text{ condition}}$ Operator

![1d0ab84c4ac344013debedffa915faa8.png](../../_resources/1d0ab84c4ac344013debedffa915faa8.png)

- Query: "For each student, find the amount of his/her donation"
    - $\text{Students }\mathring\bowtie_L\text{ Donations}$
    - All entries in the LHS of the operator are retained in $\text{Results}$
    - in natural join, all none common attributes will be removed from $\text{Results}$

![ffac155c7ac2e93283cebead21508cad.png](../../_resources/ffac155c7ac2e93283cebead21508cad.png)(note that Name attribute of Students have changed)

- we use the same method we did in theta join where we compare the attribute names directly
    - $\text{Students }\mathring\bowtie_{L\text{ Sname = Name}}\text{ Donations}$
    - All attributes (SName, Name, School, Amount) will be retained
        - since Alice and Bob do not have Name in Donations, their Name attribute will be set to NULL in Results

# Right Outerjoin $\mathring\bowtie_{R\text{ condition}}$ Operator

![78890fb2d44ee6bbe186c142b6157fce.png](../../_resources/78890fb2d44ee6bbe186c142b6157fce.png)

- Query: "For each donor, find the school he/she is in"
    - $\text{Students }\mathring\bowtie_R\text{ Donations}$
    - All entries in the RHS of the operator are retained in the results
- we can add conditions to follow when attribute names are different, similar to the example in Left Outerjoin

# Full Outerjoin $\mathring\bowtie_{\text{ condition}}$ Operator

- Combination of Left and Right Outerjoin
    ![f076d7475a99af0758764a281d68aa1f.png](../../_resources/f076d7475a99af0758764a281d68aa1f.png)
- Query: "Get the entries of everyone in the Students Table and the Donations Table"
    - $\text{Students }\mathring\bowtie\text{ Donations}$
    - All entries in BOTH tables will be retained in the results
- We can add conditions to follow similar to the example in Left Outerjoin

## Example

![beede9a62877a52b082795c394e1c29f.png](../../_resources/beede9a62877a52b082795c394e1c29f.png)

### Method 1: Using natural join, naive and incorrect method

![fda84a98f0a47d34a8b76726950ddc5d.png](../../_resources/fda84a98f0a47d34a8b76726950ddc5d.png)

1.  Select Male records from Stars and assign to R1
2.  Do a natural join between CastIn and R1

- **Meg entry is lost**

### Method 2: Using Left Outerjoin, incorrect aggregation

![5442d9f0fda12c68cb279ea500ccd4ad.png](../../_resources/5442d9f0fda12c68cb279ea500ccd4ad.png)
<img src="../../_resources/3582fa45b631509ec1e34a5bc88edf51.png" alt="3582fa45b631509ec1e34a5bc88edf51.png" width="420" height="84" class="jop-noMdConv">

1.  Select Male records from Stars and assign to R1
2.  Do a left outerjoin to bring attributes from CastIn and corresponding attributes from R1 together and assign to R2
3.  Create a new table R3 with Attributes Movie, MaleStars (with count of gender assigned to it)

- **NULL is counted as 1 count**

### Method 3: Using Left Outerjoin, correct aggregation

![53a486153f6591466b1ce5eb37f31a26.png](../../_resources/53a486153f6591466b1ce5eb37f31a26.png)
<img src="../../_resources/eb97beaea96d9ba2b8dc81e536107d68.png" alt="eb97beaea96d9ba2b8dc81e536107d68.png" width="378" height="110" class="jop-noMdConv">

1.  Select Male records from Stars and assign to R1
2.  Create new table R2 with Attributes grouped by Name, Male (Count of different gender entries) from R1
3.  Do a left outerjoin to bring attributes from CastIn and corresponding attributes from R1 together and assign to R3
4.  Create new table R4 with Attributes grouped by Movie, MaleStars (Sum of Male entries in R3)