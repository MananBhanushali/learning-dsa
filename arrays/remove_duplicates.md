# Remove Duplicates from Sorted Array

## Brute Force Approach

### Algorithm

1. Iterate through the array and insert each element in set
2. Keep an index count, iterate through the set, set index element of array to set element and increment index
3. Print index + 1 (Total number of unique elements = index+1)

### Code
```cpp
vector<int> a = {1, 1, 2, 2, 2, 3, 3};
set<int> st;

for (int i=0; i<a.size(); i++) st.insert(a[i]); 

int index=0;
for (auto it:st) { a[index]=it; index++; }

cout<<index;
```

### Time Complexity
o(n) to iterate through array, o(logn) to insert in set, overall **O(nlogn)**

## Optimal Approach

### Algorithm ( Two Pointers )
- Keep the first pointer at the first position, which will always be part of the final unique list.
- Iterate the second pointer, if the current item at the second pointer is the same as the last kept one, skip it because it’s a duplicate.
- If it’s different, place it right after the first pointer to keep all unique values grouped at the front. Then increment the first pointer
- Continue incrementing the second pointer like this until every element in the list has been checked. Finally Print first pointer + 1 ( total number of distinct elements )

### Code
```cpp
vector<int> a = {1, 1, 2, 2, 2, 3, 3};
int i=0;

for (int j=0; j<a.size(); j++) {
    if (a[j]!=a[i]) { a[i+1]=a[j]; i++; }
}
cout<<i+1<<"\n";
```

### Time Complexity
**O(n)** since only one pass of array is required


## Resources
[Blog](https://takeuforward.org/data-structure/remove-duplicates-in-place-from-sorted-array)  
[Video](https://youtu.be/37E9ckMDdTk?si=XGZV9u0xWOoNSVx9&t=1978)