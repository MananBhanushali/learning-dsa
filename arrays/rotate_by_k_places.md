# Rotate an Array by k places

**Examples**  
Input : nums = [1, 2, 3, 4, 5, 6, 7], k = 2, right  
Output : [6, 7, 1, 2, 3, 4, 5]  

Input : nums = [1, 2, 3, 4, 5, 6], k=2, left  
Output : [3, 4, 5, 6, 1, 2]  

## Brute Force Approach

### Algorithm

**Left Rotation:** 
1. Store the first k elements in a temporary array.
2. Shift the remaining elements to the left by k positions.
3. Copy the k stored elements to the end of the original array.

**Right Rotation:** 
1. Take the last k elements and store them in a temporary array.
2. Shift the first n-k elements to the right by k positions.
3. Copy the k stored elements from the temporary array to the start of the original array.

>[!IMPORTANT]
After n rotations (left or right), the array becomes equal to the original. Hence, **rotating by k places for k>n equals rotating k%n places.**

### Code

**Left Rotation:**  
```cpp
int n, k; cin>>n;
vector<int> a(n);
for (int i=0; i<n; i++) cin>>a[i];
cin>>k;
k=k%n;

vector<int> temp(k); // temp vector to store first k elements
for (int i=0; i<k; i++) temp[i]=a[i]; // copy first k elements to temp

for (int i=k; i<n; i++) a[i-k]=a[i]; // shift other elements left by k places

// put the first k elements stored in temp to the end
for (int i=(n-k); i<n; i++) a[i]=temp[i-(n-k)]; // index 0 of temp goes to n-k of a, 1->n-k+1, 2->n-k+2 and so on

for (int i=0; i<n; i++) cout<<a[i]<<" ";
cout<<"\n";
```

**Right Rotation:** 
```cpp
int n, k; cin>>n;
vector<int> a(n);
for (int i=0; i<n; i++) cin>>a[i];
cin>>k;
k=k%n;

vector<int> temp(k); // temp vector to store last k elements
for (int i=n-k; i<n; i++) temp[i-(n-k)]=a[i]; // copy last k elements to first k elements of temp

for (int i=n-k-1; i>=0; i--) a[i+k]=a[i]; // shift other elements right by k places

// put the last k elements stored in temp to the start
for (int i=0; i<k; i++) a[i]=temp[i];

for (int i=0; i<n; i++) cout<<a[i]<<" ";
cout<<"\n";
```

### Complexity Analysis
Time Complexity : **O(n)**  
Space Complexity: **O(k)** - Extra space used by temp array

## Optimal Approach

### Algorithm

**Left Rotation:**  
1. Reverse the first k elements
2. Reverse the remaining n - k elements
3. Reverse the entire array

**Right Rotation:**  
1. Reverse the entire array
2. Reverse the first k elements
3. Reverse the remaining n - k elements

### Code

**Left Rotation:** 
```cpp
int n, k; cin>>n;
vector<int> a(n);
for (int i=0; i<n; i++) cin>>a[i];
cin>>k;
k=k%n;

reverse(a.begin(), a.begin()+k); // first k elements
reverse(a.begin()+k, a.begin()+n); // last n-k elements
reverse(a.begin(), a.begin()+n); // whole array

for (int i=0; i<n; i++) cout<<a[i]<<" ";
cout<<"\n";
```

**Right Rotation:**  
```cpp
int n, k; cin>>n;
vector<int> a(n);
for (int i=0; i<n; i++) cin>>a[i];
cin>>k;
k=k%n;

reverse(a.begin(), a.begin()+n); // whole array
reverse(a.begin(), a.begin()+k); // first k elements
reverse(a.begin()+k, a.begin()+n); // last n-k elements

for (int i=0; i<n; i++) cout<<a[i]<<" ";
cout<<"\n";
```

### Complexity Analysis
**Time Complexity: O(n)**  
Reverse first k elements - O(k) 
Reverse other n-k elements - O(n-k)
Reverse the whole array - O(n)  
Total is O(2n) so the time complexity has actually increased, but still varies linearly with n  
**Space Complexity: O(1)**

## Resources
[Blog](https://takeuforward.org/data-structure/rotate-array-by-k-elements)  
[Video](https://youtu.be/wvcQg43_V8U?si=LxZD4Cj923HSuG0w&t=485)