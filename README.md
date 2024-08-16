**Functional Dependency Summary:**

1. **Definition:**
   - **Functional Dependency (FD):** For a relation R and attributes A B in R, B is functionally dependent on A (denoted A → B) if each value of A is associated with exactly one value in B in R.

2. **Examples:**

<div style="text-align: center;">

<table style="margin-left: auto; margin-right: auto;">
  <tr>
    <th>Functional Dependency Holds (✅)</th>
    <th>Functional Dependency Doesn't Hold (❌)</th>
  </tr>
  <tr>
    <td>
      <table style="margin-left: auto; margin-right: auto;">
        <tr>
          <th>A</th>
          <th>B</th>
        </tr>
        <tr>
          <td>A1</td>
          <td>B1</td>
        </tr>
        <tr>
          <td>A2</td>
          <td>B2</td>
        </tr>
        <tr>
          <td>A1</td>
          <td>B1</td>
        </tr>
      </table>
    </td>
    <td>
      <table style="margin-left: auto; margin-right: auto;">
        <tr>
          <th>A</th>
          <th>B</th>
        </tr>
        <tr>
          <td>A1</td>
          <td>B1</td>
        </tr>
        <tr>
          <td>A2</td>
          <td>B2</td>
        </tr>
        <tr>
          <td>A1</td>
          <td>B2</td>
        </tr>
      </table>
      <p>Because A1 is associated with more than one value in B</p>
    </td>
  </tr>
</table>

</div>

3. **Functional Dependency with Keys:**
   - If α is a key, then α → β always holds for any attribute β.

4. **Closure of an Attribute:**
   - Given relation R(A, B, C, D) and functional dependencies : {A → B, A → D, B → C}
   
   **Attribute Closures:**
   - $A^+$ = {A, B, C, D}
   - $B^+$ = {B, C}
   - $C^+$ = {C}
   - $D^+$ = {D}

5. **Trivial Functional Dependency:**
   - A functional dependency A → A is always satisfied (trivial).

6. **Armstrong’s Axioms:**
   - **Reflexivity Rule:** A → B holds if B ⊆ A.
   - **Augmentation Rule:** If A → B, then αA → αB holds for any set α.
   - **Transitivity Rule:** If A → B and C → D, then A → D holds.

7. **Additional Rules:**
   - **Union Rule:** If A → B and A → C, then A → BC holds.
   - **Decomposition Rule:** If A → BC, then A → B and A → C hold.

8. **Closure of a Set of Functional Dependencies:**
   - To find all possible functional dependencies from a given set, compute the closure of the attribute sets using Armstrong’s axioms and additional rules.
  

**Normalization**

- **Definition:** Normalization is the process of minimizing redundancy in a relation or set of relations.
- **Purpose:** Redundancy in a relation may cause insertion, deletion, and update anomalies.
- **Process:** It involves grouping attributes into well-structured relations that contain minimal redundancy.
- **Focus:** It emphasizes the characteristics of specific entities.

**Essence of Normalization:** One relation should have one theme.

---

**Normalization Forms:**

<table border="1">
  <thead>
    <tr>
      <th>Normalization Process</th>
      <th>Process of Transforming</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Unnormalized Relation</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>
        <ul style="list-style-type:none;">
          <li>Removing repeating groups (multi-valued attributes)</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>First Normal Form (1NF)</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>
        <ul style="list-style-type:none;">
          <li>Removing partial dependency.</li>
          <li>Partial dependency occurs when a non-key (also known as non-prime) attribute is functionally dependent on only a part of any Composite key (also known as combination of prime attributes), rather than on the entire key.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Second Normal Form (2NF)</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>
        <ul style="list-style-type:none;">
          <li>Removing transitive dependency.</li>
          <li>Make sure that no non-prime attribute is transitively dependent on the key.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Third Normal Form (3NF)</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>
        <ul style="list-style-type:none;">
          <li>Removing overlapping candidate keys.</li>
          <li>For every functional dependency A -> B, A should be a key in the relation.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Boyce-Codd Normal Form (BCNF)</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>
        <ul style="list-style-type:none;">
          <li>Removing multi-valued dependency.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Fourth Normal Form (4NF)</td>
      <td></td>
    </tr>
    <tr>
      <td></td>
      <td>
        <ul style="list-style-type:none;">
          <li>Removing non-implied dependency.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Fifth Normal Form (5NF)</td>
      <td></td>
    </tr>
  </tbody>
</table>

---
**Types of Decomposition:**

- **Lossless Decomposition:**
  - Ensures that the original relation can be perfectly reconstructed from the decomposed relations.
  - R = R1⋈R2⋈R3⋈...Rn
- **Lossy Decomposition:**
  - May not preserve all information from the original relation.
  - R ≠ R1⋈R2⋈R3⋈...Rn

**Note:** Up to 3NF, all decompositions are lossless. After that, decomposition may be either lossy or lossless.

**Dependency Preserving Decomposition:**

The decomposition is dependency preserving if:

(F1 ∪ F2 ∪ ... ∪ Fn $)^+$ = $F^+$

where:
- F1, F2, ..., Fn  are the functional dependencies derived from the decomposed relations R1, R2, ..., Rn .
- $F^+$ is the closure of the original functional dependencies \( F \).
