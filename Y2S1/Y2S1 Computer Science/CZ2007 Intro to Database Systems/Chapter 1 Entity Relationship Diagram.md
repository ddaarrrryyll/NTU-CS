# Relations

<img src="../../_resources/bf61fb0a1b802adc40eb7acf6775f9b7.png" alt="bf61fb0a1b802adc40eb7acf6775f9b7.png" width="422" height="221" class="jop-noMdConv">

- Relation is often referred to as a **table**
- Each row is called a **tuple** or a **record**
- Each column is called an **attribute**
- A database may have a large number of tables/relation

# Designing a DB for an App

1.  Model the requirements of the application
    - What needs to be stored?
    - What are the interactions?
2.  Translate the conceptual model into a set of tables
    - Using **Entity-Relationship Diagrams**
3.  Construct the tables with a DBMS

# ER Diagram

![84b61cc5c70f657a1a0f0a97d69c65dc.png](../../_resources/84b61cc5c70f657a1a0f0a97d69c65dc.png)

- Rectangle = **Entity Set**
    - Collection of real-world objects
- Oval = **Attribute**
    - Property of an Entity Set/Relationship
- Diamond = **Relationship**
    - Connection between two Entity Sets (i.e Persons `Buy` Products, Companies `Make` Products)
    - A relationship can have its own attribute

# Types of Relationships

## 1\. Many-to-Many

![e2aeafe2e14feb61c1ea4b8ad03ca492.png](../../_resources/e2aeafe2e14feb61c1ea4b8ad03ca492.png)

- One `Person` can buy multiple `Products`
- One `Product` can be bought my multiple `Persons`
- Connection Graph helps us to visualise all the relationships between Entity Sets

## 2\. Many-to-One

![c70ae3a71458a494fea90fbd0645d2e7.png](../../_resources/c70ae3a71458a494fea90fbd0645d2e7.png)

- One `Company` can make multiple `Products`
- But one `Product` can only be made by one `Company`
- An arrow is used to depict a **Many-to-One** relationship with the arrow pointing towards the 'One-Side' Entity (`Company`)

## 3\. One-to-One

![4ae3c9191ecb09d2cc87804a06699f95.png](../../_resources/4ae3c9191ecb09d2cc87804a06699f95.png)

- A `City` can be the capital of only one `Country`
- A `Country` can have only one `City` capital

## 4\. Multi-Way

![020455f41f3ccbd5c66ba040d84135eb.png](../../_resources/020455f41f3ccbd5c66ba040d84135eb.png)
(Many-to-One + Multi-way)

- One `<Person, Store>` pair can correspond to one `Product`
- But one `Product` can correspond to many `<Person, Store>` pairs
- i.e. a `Person` only buys one `Product` at one `Store`
    <img src="../../_resources/ebd4321ad661a91663179184d4e71650.png" alt="ebd4321ad661a91663179184d4e71650.png" width="535" height="356" class="jop-noMdConv">
    (Convert to Binary for easier implementation)

# Roles

- Sometimes an entity set may appear more than once in a relationship
    - `Persons`(entity set) $\to$ `Marry`(relationship) $\to$ `Persons`(entity set)
- The role of the person is specified on the edge (arrow) connecting the entity set to the relationship
- Without the roles, it is unclear whether it is Many-to-One from one Entity to another

# Constraints

## 1\. Key Constraints

![cdafc51f16d4681e4b63972a6f4c9dea.png](../../_resources/cdafc51f16d4681e4b63972a6f4c9dea.png)
(`name` is the primary key)

- Underlined attributes uniquely represent each entity in the entity set (e.g. names) (i.e. each person must have a unique name)
- A key in an entity set can contain more than **one** attribute
    ![1df08adcfe520ac0a21b7cd9f8b660fb.png](../../_resources/1df08adcfe520ac0a21b7cd9f8b660fb.png)
    (`<name, category>` is the primary 'key')
- Each product has a unique `<name, category>` combination and there can be products with the same name or category but not both
- Every entity set should(must) have a key

## 2\. Referential Integrity

![bc06a1c5439ec884fe288df3a90d96cb.png](../../_resources/bc06a1c5439ec884fe288df3a90d96cb.png)

- Required when two entity sets must have a relationship with each other (e.g. Every `Product` must be made by a `Company`)
- Cannot be used in a Many-to-Many relationship
- Depicted using a rounded arrow (similar to a Many-to-One relationship)

## 3\. Degree (not required in quiz/exam)

![37bbca8c5ad86ada5b39cad528dfd0a0.png](../../_resources/37bbca8c5ad86ada5b39cad528dfd0a0.png)
(Each `Company` must at least make 1 `Product`)
![6da35eabadb56c2f0bfdb69c0d39cf9f.png](../../_resources/6da35eabadb56c2f0bfdb69c0d39cf9f.png)
(Each `Company` can make at most 1000 `Product`)

# Subclasses

![06211aad0a4e36f588ddfedec639e66a.png](../../_resources/06211aad0a4e36f588ddfedec639e66a.png)

- The connection between a subclass and its superclass is captured by the `isa` (is a) relationship, which is represented using a triangle
- Key of a subclass is inherited from the Key of a superclass
    ![88611b36aad3c85c10316f0293784d66.png](../../_resources/88611b36aad3c85c10316f0293784d66.png)
- An entity set can have multiple subclasses
    - Superclass: Computers
    - Subclass1: Desktop
    - Subclass2: Laptop
- When to use subclasses
    - When a subclass has some attribute that is absent from the superclass
    - When a subclass has its own relationship with some other entity set

# Weak Entity Sets

- Cannot be uniquely identified by their own attributes
- Needs attributes from other entities to identify themselves; always has referential integrity with the supporting entity set
    ![5f39439c641da6672071a278d2a633c6.png](../../_resources/5f39439c641da6672071a278d2a633c6.png)
- Example: Cities with identical names so we cannot use name as key
- Relationship `In` is called the supporting relationship of `Cities`
    - Weak Entity set depicted using double-lined rectangle
    - Supporting relationship depicted using double-lined diamond
- Key of `Cities` is now `(State.name, Cities.name)`

# ER Diagram Design Principles

- From applications to ER Diagrams
    1.  Identify the objects involved in your application
    2.  Model each type of objects as an entity set
    3.  Identify the attributes of each entity set
    4.  Identify the relationships among the entity sets
- **Principles**
    1.  **Be Faithful**
        - Be faithful to the specifications of the application
        - Capture the requirements as much as possible
    2.  **Avoid Redundancy**
        - Avoid repetition of information
            ![c688bd472f5d66e24ac07ad9b606495c.png](../../_resources/c688bd472f5d66e24ac07ad9b606495c.png)
        - Waste of space + possible inconsistency
    3.  **Keep Things Simple**
        ![38de7a62eff120d7c18171fd12231d16.png](../../_resources/38de7a62eff120d7c18171fd12231d16.png)![6c9ca8201a67804ec8b5f1e9943f95cb.png](../../_resources/6c9ca8201a67804ec8b5f1e9943f95cb.png)
    4.  **Don't Over-use Weak Entity Sets**
        ![5dc831f4c4f7dde49255108d26811cd2.png](../../_resources/5dc831f4c4f7dde49255108d26811cd2.png)

# ER diagram $\to$ Relational schema

![e106e4be280c2eb11a5833a7c94ebeed.png](../../_resources/e106e4be280c2eb11a5833a7c94ebeed.png)

- Products(<u>name</u>, price)
- Persons(<u>name</u>, addr)
- Buy(<u>product_name</u>, <u>person_name</u>)
- Terminology
    - A relation schema = name of a table + names of its attribute
    - A database schema = a set of relation schema

## Entity Set $\to$ Relation

- Each entity set is converted into a relation that contains all its attributes
    - Key of the relation = key of the entity set
        ![5c766689b764ce57ceb740b04884e4df.png](../../_resources/5c766689b764ce57ceb740b04884e4df.png)

## Many-to-Many Relationship $\to$ Relation

- Converted into a relation that contains
    - all keys of the participating entity sets
    - the attributes of the relationship (if any)![5bca8ef096ff73d17ef2d6b4c9e016b6.png](../../_resources/5bca8ef096ff73d17ef2d6b4c9e016b6.png)
    - Key of Relation = Keys of the participating entity sets (<u>Bars-ID</u>, <u>Beers-ID</u>) (composite key)
    - If an entity is involved multiple times in a relationship
        - Its key will appear in the corresponding relation multiple times $\therefore$ we re-label key using the roles of the entity (e.g. (<u>husband-ID</u>, <u>wife-ID</u>))

## Weak Entity Set $\to$ Relation

- Each weak entity set is converted to a relation that contains
    - **all** of its attributes
    - the key attributes of the supporting entity set
- Supporting relationship is ignored (i.e. label is the Name of the weak entity set)
    ![e530f32a61dd45f56efd5fd0d419ec8f.png](../../_resources/e530f32a61dd45f56efd5fd0d419ec8f.png)
    ![4b402a9f307125a39903517840f28260.png](../../_resources/4b402a9f307125a39903517840f28260.png)

## Subclass $\to$ Relation

- 3 different ways
    - ER Approach (Each record may appear in **multiple** relations)
    - OO Approach (Each record will appear in **one** relation; potentially many multiple relations since we need to generate a relation for each combination)
    - NULL Approach (One big relation, may have a lot of NULL entries)
- Subclasses can be converted into a relational schema using all 3 approaches

### 1.ER Approach

![13c3c25945f9db2b456dfacafaeb0be0.png](../../_resources/13c3c25945f9db2b456dfacafaeb0be0.png)

- A **Movie** which has genre **Cartoon** and **Sci-Fi** will be placed in all 3 relation tables (Movies, Cartoon and Sci-Fi)

### 2\. OO Approach

![60c8c62bb177bca4dd9963fd323d6db4.png](../../_resources/60c8c62bb177bca4dd9963fd323d6db4.png)

- Subclass will inherit all the attributes from the superclass $\therefore$ a **Cartoon** **Movie** will only be placed in the **Cartoon** relation table

### 3\. NULL Approach

![a128e2c003bdcdd1eaa36a67e139b76e.png](../../_resources/a128e2c003bdcdd1eaa36a67e139b76e.png)
![e57d208f2f78ace76baac012a5a5f576.png](../../_resources/e57d208f2f78ace76baac012a5a5f576.png)

- For a **Movie** that is **not Cartoon** or **not Sci-Fi**, it will be recorded as **NULL** under those attributes in the relation table
- All records will only appear in one relation

### Which is best?

- Depends
    - NULL approach
        - Advantage - Only needs 1 relation
        - Disadvantage - May have many NULL values
    - OO approach
        - Advantage - Good for searching subclass combinations
        - Disadvantage - May have too many tables (need to account for all the combinations)
    - ER approach
        - Middle ground between OO approach and NULL approach

## Many-to-One Relationship $\to$ Relation

![6ad293d62c8184b4723e0ef2cd15167c.png](../../_resources/6ad293d62c8184b4723e0ef2cd15167c.png)

- Intuitive translation:
    - Products(<u>Pname</u>, price)
    - Companies(<u>Cname</u>, country)
    - Make(<u>Pname</u>, <u>Cname</u>)
- Observation: in `Make`, each Pname has only one Cname $\implies$ Cname is already unique $\implies$ we can re express `Make` schema as Make(<u>Pname</u>,Cname)
- Simplification: Merge `Make` and `Products` schema since they share the same key attribute
- Results
    - Products(<u>Pname</u>, price, Cname)
    - Companies(<u>Cname</u>, country)
- **In general, we do not need to create a relation for a many-to-one relationship**
    - Only need to put the key of the "one" side into the relation of the "many" side as an ordinary (not key) attribute

## One-to-One Relationship $\to$ Relation

![778e190170f78586e7da940011b7e08b.png](../../_resources/778e190170f78586e7da940011b7e08b.png)

- Similar to Many-to-One $\to$ Relation
    - No need to create a relation for a one-to-one relationship
    - Only need to put the key of one side into the other
- Translation 1 (Key of `Cities` in `Countries`)
    - Cities (<u>CityID</u>, Cityname)
    - Countries(<u>Countryname</u>, pop, CityID)
    - CityID in `Countries` schema will not be NULL since there is a referential integrity (i.e. every Country will have a City as capital)
- Translation 2 (Key of `Countries` in `Cities`)
    - Cities (<u>CityID</u>, Cityname, Countryname)
    - Countries(<u>Countryname</u>, pop)
    - Countryname in `Cities` schema may be NULL since there is no referential integrity (i.e. not every City will be the capital of a Country)
- **Translation 1 is preferred**