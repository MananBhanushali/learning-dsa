# Longest Subarray with Given Sum K

**Examples**  
Input: nums = [10, 5, 2, 7, 1, 9], k = 15   
Output: 4 ( Subarray [5, 2, 7, 1] )

Input: nums = [-3, 2, 1], k = 6   
Output: 0    

## Brute Force Approach - Two Pointers

### Algorithm

1. Starting index of subarray i goes from 0 to n-1
2. Ending index j goes from i to n-1 inside the i loop
3. Calculate the sum of each subarray from i to j, either using another loop inside ( n^3 complexity ), or by adding the just new element to the previous sum ( n^2 complexity ). 
4. If the sum equals k, we consider its length, which is (j - i + 1) if it is greater than the current max length.

### Code
```cpp
int n, k; cin>>n>>k; vector<int> a(n);
int maxLength=0;
for (int i=0; i<n; i++) cin>>a[i];

for (int startIndex = 0; startIndex < n; startIndex++) { 
    for (int endIndex = startIndex; endIndex < n; endIndex++) { 
        // add all the elements of subarray
        int currentSum = 0;
        for (int i = startIndex; i <= endIndex; i++) {
            currentSum += nums[i];
        }

        if (currentSum == k)
            maxLength = max(maxLength, endIndex - startIndex + 1);
    }
}
cout<<maxLength<<"\n";
```

### Complexity Analysis
**Time Complexity : O(n^3)**

**Space Complexity : O(1)**

## Better Approach - Prefix Sum

>[!NOTE]
**This is the optimal approach if the array contains positive, negative as well as zeros.**

### Algorithm
1. Store the sum till the i'th element in a map
2. Store the maxLen and sum from start till the current element 
3. If sum from start to the current element is directly equal to k, update maxLen i+1 is greater ( number of elements till i'th index from start )
4. Else, check if (sum-k) exists in the map, if it does then length = i - index in map. Update the maxLen if this length is greater. 
5. Add the sum till current element to the map with the value of the current index. 

For example, if the sum till current index n is 8, k is 3, then check if 5 exists in the map, if it does exist and the index till which the sum is 5 is i, then the length of the subarray with sum 3 is n-i

>[!IMPORTANT]
If the array also contains zeros, then before adding the current sum, check if the sum key already exists. Only update it if it doesn't exist, since we want the longest subarray of sum k, we need shortest subarray of sum (sum-k).

For example, if the array is [2, 0, 0, 3], we need to make sure that the map stores the sum-index pair (2, 0) and not (2, 2). This way, the longest length of subarray becomes 3 and not 1.

### Code
```cpp
int n, k; cin>>n>>k;
map<int, int> preSum; vector<int> a(n);
int sum=0, maxLen=0;
for (int i=0; i<n; i++) cin>>a[i];

for(int i=0; i<n; i++) {
    sum+=a[i]; // sum from start till current index

    if (sum==k) { // number of elements in subarray = i+1 if sum from 0'th to i'th index is k
        maxLen = max(maxLen, i+1); 
    }

    // if a previous subarray of sum (currentSum-k) is found, then the length of subarray of sum k will be i-that index
    // for example, current sum 7 at index 4, k=5, we find sum 2 at index 1, hence the length of subarray with sum 5 is 4-1=3
    if (preSum.find(sum-k)!=preSum.end()) { 
        maxLen = max(maxLen, i-preSum[sum-k]);
    }

    // before adding current sum, check if it doesn't exist ( if it does, don't update ) incase array has zeros
    if (preSum.find(sum)==preSum.end()) preSum[sum]=i; 
}

cout<<maxLen<<"\n";
```

### Complexity Analysis

**Time Complexity : O(nlogn)** - n times O(logn) for iterating through the array and inserting in ordered map. Incase of unordered map, insertion takes O(1) but in worst case ( collisions ), insertion will take O(n).

**Space Complexity : O(n)** - Size of hashmap in worst case ( each index having different sum )

## Optimal Approach - Sliding Window and Greedy

### Algorithm
1. Two pointers left and right represent the start and end of the current subarray.
2. A sum variable is used to keep track of the sum of the elements in the current window between left and right.
3. The right pointer expands the window by including new elements, increasing the sum.
4. If the sum of the window exceeds k, the left pointer shrinks the window by removing elements from the start until the sum is less than or equal to k.
5. If the sum of the current window equals k, the maximum length of such a subarray is updated.
6. The process continues until the right pointer traverses the entire array.
Finally, the maximum length of the subarray with sum k is returned as the result.

### Code

```cpp
int n, k; cin>>n>>k; vector<int> a(n);
int sum=0, left=0, right=0, maxLen=0;
for (int i=0; i<n; i++) cin>>a[i];

for (right=0; right<n; right++) {
    sum+=a[right];
    if (sum==k) maxLen=max(maxLen, right-left+1);
    while (left<=right && sum>k) { sum-=a[left]; left++; }
}

cout<<maxLen<<"\n";
```

### Complexity Analysis
**Time Complexity: O(N)** - The algorithm traverses the array once with two pointers, making it linear in time complexity.

**Space Complexity: O(1)** - as it uses a constant amount of space.

## Resources
[Blog](https://takeuforward.org/data-structure/longest-subarray-with-given-sum-k)  
[Video](https://www.youtube.com/watch?v=frf7qxiN2qU)   

