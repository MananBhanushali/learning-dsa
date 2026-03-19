# Basic Maths

- [Basic Maths](#basic-maths)
  - [Abstraction of Digits of a Number](#abstraction-of-digits-of-a-number)
    - [Count all digits of a Number](#count-all-digits-of-a-number)
    - [Reverse Digits of a Number](#reverse-digits-of-a-number)
    - [Armstrong Number](#armstrong-number)
  - [Print All Divisors](#print-all-divisors)
  - [GCD / HCF of two numbers](#gcd--hcf-of-two-numbers)
    - [Euclidian Algorithm for GCD](#euclidian-algorithm-for-gcd)

## Abstraction of Digits of a Number

```cpp
int n = 7789;

while (n>0) {
    lastDigit = n % 10;
    n = n / 10;
}
```

Ex) n= 7789  
First Iteration: n%10 = 9, n = 778  
Second Iteration: n%10 = 8, n = 77  
Third Iteration: n%10 = 7, n = 7    
First Iteration: n%10 = 7, n = 0  -> stop

### Count all digits of a Number

```cpp
// bruteforce approach
int cnt = 0;
while (n>0) {
    cnt+=1;
    n/=10;
}
cout<<cnt;

// optimal approach
cout << (int)(log10(n) + 1)
```

The time complexity here will be O(log10 n), since the loop runs the number of times the number is divisible by 10.

>[!IMPORTANT]
If the algorithm is based on division by x, time complexity will be **O(logx n)**


### Reverse Digits of a Number

```cpp
int reversedNum = 0;
while (n>0) {
    lastDigit = n%10;
    reversedNum = ( reversedNum * 10 ) + lastDigit;
    n /= 10;
}
cout << reversedNum;
```

Time Complexity = O(log10 n)

### Armstrong Number

If the sum of cube of digits of a number is equal to that number, then it is called an Armstrong Number.
Ex) 371 = 27 + 343 + 1

```cpp
int sum = 0;
while (n>0) {
    sum += (n%10)**3;
    n /= 10;
}
cout << sum;
```

## Print All Divisors

Brute Force Approach ( O(n) )
```cpp
for (int i=1; i<=n; i++) {
    if (n%i==0) {
        cout<<i<<" ";
    }
}
```

**Optimal Approach** - Time Complexity = O( sqrt(n) )  
For Ex) For factors of 36,   
1 x 36 = 36, 2 x 18 = 36, 3 x 12 = 36 ... 6 x 6 = 36, 9 x 4 = 36 ( repeating pair)

Hence we can split the pairs into two parts, before **i^2 <= n** and after i^2 <= n ( repeating )

```cpp
for (int i=1; i*i<=n; i++) {
    if (n%i==0) {
        cout<<i<<" ";

        if (n/i != i) { cout << n/i << " "; } // printing the second factor and making sure it doesn't print repeated factor in case of perfect square
    }
}
```

In Order to sort the factors, they can be put in a vector

## GCD / HCF of two numbers

From 1 to min(n1, n2) - Increasing
```cpp
int gcd = 1;
for (int i=1; i<*min(n1, n2); i++) {
    if (n1%i==0 && n2%i==0) { gcd = i; }
}
```

From min(n1, n2) to 1 - Decreasing
```cpp
int gcd = 1;
for (int i=*min(n1, n2); i>=1; i--) {
    if (n1%i==0 && n2%i==0) { 
        gcd = i;
        break; // on finding a common factor, break instantly because it is going to be the largest ( decreasing i)
    }
}
```

**Time Complexity in both the cases is O( min(n1, n2) )** ( Worst Case Scenario)

### Euclidian Algorithm for GCD

**1. gcd(a, b) = gcd (a-b, b) 
i.e. gcd of difference and the smaller number**

**2. gcd(a, b) = gcd (a%b, b) - More Important  
i.e. gcd of remainder and smaller number**

>[!NOTE]
**gcd(a, 0) = a**

[Euclidian Algorithm Proof](https://www.khanacademy.org/computing/computer-science/cryptography/modarithmetic/a/the-euclidean-algorithm)

```cpp
while (n1>0 && n2>0) { // run till any one number becomes 0
    if (n1>n2) {
        n1 = n1 % n2;
    } else {
        n2 = n2 % n1;
    }
}
if (n1 == 0) cout << n2; // print the other non zero number
else cout << n1;
```

For Ex) gcd (55, 10)
gcd(55, 10) = gcd(5, 10) = gcd(5, 0) = 5

**Time Complexity = O( log phi min(a, b) )**   
( Since division/modulo is involved, TC is in log )   
phi = some constant ( ignore )