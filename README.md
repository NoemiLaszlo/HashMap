# HashMap
A Hash Map (or often called a Hash Table or Dictionary) is a data structure that can map keys to values. Keys are unique, but multiple keys can hold the same value. Keys and Values can hold any type of data with some implementation-specific exceptions (for example, can null be a key?)

The common operations in a HashMap are:

Add a new key-value pair -- O(1)
Get a value when the key is known -- O(1)
Update a value when the key is known -- O(1)
Iterate over elements -- O(n)
Delete an element -- O(1)
...
Its main advantage over Lists is its speed: In Linked Lists getting an element has O(n) time complexity, in ArrayLists adding/removing an element is O(n). On the downside the elements are not stored in an order.

HashMap is implemented (among others) in C# by the Dictionary (Links to an external site.)Links to an external site., in Java by the HashMap (Links to an external site.)Links to an external site. class in the standard library.

How does it work?
A hash map stores its data in a primitive array, lets say it has a size N and call this the base array. When adding an element to the HashMap it calculates the hash of the key as an integer between 0 and N (lets say this value is H), and adds it to the Hth element of the array.
But there is an issue: multiple strings can hash to the same value (if this happens its called a hash collision). To work around this the base array's elements are Linked Lists (or sometimes Binary Search Trees), and the elements are added here.
Retrieving works the reverse way: First we calculate the hash of the key whose value we want to get to find the position in the base array. Then we loop trough the List there to find the value we are looking for.

I think it can be explained the best by looking at visualizations and pseudocode:

// Helper class, holds a key-value pair.
class KeyValue {
    public K key;
    public V value; 
}


class HashMap<K, V> {

private int bucketSize = 16;

// This holds all the data. Its a primitive array where every element is a Linked List.
// They Linked List holds elements of type KeyValue
private LinkedList<KeyValue>[] elements = new LinkedList[bucketSize];

public void add(K key, V value) {
    // find out which position of the primitive array to use: 
    int position = getHash(key);
    LinkedList list = elements[position];
    
    // If the key already exists throw an error.    
    // Make a new instance of the KeyValue class, fill it with the key, value parameters, then add it to the list.
    
    resizeIfNeeded();
}

public V getValue(K key) {
    // 1. Calculate the hash of the key. This defines which element to get from the "elements" array
    // 2. Find in the List in this position the KeyValue element that has this key, then return its value.
    //    If none of the items in the list has this key throw error.
}

private int getHash(K key) {
    // This function converts somehow the key to an integer between 0 and bucketSize
    // In C# GetHashCode(), in Java hashCode() is a function of Object, so all non-primitive types
    // can easily be converted to an integer.
}

private void resizeIfNeeded()
    // If it holds more elements than bucketSize * 2, destroy and recreate it
    // with the double size of the elements array.
    // if it holds less elements than bucketSize / 2, destroy and recreate it 
    // with half size of the elements array.
}

// + other functions, like clearAll(), delete(),..

}
Note: To find out more about how it works in your favorite language we suggest that you look at its source code - here (Links to an external site.)Links to an external site. it is in Java, here in C# (Links to an external site.)Links to an external site..

Please read the Wikipedia article (Links to an external site.)Links to an external site. and look at a visualization  (Links to an external site.)Links to an external site.of how it works.

The assignment
Your task will be to create your own HashMap with the following requirements:

It should have the following functions: add(key, value), getValue(key), remove(key), clearAll()
Its keys are Strings, its values Integers.
Its initialized with the size of 16, you don't need to resize it when it gets too big.
Hint: You can easilly convert an Object to a number between 0 and N with the following code: obj.GetHashCode() % N (C#), obj.hashCode() % N (Java).

As a bonus exercise you can remove the easing constraints (make it generic, auto resize it)
