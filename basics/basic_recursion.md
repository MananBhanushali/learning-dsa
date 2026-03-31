# Basic Recursion and Backtracking

- [Basic Recursion and Backtracking](#basic-recursion-and-backtracking)
  - [Print 1 to N using Recursion](#print-1-to-n-using-recursion)
  - [Print N to 1 using Recursion](#print-n-to-1-using-recursion)
- [Backtracking](#backtracking)
  - [Print 1 to N using Backtracking](#print-1-to-n-using-backtracking)
  - [Print N to 1 using Backtracking](#print-n-to-1-using-backtracking)
- [Parameterised Recursion](#parameterised-recursion)
  - [Sum of N numbers using Recursion](#sum-of-n-numbers-using-recursion)
- [Functional Recursion](#functional-recursion)
  - [Sum of N numbers using Functional Recursion](#sum-of-n-numbers-using-functional-recursion)
  - [Factorial of N using Functional Recursion](#factorial-of-n-using-functional-recursion)
  - [Reverse an array](#reverse-an-array)
  - [Check if a string is palindrome](#check-if-a-string-is-palindrome)
  - [Fibonacci Series](#fibonacci-series)

Recursion - When a Function calls itself until a specific condition is met

If stop condition is not set, the infinite recursions lead to segmentation fault / stack overflow

## Print 1 to N using Recursion
```cpp
void main(int n) {
    f(1, n);
}

void f(int i, int n) {
    if (i>n) return; // end condition
    cout << i << "\n";
    f(i+1, n);
}
```

## Print N to 1 using Recursion
```cpp
void main(int n) {
    f(n);
}

void f(int n) {
    if (n==0) return; // end condition
    cout << n << "\n";
    f(n-1);
}
```

**Time Complexity: O(N)**, we print every number from 1 to N using recursion.  
**Space Complexity: O(N)**, stack space used for recursive calls. 

# Backtracking

Backtracking builds solutions by exploring all options and undoing choices when needed.  
All the recursive functions are executed first until we reach the base case and then printing occurs on the way back (not before the recursive call).  
This way, numbers are printed in reverse order because the print happens after the recursive call during backtracking. 

## Print 1 to N using Backtracking

```cpp
void main(int n) {
    f(n, n);
}

void f(int i, int n) {
    if (i<1) return; // end condition
    f(i-1, n);
    cout << i << "\n";
}
```

## Print N to 1 using Backtracking

```cpp
void main(int n) {
    f(1, n);
}

void f(int i, int n) {
    if (i>n) return; // end condition
    f(i+1, n);
    cout << i << "\n";
}
```

# Parameterised Recursion

Give a parameter variable along with N to the recursive function.

## Sum of N numbers using Recursion

```cpp
void NnumbersSum(int N){
    calculateSum(N, 0);
}
void calculateSum(int n, int sum) {
    if (n<1) {
        cout<<sum<<"\n";
        return;
    } 
    sum+=n;
    calculateSum(n-1, sum);
}
```

# Functional Recursion

Used when the function needs to return the final answer ( not print )

## Sum of N numbers using Functional Recursion

sum(N) = N + sum(N-1)
sum(N-1) = N-1 + sum(N-2) ...
sum(1) = 1 + sum(0) 
sum(0) = 0 -> Base Case

```cpp
void main() {
    cout << calculateSum(7);
}
int calculateSum(int n) {
    if (n==0) {
        return 0;
    } 
    return sum + calculateSum(n-1);
}
```

## Factorial of N using Functional Recursion

```cpp
void main() {
    cout << factorial(7);
}
int factorial(int n) {
    if (n==0) return 1;
    return n * factorial(n-1);
}
```

## Reverse an array

Pseudo Code (using two pointers):  
```cpp
f(l, r) {  
    if (l>=r) return;  
    swap(l, r);
    f(l+1, r-1);  
}  

f(0, n-1) // n is length of array
```

Space complexity is O(1) since the array is reversed in place (no new array created)  

```cpp
void main(int arr[], int n){
    reverse(0, n-1, arr);

    for (int i=0; i<n; i++) {
        cout<<arr[i]<<" ";
    }
    cout<<"\n";
}
void reverse(int l, int r, int arr[]) {
    if (l>=r) return;
    swap(arr[l], arr[r]);
    reverse(l+1, r-1, arr);
}
```

Using Single Pointer:  
Since l + r = n - 1; r = n - l - 1
So we can use a single variable i ( till i<n/2 )

```cpp
void main(int arr[], int n){
    reverse(0, arr, n);

    for (int i=0; i<n; i++) {
        cout<<arr[i]<<" ";
    }
    cout<<"\n";
}
void reverse(int i, int arr[], int n) {
    if (i>=n/2) return;
    swap(arr[i], arr[n-i-1]);
    reverse(i+1, arr, n);
}
```

## Check if a string is palindrome

Check if i and n-i-1 letter is equal, if yes then increment i till i crosses n/2, else return false.

```cpp
void main(string s){
    cout<<check(s, 0)<<"\n";
}
bool check(string s, int i) {
    if (i>=s.size()/2) return true;
    if (s[i]!=s[s.size()-i-1]) return false;
    return check(s, i+1);
}
```

## Fibonacci Series

nth number = n-1 + n-2 number

For Ex) N = 6 
0 1 1 2 3 5 is the fibonacci series up to 6th term.(1 based indexing)  

```cpp
int fib(int n) {
    if (n==1) return 0;
    if (n==2) return 1;
    return fib(n-1) + fib(n-1);
} 00
```

