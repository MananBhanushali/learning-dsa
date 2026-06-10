# Find the Second Largest Element in Array

## Brute Force Approach

### Algorithm
1. Sort the array in ascending order.
2. The element at the second index from the end (index length-2) is the second largest element(if it is not equal to the last element).

### Code
```cpp
vector<int> a = {1, 4, 2, 7, 5};
sort(a.begin(), a.end());
int largest=a[a.size()-1]; int secondLargest=-1;

for (int i=a.size()-2; i>=0; i--) { // start from second last element, last element already stored in largest
    if (a[i]!=largest) { secondLargest = a[i]; break; }
}
cout<<secondLargest<<"\n";
```

### Time Complexity
O(nlogn) for sorting the array, O(n) for for loop, overall **O(nlogn)**

## Better Approach

### Algorithm
1. Find largest element by iterating through every element ( O(n) )
2. set secondLargest to -1, iterate through every element and update if greater than previous value and also not equal to largest

### Code
```cpp
vector<int> a = {1, 4, 2, 5, 6, 7};
int largest=-1; int secondLargest=-1;

for (int i=0; i<a.size(); i++) { // find largest
    if (a[i]>largest) largest=a[i];
}

for (int i=0; i<a.size(); i++) { // find second largest
    if (a[i]>secondLargest && a[i]!=largest) secondLargest=a[i];
}
cout<<secondLargest<<"\n";
```

### Time Complexity
**O(2n)** - one pass through for largest, one for second largest

## Optimal Approach

### Algorithm
1. Set largest to first element, secondLargest to -1 or INT_MIN
2. Iterate from second element to last
3. If element greater than largest, move largest -> secondLargest and element -> largest and continue
4. If element greater than secondLargest but smaller than largest, just replace secondLargest and continue

### Code
```cpp
vector<int> a = {1, 4, 2, 5, 6, 7};
int largest=a[0]; int secondLargest=INT_MIN;

for (int i=0; i<a.size(); i++) { 
    if (a[i]>largest) { secondLargest=largest; largest=a[i]; }
    else if (a[i] > secondLargest) secondLargest=a[i]; 
}
cout<<secondLargest<<"\n";
```

### Time Complexity
**O(n)** since only one pass through the array is required
 
## Resources
[Blog](https://takeuforward.org/data-structure/find-second-smallest-and-second-largest-element-in-an-array)  
[Video](https://youtu.be/37E9ckMDdTk?si=5M2lWOckxGjvbi9W&t=816)