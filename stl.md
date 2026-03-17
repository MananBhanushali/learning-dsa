# STL and Basic Functions in C++

STL stands for standard template library.  
It contains a lot of pre-defined templates in terms of containers and classes which makes it very easy for programmers to implement different data structures easily without having to write complete code and worry about space-time complexities.  

- [STL and Basic Functions in C++](#stl-and-basic-functions-in-c)
  - [Pairs](#pairs)
  - [Vectors](#vectors)
    - [Accessing elements of vector](#accessing-elements-of-vector)
    - [Most used functions in Vector](#most-used-functions-in-vector)
  - [Lists](#lists)
    - [Functions in List](#functions-in-list)
  - [Stack](#stack)
    - [Functions in Stack](#functions-in-stack)
  - [Queue](#queue)
    - [Functions in Queue](#functions-in-queue)
  - [Priority Queue](#priority-queue)
    - [Functions in Priority Queue](#functions-in-priority-queue)
  - [Deque](#deque)
    - [Functions in Deque](#functions-in-deque)
  - [Set](#set)
    - [Functions in Set](#functions-in-set)
  - [Multiset](#multiset)
    - [Functions in Multiset](#functions-in-multiset)
    - [Unordered Set and Multiset](#unordered-set-and-multiset)
  - [Maps](#maps)
    - [Functions in map](#functions-in-map)
    - [Multimap and Unordered Map](#multimap-and-unordered-map)
- [Basic Functions](#basic-functions)
  - [sort()](#sort)
    - [Custom Comparators](#custom-comparators)
  - [\_\_builtin\_popcount()](#__builtin_popcount)
  - [next\_permutation()](#next_permutation)
  - [min\_element() and max\_element()](#min_element-and-max_element)

## Pairs
A part of \<utility> library.  
It is used to store 2 objects.

To Define a Pair:  
**pair<datatype1, datatype2> name = {obj1, obj2};**

**To access the elements in a pair, pair.first, pair.second can be used.**

For Ex.
```cpp
pair<int, int> p = {1, 3};
cout << p.first << " " << p.second << "\n";
// prints 1 3
```

Nesting can also be done
```cpp
pair<int, pair<int, int>> p = {1, {2, 3}};
cout << p.first << " " << p.second.first << " " << p.second.second << "\n";
// prints 1 2 3
```

Declaring a pair array ( All elements in the array must be pairs)
```cpp
pair<int, int> arr[] = { {1, 4}, {2, 3}, {6, 7}};
cout << arr[2].second << "\n";
// prints 7
```

## Vectors
Vectors are basically **dynamic arrays that have the ability to change size whenever elements are added or deleted from them.**  
Vector elements can be easily accessed and traversed using iterators.  
A vector stores elements in contiguous memory locations.

To Define a vector:  
**vector\<datatype> name;**  
Datatype can be anything, like int, char, string, pair etc

For Ex.
```cpp
vector<int> v;
v.push_back(1); // v = {1}

vector<pair<int, int>> v2;
v.push_back({6, 7}); // v2 = { {6, 7} }
```

To define a vector with default values, use
```cpp
vector<int> v(5, 20); // creates a vector v with 5 instances of 20 {20, 20, 20, 20}
vector<int> v2(10); // creates a vector of size 10
vector<int> v3(v2); // create v3 which is a copy of v2
```

>[!NOTE]
Even after defining the size of the vector during initialization, more elements can still be added

### Accessing elements of vector

Elements of vector can be accessed just like arrays - using **vector\[index]**

Another Method is using iterators.
```cpp
vector<int> v = {20, 10, 15, 6, 7};
vector<int>::iterator it = v.begin(); // iterator now contains address of first element of v 

cout << *(it); // using *() to print the content of memory location stored in the iterator
it++; // increment iterator ( point to next memory location )
```

**Instead of writing vector<int>::iterator it, we can just use auto it, which automatically assigns the datatype to the variable.**

Another Method is using for each loop.
```cpp
for (int element : v) {
  cout << element << " ";
}
```

### Most used functions in Vector

**size()** - returns the size of the vector
v1.size();

**empty()** - to check if the vector is empty or not.
v1.empty();

**begin()** - it returns an iterator pointing to the first element of the vector.  

**end()** - it returns an iterator pointing to the element theoretically after the last element of the vector.  

**push_back()** - it accepts a parameter and insert the element passed in the parameter in the vectors, the element is inserted at the end.  

**insert()** - it is used to insert an element at a specified position.
```cpp
auto it= v1.begin();
v1.insert(it,5); //inserting 5 at the beginning

v1.insert(it+1, 2, 100) // insert two 100s at 2nd and 3rd position ( .begin() + 1 )
```

**erase()** - it is used to delete a specific element

```cpp
vector<int> v1;
auto it= v1.begin();
v1.erase(it); // erasing the first element
v1.erase(it+1, it+3); // erase the second and third element ( index it+3 excluded )
```

**pop_back()** - it deletes the last element and returns it to the calling function.

**clear()**- deletes all the elements from the vector.  
v1.clear();

**front()** - it returns a reference to the first element of the vector.  
v1.front();

**back()** - it returns a reference to the last element of the vector.  
v1.back();

**swap()** - swaps both the vectors.  
v1.back(v2);


```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
  vector <int> v;

  for (int i = 0; i < 10; i++) {
    v.push_back(i); //inserting elements in the vector
  }

  cout << "the elements in the vector: ";
  for (auto it = v.begin(); it != v.end(); it++)
    cout << * it << " ";

  cout << "\nThe front element of the vector: " << v.front();  //The front element of the vector
  cout << "\nThe last element of the vector: " << v.back(); //The last element of the vector
  cout << "\nThe size of the vector: " << v.size();  //The size of the vector
  cout << "\nDeleting element from the end: " << v[v.size() - 1];  //Deleting element from the end
  v.pop_back();

  cout << "\nPrinting the vector after removing the last element:" << endl;
  for (int i = 0; i < v.size(); i++)
    cout << v[i] << " ";

  cout << "\nInserting 5 at the beginning:" << endl;
  v.insert(v.begin(), 5);
  cout << "The first element is: " << v[0] << endl;
  cout << "Erasing the first element" << endl;
  v.erase(v.begin());  //Erasing the elements 
  cout << "Now the first element is: " << v[0] << endl;

  if (v.empty())
    cout << "\nvector is empty";  //If empty then print empty else print not empty
  else
    cout << "\nvector is not empty" << endl;  //vector is not empty

  v.clear();
  cout << "Size of the vector after clearing the vector: " << v.size();  //Return the size of the vector
}
```

## Lists
A list in STL is a contiguous container that allows the inserting and erasing of elements in constant time and iterating in both directions.

Syntax:  
**list<object_type> variable_name;**

### Functions in List
**push_back()** – to insert an element at the end of the list.

**push_front()** – to insert an element at the front of the list.

**pop_back()** – deletes the last element of the list.

**pop_front()** – deletes the front element of the list.

**front()** – it gives a reference to the first element of the list.

**back()** – it gives a reference to the last element of the list.

**reverse()** – reverse the list.

**sort()** – sorts the list in ascending order.

**size()** – returns the number of elements on the list.

**empty()** – to check if the list is empty or not.

**begin()** – it refers to the first element of the list.

**end()** – it refers to the theoretical element after the last element of the list.

**clear()** – to delete all the elements of the list.

**erase()** – to delete a single element or elements between a particular range.

```cpp
#include<bits/stdc++.h>
using namespace std;
void printlist(list<int> li)
{
    list<int>::iterator it;
    for(it=li.begin();it!=li.end();it++)
    {
        cout<<*it<<" ";
    }
    cout<<endl;
}
int main()
{
    list<int> li;
    li.push_back(10);
    li.push_back(20);
    li.push_front(30);
    li.push_front(40);
    li.push_front(50);
    
    cout<<"The elements in the list are: ";
    printlist(li);
    cout<<"Reversing the list: ";
    li.reverse();
    printlist(li);
    cout<<"Sorting the list: ";
    li.sort();
    printlist(li);
    cout<<"The size of the list is: "<<li.size()<<endl;
    cout<<"The first element in the list: "<<li.front()<<endl;
    cout<<"Deleting the first element"<<endl;
    li.pop_front();
    printlist(li);
    cout<<"The last element of the list: "<<li.back()<<endl;
    cout<<"Deleting the last element"<<endl;
    li.pop_back();
    printlist(li);
    
}
/*
Output:
The elements in the list are: 50 40 30 10 20
Reversing the list: 20 10 30 40 50
Sorting the list: 10 20 30 40 50
The size of the list is: 5
The first element in the list: 10
Deleting the first element
20 30 40 50
The last element of the list: 50
Deleting the last element
20 30 40
*/
```

## Stack

**Last In First Out**

Syntax:  
**stack<object_type> variable_name;**

### Functions in Stack

**push()** – to insert an element in the stack.

**pop()** – deletes the last element of the stack.

**top()** – returns the element at the top of the stack.

**emplace()** – to insert an element in the stack.

**size()** – returns the number of elements on the stack.

**empty()** – to check if the stack is empty or not.

**swap()** - swap the stack

```cpp
stack<int> s;
s.push(110);
s.push(220); // {110, 220}
s.top(); // 220
s.pop(); // {110}
s.size(); // 1
s.empty(); // false

stack<int> s2;
s.swap(s2);
```

## Queue

**First in First Out**

Syntax:
**queue<object_type> q;**

### Functions in Queue
**push()** - to insert an element in the queue.  

**pop()** - deletes the first element of the queue.  

**front()** - returns a reference to the first element of the queue.  

**back()** - returns a reference to the last element of the queue.  

**emplace()** - to insert an element in the queue.  

**size()** - returns the number of elements on the queue.  

**empty()** - to check if the queue is empty or not.  

```cpp
queue<int> q
q.push(110);
q.push(220); // {110, 220}
q.front(); // 110
q.back(); // 220
q.pop(); // {220}
q.size(); // 2
q.empty(); // false
```

## Priority Queue

**Queue but the lexicographically largest stays at top ( first to remove ) (like descending order)**

Syntax:
**priority_queue<object_type> pq;**

### Functions in Priority Queue
**push()** - to insert an element in the priority queue.  

**pop()** - deletes the first element of the priority queue.  

**front()** - returns a reference to the first element of the priority queue.  

**back()** - returns a reference to the last element of the priority queue.  

**emplace()** - to insert an element in the priority queue.  

**size()** - returns the number of elements on the priority queue.  

**empty()** - to check if the priority queue is empty or not.  

```cpp
priority_queue<int> pq
pq.push(5); // {5}
pq.push(2); // {5, 2}
pq.push(8); // {8, 5, 2}
pq.push(10); // {10, 8, 5, 2}
pq.top(); // 10 
pq.pop(); // {8, 5, 2}
pq.size(); // 3
```

>[!IMPORTANT]
For minimum heap (priority queue storing minimum at top like ascending order), use
**priority_queue<int, vector\<int>, greater\<int>> pq;**

## Deque 
Double Ended Queue which is also called Deque is a type of queue data structure in which the insertion and deletion of elements can be either in front or rear. 

Syntax:  
**deque<object_type> variable_name;**

### Functions in Deque
**push_back()** – to insert an element at the end of the deque.

**push_front()** – to insert an element at the front of the deque.

**pop_back()** – deletes the last element of the deque.

**pop_front()** – deletes the front element of the deque.

**front()** – it gives a reference to the first element of the deque.

**back()** – it gives a reference to the last element of the deque.

**size()** – returns the number of elements on the deque.

**empty()** – to check if the deque is empty or not.

## Set
A set stores unique elements in a sorted order. Every operation on a set takes O(n) in the worst case.

Syntax:  
**set\<int> st;**

### Functions in Set
**insert()** – to insert an element in the set.  

**begin()** – return an iterator pointing to the first element in the set.  

**end()** – returns an iterator to the theoretical element after the last element.  

**count()** – returns true or false based on whether the element is present in the set or not.  

**clear()** – deletes all the elements in the set.  

**find()** – to search an element in the set.  

**erase()** – to delete a single element or elements between a particular range.  

**size()** – returns the size of the set.  

**empty()** – to check if the set is empty or not.  


cbegin() – it refers to the first element of the set.
cend() – it refers to the theoretical element after the last element of the set.
rbegin() – it points to the last element of the set.
rend() – it points to the theoretical element before the first element of the set.
bucket_size() – gives the total number of elements present in a specific bucket in a set.
emplace() – to insert an element in the set.
max_size() – the maximum elements a set can hold.
max_bucket_count() – to check the maximum number of buckets a set can hold.

```cpp
set<int> s;
s.insert(1);
s.insert(2);
s.insert(3);
s.insert(4);
s.insert(2); // {1, 2, 3, 4} - stores in sorted order
s.begin(); // returns iterator pointing to 1
s.end(); 
s.count(2); // returns 1 if present ( since set only has unique occurence ), 0 if not
s.find(2)!=s.end(); // returns true (st.find returns iterator pointing to 2 if 2 in set, else returns iterator pointing to s.end
s.clear();
s.erase(3); // removes 3, iterator can also be given as the argument
s.erase(it_first, it_last); // erase from it_first to it_last
```

## Multiset
A multiset is a container similar to a set, but it allows duplicate elements and stores them in sorted order.

Syntax: 
**multiset<datatype> variable_name;**

### Functions in Multiset
**insert()** - to insert an element

**begin()** - returns iterator to first element

**end()** - returns iterator after last element

**count()** - count occurrences of an element

**erase()** - delete all occurences of a single element or range

**clear()** - deletes all elements

**find()** - search an element

**size()** - returns number of elements

**empty()** - checks if multiset is empty

```cpp
multiset<int> ms;
ms.insert(1);
ms.insert(1);
ms.insert(2); // {1, 1, 2}
ms.count(1); // returns 2
if (ms.find(2) != ms.end()) // check if 2 exists , if not .find() returns .end()
    cout << "true" << endl;
ms.erase(1); // erases all 1s
// to delete a only the first occurence of 1, use .find()
ms.erase(ms.find(1));
```

### Unordered Set and Multiset
Unordered set stores unique elements in no particular order. Every operation on an unordered set takes O(1) complexity in the average case and takes O(n) in the worst case.  

An unordered_multiset is just like an unordered set the only difference is it can store duplicate elements in it.  

## Maps
Maps are associative containers where each element consists of a unique key and a mapped value. Two mapped values cannot have the same key value.  

>[!IMPORTANT]
**The keys are stored in a sorted manner (like a set).**  
**The key and values are stored in a pair**

Syntax:
**map<key_datatype, value_datatype> variable_name;**

### Functions in map
**insert()** – to insert a key-value pair in the map.

**begin()** – return an iterator pointing to the first element in the map.

**end()** – returns an iterator to the theoretical element after the last element.

**clear()** – deletes all the elements in the map.

**find()** – to search for an element in the map.
map<int,int> mp;
mp.insert({1,10});
mp.insert({2,20});
if(mp.find(2)!=mp.end())
cout<<"true"<<endl;
**erase()** – to delete a single element or elements between a particular range.
mp.erase(key);
mp.erase(iterator position);
mp.erase(iterator position 1, iterator position 2);
**size()** – returns the number of elements on the map.

**empty()** – to check if the map is empty or not.


```cpp
map<int,int> mp;
mp.insert({2,20});
mp.insert({1,10}); // [ {1, 10}, {2, 20} ] - sorted by keys

// other ways to insert into a map
mp[3] = 30;
mp.emplace({4, 40});

// accessing elements of map
cout<<mp[4]; // prints 40
cout<<mp[5]; // does not exist, hence prints 0

auto it = mp.find(3); // gives iterator to {3, 30} pair, if does not exist then points to .end()
cout<<*(it).second; // will print 30

// iterating through a map
for (it : mp) { // it will store key-value pair, .first will have key, .second will have value
  cout << it.first << " " << it.second << "\n";
}
// .begin() , .end() can also be used to iterate
```

### Multimap and Unordered Map
**Multimap** - Can store multiple keys, stores in sorted order
**Unordered Map** - Stores only unique keys, unsorted order

# Basic Functions

## sort()

Syntax:  
**sort(begin, end);**

Examples:
```cpp
int arr[] = {4,2,1};
sort(arr, arr+3);  // Sort from arr to arr+3 

vector<int> vec = {4,2,1};
sort(vec.begin(), vec.end());  // Sort the vector
```

To Sort in Descending order, the **greater<>** comparator can be used. The comparator tells the sort function how to compare elements.

For Ex:
```cpp
vector<int> vec = {4,2,1};
sort(vec.begin(), vec.end(), greater<int>);  // Sort in Descending Order
```

### Custom Comparators
A comparator is just **a function that takes two elements as input and returns a boolean value**, so in order to sort a data structure in a specific way, a custom function which accepts it as inputs and returns true/false by custom logic can be created and used as comparator

For Ex:   
arr = { {2, 1}, {3, 2}, {4, 1} }   
Sort by ascending order of second element,  
If second element is same, sort by descending order of first element  

To Design such a sorting comparator, 
```cpp
#include <bits/stdc++.h>
using namespace std;

bool comp(pair<int, int> p1, pair<int, int> p2) // elements of array are pairs, so accept them as input
  if (p1.second < p2.second) {
    return true; // true if already sorted, false if not
  } else if (p1.second == p2.second) { if (p1.first>p2.first) return true; }
  else return false;
```

## __builtin_popcount()

It counts the number of set bits.  
Counting set bits in an integer means finding the number of 1’s in its binary representation. For example, the binary form of 7 is 111, which has 3 set bits.

Naive Solution:  
```cpp
int count_setbits(int N) { 
    int cnt = 0;

    while (N > 0) {
        cnt += (N & 1);  // check last bit
        N = N >> 1;      // right shift
    }

    return cnt;
}
```

How it Works?
Keep checking the least significant bit using bitwise AND with 1.
Right shift the number by 1 to move to the next bit.
Continue until the number becomes 0.
Increment count for each set bit encountered.

Using __builtin_popcount():  
Syntax:   
**__builtin_popcount(int num);**

**For Long Long Integers:**  
If the number is of type long long and does not fit into an int, we use **__builtin_popcountll()**.  

Example:
```cpp
int main() {
    int n = 7;
    cout << __builtin_popcount(n); // prints 3

    long long lln = 77777777777777;
    cout << __builtin_popcountll(n); // prints 23
    return 0;
}
```

## next_permutation()
Overwrites and gives the next permutation of the current string.  
For Ex: if s="123", next permutations ( sorted ) will be 132, 213, 231, 312, 321  
If s="231", next permutations will only be 312, 321

Hence to get all the permutations of a given string, make sure to sort the string first so that it starts from the first permutation ( in this case, 123 )

For Ex:
```cpp
string s="213";
sort(s.begin(), s.end());

do {
  cout << s << "\n";
} while (next_permutation(s.begin(), s.end()));
```

When it is at the last permutation, next_permutation() will return null

## min_element() and max_element()

*min_element(start_i, end_i) and *max_element(start_i, end_i) return the min and max element respectively.

without the *, it returns the address

```cpp
vector<int>v {4,2,5,9,1};
cout << *min_element(v.begin(),v.end());
cout << *max_element(v.begin(),v.end());
```