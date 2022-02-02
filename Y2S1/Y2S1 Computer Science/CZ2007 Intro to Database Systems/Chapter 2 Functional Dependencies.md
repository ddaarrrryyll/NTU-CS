# Data Anomalies

- Anomalies occur in tables due to
    - bad combination of attributes
    - correlations among attributes
    - functional dependencies among attributes
- **Redundancies**
    - Data appearing more than once
- **Update anomalies**
    - Updating one entry without changing the other $\to$ corrupted table
- **Deletion anomalies**
    - Primary key attributes cannot be NULL
- **Insertion anomalies**
    - Inserting entries with NULL for some primary key values will lead to problems
- <span style="background-color: #9ee7e2;">if a relational schema is not properly formulated, certain attributes may have duplicate values in the table</span>

## 1\. Normalization (Decomposing)

**Before Decomposing**
![36928255b6265e62140db0acef8ec541.png](../../_resources/36928255b6265e62140db0acef8ec541.png)
**After Decomposing**
<img src="../../_resources/f7aee89710997dbcfd2ee4952e034040.png" alt="f7aee89710997dbcfd2ee4952e034040.png" width="432" height="127" class="jop-noMdConv">
(NRIC and PhoneNumber are Primary Keys)

- Alice's address is no longer duplicated (no more redundancies)
- Address of Alice can be updated without changing changing another row (no more update anomalies)
- We can freely delete Bob's phone number without any problems (no more deletion anomalies)
- Inserting entries without a phone can be done now (no more insertion anomalies)

# Functional Dependencies

## Intuition

![36928255b6265e62140db0acef8ec541.png](../../_resources/36928255b6265e62140db0acef8ec541.png)

- Table is **bad** because it has a lot of anomalies
- <span style="background-color: #9ee7e2;">Table contains a bad combination of attributes</span>
- To know if a combination of attributes is bad, <span style="background-color: #9ee7e2;">we need to check the correlations among those attributes</span> **(Functional Dependencies)**
- Example:
    - Given an NRIC we can determine a person's name, but given a person's name, we cannot determine their NRIC
    - Functional dependency - NRIC $\to$ Name, but **not** Name $\to$ NRIC

## Definition

- Given attributes $A_1, A_2, ...\space A_m$ and $B_1, B_2, ...\space B_n$
    - $A_1, A_2,...\space A_m \to B_1, B_2, ...\space B_n$
    - i.e. There do not exist two records that have the same values on $A_1, A_2, ...\space A_m$ but different values on $B_1, B_2, ...\space B_n$
    - i.e. For some $A_i$ and $A_j$, if $A_i \to B_x$ and $A_j \to B_x$, $A_i = A_j$

## How to determine Functional Dependencies

- Common sense, Application's requirements

# Armstrong's axioms

## Axiom of Reflexivity

- A set of attributes $\to$ a subset of the attributes
    <img src="../../_resources/7227774480384a65b75cb0ffe5caac3b.png" alt="7227774480384a65b75cb0ffe5caac3b.png" width="332" height="176" class="jop-noMdConv">

## Axiom of Augmentation

- Given $A \to B$, we will always have $AC \to BC$, for any $C$
    <img src="../../_resources/b02891e9492968a5f0eedf1479106a9a.png" alt="b02891e9492968a5f0eedf1479106a9a.png" width="414" height="133" class="jop-noMdConv">

## Axiom of Transitivity

- Given $A \to B$ and $B \to C$, we can deduce $A \to C$ (transitive nature)
    <img src="../../_resources/fc7d164f605f14b31e69f2262a1d0492.png" alt="fc7d164f605f14b31e69f2262a1d0492.png" width="320" height="74" class="jop-noMdConv">

## Reasoning with Functional Dependencies

- Given $A \to B$ and $BC \to D$ show $AC \to D$
    - $A \to B \implies AC \to BC$ (Augmentation)
    - $AC \to BC$ and $BC \to D \implies AC \to D$ (Transitivity)
- Given $A \to B$ and $D \to C$ show $AD \to BC$
    - $A \to B \implies AD \to BD$ (Augmentation)
    - $BD \to B$ (Reflexivity) $\therefore AD \to B$ (Transitivity)
    - $D \to C \implies AD \to AC$ (Augmentation)
    - $AC \to C$ (Reflexivity) $\therefore AD \to C$ (Transitivity)
    - $AD$ determines $B$ and $C$, i.e. $AD \to BC$
- Given $A \to C$, $AC \to D$, $AD \to B$, show $A \to B$
    - Given $A \to C$ and $A \to A$, we get $A \to AC$ (Augmentation)
    - $A \to D$ is trivial (Transitivity)
    - Similarly, $A \to AD$ (Augmentation)
    - $A \to B$ is trivial (Transitivity)
- **Intuitive Solution**
    ![8f98897650520131bca61482b9d889ce.png](../../_resources/8f98897650520131bca61482b9d889ce.png)
    (If there is a path from $B$ to $C$, then we can show that $B \to C$)
    (the final set is known as the **closure** of $B$)

# Closure

- let $S = \{A_1, A_2, ..., A_n\}$ be a set $S$ for attributes
    - Closure of $S$ i.e. $\{A_1, A_2,..., A_n\}^+$is the set of attributes that are reachable from $A_1, A_2, ..., A_n$
    - e.g. given $A\to B, B\to C, C\to, D$
        - $\{A\}^+ = \{A, B, C, D\}$
        - $\{B\}^+ = \{B, C, D\}$
        - $\{C\}^+ = \{C, D\}$
        - $\{D\}^+ = \{D\}$
            <img src="../../_resources/a9b9c8a4cf3bc3c5fe1bb42d2f1fb1d0.png" alt="a9b9c8a4cf3bc3c5fe1bb42d2f1fb1d0.png" width="576" height="309" class="jop-noMdConv">
            (note that $C \notin \{B\}^+$ in the first example and position of $F$ does not matter for the last example)
- To prove that $X \to Y$ holds, we only need to show that $Y \in \{X\}^+$
    <img src="../../_resources/d15daa1fdea94d014ce7c52f448553aa.png" alt="d15daa1fdea94d014ce7c52f448553aa.png" width="342" height="114" class="jop-noMdConv">
- Similarly, to prove that $X \to Y$ does not hold, we only need to show that $Y \notin \{X\}^+$

# Keys

## Superkeys

- A set of attributes in a table that decides all other attributes
    <img src="../../_resources/ffc10c167fa2b0c5e8669009102a9366.png" alt="ffc10c167fa2b0c5e8669009102a9366.png" width="427" height="80" class="jop-noMdConv">
- {NRIC} is a superkey
    - NRIC $\to$ Name, Postal, Address and {NRIC, Name} $\to$ Postal, Address
        - {NRIC, Name} is also a superkey

## Keys

- **A Key is a superkey that is minimal** (removing any attribute from the superkey causes it to lose its status as a superkey)
- **A minimal set of attributes that decides all other attributes**
    - {NRIC, Name} is a superkey but it is not minimal
    - NRIC is a **key** but {NRIC, Name} is **not a key**
    - all keys are superkeys but not all superkeys are keys
- Keys in a table $\neq$ Keys in an entity set

## Candidate keys

<img src="../../_resources/73d816a426d5bcefdd9bceb3e3f9dd16.png" alt="73d816a426d5bcefdd9bceb3e3f9dd16.png" width="430" height="5" class="jop-noMdConv">

(NRIC, StudentID are keys in this table)

- Each key in a table with multiple keys is referred to as a candidate key
    - both NRIC and StudentID are candidate keys

## Primary / Secondary keys

- For a table with multiple keys (candidate keys), we **choose one of them as the primary key** and the others are referred to as **secondary keys**

# Finding keys

- We need to find the keys of the table to check whether a table is 'good'
    <img src="../../_resources/4c76986b39d317b5e764fda204139606.png" alt="4c76986b39d317b5e764fda204139606.png" width="284" height="210" class="jop-noMdConv">

## Algorithm

1.  Check all possible combinations of attributes in the table
2.  Compute closure for each combination
3.  If a closure contains all attributes, then the combination is a superkey and **might be a key**
    - always check smaller combinations first

- <span style="background-color: #9ee7e2;">if an attribute does not appear in the RHS of any functional dependencies, then it must be in every key</span>

# Normal forms

![55b3cf2033cd4eb1cf2b07caeab56492.png](../../_resources/55b3cf2033cd4eb1cf2b07caeab56492.png)

- A method to detect 'bad tables' like this (i.e. conditions for a 'good' table)

## 4 normal forms in this course

1.  First normal form \[least strict\]
2.  Second normal form
3.  Third normal form (3NF)
4.  Boyce-Codd normal form (BCNF) \[strictest\]