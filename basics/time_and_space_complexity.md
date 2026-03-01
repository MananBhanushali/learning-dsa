# Time and Space Complexity

Time complexity helps to judge different codes and also helps to decide which code is better.  

Time complexity does not refer to the time taken by the machine to execute a particular code. 

**The rate at which the time, required to run a code, changes with respect to the input size, is considered the time complexity.**

To represent the time complexity, we generally use the Big O notation.

Let’s understand this using the following example:
```cpp
for (int i=1;i<=5;i++) {
    cout<<i;
}
```

The time complexity for this code will be nothing but the number of steps, this code will take to be executed. So, if we write this in terms of Big O notation, it will be like O(no. of steps).  
This flow will continue until the value of i becomes greater than 5(i.e. 6). In a broader sense, we can observe that the ‘for loop’ will run 5 times.  
Now, if we write N instead of 5, the number of steps will be then N*3 = 3N and the time complexity will be O(3*N).  

Here come the three rules, that we are going to follow while calculating the time complexity:  

- [Always calculate the time complexity for the worst-case scenario:](#always-calculate-the-time-complexity-for-the-worst-case-scenario)
- [Avoid including the constant terms:](#avoid-including-the-constant-terms)
- [Avoid the lower values:](#avoid-the-lower-values)

### Always calculate the time complexity for the worst-case scenario:

**Best Case:** This term refers to the case where the code takes the least amount of time to get executed.   
**Worst Case:** This term refers to the case where the code takes the maximum amount of time to get executed.   
**Average Case:** This term is pretty self-explanatory. This is basically the case between the best and the worst.  

Now, as we always want that our system serves the maximum number of clients, we need to calculate the time complexity for the worst-case scenario. With this, we can actually judge the robustness of any code or any system.

### Avoid including the constant terms:

Let’s understand this rule considering the time complexity: O(4N3 + 3N2 + 8). Now, if we consider the value of N as 10^5 the time complexity will be like this:  O(4*10^15 + 3*10^10 + 8). In this case, the constant term 8 is very less significant in terms of changing the time complexity with different values of N. That is why we should avoid the constant terms while calculating the time complexity.  

### Avoid the lower values:

Now, in the previous example, the given time complexity is O(4N3 + 3N2 + 8) and we have reduced it to O(4N3 + 3N2). Here, we can clearly observe if the value of N is a large number, the second term i.e. 3N2 will also be a less significant term. For example, if the value of N is 105 then the term 3*10^10 becomes less significant with respect to 4*10^15. So, we can also avoid the lower values and the final time complexity will be O(4N3 ). 

Note: A point to remember is that we can actually ignore the constant coefficients as well. For example, considering the time complexity O(4N^3 ) as O(N^3 ) is also correct.
