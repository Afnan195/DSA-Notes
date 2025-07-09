# Concept

[geeks for geeks - for concepts](https://www.geeksforgeeks.org/dsa/hashing-data-structure/)

## 1. unordered_set example

```c++
#include <iostream>
#include <unordered_set>
using namespace std;

int main() {
    // Step 1: Create an unordered_set of integers
    unordered_set<int> s;

    // Step 2: Insert elements
    s.insert(10);
    s.insert(20);
    s.insert(30);
    s.insert(20);  // Duplicate, will be ignored automatically

    // Step 3: Print the elements
    cout << "Set elements: ";
    for (int x : s) {
        cout << x << " ";
    }
    cout << endl;
    // Note: Order is not guaranteed (unordered_set)

    // Step 4: Check if an element is present using count()
    int x = 20;
    if (s.count(x)) {
        cout << x << " is present in the set" << endl;
    } else {
        cout << x << " is NOT present in the set" << endl;
    }

    // Step 5: Remove an element using erase()
    s.erase(20); // Removes 20 from the set

    // Step 6: Use find() to get an iterator to an element
    auto it = s.find(30); // Returns iterator to 30 if found, else s.end()
    if (it != s.end()) {
        cout << "Found element: " << *it << endl;
    } else {
        cout << "Element not found" << endl;
    }

    // Step 7: Try to find a removed element
    if (s.find(20) == s.end()) {
        cout << "20 is no longer in the set" << endl;
    }

    // Step 8: Final set state
    cout << "Final set: ";
    for (int val : s) {
        cout << val << " ";
    }
    cout << endl;

    return 0;
}
```

## 2. unordered_map example

```c++
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    // Step 1: Create an unordered_map
    unordered_map<int, string> m; // Key: int, Value: string

    // Step 2: Insert elements into the map
    m[1] = "Apple";
    m[2] = "Banana";
    m[3] = "Cherry";
    m[2] = "Blueberry";  // Overwrites "Banana" with "Blueberry"

    // Step 3: Print all key-value pairs
    cout << "Map contents:" << endl;
    for (auto pair : m) {
        cout << "Key: " << pair.first << ", Value: " << pair.second << endl;
    }
    // Note: Order is not guaranteed (unordered_map)

    // Step 4: Access value by key
    cout << "Value at key 1: " << m[1] << endl;

    // Step 5: Check if a key exists using count()
    int key = 4;
    if (m.count(key)) {
        cout << "Key " << key << " is present with value: " << m[key] << endl;
    } else {
        cout << "Key " << key << " is NOT present in the map" << endl;
    }

    // Step 6: Insert using insert() method
    m.insert({4, "Dates"});  // Insert key=4 with value="Dates"

    // Step 7: Remove a key using erase()
    m.erase(3); // Removes the key 3 (Cherry)

    // Step 8: Use find() to get an iterator to a key
    auto it = m.find(2); // Try to find key=2
    if (it != m.end()) {
        cout << "Found key 2 with value: " << it->second << endl;
    } else {
        cout << "Key 2 not found." << endl;
    }

    // Step 9: Try to find a removed key
    if (m.find(3) == m.end()) {
        cout << "Key 3 is no longer in the map" << endl;
    }

    // Step 10: Final state of the map
    cout << "Final map state:" << endl;
    for (auto p : m) {
        cout << "Key: " << p.first << ", Value: " << p.second << endl;
    }

    return 0;
}
```

## A) Hash set

Note: Use unordered_set when you need to store unique elements, check for duplicates, or perform fast O(1) presence lookups without caring about order.

### Brute force for hash set problems

```c++
// Brute-force: O(n^2) approach
bool hasDuplicate(vector<int>& nums) {
    for (int i = 0; i < nums.size(); i++) {
        for (int j = i + 1; j < nums.size(); j++) {
            if (nums[i] == nums[j]) {
                return true; // Duplicate or match found
            }
        }
    }
    return false; // All elements are unique
}
```

### Optimized approach for hash set problems

```c++
// time complexity: O(n)
bool solve(vector<int>& nums) {
    unordered_set<int> s;  // To store unique elements

    for (int num : nums) {
        if (s.count(num)) {
            // Element already exists — duplicate or match found
            return true;  // Or perform other logic
        }
        s.insert(num);  // Add to set if not present
    }

    // If needed, return something based on the use case
    return false;  // No duplicates or match found
}
```

## B) Hash map

Note: Use unordered_map when you need to store key-value pairs for fast O(1) access, counting, indexing, or mapping relationships.

### Brute force for hash map problems

```c++
// time complexity: O(n^2)

bool solve(vector<int>& nums) {
    int n = nums.size();

    for (int i = 0; i < n; i++) {
        int count = 0;

        // Count how many times nums[i] appears in the entire array
        for (int j = 0; j < n; j++) {
            if (nums[j] == nums[i]) {
                count++;
            }
        }

        // Example use: check for duplicates
        if (count > 1) {
            return true;
        }
    }

    return false;
}
```

OR

```c++
// For array input
void solve(vector<int>& nums) {
    int n = nums.size();

    for (int i = 0; i < n; i++) {
        int key = nums[i];
        int count = 0;

        // Count frequency of nums[i]
        for (int j = 0; j < n; j++) {
            if (nums[j] == key) {
                count++;
            }
        }

        // Use count for your condition:
        // if (count > 1) → duplicate
        // if (count > n / 2) → majority
        // if (count == 1) → first unique (track index)
    }
}
```

### optimized approach for hash map problems

```c++
// time complexity: O(n)

unordered_map<int, int> m;

for (int i = 0; i < n; i++) {
    // requency Count
    m[arr[i]]++;  // Count occurrences of arr[i]

    // Complement Check (e.g. Two Sum)
    int complement = target - arr[i];
    if (m.count(complement)) {
        // Found a pair: arr[i] + complement = target
    }

    //  Index Tracking (e.g. Two Sum optimized)
    m[arr[i]] = i;  // Store latest index of arr[i]
}
```
