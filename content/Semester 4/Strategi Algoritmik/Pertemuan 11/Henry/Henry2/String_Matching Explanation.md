> [!note] Material Source
> IN244-Strategi Algoritmik > P12-String Matching > Slides teori
> <small>*Powerpoint slides will not be included here to prevent redundancy*</small>

> [!warning] Warning! This file can not be exported effectively by default. 
> 
> If still needed to be exported:  
> * Lower the downscale percent is required for the contents to be universally exists
> * ~~Plugin Fast Text Color is used [obsidian://show-plugin?id=fast-text-color] There will be no color text (Obsidian community plugin) to guide the step-by-step algorithm.~~
> 	* Had been fixed by using another plugin
> 	obsidian://show-plugin?id=colored-text

# Boyer-Moore Algorithm

> [!quote] The Boyer-Moore Algorithm: Core Heuristics and Case Analysis
> 
> The Boyer-Moore algorithm relies fundamentally on two core techniques to optimize pattern matching. The first is the looking-glass technique, which dictates searching for the pattern P within the text T by moving backward, starting the character comparison from the last character in P. The second is the character-jump technique, which triggers a calculated shift whenever a mismatch occurs at the condition where T[i] equals P[j] evaluates to false. Depending on the nature of the mismatched character in the text, the algorithm determines its next move based on three distinct possible cases.

### The Three Shift Cases in Boyer-Moore, in-depth theoretical explanation

#### Case 1: The Mismatched Character Exists in the Pattern

![[Pasted image 20260531035228.png]]

> [!note] Please note that the string tracking starts from the last

**Rule:** If the pattern P contains the mismatched character from the text (denoted as x), the pattern P is shifted to the right. The structural goal of this shift is to perfectly align the occurrence of the character x within the pattern P with the mismatched character T[i] located in the text.

> **Example:** If the text T is currently evaluating "xa" and the pattern P is "xcba". First iteration, T[i] = P[j] is correct because both is "a". Then a mismatch occurs at the character 'x'. The algorithm immediately shifts the indices i and j to the right so that the 'x' in "xcba" aligns directly with the 'x' in the text.


#### Case 2: The Mismatched Character Exists, but Case 1 is Impossible

![[Pasted image 20260531051940.png]]

 **Rule:** If the pattern P contains the character x, but executing the alignment shift described in Case 1 is not possible (because it would result in moving the pattern backward), the algorithm simply shifts the pattern P to the right by exactly one character, aligning it at T[i+1].

>   **Example:** Consider a text T containing "xax" and a pattern P of "cwax". A mismatch happens, and while 'x' is present in the pattern, it is positioned after the current index position j. Therefore, the algorithm shifts the pattern one position to the right to generate a new j position and resume comparison.


#### Case 3: The Mismatched Character is NOT in the Pattern

![[Pasted image 20260531052003.png]]

**Rule:** If neither Case 1 nor Case 2 applies because the mismatched character x does not exist within the pattern P at all, the pattern P is shifted significantly to place P[0] in alignment with T[i+1].
    
>   **Example:** If the text T evaluates "xa" against a pattern P of "dcba", there is no 'x' present in the pattern. Consequently, the algorithm slides the pattern entirely, shifting the i and j indices completely past the mismatched 'x' to establish a new j position.
    

### Visualizing the Last Occurrence Function

To execute these character jumps efficiently during the search process, the Boyer-Moore algorithm performs preprocessing on both the pattern P and the target alphabet A to construct a last occurrence function, represented as L().

- The L() function maps every letter found in the alphabet A into an integer value.
    
- Specifically, L(x) is defined as the largest index i such that P[i] equals x, or it returns -1 if the character x does not appear in the pattern P at all.
    
- In this context, x represents any letter within the defined alphabet A.
    

Based on an example where the pattern P is "abacab" and the alphabet A consists of {a, b, c, d}, here is the step-by-step visualization of the mapped L() table:

|**Character (x)**|**a**|**b**|**c**|**d**|
|---|---|---|---|---|
|**Last Occurrence $L(x)$**|4|5|3|-1|

Note: The values in the table are derived directly from the largest 0-based index position of each respective character within the string "abacab".

___

> [!example] 
> Boyer Moore Algorithm
> - String T (Text):
> 	"a pattern matching algo==rithm=="
> - String P (Searching):
> 	"rithm"


> [!warning] Core Concept: Heuristic Search
> The Boyer-Moore algorithm searches for a pattern **P** within a text **T** by moving backward through the pattern (Looking-Glass Technique). When a mismatch occurs, it calculates a strategic leap to bypass multiple invalid alignments simultaneously (Character-Jump Technique).

**T** (Text) = "a pattern matching algorithm" (Length: 28)
**P** (Pattern) = "rithm" (Length: 5)

### Preprocessing: Last Occurrence Function $L(x)$

> [!info] The Last Occurrence Table
> Before searching, the algorithm maps every character in the pattern to its rightmost index. If a character is not in the pattern, its value defaults to -1[.

| Character ($x$) | r | i | t | h | m | All others (a, p, e, n, space, etc.) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **$L(x)$** | 0 | 1 | 2 | 3 | 4 | -1 |

---

### Step 1: First Alignment

> [!abstract] Looking-Glass Technique
> The character comparison strictly begins from the **last** character in the pattern P.

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | a | | p | a | <span style="color:#F44336; font-weight:bold">t</span> | t | e | r | n | | m | a | t | c | h | i | n | g | | a | l | g | o | r | i | t | h | m |
| **P** | r | i | t | h | <span style="color:#F44336; font-weight:bold">m</span> | | | | | | | | | | | | | | | | | | | | | | | |
| **P[j]**| 0 | 1 | 2 | 3 | 4 | | | | | | | | | | | | | | | | | | | | | | | |

* **Rationale:** We compare $P[4]$ ('m') with $T[4]$ ('t'). They mismatch.
* The mismatched text character is $x$ = **'t'**.
* **Case Occurred = Case 1:** The character 't' exists in the pattern P at index 2 ($L(\text{'t'}) = 2$)
* **Action:** Shift P to the right to align the occurrence of 't' in P with the mismatched 't' in the text. 
* **Shift Amount:** $j - L(x) = 4 - 2 = 2$. Move P to the right 2 times.

---

### Step 2

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | a | | p | a | t | t | <span style="color:#F44336; font-weight:bold">e</span> | r | n | | m | a | t | c | h | i | n | g | | a | l | g | o | r | i | t | h | m |
| **P** | | | r | i | t | h | <span style="color:#F44336; font-weight:bold">m</span> | | | | | | | | | | | | | | | | | | | | | |
| **P[j]**| | | 0 | 1 | 2 | 3 | 4 | | | | | | | | | | | | | | | | | | | | | |

* **Rationale:** Compare $P[4]$ ('m') with $T[6]$ ('e'). Mismatch.
* The mismatched text character is $x$ = **'e'**.
* **Case Occurred = Case 3:** The character 'e' does NOT exist anywhere in the pattern P ($L(\text{'e'}) = -1$).
* **Action:** Shift the entire pattern completely past the mismatch to align $P[0]$ with $T[i+1]$ (which is index 7).
* **Shift Amount:** $j - L(x) = 4 - (-1) = 5$. Move P to the right 5 times.

---

### Step 3

| `i`      |  0  |  1  |  2  |  3  |  4  |  5  |  6  |  7  |  8  |  9  | 10  |                           11                           | 12  | 13  | 14  | 15  | 16  | 17  | 18  | 19  | 20  | 21  | 22  | 23  | 24  | 25  | 26  | 27  |
| :------- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :----------------------------------------------------: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T**    |  a  |     |  p  |  a  |  t  |  t  |  e  |  r  |  n  |     |  m  | <span style="color:#F44336; font-weight:bold">a</span> |  t  |  c  |  h  |  i  |  n  |  g  |     |  a  |  l  |  g  |  o  |  r  |  i  |  t  |  h  |  m  |
| **P**    |     |     |     |     |     |     |     |  r  |  i  |  t  |  h  | <span style="color:#F44336; font-weight:bold">m</span> |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| **P[j]** |     |     |     |     |     |     |     |  0  |  1  |  2  |  3  |                           4                            |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |     |

* **Rationale:** Compare $P[4]$ ('m') with $T[11]$ ('a'). Mismatch.
* The mismatched text character is $x$ = **'a'**.
* **Case Occurred = Case 3:** The character 'a' does NOT exist in P ($L(\text{'a'}) = -1$).
* **Action:** Shift P completely past 'a' to align $P[0]$ with index 12.
* **Shift Amount:** 5. Move P to the right 5 times.

---

### Step 4

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | a | | p | a | t | t | e | r | n | | m | a | t | c | h | i | <span style="color:#F44336; font-weight:bold">n</span> | g | | a | l | g | o | r | i | t | h | m |
| **P** | | | | | | | | | | | | | r | i | t | h | <span style="color:#F44336; font-weight:bold">m</span> | | | | | | | | | | | |
| **P[j]**| | | | | | | | | | | | | 0 | 1 | 2 | 3 | 4 | | | | | | | | | | | |

* **Rationale:** Compare $P[4]$ ('m') with $T[16]$ ('n'). Mismatch.
* The mismatched text character is $x$ = **'n'**.
* **Case Occurred = Case 3:** The character 'n' does NOT exist in P.
* **Action:** Shift P completely past 'n' to align $P[0]$ with index 17.
* **Shift Amount:** 5. Move P to the right 5 times.

---

### Step 5

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | a | | p | a | t | t | e | r | n | | m | a | t | c | h | i | n | g | | a | l | <span style="color:#F44336; font-weight:bold">g</span> | o | r | i | t | h | m |
| **P** | | | | | | | | | | | | | | | | | | r | i | t | h | <span style="color:#F44336; font-weight:bold">m</span> | | | | | | |
| **P[j]**| | | | | | | | | | | | | | | | | | 0 | 1 | 2 | 3 | 4 | | | | | | |

* **Rationale:** Compare $P[4]$ ('m') with $T[21]$ ('g'). Mismatch.
* The mismatched text character is $x$ = **'g'**.
* **Case Occurred = Case 3:** The character 'g' does NOT exist in P.
* **Action:** Shift P completely past 'g' to align $P[0]$ with index 22.
* **Shift Amount:** 5. Move P to the right 5 times.

---

### Step 6

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | a | | p | a | t | t | e | r | n | | m | a | t | c | h | i | n | g | | a | l | g | o | r | i | t | <span style="color:#F44336; font-weight:bold">h</span> | m |
| **P** | | | | | | | | | | | | | | | | | | | | | | | r | i | t | h | <span style="color:#F44336; font-weight:bold">m</span> | |
| **P[j]**| | | | | | | | | | | | | | | | | | | | | | | 0 | 1 | 2 | 3 | 4 | |

* **Rationale:** Compare $P[4]$ ('m') with $T[26]$ ('h'). Mismatch.
* The mismatched text character is $x$ = **'h'**.
* **Case Occurred = Case 1:** The character 'h' exists in the pattern P at index 3 ($L(\text{'h'}) = 3$).
* **Action:** Shift P to the right to align $P[3]$ ('h') with $T[26]$.
* **Shift Amount:** $j - L(x) = 4 - 3 = 1$. Move P to the right 1 time.

---

### Step 7 - Last (String Found)

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | a | | p | a | t | t | e | r | n | | m | a | t | c | h | i | n | g | | a | l | g | o | <span style="color:#4CAF50; font-weight:bold">r</span> | <span style="color:#4CAF50; font-weight:bold">i</span> | <span style="color:#4CAF50; font-weight:bold">t</span> | <span style="color:#4CAF50; font-weight:bold">h</span> | <span style="color:#4CAF50; font-weight:bold">m</span> |
| **P** | | | | | | | | | | | | | | | | | | | | | | | | <span style="color:#4CAF50; font-weight:bold">r</span> | <span style="color:#4CAF50; font-weight:bold">i</span> | <span style="color:#4CAF50; font-weight:bold">t</span> | <span style="color:#4CAF50; font-weight:bold">h</span> | <span style="color:#4CAF50; font-weight:bold">m</span> |
| **P[j]**| | | | | | | | | | | | | | | | | | | | | | | | 0 | 1 | 2 | 3 | 4 |

**Iteration Process (Right to Left):**
* Check $P[4]$ ('m') == $T[27]$ ('m') $\rightarrow$ **Match!** Move left.
* Check $P[3]$ ('h') == $T[26]$ ('h') $\rightarrow$ **Match!** Move left.
* Check $P[2]$ ('t') == $T[25]$ ('t') $\rightarrow$ **Match!** Move left.
* Check $P[1]$ ('i') == $T[24]$ ('i') $\rightarrow$ **Match!** Move left.
* Check $P[0]$ ('r') == $T[23]$ ('r') $\rightarrow$ **Match!** 
 
> [!check] Finalize
> The entire pattern has been checked and matched successfully.
> Thus, it is concluded that String **P** = "rithm" exists in **T** = "a pattern matching algorithm" at indices **23 to 27**.

<br>

---

<br>

# KMP (Knuth-Morris-Pratt) Algorithm

> [!quote] The Knuth-Morris-Pratt (KMP) Algorithm: Core Philosophy and Strategy
> 
> The Knuth-Morris-Pratt (KMP) algorithm searches for a pattern $P$ within a text $T$ in a progressive, left-to-right order. Unlike the naive brute-force method, KMP shifts the pattern much more intelligently when a mismatch occurs. By precomputing a failure function from the pattern itself, the algorithm knows exactly how far to slide the pattern ahead, completely eliminating the need to backtrack through characters in the text that have already been evaluated.

### The Three Operational Cases in KMP String Matching

During the search phase, the algorithm maintains a text index $i$ and a pattern index $j$. At each step, it evaluates the relationship between the current characters and chooses its next action based on three distinct logic cases:

#### Case 1: The Characters Match ($P[j] == T[i]$)

- **Rule:** If the character in the pattern matches the current character in the text, the algorithm advances forward. If the matched character is the last character of the pattern ($j == m-1$), the pattern has been fully located within the text. Otherwise, both pointers are incremented by 1 to check the next sequential alignment.

>  **Example:** If you are matching the pattern "abacab" against a text, and the first three characters "aba" successfully match, both index pointers $i$ and $j$ increment continuously together to verify the fourth character.

#### Case 2: Character Mismatch with a Partial Match History ($P[j] \neq T[i]$ and $j > 0$)

- **Rule:** If a mismatch occurs but some characters have already been successfully matched (indicated by $j > 0$), the algorithm does not reset back to the beginning of the pattern. Instead, it references the precomputed failure function to update the pattern pointer to $j = F(j-1)$. This shifts the pattern to the right by aligning the largest proper prefix of the matched substring that is also a valid suffix of that substring.

>  **Example:** Consider searching for the pattern $P =$ "abaaba" inside the text $T =$ "abaabx". A mismatch happens at index $j = 5$ because $P[5] = \text{'a'}$ does not match $T[5] = \text{'x'}$. Because $j > 0$, the algorithm computes the longest prefix of "abaab" that is also a suffix of "baab", which is "ab" (length of 2). It shifts the pattern by 3 spaces, automatically safety-skipping redundant checks and seamlessly resuming the comparison at `len("abaab") - len("ab) = `$j_{\text{new}} = 5 - 2 = 2$.


#### Case 3: Character Mismatch at the Absolute Start of the Pattern ($P[j] \neq T[i]$ and $j == 0$)

- **Rule:** If a mismatch occurs immediately on the very first character of the pattern ($j == 0$), it means there is no historical matching prefix to build upon. The pattern cannot shift backwards any further. Therefore, the pattern stays fixed relative to its starting alignment, and the text pointer is incremented by 1 ($i = i + 1$) to evaluate the next character position in the text.

> **Example:** If your text begins with the character 'c' and your search pattern is "abacab", a mismatch occurs immediately at the first step ($j = 0$). Since no partial match exists, the algorithm slides the pattern past 'c' by incrementing the text index $i$ to check the next position.


### Preprocessing: Visualizing the KMP Failure Function Table

To run seamlessly without physical text backtracking, the KMP algorithm maps out the pattern's self-similar structures before running the main text search. This is formally saved as the failure function, $F(k)$, which records the size of the largest prefix of $P[0..k]$ that is also a suffix of $P[1..k]$.

> [!note]
> Failure Function $F(k)$ can also be generally referred online as Longest Proper Prefix (LPS)

> Based on the example provided for the pattern $P =$ "abacab", here is the precomputed step-by-step failure function table:
> 
> |**Index (k)**|**0**|**1**|**2**|**3**|**4**|
> |---|---|---|---|---|---|
> |**Pattern Character $P[k]$**|a|b|a|c|a|
> |**Failure Function $F(k)$**|0|0|1|0|1|

_Note: For instance, $F(4) = 1$ because for the substring $P[0..4] =$ "abaca", the longest proper prefix that is also a matching suffix is simply "a", which yields a length of 1._

---
> [!example] Brief Example
> KMP algorithm
> T = "abaabx"
> P = "abaaba"

Solution

|0|1|2|3|4|5|6|7|8|
|---|---|---|---|---|---|---|---|---|
|<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">b</span>|<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">b</span>|<span style="color:rgb(255, 200, 0)">x</span>||||
|<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">b</span>|<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">b</span>|<span style="color:rgb(255, 0, 0)">a</span>||||
||||<span style="color:rgb(200, 200, 0)">a</span>|<span style="color:rgb(200, 200, 0)">b</span>|<span style="color:rgb(0, 176, 240)">a</span>|a|b|a|
No need to repeat ab in ==ab==aaba, continue comparing ab==aaba==

Find largest prefix (start) of:
	"==a b== a a b" (P[0..j-1])
That is the suffix (end) of:
	"b a ==a b==" (P[1..j-1])

### Failure Function

> Defined as F(k) which is the size of the largest prefix P[0,,k] that is the suffix of P[1..k]

| Index |0|1|2|3|4|5|
|---|---|---|---|---|---|
| String |a|b|a|a|b|a|
|F(k)|0|||||
Nothing repeated, continue

| Index |0|1|2|3|4|5|
|---|---|---|---|---|---|
| String |a|b|a|a|b|a|
|F(k)|0|0||||
Nothing repeated, continue

| Index |0|1|2|3|4|5| 
|---|---|---|---|---|---|
| String |<span style="color:rgb(0, 176, 80)">a</span>|b|<span style="color:rgb(0, 176, 80)">a</span>|a|b|
|F(k)|0|0|1|||
String "a" is repeated. F(k) = 1

| Index |0|1|2|3|4|5| 
|---|---|---|---|---|---|
| String |<span style="color:rgb(0, 176, 80)">a</span>|b|a|<span style="color:rgb(0, 176, 80)">a</span>|b|
|F(k)|0|0|1|1||
String "a" is repeated. F(k) = 1

| Index |0|1|2|3|4|5| 
|---|---|---|---|---|---|
| String |<span style="color:rgb(0, 176, 80)">a</span>|<span style="color:rgb(0, 176, 80)">b</span>|a|<span style="color:rgb(0, 176, 80)">a</span>|<span style="color:rgb(0, 176, 80)">b</span>|
|F(k)|0|0|1|1|2|
String "ab" is repeated. F(k) = 2

---
# Full Example: KMP Algorithm

> [!warning] Core Concept: Failure Function
> The Knuth-Morris-Pratt (KMP) algorithm searches for a pattern $P$ within a text $T$ in a progressive, left-to-right order. The Failure Function $F(k)$ is precomputed strictly from the **pattern itself**, completely eliminating the need to backtrack through evaluated characters. 

**T** = "abacaabaccabacabaabb"
**P** = "abacab"

### Preprocessing: Failure Function $F(k)$

> [!info] Longest Prefix Suffix (LPS)
> $F(k)$ records the size of the largest proper prefix of $P[0..k]$ that is also a suffix. 
> *Note: $F(4) = 1$ because for the substring $P[0..4]$ ("abaca"), the longest proper prefix that is also a matching suffix is simply "a".*

| Index ($k$) | 0 | 1 | 2 | 3 | 4 | 5 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Pattern $P[k]$** | a | b | a | c | a | b |
| **$F(k)$** | 0 | 0 | 1 | 0 | 1 | 2 |

---

### Step 1: First Mismatch

> [!abstract] Initial Phase
> During the search phase, the algorithm maintains a text index `i` and a pattern index `j`. If the character in the pattern matches the current character in the text, the algorithm advances forward.

If first value matches, increment `i` and `j` by one.

```python
if matched:
	i += 1
	j += 1
```

| `i` | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">c</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#F44336; font-weight:bold">a</span> | b | a | c | c | a | b | a | c | a | b | a | a | b | b |
| **P** | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">c</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#F44336; font-weight:bold">b</span> | | | | | | | | | | | | | | |
| **P[j]**| 0 | 1 | 2 | 3 | 4 | 5 | | | | | | | | | | | | | | |

When it is a mismatch and `j != 0`:

> [!example] Rule: Mismatch with Partial History
> The algorithm references the precomputed failure function to update the pattern pointer to $j = F(j-1)$.

```python
if not matched:
	if j != 0:
		j = F(k) # This will be executed
	else:
		i += 1 
```

**Reminder:**
`k = j - 1`
`k = 5 - 1 = 4`
`F(4) = 1`

So, the new pattern index `j` will be **1**. The pattern shifts to align `P[1]` with `T[5]`.

---

### Step 2: Evaluating Shifted Alignment

| `i` | ... | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | ... |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | ... | a | <span style="color:#F44336; font-weight:bold">a</span> | b | a | c | c | a | b | ... |
| **P** | | a | <span style="color:#F44336; font-weight:bold">b</span> | a | c | a | b | | | |
| **P[j]**| | 0 | 1 | 2 | 3 | 4 | 5 | | | |

There is another mismatch spot at `T[5] = 'a'` and `P[1] = 'b'`.

```python
if not matched:
	if j != 0:
		j = F(k) # Executed
```
`k = 1 - 1 = 0`
`F(0) = 0`

So the new pattern index `j` becomes **0**. Align `P[0]` with `T[5]`.

---

### Step 3: Match Continued until Next Mismatch

Match successfully continues from `T[5]` and `P[0]`.

| `i` | ... | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | ... |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | ... | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">c</span> | <span style="color:#F44336; font-weight:bold">c</span> | a | b | a | ... |
| **P** | | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">c</span> | <span style="color:#F44336; font-weight:bold">a</span> | b | | | |
| **P[j]**| | 0 | 1 | 2 | 3 | 4 | 5 | | | |

Mismatch occurs at `T[9] = 'c'` and `P[4] = 'a'`.

```python
if not matched:
	if j != 0:
		j = F(k) # Executed
```
`k = 4 - 1 = 3`
`F(3) = 0`
New `j = 0`.

---

### Step 4: Instant Mismatch

> [!example] Rule: Absolute Start Mismatch
> If a mismatch occurs immediately on the very first character of the pattern ($j == 0$), there is no historical matching prefix. The pattern stays fixed, and the text pointer is incremented by 1 ($i = i + 1$).

| `i` | ... | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | ... |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | ... | c | <span style="color:#F44336; font-weight:bold">c</span> | a | b | a | c | a | b | ... |
| **P** | | | <span style="color:#F44336; font-weight:bold">a</span> | b | a | c | a | b | | |
| **P[j]**| | | 0 | 1 | 2 | 3 | 4 | 5 | | |

String mismatches instantly (`j == 0`).

```python
if not matched:
	if j != 0:
		j = F(k)
	else:
		i += 1 # This will be executed
```
Increment `T[i]` by 1. Text pointer `i` becomes **10**.

---

### Step 5: Solution Found!

| `i` | ... | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | ... | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">c</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | a | a | b | b |
| **P** | | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">c</span> | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#4CAF50; font-weight:bold">b</span> | | | | |
| **P[j]**| | 0 | 1 | 2 | 3 | 4 | 5 | | | | |

**Strings Matched!**
> [!check] Match Complete
> If the matched character is the last character of the pattern ($j == m-1$), the pattern has been fully located within the text[.

---

### Continued - Step 6

In case we want to continue the String Matching to find other occurrences.
Treat it as if a mismatch happened to safely slide it forward:

`j = 5` (matched completely)
`k = 5`
`j = F(5) = 2`

| `i` | ... | 14 | 15 | 16 | 17 | 18 | 19 |
| :--- | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **T** | ... | a | b | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#F44336; font-weight:bold">a</span> | b | b |
| **P** | | | | <span style="color:#4CAF50; font-weight:bold">a</span> | <span style="color:#F44336; font-weight:bold">c</span> | a | b |
| **P[j]**| | | | 0 | 1 | 2 | 3 |

* Match at `T[16]` and `P[0]`.
* Mismatch at `T[17]` and `P[1]`.
* Algorithm safely bounds its way to the end of the string.

At this point, index `i` reached its end. Stop the program.
```python
if i >= 19:
	return
```