> [!note] Material Source
> IN244-Strategi Algoritmik > P12-String Matching > Slides teori
> <small>*Powerpoint slides will not be included here to prevent redundancy*</small>

> [!warning] Warning! This file can not be exported effectively. 
> 
> If still needed to be exported:  
> * Lower the downscale percent is required for the contents to be universally exists
> * There will be no color text to guide the step-by-step algorithm

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

### Step 1
|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|a||p|a|~={red}t=~|t|e|r|n||m|a|t|c|h|i|n|g||a|l|g|o|r|i|t|h|m|
|r|i|~={green}t=~|h|~={red}m=~||||||||||||||||||||||||

##### Case occured = case 1: 

| iteration | index | T | P | rationale |
| --- | --- | --- | --- | --- |
| 1 | 4 | t | m | different and case 1 occured|

> Case 1 occured because there are `t` in string P
> We're currently checking `P[4] = "t"` and `T[4] = "m"` which are different, but `P[4] = "t"` existed in T which is T[2]

Make t in P align with T which is `P[2]` to `T[4]`.
Or basically move P to the right 2 times.

### Step 2

|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|a||p|a|t|t|~={red}e=~|r|n||m|a|t|c|h|i|n|g||a|l|g|o|r|i|t|h|m|
|||r|i|t|h|~={red}m=~||||||||||||||||||||||

##### Case occured = case 3

| iteration | index | T | P | rationale |
| --- | --- | --- | --- | --- |
| 1 | 6 | e | m | different and case 3 occured|

> It is intended to find `T[6] = "e"` but P = `"rithm"` meaning that there is **no e in P**. 
> Thus, case 3 occured

Move P to place P[0] with T[i+1]
or basically move P to the right one time

### Step 3

|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|a||p|a|t|t|e|~={red}r=~|n||m|a|t|c|h|i|n|g||a|l|g|o|r|i|t|h|m|
||||~={green}r=~|i|t|h|~={red}m=~|||||||||||||||||||||

##### case occured = case 1

| iteration | index | T | P | rationale |
| --- | --- | --- | --- | --- |
| 1 | 7 | r | m | different and case 1 occured|

> Case 1 occured because `T[7] = "r"` that is currently mismatch with `P[7] = "m"` exist in P which is in `P[3] = "r"`

Move current `P[3]` until it matched the string with T in `T[7]`
Or basically move P to the right 4 times

### Step 4

|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|a||p|a|t|t|e|r|n||m|~={red}a=~|t|c|h|i|n|g||a|l|g|o|r|i|t|h|m|
||||||||r|i|t|h|~={red}m=~|||||||||||||||||

##### Case occured = case 3

| iteration | index | T | P | rationale |
| --- | --- | --- | --- | --- |
| 1 | 11 | a | m | different and case 3 occured|

> It is intended to find `T[11] = "a"` but P = `"rithm"` meaning that there is **no a in P**. 
> Thus, case 3 occured

Move P to place P[0] with T[i+1]
or basically move P to the right one time

### step 5
|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|a||p|a|t|t|e|r|n||m|a|~={red}t=~|c|h|i|n|g||a|l|g|o|r|i|t|h|m|
|||||||||r|i|~={green}t=~|h|~={red}m=~||||||||||||||||

##### Case occured = case 1

| iteration | index | T | P | rationale |
| --- | --- | --- | --- | --- |
| 1 | 12 | t | m | different and case 1 occured|

> Case 1 occured because `T[12] = "t"` that is currently mismatch with `P[12] = "m"` exist in P which is in `P[10] = "t"`

Move current `P[10]` until it matched the string with T in `T[12]`
Or basically move P to the right 2 times

### Step 6 - Step 13
This continues until it has found the matching string

|step|case|move right x times|
|---|---|---|
|6|3|1|
|7|1|3|
|8|3|1|
|9|3|1|
|10|3|1|
|11|3|1|
|12|3|1|
|13|1|4|

### Step 14 - Last
|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|a||p|a|t|t|e|r|n||m|a|t|c|h|i|n|g||a|l|g|o|r|i|t|h|m|
||||||||||||||||||||||||r|i|t|h|m|

##### String found

|iteration|index|T|P|rationale|
|---|---|---|---|---|
|1|27|m|m|Strings are the same, move left one time|
|1|26|h|h|Strings are the same, move left one time|
|1|25|t|t|Strings are the same, move left one time|
|1|24|i|i|Strings are the same, move left one time|
|1|23|r|r|Strings are the same, move left one time|

![[Pasted image 20260531052028.png]]

> [!success] Finalize
> Thus, it is concluded that 
> > - String P ="rithm" exists in T = "a pattern matching algo==rithm=="

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
> Failure Function can also be generally referred online as Longest Proper Prefix (LPS)

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
|~={yellow}a=~|~={yellow}b=~|~={yellow}a=~|~={yellow}a=~|~={yellow}b=~|~={orange}x=~||||
|~={yellow}a=~|~={yellow}b=~|~={yellow}a=~|~={yellow}a=~|~={yellow}b=~|~={red}a=~||||
||||~={yellow}a=~|~={yellow}b=~|~={cyan}a=~|a|b|a|
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
| String |~={green}a=~|b|~={green}a=~|a|b|
|F(k)|0|0|1|||
String "a" is repeated. F(k) = 1

| Index |0|1|2|3|4|5| 
|---|---|---|---|---|---|
| String |~={green}a=~|b|a|~={green}a=~|b|
|F(k)|0|0|1|1||
String "a" is repeated. F(k) = 1

| Index |0|1|2|3|4|5| 
|---|---|---|---|---|---|
| String |~={green}a=~|~={green}b=~|a|~={green}a=~|~={green}b=~|
|F(k)|0|0|1|1|2|
String "ab" is repeated. F(k) = 2

> [!example] Full Example
> KMP algorithm
> T = "abacaabaccabacabaabb"
> P = "abacab"

### Step 1

If first value matches, increment i and j by one
```python
if matched:
	i += 1
	j += 1
```

|T[i]|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|T |a|b|a|c|a|~={red}a=~|b|a|c|c|a|b|a|c|a|b|a|a|b|b|
|P|a|b|a|c|a|~={red}b=~|||||||||||||||
|P[i]|0|1|2|3|4|5|||||||||||||||

> When it is mismatch and `j != 0`
> "abaca" is repeatable
> with failure function F(k) = 1, since there is only string "a" at index 4
> 
|**Index (k)**|**0**|**1**|**2**|**3**|**4**|**5**|**6**|**7**|**8**|**9**|**10**|**11**|**12**|**13**|**14**|**15**|**16**|**17**|**18**|**19**|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|**String**|a|b|a|c|~={yellow}a=~|a|b|a|c|c|a|b|a|c|a|b|a|a|b|b|
|**$F(k)$**|0|0|1|0|~={yellow}1=~|1|2|3|4|0|**1**|2|3|4|5|2|3|1|**2**|**0**|
> ```python
> if not matched:
> 	if j != 0:
> 		j = F(k) # This will be executed
> 	else:
> 		i += 1 
>```
> > [!important] Reminder
> > k = j - 1
>
>  k = 5 - 1 = 4
> 
> So, the prefix will be "a"

### Step 2

|T[i]|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|T |a|b|a|c|a|a|b|a|c|~={red}c=~|a|b|a|c|a|b|a|a|b|b|
|P||||||~={yellow}a=~|~={orange}b=~|a|c|~={red}a=~|b||||||||||
|P[i]||||||0|1|2|3|4|5||||||||||

> Notice that there is repeatable "ac"
> ```python
> if not matched:
> 	if j != 0:
> 		j = F(k) # This will be executed
> 	else:
> 		i += 1 
>```
> - F(k) = 9 - 1 = 8
> 
>
|**Index (k)**|**0**|**1**|**2**|**3**|**4**|**5**|**6**|**7**|**8**|**9**|**10**|**11**|**12**|**13**|**14**|**15**|**16**|**17**|**18**|**19**|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|**String**|a|b|a|c|a|a|b|a|c|c|a|b|a|~={yellow}c=~|a|b|a|a|b|b|
|**$F(k)$**|0|0|1|0|1|1|2|3|~={yellow}4=~|0|**1**|2|3|4|5|2|3|1|**2**|**0**|
"==abac==a==abac==cabacabaabb"

So the prefix will be "ac"

### Step 3
|T[i]|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|T|a|b|a|c|a|a|b|a|c|~={red}c=~|a|b|a|c|a|b|a|a|b|b|
|P||||||||||~={red}a=~|b|a|c|a|b||||||
|P[i]||||||||||0|1|2|3|4|5||||||
> String mismatches instantly and there is no recorded repeatable strings
Increment P[i] by 1
> ```python
> if not matched:
> 	if j != 0:
> 		j = F(k)
> 	else:
> 		i += 1 # This will be executed
>```


Or move P to the right once

### Step 4
|T[i]|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|T|a|b|a|c|a|a|b|a|c|c|a|b|a|c|a|b|a|a|b|b|
|P|||||||||||a|b|a|c|a|b|||||
|P[i]|||||||||||0|1|2|3|4|5|||||
> Found

### Continued - Step 5
In case we want to continue the String Matching

> First, increment i and j by one
> ```python
> if Matched:
> 	i += 1
> 	j += 1
> ```

> And track the Failure Function again
> ```
> j = F(k)
> ```
> - j had been incremented = 16
> k = j -1
> k = 16 - 1 = 15
>
> |**Index (k)**|**0**|**1**|**2**|**3**|**4**|**5**|**6**|**7**|**8**|**9**|**10**|**11**|**12**|**13**|**14**|**15**|**16**|**17**|**18**|**19**|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|**String**|a|b|a|c|a|a|b|a|c|c|a|b|a|c|a|b|a|a|b|b|
|**$F(k)$**|0|0|1|0|1|1|2|3|4|0|**1**|2|3|4|5|2|3|1|**2**|**0**|

Result:

|T[i]|0|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|T|a|b|a|c|a|a|b|a|c|c|a|b|a|c|a|~={orange}b=~|a|~={red}a=~|b|b|
|P[i]|||||||||||||||a|b|a|~={red}c=~|a|b|
|P[i]|||||||||||||||0|1|2|3|4|5|

At this point, index i reached it's end. Stop the program
```python
if i >= 19:
	return
```