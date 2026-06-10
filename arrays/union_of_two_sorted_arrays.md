# Union of Two Sorted Arrays

**Examples:**  
Input: n = 5, m = 5, arr1[] = {1,2,3,4,5}, arr2[] = {2,3,4,4,5}
Output: {1,2,3,4,5}

Input: n = 10, m = 7, arr1[] = {1,2,3,4,5,6,7,8,9,10}, arr2[] = {2,3,4,4,5,11,12}  
Output: {1,2,3,4,5,6,7,8,9,10,11,12}

## Brute Force Approach - Using Set

### Algorithm

1. Initialize an empty set.
2. Insert all elements from the first array into set.
3. Insert all elements from the second array into set.
4. Convert the set into a list/array to get the result.
5. In C++, set is already sorted

### Code

```cpp
int n, m; 
cin>>n; vector<int> arr1(n);
for (int i=0; i<n; i++) cin>>arr1[i];
cin>>m; vector<int> arr2(m);
for (int i=0; i<m; i++) cin>>arr2[i];

set<int> st;

for (int i = 0; i < n; i++) st.insert(arr1[i]);
for (int i = 0; i < m; i++) st.insert(arr2[i]);

vector<int> ans(st.begin(), st.end()); // set to vector
for (int i=0; i<ans.size(); i++) cout<<ans[i]<<" ";
```

### Complexity Analysis
**Time Compleixty : O( (m+n)log(m+n) )**  
Inserting an element in a set takes logN time, where N is no of elements in the set. At max set can store m+n elements {when there are no common elements and elements in arr,arr2 are distinct}. So Inserting m+n th element takes log(m+n) time. Upon approximation across inserting all elements in worst, it would take O( (m+n)log(m+n) ) time.

Using HashSet also takes the same time, On average insertion in unordered_set takes O(1) time but sorting the union vector takes O((m+n)log(m+n))  time. Because at max union vector can have m+n elements.

**Space Complexity : O(m+n)** for set at worst ( + O(m+n) creating new vector for returning the answer )

## Optimal Approach - Using Two Pointers

### Algorithm
1. Initialize two pointers at the start of both arrays.  
2. While neither pointer has reached the end:  
If element pointed by first pointer is smaller and not duplicate, move first pointer.  
If element pointed by second pointer is smaller and not duplicate, move second pointer.  
If both elements are equal and not duplicate, add one to result, move both pointers.  
1. After exiting loop, append remaining elements from either array, skipping duplicates.

### Code

```cpp
int n1, n2; 
cin>>n1; vector<int> arr1(n1);
for (int i=0; i<n1; i++) cin>>arr1[i];
cin>>n2; vector<int> arr2(n2);
for (int i=0; i<n2; i++) cin>>arr2[i];

vector<int> unionArr;
int i=0; int j=0;
while (i<n1 && j<n2) { // both arrays have elements left
    if (arr1[i] <= arr2[j]) {
        // check if last element of union arr is same as the smaller element ( duplicate ), if not only then add to union arr
        if ( unionArr.size()==0 || unionArr.back()!=arr1[i] ) unionArr.push_back(arr1[i]);
        i++; // increment the i pointer in both cases ( either the element was added, or it was duplicate )
    } else {
        if ( unionArr.size()==0 || unionArr.back()!=arr2[j] ) unionArr.push_back(arr2[j]);
        j++;
    }
}
while (i<n1) {
    if ( unionArr.size()==0 || unionArr.back()!=arr1[i] ) unionArr.push_back(arr1[i]);
    i++;
} 
while (j<n2) {
    if ( unionArr.size()==0 || unionArr.back()!=arr2[j] ) unionArr.push_back(arr2[j]);
    j++;
}

for (int i=0; i<unionArr.size(); i++) cout<<unionArr[i]<<" ";
```

### Complexity Analysis

**Time Complexity : O(m+n)** Because at max i runs for n times and j runs for m times, when there are no common elements in arr1 and arr2 and all elements in arr1, arr2 are distinct. 

**Space Complexity : O(m+n)** Space required for returning the answer, else O(0) since no extra data structure is used.

## Resources
[Blog](https://takeuforward.org/data-structure/union-of-two-sorted-arrays)  
[Video](https://youtu.be/wvcQg43_V8U?si=48Z1WPZf9cmu78TW&t=2585)   