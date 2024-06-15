Design for assignment 7

Diagram

+----------------------------+
|         Hashtable          |
+----------------------------+
| - table: vector<pair<K, V>>|----+
| - size: size_t             |    |
+----------------------------+    |
| + hash(key: K): size_t     |    |
| + insert(key: K, value: V) |    |
| + contains(key: K): bool   |    |
+----------------------------+    |
                                   |
           +-----------------------+
           |
+----------------------------+
|    SimpleHashtable<K, V>   |
+----------------------------+
| + insert(key: K, value: V) |
| + contains(key: K): bool   |
+----------------------------+

           +-----------------------+
           |
+----------------------------+
|    SmarterHashtable<K, V>  |
+----------------------------+
| + doubleHash(key: K, p: sz)|    
| + insert(key: K, value: V) |
| + contains(key: K): bool   |
+----------------------------+

Explanaion

int main() {
    // Simple Hashtable Tests
    SimpleHashtable<int, std::string> simpleHashtable(10);
    simpleHashtable.insert(5, "apple");
    simpleHashtable.insert(15, "banana");
    std::cout << "Contains 5: " << simpleHashtable.contains(5) << std::endl; // true
    std::cout << "Contains 10: " << simpleHashtable.contains(10) << std::endl; // false

    // Smarter Hashtable (Double Hashing) Tests
    SmarterHashtable<int, std::string> smarterHashtable(10);
    smarterHashtable.insert(5, "apple");
    smarterHashtable.insert(15, "banana");
    std::cout << "Contains 5: " << smarterHashtable.contains(5) << std::endl; // true
    std::cout << "Contains 10: " << smarterHashtable.contains(10) << std::endl; // false

    return 0;
}

These tests ensure the hashtables behave as expected.

size_t hash(const KeyType& key) {
    return std::hash<KeyType>{}(key) % size;
}

hashtable classes use simple modulo hashing to compute the index from the key.


void insert(const KeyType& key, const ValueType& value) {
    size_t index = hash(key);
    table[index] = std::make_pair(key, value);
}

The insert function computes the index using the hash function and places the key-value pair at the computed index. In SimpleHashtable, it overwrites any existing value at that index.

bool contains(const KeyType& key) {
    size_t index = hash(key);
    return table[index].first == key;
}

The contains function checks if a given key exists in the hashtable. It computes the index using the hash function and checks if the key at that index matches the given key.

size_t doubleHash(const KeyType& key, size_t probe) {
    return (hash(key) + probe) % size;
}

void insert(const KeyType& key, const ValueType& value) {
    size_t index = hash(key);
    if (table[index].first == key) {
        table[index].second = value;
    } else {
        size_t probe = 1;
        while (table[index].first != KeyType()) {
            index = doubleHash(key, probe++);
        }
        table[index] = std::make_pair(key, value);
    }
}

bool contains(const KeyType& key) {
    size_t index = hash(key);
    if (table[index].first == key) {
        return true;
    } else {
        size_t probe = 1;
        while (table[index].first != KeyType()) {
            index = doubleHash(key, probe++);
            if (table[index].first == key) {
                return true;
            }
        }
        return false;
    }
}

The SmarterHashtable class implements double hashing to handle collisions more efficiently.
