# Basic Hashing

Hashing - pre-storing the data once (linear time) and fetching in constant time

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    //precompute:
    int hash[13] = {0}; // size=13 since max query goes from 1-12, and add first element as 0 so that hash[1] gives count of 1
    for (int i = 0; i < n; i++) {
        hash[arr[i]]++; 
    }

    int q;
    cin >> q;
    while (q--) {
        int number;
        cin >> number;
        // fetching:
        cout << hash[number] << endl;
    }
    return 0;
}

/*
Input:
5
1 3 2 1 3
5 
1
4 
2
3
12
Output:
2
0
1
2
0
*/
```

## Character Hashing

### If the string contains only uppercase / only lowercase letters

corresponding value = given character - 'a'

For Ex), if the given character is ‘f’, we will get the value as (‘f’ - ‘a’) = (102-97) = 5.

Here, we can easily observe that the maximum value can be 25.  
So, for character hashing in this case, we need a hash array of size 26. 

And while pre-storing we will do hash[s[i]-’a’] += 1 instead of hash[arr[i]] += 1, and while fetching we will do hash[character-’a’] instead of hash[number]. The rest of the methods will be as same as in the case of number hashing.

### If the string contains both uppercase and lowercase letters

Create hash of size 256. 
Store each character by their ASCII.  
For Ex) 'a' = 97, 'z' = 122

## Maps and Unordered Maps in C++

The size of an array in C++ can only be 1e7 ( if defined globally ) or 1e6 ( if defined in main ).  
For values like 1e9, 1e12 etc, hashmaps are used.  

The value of the elements(keys) not present in the map is automatically 0.  
Since the size of the map is equal to the size of the unique keys, it is more efficient than array hashing.   

Syntax:  
**map <key, value>**   
**unordered_map <key, value>**

Map stores elements in order of their keys, while Unordered Map does not.

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n; cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // precompute:
    map<int, int> mp;
    for (int i = 0; i < n; i++) {
        mp[arr[i]]++;
    }

    int q; cin >> q;
    while (q--) {
        int number; cin >> number;
        // fetch:
        cout << mp[number] << endl;
    }

    // iterate over the map:
    /* for(auto it : mp){ // outputs key, value in sorted order of keys
            cout << it.first << "->" << it.second << endl;
        }
    */

    return 0;
}

/*
Input: 
7
1 2 3 1 3 2 12
5
1 2 3 4 12

Output: 
2
2
2
0
1
*/
```

Maps can also be used in character hashing.  
map <char, int> 

### Time complexity of map and unordered_map

Insertio and retrieval in a **map** take always **O(logN)** time complexity,

**Unordered Map** takes **O(1)** time complexity to perform insertion and retrieval for the best case and the average case. O(N) in the worst case.  

>[!NOTE]
First priority should be always to use unordered_map and then map. If unordered_map gives a time limit exceeded error(TLE), we will then use the map.

**The time complexity in the worst case is O(N) because of the internal collision.**