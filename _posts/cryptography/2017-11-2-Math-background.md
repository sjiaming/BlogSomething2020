---
layout: default
title: Math Background for Public Key Cryptography
description: Basic number theory knowledge
imgsrc: assets/pics/crypto/1.jpg
banner: assets/pics/crypto/math_banner.jpg
date: 2017-11-02
category: cryptography
tags: [Math,Cryptography]
author: Song Jiaming
---
This blog is my study note for CS4236 Cryptography, Chapter 8.

### 1. Prime Numbers

__Notation__<br>

- **a** divides **b** (notation: a\|b), if there exists an integer __c__ s.t. __b = ac__
- For any 2 integers **a** and **b**, there exists 2 unique integers **r** and **q** such that:
    - __0 ≤ r < q__ and
    -  __a = qb + r__. 
    - Note that: __a mod b = r__
- 2 integers __a__ and __b__ are relatively prime or co-prime if __gcd(a,b)=1__
    + __gcd(a,b)__: greatest common divisor of a and b
- (Congruence) Let __a__,__b__ and __n__ be integers (\\(n \not = 0\\)): if __(a mod n) = (b mod n)__, then __a ≡ b  (mod n)__

---


__Properties__<br>
Suppose __a ≡ x  (mod n)__ and __b ≡ y  (mod n)__, then:
- (a+b) ≡ (x+y) (mod n)
- (a-b) ≡ (x-y) (mod n)
- (ab) ≡ (xy) (mod n)
- Caution: \\(2^{a} \not \equiv 2^{x}\\)(mod n)

---


__Extended Euclidean Algorithm__<br>
Purpose: to find the gcd d.
Input: 2 integers __a__ and __b__<br>
Output: __d=gcd(a,b)__ and 2 integer __s__ and __t__ such that:
- __as+bt=d__ and __0 ≤ s < b__

```python
if b = 0:
    d = a, s = 1, t = 0
else:
    set s2 = 1, s1 = 0, t2 = 0, t1 = 1
    while b > 0:
        set q = floor(a/b), r = a - q*b
            s = s2 - q*s1, t = t2 -q*t1
        set a = b, b = r,
            s2 = s1, s1 = s, t2 = t1, t1 = t
    set d = a, s = s2, t = t2
return (d,s,t)            
```

If __a__ and __b__ are at most m-bit long, running time is O(\\(m^{2}\\))
If gcd(x,n) = 1, we can find __s,t__ such that:
- __xs+nt = 1__
- That is, __xs = 1 (mod n)__
<br>


Mathematically, suppose __b < \|a\|__, to find gcd(a,b):

| Step   | Equation  | Condition |
| :----: | :------: | :--------:    |
| 1      | \\(a=b\times q_{1}+r\\)  | 0 ≤ \\(r_{1}\\) < b       |
| 2      | \\( b=r_{1}\times q_{2}+r_{2} \\)   |   0 ≤ \\(r_{2}\\) < \\(r_{1}\\)       |
| 3      | \\(r_{1}=r_{2}\times q_{3}+r_{3} \\)  |    0 ≤ \\(r_{3}\\) < \\(r_{2}\\)       |
| ...    | ...   |    ...       |
| k      | \\(r_{k−2}=r_{k−1}\times q_{k}+r_{k} \\)  |   0 ≤ \\(r_{k}\\) < \\(r_{k−1}\\)      |

The process continues until we obtain in Step n, a remainder \\(r_{n}\\)= 0.<br>
In that case, the last non-zero remainder \\(r_{n-1}\\)= gcd(a,b).<br>
By applying backward substitutions, we can obtain integers s and t such that gcd(a,b) = as + bt
<br>

Example.Find gcd(33,93).
1. 93 = 33×2 + 27 and r1= 27
2. 33 = 27×1 + 6 and r2= 6
3. 27 = 6×4 + 3 and r3= 3
4. 6 = 3×2 and r4= 0

Therefore, gcd(33,93) = 3.

<br>

### 2. Arithmetic in the real field R
Infinite, every element (except zero) has a multiplicative inverse

- In the set __R__ of real numbers, we have binary operation: R x R \\(\rightarrow\\) R, 'x' denotes an operator, not 'times'
- Close under an operation: if __a,b__ ∈ R, then a x b ∈ R
- 2 operators:
    - +: addition, 0: additive identity
    - •: multiplication, 1: multiplicative identity
- Inverse:
    + additive inverse: for __a__ ∈ R, __b__ is its inverse iff a+b=0. b=-a
    + multiplicative inverse: for __a__ ∈ R \ {0}, b is its inverse iff a • b = 1. b = \\(a^{-1}\\)
- (R , + , • ) is an infinite field.

<br>

### 3. Arithmetic in the integer ring Z
Infinite. Only “1” and “-1” have multiplicative inverse
- Z is not a field
- Given int x, to determine whether its square root exists, and what is the squre root:
    + Find the integer y s.t. \\(y^{2}\\) = y • y = x   
- Given int x, g, to determine whether ∃ an integer y s.t. \\(g^{y}\\) = x
    - __y = \\(\log_{g}\\) x__
- The above 2 algorithems are efficient in the sense that:
    - suppose __x, g, y__ are m-bit integers
    - the running time is polynomial w.r.t. __m__


<br>


### 4. Arithmetic in the Finite field \\(Z_{p}\\)
- \\(Z_{p}\\) = {0, 1, 2, ..., p-1} where p is prime
For any __a,b ∈ \\(Z_{p}\\):
- a + b = c where c = (a + b) mod p
- a • b = d where d = (a b) mod p

Any x ∈ \\(Z_{p}\\), except 0, has a multiplicative inverse,
- ∃ a __y__ s.t. xy ≡ 1 (mod p)
- These elements are included in a group \\(Z_{p}^{*}\\) = {1, 2, ..., p-1}

- Given __x, p__, we can compute its multiplication inverse__
    - using Extended Euclidean Algorithm to compute gcd(x,p)
    - We will have a•p + k•x = 1 ⇒ 1 ≡ k • x ⇒ k or -k mod p is the inverse
    - e.g. Find multiplicative inverse of 19 congruent 125:
        + Find gcd(19,125), let x = 19, p = 125
        + 125 = 6•19 + 11 ⇒ p = 6x + 11 ⇒  11 = p - 6x
        + 19 = 1•11 + 8 ⇒ x = p-6x + 8 ⇒ 8 = -p+7x
        + 11 = 1•8 + 3 ⇒ p-6x = -p + 7x +3⇒ 3 = 2p-13x
        + 8 = 2•3 + 2 ⇒ -p+7x = 2(2p-13x) + 2 ⇒ 2 = -5p + 33x
        + 3 = 1•2 + 1 ⇒ 2p-13x = -5p+33x +1 ⇒ 1 = 7p - 46x
        + ⇒ -46•19 ≡ 1 mod 125 ⇒ (-46) = 79 mod 125
        + The inverse is 79
-  Given __x, d, p__, we want to compute \\(x^{d}\\)__mod p__ efficiently.
    - The sequence $c^{2},c^{4},c^{8}$ can be computed fast by successive squaring
    - $c^{54} = c^{2+4+16+32}=c^{2}\cdot c^{4}\cdot c^{16} \cdot c^{32}$
    - Fast Algorithm for exponentiation: Suppose d = $b_{0}b_{1}...b_{k-1}$ (binary)
    ```
    temp = 1;
    for i in range(k):
        temp = (temp*temp) mod p 
        if (b[i] == 1):
            temp = (temp*x) mod p
    return temp
    ```
    

<br>

### 5 Arithmetic in Modulo Composite (finite ring) \\(Z_{n}^{*}\\)
- __x__ ∈ $Z_{n}$ has an multiplicative inverse iff __gcd(x,n)=1__
- $Z_{n}^{*}$ = {x: x has inverse}

<br>
__Computation complexity: given m-bits x,y,r:__<br>

| Operations   | Running Time |
| :----------: | :----------: |
| Addition: __x+y__ | __O(m)__  |
| Multiplication: __x•y__ | __O($m^{2}$), O(m log m)__ |
| Inverse $x^{-1}$| __O($m^{2}$)__ |
| Exponentiation: $x^{r}$ | __O($m^{3}$), O($m^{2}$ log m)__ |


---

__Multiplying 2 integers faster__<br>
- m-bits __x,y__
- compute x•y
- Inefficient method:
```
temp = 0
for i = 1 to x:
    temp = temp + y
return temp
```

- Efficient method: Shift-and-Add
```python
temp = 0 
n = len(y)
for i in range(n):
    temp = temp + x * y[n-1-i] * 10**(i)
    # multiply x with the bits of y (from last to the first)
    # each time shift left by 1 bit
```

<br>

### 6. More on \\(Z_{p}\\)

__Fermat's theorem:__<br>
$g^{p-1}$ ≡ 1 (mod p) for all $g \not = 0$ (mod p)
- e.g. $3^{4}$ mod 5 ≡ 1
- 2nd method to find multiplicative inverse
    - $x^{-1}$ ≡ $x^{p-2}$ (mod p)

---

__Some definitions:__<br>
- $Z_{p}^{*}$ = ${1, g, g^{2}, g^{3},..., g^{p-1}}$
    - g: generator of $Z_{p}^{*}$
    - This group generated by g  can be denoted as <g>
    - e.g. 3 is a generator in $Z_{7}^{*}$
        - <3> = ${1, 3, 3^{2},..., 3^{6}}$ = {1,3,2,6,4,5}⇒ $3^{-1}$ ≡ $3^{7-2}$ (mod 7) ⇒ $3^{6}$ (mod 7) ⇒ 5
- For any x ∈ $Z_{p}^{*}$, __order(x)__ = smallest positive integer __a__
    + s.t. $x^{a}$ ≡ 1 (mod p)
    + e.g. order of 3 in $Z_{7}^{*}$ is 6
+ For all x ∈ $Z_{p}^{*}$, ⇒ __order(x) \| (p-1)__

---

__Quadratic Residues in $Z_{p}^{\ast}$__<br>
\\( \sqrt{x} \in Z_{p}^{\ast} \\)  is a number $y \in Z_{p}^{\ast}$ s.t.
- $y^{2} \equiv x$ (mod p)
- e.g. $\sqrt{2}$ mod 7 = 3.
    + Since $3^{2} = 2$ mod 7

An element $x \in Z_{p}^{\ast} $ is __QR(quadratic residue)__ if its square root exits in $Z_{p}^{\ast}$
- Each x has either 0 or 2 square roots
    + If y is a square root of x mod p, then so is -y
- Given x, determine whether x is QR is computationally easy
    + The __Lengendre Symbol__ of x is calculated as:
        * $(\frac{x}{p}) = x^{\frac{p-1}{2}}$ (mod p) 
    + $(\frac{x}{p})$ = 
        * __1__ if x is QR
        * __-1__ if x is not a QR (when ls = p-1)
        * 0 if x ≡ 0 (mod n)
    + For __a,b__,
        * $(\frac{ab}{p}) = (\frac{a}{p})(\frac{b}{p})$ 
- Easy fact: let g be a generator of $Z_{p}^{\ast}$
    - Let x = $g^{r}$ for some integer r.
    - Then x is a QR in Zp if and only if r is even 
    - ⇒ Exactlt half of the elemnets in $Z_{p}^{\ast}$ are QR
- Computing square roots in $Z_{p}^{\ast}$ is computationally feasible
    + $O(n^{4})$ randomized algorithm exists
    + Special cases of __p__: when __p = 3 mod 4__,
        * $\sqrt{x}$ mod p = $x^{\frac{p+1}{4}}$ mod p
        * Why? Let a  = $\sqrt{x}$
        * Then $a^{2} = x^{\frac{2(p+1)}{4}} = x^{\frac{p+2-1}{2}} =x\cdot x^{\frac{p-1}{2}} = x \cdot 1 = x$ mod p        


<br>

### 7. More on \\(Z_{n}\\)

__Euler's totient function__ $\varphi(n)$: <br>
Definition: For any integer $n>1$, $\varphi(n)$ = the no. of integers in $Z_{n}$ which are coprime to n.
- For a prime __p__, $\varphi(p) = p-1$
- if __n = pq__, and p,q are primes,
    + $\varphi(n) = (p-1)(q-1)$
- e.g. n=15, $\varphi(15) = \|{1,2,4,5,8,11,13,14}\|=8$

---

__Euler's Theorem__<br>
$a^{\varphi(n)} = 1$ (mod n) for all $a \in Z_{n}^{\ast}$
- The above is a generalization of Fermat's Theorem in $Z_{p}$
- Useful property:
    + if __x ≡ y__ (mod $\varphi(n)$), then $g^{x} \equiv g^{y}$ (mod n) for any g

---

__Chinese Remainder Theorem (CRT)__<br>
Relate $Z_{n}$ to $Z_{p}$ using the mapping __n = pq__ where __p,q__ are primes and $p \not = q$
- Then map $Z_{n} \rightarrow Z_{p}\times Z_{q}$ 
    - for $x \in Z_{n}$, maps it to 2-tuple (x mod p, x mod q)
    - e.g. n = 15, 7 → (7 mod 3, 7 mod 5) = (4,2)
- Supose __x__ maps to $(x_{1},x_{2})$, __y__ maps to $(y_{1},y_{2})$
    + __x+y__ → $(x_{1}+y_{1},x_{2}+y_{2})$
    + __x•y__ → $(x_{1}\cdot y_{1},x_{2}\cdot y_{2})$
- CRT states that: Let __p,q__ be relatively prime and __n=pq__:
    - Given $x_{1} \in Z_{p}, x_{2} \in Z_{q}$, there exists a unique element $x\in Z_{n}$ s.t
        + $x_{1} = x$ mod p, $x_{2} = x$ mod q
- E.g. to compute $7^{6}$ mod 15:
    + map $Z_{15} \rightarrow Z_{5}\times Z_{3}$: 7 → (2,1)
    + Perform $(2^{6},1^{6})$ → (4,1)
    + map $Z_{5}\times Z_{3} \rightarrow Z_{15}$: (4,1) ->4

---

__Quadratic Residue__<br>
Suppose __n = pq__, where __p,q__ are primes and $p \not = q$
- __Jacobi Symbol__ is defined as:
    + $(\frac{x}{n}) = (\frac{x}{p})(\frac{x}{q})$
    + Jacobi symbol of x =
        * 1, if gcd(x,n) = 1, x can be either a QR or non-QR
        * -1, if gcd(x,n) = 1, x is not a QR
        * 0, if gcd(x,n)>1, x is a multiple of p and/or q. x can be either a QR or non-QR
    + we can't tell whether x is a QR from jacobi symbol
    + If gcd(x,n) = 1:
        + if x is a QR mod n, then $\frac{a}{n} = 1$



<br>

### 8. Computational problems in $Z_{p}$ and $Z_{n}$

__Easy Problems in $Z_{p}$__<br>
1. Suppose p is a large prime number. (say 2048-bit)
    - Generating a random element
    - Add/Multiply elements
    - Find Inverse, exponentiation
    - Test whether an element is QR
    - Compute square root mod p
    - Solve polynomial equations of degree d (polynomial time in d)
    - Given x,d,p, find y s.t. $x = y^{d}$ mod p
2. Decisional Diffie-Hellman (DDH) problem
    + Let g be a generator of cyclic group G with ord(G) = q
    + Given 3-tuples (x,y,z) ∈ G
    + Distinguish whether it is generated by process A or B
        * A: Randomly pick a,b,c from $Z_{q}$, outputs ($g^{a},g^{b},g^{c}$)
        * B: Randomly pick a,b from $Z_{q}$, outputs ($g^{a},g^{b},g^{ab}$)
    + The problem is easy in $Z_{p}^{\ast}$ 
        + Solution: given (x,y,z), compute Jacobi symbol of x,y,z
            * if (x,y,z) ∈ A, the Jacobi symbol of z does not depend on x's and y's
            * if (x,y,z) ∈ B, the Jacobi symbol of z = x's times y's
    + This problem may be hard if the group is the set of QR in $Z_{p}^{\ast}$
        * All element has Jacobi symbol 1

---

__Believed-to-be Hard Problems in $Z_{p}$__<br>
- Discrete log (DL) prolem:
    + Let g be a generator of a cyclic group.
    + Given x, find r s.t. $x = g^{r}$
- Computing Diffie-Hellman (CDh)  problem:
    + Let g be a generator of a cyclic group
    + Given $g^{a},g^{b}$, find $g^{ab}$

For DL in $Z_{p}^{\ast}$ is computationally feasible
- DL can be easy if prime p is of the form $p=2^{m} -1$
- DL can be difficult if prime p is of the form $p = 2q+1$, q is another prime

---

__Easy Problems in $Z_{n}$__<br>
Given a large composite number __n__ (say 2048-bit), n = pq (2 large primes, 1024 bits)
- Generate a random element
- Add/Multiply elements
- Finding inverse, exponentiation
- Finding the Jacobi symbol


---

__Believed-to-be Hard Problems in $Z_{n}$__<br>
If the factorization of n is unknown __BUT__ becoming easy if the factorization of n is known
- Test whether an element is a QR
    + Compute the jacobi symbol cannot solve this problem
- Compute square root of a QR
    - As hard as factoring n
    - Rabin Cryptosystems based on this hardness
- Compute $\varphi(n)$
    + As hard as factoring n
- compute the e-th roots (mod n) when $gcd(e, \varphi(n)) = 1$
    + RSA cryptocsystems based on this hardness


---

__Hard Problems in $Z_{n}$__<br>
Even if factorization are known
- Discrete log (DL) problem
- Computational Diffie-Hellman (CDH) problem

<br>

---




