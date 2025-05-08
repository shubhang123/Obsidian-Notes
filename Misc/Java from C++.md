Got it! I’ll prepare a Java-focused DSA prep guide that covers:

- Key differences from C++
    
- Java syntax essentials for DSA
    
- Core Java collections (like ArrayList, HashMap, HashSet)
    
- How to write LeetCode-style solutions in Java
    
- Quick primer on OOP concepts in Java (classes, inheritance, interfaces) I'll get this guide ready for you to review shortly!
    

# Java Coding Interview Prep Guide for C++ Programmers

## Java vs C++: Key Differences for DSA Coding

- **Input/Output:** Java uses `System.in` and `System.out` streams for console I/O (commonly via `Scanner` for input and `System.out.println` for output), whereas C++ uses `std::cin` and `std::cout` ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Input,C%2B%2B%20supports%20the%20goto%20keyword)). For example, reading an integer and a string in Java:
    
    ```java
    Scanner sc = new Scanner(System.in);
    int n = sc.nextInt();
    String s = sc.next();
    ```
    
    In C++ this would be `std::cin >> n >> s;`. Java’s `Scanner` is convenient but can be slower; for very large input, you might use `BufferedReader`. Output in Java is typically done with `System.out.println()` (or `System.out.printf` for formatted output) instead of C++'s `std::cout`.
    
- **Arrays:** In Java, arrays are objects that are created with `new` and have a fixed length property `length`. For example: `int[] arr = new int[10];`. Java arrays are always 0-indexed and **bound-checked** (accessing out of range throws an exception instead of causing undefined behavior). In C++, you can have static or dynamic arrays (e.g. `int arr[10];` or using `new` or `std::vector`). C++ arrays (or `std::vector`) can be accessed without automatic bounds checking (potentially unsafe). Java does not have an exact equivalent of C++’s `std::vector` in the core language – instead, you use **ArrayList** from the Collections framework for dynamic arrays. (See **ArrayList** below.) Java arrays and collections use **generics** for type safety, meaning you must specify the element type. One key difference: Java generics do **not** work with primitive types directly, so you use wrapper classes (e.g. `ArrayList<Integer>` for a list of ints) ([Collections in Java | GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/#:~:text=ArrayList%20provides%20us%20with%20dynamic,130%20for%20such%20cases)). Java will auto-convert (auto-box) primitives to their wrappers when needed, but using many boxed objects can impact performance.
    
- **Strings:** Java `String` is an immutable object – once created, it cannot be changed ([Strings in Java vs. Strings in CPP: A Comparative Analysis](https://www.upgrad.com/tutorials/software-engineering/java-tutorial/strings-in-java-vs-strings-in-cpp/#:~:text=2)). All string manipulations in Java (`substring`, concatenation, etc.) produce new `String` objects. In contrast, C++ `std::string` is mutable (you can modify it in-place) ([Strings in Java vs. Strings in CPP: A Comparative Analysis](https://www.upgrad.com/tutorials/software-engineering/java-tutorial/strings-in-java-vs-strings-in-cpp/#:~:text=2)). As a result, in Java if you need to build a string efficiently (e.g., inside loops), you should use `StringBuilder` (mutable buffer) to avoid creating many temporary String objects. Another crucial difference is how equality is checked: In C++, `str1 == str2` with `std::string` compares content (because `operator==` is overloaded). In Java, `str1 == str2` checks **reference** equality (whether they are the same object in memory), not content. To compare string contents in Java, use `str1.equals(str2)` ([Difference Between == Operator and equals() Method in Java | GeeksforGeeks](https://www.geeksforgeeks.org/difference-between-and-equals-method-in-java/#:~:text=In%20Java%2C%20the%20equals,the%20same%20location%20or%20not)). For example:
    
    ```java
    String a = "hello";
    String b = new String("hello");
    System.out.println(a == b);      // false, different objects
    System.out.println(a.equals(b)); // true, same content
    ```
    
    Java strings have many built-in methods (length, charAt, substring, indexOf, etc.), similar to C++ `std::string`. Also, Java uses Unicode for `char` (16-bit), so it can handle Unicode text by default (whereas C++ `char` is typically 8-bit and `std::string` can hold bytes or encoded text).
    
- **Memory Management & Pointers:** Java manages memory automatically with **garbage collection** – you do not explicitly delete objects. C++ requires manual memory management (or usage of smart pointers/RAII) for dynamically allocated memory ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Memory%20Management%20Memory%20Management%20is,It%20strongly%20supports%20pointers)) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Object%20Management%20Automatic%20object%20management,value%20and%20call%20by%20reference)). In Java, there is **no pointer arithmetic** or explicit memory address manipulation ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Virtual%20Keyword%20It%20doesn%27t%20have,It%20strongly%20supports%20pointers)). You cannot directly get the address of an object or do pointer math as in C++; instead, all objects are accessed by references. A Java reference behaves like a pointer to an object, but you can’t do arithmetic on it and you can’t have dangling references (if no reference points to an object, it’s eventually garbage-collected). Also, Java has no concept of pointer vs. reference vs. value semantics for objects – **all non-primitive types are references**. For example, if you pass an object to a function, you’re passing a reference _by value_. (Java is strictly **pass-by-value** for all parameters ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Parameter%20Passing%20Java%20supports%20only,value%20and%20call%20by%20reference)), which means the reference itself is copied, but it still refers to the same object; the called method can mutate the object’s data via that reference, but cannot change the caller’s reference to point to a new object.) The lack of pointers means you also don’t have to worry about things like freeing memory or memory leaks in the same way (though you should still null out references not needed in long-lived structures to help GC).
    
- **Syntax and Other Differences:** The basic syntax for loops and conditionals in Java is very similar to C++ (see below), and both are curly-brace languages. However, Java **does not support multiple inheritance of classes** – a Java class can `extends` at most one base class (additional “base” types can be implemented via interfaces) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Virtual%20Keyword%20It%20doesn%27t%20have,It%20strongly%20supports%20pointers)). There is also no concept of C++-style templates; Java uses generics which are checked at compile time but use type erasure at runtime. Java **does not allow operator overloading** (except for string concatenation with `+`) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Overloading%20It%20supports%20only%20method,It%20strongly%20supports%20pointers)), so you can’t define custom `operator<` or `operator+` as in C++ – you’ll use regular methods or Comparators instead. All functions in Java must be methods of a class; there are **no free functions or global variables** (you can use static class members to emulate globals) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Parameter%20Passing%20Java%20supports%20only,value%20and%20call%20by%20reference)). Also, Java has no `struct` or union types outside classes (C++ structs are basically classes with default public visibility). The entry point of a Java program is a static `main` method inside some class, rather than a free `main` function. Finally, Java keywords differ slightly (`extends` vs C++ `:` for inheritance, `implements` for interfaces, no `->` operator – use `.` for member access, etc.), but you’ll find most control structures and expressions feel familiar.
    

## Java Syntax Essentials (Loops, Conditionals, Classes, Functions)

Java’s control flow uses syntax almost identical to C++ for common structures:

- **Loops and Conditionals:** You have `if, else if, else` with conditions in parentheses (and Boolean conditions must be true/false values, not integers as in C++ older style). The `for` loop and `while` loop work the same way. For example:
    
    ```java
    // Java loop examples
    for (int i = 0; i < 10; i++) {
        System.out.println(i);
    }
    
    int j = 0;
    while (j < 10) {
        System.out.println(j);
        j++;
    }
    
    if (j == 10) {
        System.out.println("j is ten");
    } else if (j > 10) {
        System.out.println("j is greater than ten");
    } else {
        System.out.println("j is less than ten");
    }
    ```
    
    Java also has an enhanced **for-each loop** similar to C++11 range-based for. Example: `for (int x : arr) { ... }` will iterate through array or collection elements (just like `for(int x : vector) { ... }` in C++). The **switch** statement exists in Java and is similar to C++ (one notable improvement is that Java `switch` can work on `String` types and enum types, not just integers/char). Case blocks in Java switch require `break` statements to avoid fall-through (unless you intentionally want it). There’s no `goto` in Java (not supported) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Input,C%2B%2B%20supports%20the%20goto%20keyword)), so structured loops and conditionals are the norm.
    
- **Defining Classes and Methods:** Every function in Java must be inside a class (except for lambdas which still are attached to a functional interface). A simple class example in Java:
    
    ```java
    class Point {
        // Fields (instance variables)
        public int x;
        public int y;
    
        // Constructor
        public Point(int x, int y) {
            this.x = x;
            this.y = y;
        }
    
        // Method
        public int sumCoordinates() {
            return this.x + this.y;
        }
    }
    ```
    
    This is analogous to a C++ class with public data members and methods. Some syntax notes: Java uses the keyword **`class`** to declare a class. There’s no trailing semicolon after the class definition (unlike C++). The constructor in Java is a method with the same name as the class and no return type. The `this` keyword in Java is like C++ `this` pointer (refers to the current object). Java access modifiers are `public`, `protected`, `private` (and package-private if no modifier is given). By default, members without an explicit modifier have package-private visibility (accessible to other classes in the same package). For top-level classes, `public` means the class is accessible anywhere (and the file name must match the public class name). In an interview setting or LeetCode, you often won’t worry about multiple files/packages – you’ll typically write a single class.
    
- **Functions (Methods) Syntax:** A method in Java is defined inside a class. General form is:
    
    ```java
    [modifier] [return_type] methodName([parameter_list]) {
        // ... body ...
    }
    ```
    
    For example: `public int add(int a, int b) { return a + b; }`. Unlike C++, Java does not support **free functions** or **default parameter values** – if you need overloaded behavior, you must define another method with a different parameter list. Method overloading is supported (same name, different parameter types or counts). Method overriding (in subclasses) is also supported – and in Java all non-final instance methods are virtual by default (no `virtual` keyword needed) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Virtual%20Keyword%20It%20doesn%27t%20have,It%20strongly%20supports%20pointers)). It’s good practice to use the `@Override` annotation when overriding a method from a superclass to catch errors. Java doesn’t have C++’s scope resolution operator `::` for defining methods outside class definition – you always implement methods within the class body (or in some cases, define in one class and override in subclass).
    
- **Main Method:** In a standalone Java program, the entry point is `public static void main(String[] args)`. For example:
    
    ```java
    public static void main(String[] args) {
        // your code here
    }
    ```
    
    This is only needed if you are writing a full program. In LeetCode or similar coding challenges, you typically won’t write the `main` method – the platform calls your solution method directly. But it’s useful to know for running your own tests. The `String[] args` parameter is the command-line arguments array (similar to `argv` in C++). The `static` means it can run without an instance of the class.
    
- **Error Handling:** Java uses exceptions for error handling (e.g., `throw` and `try-catch` blocks), similar to C++ exceptions. In coding interviews for algorithms, you typically won’t need to write custom exception handling, but be aware that some Java methods throw checked exceptions (e.g., using `Scanner` or `BufferedReader` might require handling `IOException`). For algorithm problems, this is rarely an issue on LeetCode as they provide input directly to your function.
    

## Important Java Collections (with Examples)

Java’s standard library (java.util package) provides a Collections Framework which is analogous to C++ STL containers. Here are some commonly used collections for interviews and how to use them:

### ArrayList (Resizing Array)

**What it is:** `ArrayList` is essentially a resizable array (similar to `std::vector<T>` in C++). It implements the List interface, maintaining insertion order and allowing indexed access. It auto-resizes as you add/remove elements. Random access by index is O(1). In Java, `ArrayList` is not synchronized and allows duplicate elements.

**Example usage:**

```java
import java.util.ArrayList;

ArrayList<Integer> arr = new ArrayList<>();   // create an ArrayList of Integer
arr.add(5);
arr.add(10);
System.out.println(arr.size());    // 2 (number of elements)
System.out.println(arr.get(1));    // 10 (element at index 1)
arr.remove(0);                     // remove element at index 0
System.out.println(arr);           // prints [10]
```

In the above, `arr` started empty, we added two elements (5 at index0, 10 at index1). After removal, only 10 remains. **Note:** `ArrayList` can only hold objects, not primitive types. For primitive values, use their wrapper classes (`Integer` for `int`, etc.) ([Collections in Java | GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/#:~:text=ArrayList%20provides%20us%20with%20dynamic,130%20for%20such%20cases)). Java will automatically box/unbox in many cases (e.g., `arr.add(5)` auto-boxes `5` to `Integer`), but it’s good to remember because `ArrayList<int>` is invalid. You can convert an `ArrayList<Integer>` to a primitive array if needed by iterating or using streams, but usually just working with the list is fine. The capacity of an ArrayList grows as needed; you can also initialize with a capacity (e.g. `new ArrayList<>(100)`).

### LinkedList (Doubly-Linked List)

**What it is:** `LinkedList` is a doubly-linked list implementation of the List and Deque interfaces. It allows fast insertions or deletions at the ends and maintains insertion order, but random access by index is O(n) (so use it when you need frequent add/remove in the middle or as a queue). It can be used both as a list and as a queue/deque. Under the hood, each element is a node object holding the data and pointers to next (and prev) nodes ([Collections in Java | GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/#:~:text=The%20LinkedList%20class%20is%20an,is%20known%20as%20a%20node)).

**Example usage:**

```java
import java.util.LinkedList;

LinkedList<String> list = new LinkedList<>();
list.add("a");
list.add("b");
list.addFirst("z");                 // add at beginning
System.out.println(list);           // prints [z, a, b]
list.remove(1);                     // remove element at index 1 (which was "a")
System.out.println(list);           // prints [z, b]
for (String s : list) {
    System.out.println(s);
}
// Output:
// z
// b
```

Here we used `addFirst` (from Deque interface) to add at the head. You could also use `addLast` (or just `add` which appends to end). `LinkedList` supports `removeFirst`, `removeLast`, `poll()` (remove first like a queue) and so on, making it handy for queue or deque operations. In interviews, if you need a queue, you can use `LinkedList` or Java’s `ArrayDeque` for efficiency. For stack, there’s `Stack` class or just use `Deque` methods (`push`, `pop`). Generally, prefer `ArrayList` for most cases where you don’t specifically need frequent head/tail operations, since `ArrayList` is faster for random access.

### HashSet (Unordered Set)

**What it is:** `HashSet` is an implementation of the Set interface using a hash table (actually a wrapper around `HashMap`). It stores **unique elements** only (no duplicates) and offers average O(1) add, remove, and contains operations ([HashMap in Java | GeeksforGeeks](https://www.geeksforgeeks.org/java-util-hashmap-in-java/#:~:text=duplicate%20key%2C%20it%20will%20replace,1%29%20time%20complexity)) ([Java HashSet | GeeksforGeeks](https://www.geeksforgeeks.org/hashset-in-java/#:~:text=HashSet%20in%20Java%20implements%20the,any%20specific%20order%20of%20elements)). It **does not preserve any order** of elements. This corresponds to C++ `std::unordered_set` (or `std::set` in concept, except C++ `std::set` is ordered and implemented as a tree, whereas Java `HashSet` is unordered and hash-based).

**Example usage:**

```java
import java.util.HashSet;

HashSet<Integer> set = new HashSet<>();
set.add(42);
set.add(13);
set.add(42);                      // duplicate, will be ignored
System.out.println(set.size());   // 2
System.out.println(set.contains(13));  // true
set.remove(13);
System.out.println(set.contains(13));  // false
System.out.println(set);          // e.g. prints [42]
```

Common interview uses for HashSet: checking membership (e.g. seen elements in an array, detecting duplicates), filtering unique values, etc. Iterating a HashSet gives elements in an undefined order. If you need a sorted set, use `TreeSet` instead (which is like C++ `std::set`, typically O(log n) operations). But for most “does this exist?” checks, `HashSet` is the go-to. Remember that elements added to a HashSet (or used as keys in HashMap) should have proper `hashCode()` and `equals()` methods defined. For Java’s built-in classes (String, Integer, etc.), these are already implemented appropriately.

### HashMap (Unordered Map/Dictionary)

**What it is:** `HashMap<K, V>` is a hash table based implementation of the Map interface, storing key-value pairs. It provides average O(1) time for put, get, and remove operations on keys ([HashMap in Java | GeeksforGeeks](https://www.geeksforgeeks.org/java-util-hashmap-in-java/#:~:text=duplicate%20key%2C%20it%20will%20replace,1%29%20time%20complexity)). Keys must be unique (adding a key that exists will overwrite the old value). This is analogous to C++ `std::unordered_map`. (Java also has `TreeMap` for sorted keys, but that’s less commonly needed in interviews unless explicitly required.)

**Example usage:**

```java
import java.util.HashMap;

HashMap<String, Integer> age = new HashMap<>();
age.put("Alice", 30);
age.put("Bob", 25);
System.out.println(age.get("Alice"));        // 30
System.out.println(age.containsKey("Bob"));  // true
age.put("Alice", 31);                        // update Alice's value
System.out.println(age.getOrDefault("Charlie", 0)); // 0 (Charlie not present)
age.remove("Bob");
System.out.println(age);  // prints something like {Alice=31}
```

In this example, `age` maps names to ages. We show `getOrDefault` which is a handy method to provide a default if a key isn’t present (here returning 0 for "Charlie"). This is useful for frequency counting patterns (e.g., `map.put(x, map.getOrDefault(x, 0) + 1)` to count occurrences). A HashMap can have at most one `null` key and any number of `null` values (though using null as key is rare). Iterating through a HashMap (e.g., with `for(Map.Entry<K,V> e : map.entrySet())`) will traverse in some hash-dependent order, not sorted. If order matters by insertion, Java 1.8+ has `LinkedHashMap` (which preserves insertion order). But usually, for algorithm problems, order isn’t important unless explicitly stated – you use HashMap for fast lookups (like using a dictionary to count frequencies, check complements in two-sum, etc.). **Note:** Just as with HashSet, the key type must have proper `equals` and `hashCode`. Standard types are fine; for custom classes, you’d implement those if you ever used them as keys.

### PriorityQueue (Min-Heap)

**What it is:** `PriorityQueue<E>` in Java is a heap-based priority queue. By default, **Java’s PriorityQueue is a min-heap** (the smallest element is given priority and comes out first) ([priority queue - How does Java's PriorityQueue differ from a min-heap? - Stack Overflow](https://stackoverflow.com/questions/6065710/how-does-javas-priorityqueue-differ-from-a-min-heap#:~:text=119)) ([Min Heap in Java | GeeksforGeeks](https://www.geeksforgeeks.org/min-heap-in-java/#:~:text=,in%20below%20example%20as%20follows)). This is the opposite of C++’s `std::priority_queue` which is a max-heap by default (largest element first). You can provide a custom `Comparator` to the PriorityQueue constructor to change the ordering (for example, to make it a max-heap or to define a custom sort order for objects).

**Example usage (min-heap by default):**

```java
import java.util.PriorityQueue;

PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(10);
pq.add(5);
pq.add(7);
System.out.println(pq.peek());  // 5 (smallest element)
System.out.println(pq.poll());  // 5 (removes and returns smallest)
System.out.println(pq.poll());  // 7 (next smallest)
```

The elements come out in increasing order in this case. If you need a max-heap (e.g., always extract the largest element first), you can do:

```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
maxHeap.add(10);
maxHeap.add(5);
maxHeap.add(7);
System.out.println(maxHeap.poll()); // 10 (largest first)
```

Here we used `Comparator.reverseOrder()` which provides a comparator that inverts the natural order. You could also write `new PriorityQueue<>((a,b) -> b - a)` using a lambda for the comparator. PriorityQueue is commonly used in problems like “merge k sorted lists,” Dijkstra’s algorithm (min-heap for picking the next shortest distance), or anytime you need quick access to the smallest or largest element dynamically. Just remember the default is min-heap (this trips up many C++ programmers initially) ([priority queue - How does Java's PriorityQueue differ from a min-heap? - Stack Overflow](https://stackoverflow.com/questions/6065710/how-does-javas-priorityqueue-differ-from-a-min-heap#:~:text=119)). Also, PriorityQueue in Java does not allow `null` elements and is not synchronized.

## Writing LeetCode-Style Code in Java

When solving LeetCode or similar coding challenge problems in Java, you typically write a solution method within a class (often named `Solution`). Here are some tips:

- **Function Signature:** LeetCode provides the function signature (and often the class definition) that you should implement. For example, for a two-sum problem, you might see:
    
    ```java
    class Solution {
        public int[] twoSum(int[] nums, int target) {
            // ... implementation ...
        }
    }
    ```
    
    You just need to fill in the method body. The method is usually `public` (or default) and often `static` is not used in the LeetCode context (the judge instantiates your `Solution` class and calls the method). Ensure you match the exact signature (including return type and parameter types/order) that the platform specifies. If the problem expects an output of an array or list, make sure to return the correct type (`int[]`, `List<Integer>`, etc., as specified).
    
- **Input/Output Handling:** On LeetCode and most online judges, you **do not** handle input/output formatting – the platform does it for you. You just implement the function logic and return the result, and the platform takes care of reading input and printing your return value (or comparing it to expected output). This is different from a typical `main` in C++ where you might read and write. **So, you generally won’t use `Scanner` or `System.out.println` in your LeetCode solution function** (unless for debugging). For example, if the problem is to merge two sorted lists, the online judge will call your `mergeTwoLists(ListNode l1, ListNode l2)` and check the returned ListNode.
    
    However, if you are doing a coding test on a site like HackerRank or CodeChef, they might require reading from `System.in` and printing to `System.out`. In those cases, use `Scanner sc = new Scanner(System.in)` (or `BufferedReader`) to read inputs and `System.out.println` for outputs as illustrated earlier. Always read the problem instructions carefully to see if you should write a full program or just a function. In an interview using an online IDE, the interviewer might provide a `main` or test harness, or just ask you to write the method.
    
- **Returning Results:** Make sure to return the correct type and format. For example, if asked to return a list of integers, you might return a `List<Integer>` (e.g., an `ArrayList<Integer>`). If an array is needed, you can create a new array and return it (e.g., `return new int[]{a, b};`). In Java, returning an array or object is straightforward (no need for special memory management). If the problem requires printing output (some older judge problems do), you would accumulate the result and print it in the required format, but again LeetCode-style usually expects a return value.
    
- **Class Definitions for Data Structures:** Some LeetCode problems use custom classes like `ListNode` for linked list nodes or `TreeNode` for binary tree nodes. These are usually provided by the platform (you don’t need to implement them, but you need to know how to use them). For example, if you have `public ListNode addTwoNumbers(ListNode l1, ListNode l2)`, you can use `l1.val` and `l1.next` just like you would use a struct in C++. Just be comfortable with the dot notation (there’s no `->` in Java, since everything is a reference, you always use `.`). Also, be mindful that Java references can be null – if a ListNode is null, `node.next` would throw a `NullPointerException`, similar to dereferencing a null pointer in C++ (segfault). So check for null where appropriate.
    
- **Performance Considerations:** Java can be a bit slower than C++ for very large computations due to overhead (like bounds checking, garbage collection, etc.), but for most interview-level problem sizes, Java is fine. Just be aware of using faster I/O for huge input (e.g., `BufferedReader` instead of `Scanner`) and consider using primitives instead of objects in hot loops when possible (to avoid GC overhead). Also, Java’s large recursion might hit the stack limit (as in C++), but tail recursion isn’t optimized. Prefer iterative solutions if recursion depth could be large (to avoid `StackOverflowError`). For most LeetCode problems, this isn’t a big issue, but for very deep tree recursion it could be.
    
- **Example Integration:** Suppose you want to test your solution locally, you might write a `main` method to create an instance of `Solution` and call the method. For instance:
    
    ```java
    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] result = sol.twoSum(new int[]{2,7,11,15}, 9);
        System.out.println(Arrays.toString(result));  // expect [0, 1] for two-sum example
    }
    ```
    
    But on LeetCode, you wouldn’t include that main method – it’s just for your own testing.
    

In summary, for LeetCode style, focus on implementing the given function correctly. Use the appropriate data structures (as discussed above) to store and compute results. The platform will handle input and output around your code. Make sure to practice a few problems in the LeetCode environment to get used to the syntax (especially dealing with Java specifics like classes for list nodes, etc.).

## Object-Oriented Programming Essentials in Java

Java is an **object-oriented** language, much like C++, but with some differences in how OOP concepts are implemented. If you’re strong in C++ OOP, the concepts will sound familiar. Here’s a quick overview focused on Java’s approach to OOP, covering the key principles:

- **Class and Object:** A **class** in Java is a blueprint for creating objects, defining a type with fields (data) and methods (functions) that operate on that data. An **object** is an instance of a class, created at runtime using the `new` keyword (e.g., `Point p = new Point(1,2);`). In Java, all objects are allocated on the heap and accessed through references; you can’t have an object “by value” the way you can in C++ (in C++, you can do `Point p;` which constructs on the stack – in Java, `Point p;` just declares a reference, you still need `new Point()` to actually create the object) ([methods - Is Java "pass-by-reference" or "pass-by-value"? - Stack Overflow](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value#:~:text=I%20just%20noticed%20you%20referenced,my%20article)). Classes in Java can contain **fields** (instance variables), **methods**, **constructors**, inner classes, etc. Java does not have destructors (resource cleanup is usually done via try-with-resources or finalizers which are rarely used). Every class in Java (except `Object`) has a single inheritance parent (at most one direct superclass). Example:
    
    ```java
    class Person {
        private String name;
        public Person(String name) { this.name = name; }
        public void greet() { System.out.println("Hello, I'm " + name); }
    }
    
    Person alice = new Person("Alice");  // creating an object
    alice.greet();  // calls method -> prints "Hello, I'm Alice"
    ```
    
    Here `Person` is a class, and `alice` is an object (instance) of that class. In an interview, you might not need to write your own classes from scratch unless designing something, but you should understand Java syntax for classes and how to instantiate and use objects.
    
- **Encapsulation:** Encapsulation is the principle of hiding internal details of an object and only exposing a public interface. In Java, this is achieved with access modifiers: you typically declare class fields as `private` and provide public **getter/setter** methods to read or modify them if needed. This way, you control how the data is accessed or changed. For example:
    
    ```java
    class Counter {
        private int count = 0;         // internal state hidden
    
        public void increment() {      // public method to change state
            count++;
        }
        public int getCount() {        // public method to access state
            return count;
        }
    }
    ```
    
    Here, the field `count` is encapsulated – external code can’t directly set it arbitrarily (like `counter.count = 5` would be illegal if `count` is private). They must call `increment()` or other provided methods. Encapsulation helps maintain invariants and reduces interdependency between components. In C++, you have the same concept (making members private/protected). Java has no friend functions, so private is strictly private to the class. Encapsulation is often described as wrapping data and methods into one unit (the class) and protecting the data from outside interference ([Java OOP(Object Oriented Programming) Concepts | GeeksforGeeks](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/#:~:text=It%20is%20defined%20as%20the,the%20code%20outside%20this%20shield)).
    
- **Inheritance:** Inheritance is the mechanism by which one class (subclass) can extend another (superclass), inheriting its properties and behaviors. In Java you use the `extends` keyword for classes. E.g., `class Student extends Person { ... }` means `Student` inherits all non-private members of `Person`. Inheritance promotes code reuse – the subclass can use methods of the parent, and override them if needed. As noted earlier, Java only allows **single inheritance** for classes (a class can have only one direct superclass) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Virtual%20Keyword%20It%20doesn%27t%20have,It%20strongly%20supports%20pointers)). This is a difference from C++, which allows multiple inheritance – Java avoids the diamond problem by not allowing multiple base classes. If you need to model something like multiple inheritance, you use **interfaces** (see below). In a subclass, you can call the superclass constructor or methods via `super` keyword (e.g., `super()` as first line in constructor to call base constructor, or `super.someMethod()` to call a base class method that’s been overridden). Example:
    
    ```java
    class Student extends Person {
        private int studentId;
        public Student(String name, int id) {
            super(name);       // call Person(String) constructor
            this.studentId = id;
        }
        // Inherit greet() from Person, or override it if we want a different behavior
        @Override
        public void greet() {
            System.out.println("Hi, I'm " + super.name + ", student ID: " + studentId);
        }
    }
    ```
    
    In this example, `Student` inherits `Person`. If `name` was private in Person, we’d typically have a protected getter or use super.greet(). (Note: using `super.name` would only work if `name` were protected, not private). In interviews, inheritance might come up if you need to use or design class hierarchies. Remember in Java all classes ultimately inherit from `java.lang.Object` (the root of the hierarchy), which provides methods like `toString()`, `equals()`, `hashCode()`, etc.
    
- **Interface:** An interface in Java is a pure abstract type that defines a contract (a set of abstract methods that implementing classes must provide). Interfaces are declared with the `interface` keyword. For example:
    
    ```java
    interface Movable {
        void move(int dx, int dy);   // abstract method, no body
    }
    class Car implements Movable {
        public void move(int dx, int dy) {
            // implementation for moving the car
        }
    }
    class Person extends Animal implements Movable {
        public void move(int dx, int dy) {
            // person walking implementation
        }
    }
    ```
    
    Here `Car` and `Person` both **implement** the Movable interface, so both provide a `move` method. Interfaces in Java are similar to C++ pure virtual classes (abstract classes with all methods pure virtual), but Java makes a clear distinction between class inheritance and interface implementation. A class can implement multiple interfaces, allowing a form of multiple inheritance of _type_. For instance, `Person` could also implement other interfaces. Interfaces are often used in Java to define roles or capabilities (e.g., `Comparable<T>` interface requires a `compareTo` method, which allows objects to be sorted). Java 8+ allows interfaces to have `default` methods (with a body) and static methods, but the primary purpose remains specifying a contract. In an interview, you might use an interface if a problem asks for a common API between different classes or to simulate multiple inheritance. For example, many collections implement the `Collection` interface, meaning they promise certain methods like `iterator()` exist.
    
- **Abstraction:** Abstraction means highlighting the necessary and relevant features of an object while hiding the unnecessary details. In practice, abstraction in OOP is often achieved through **abstract classes** and interfaces. An **abstract class** in Java is a class that cannot be instantiated and may contain abstract methods (methods without implementation). You declare it with the `abstract` keyword. For example:
    
    ```java
    abstract class Shape {
        abstract double area();        // abstract method
        public void info() {
            System.out.println("I am a shape.");
        }
    }
    class Circle extends Shape {
        private double radius;
        public Circle(double r) { this.radius = r; }
        @Override
        double area() {
            return Math.PI * radius * radius;
        }
    }
    ```
    
    Here `Shape` is abstract, defining a general concept of a shape with an abstract method `area()`. `Circle` extends `Shape` and provides an implementation for `area()`. Abstraction lets you work at a higher level: e.g., you could have a `List<Shape>` and call `shape.area()` polymorphically on each, without needing to know if it’s a Circle, Rectangle, etc. Java’s abstract classes are similar to C++ abstract classes (classes with pure virtual functions). The difference from interfaces is that an abstract class can have some concrete methods or fields, and you can have constructors, maintain state, etc., whereas interfaces cannot (at least prior to default methods feature). Use an abstract class when you have a base class that should not be instantiated on its own, but provides some common implementation to subclasses. Use interfaces when you just want to define a role or capability without tying to an inheritance tree. In many interview scenarios, you won’t need to write your own abstract class unless designing a system, but you should understand the concept if asked.
    
- **Polymorphism:** Polymorphism is the ability for an entity to take on many forms. In Java (and C++), this primarily comes in two flavors: **compile-time polymorphism** (method overloading) and **run-time polymorphism** (method overriding and dynamic dispatch).
    
    - _Method Overloading:_ You can have multiple methods in the same class with the same name but different parameter lists. This is resolved at compile time (the compiler chooses the correct method signature based on arguments). Java and C++ both support this. (Java doesn’t support operator overloading, as mentioned, so polymorphism via operators is limited to what the language defines.)
        
    - _Method Overriding and Dynamic Dispatch:_ If a subclass overrides a method from its superclass, and you have a reference of the superclass type referring to a subclass object, Java will invoke the subclass’s version of the method at runtime. For example:
        
        ```java
        Person p = new Student("Bob", 123);
        p.greet();  // calls Student's override of greet(), not Person's, because actual object is Student
        ```
        
        This is polymorphism in action – a `Person` reference that at runtime is actually a `Student` object, and the call to `greet` is dispatched to the overriding method in `Student`. In C++, you achieve this with virtual functions; in Java, all instance methods are virtual by default (unless marked `final` or in a `final` class, or static/private which are not virtual). So Java’s dynamic polymorphism is straightforward – just override and it works. Polymorphism allows code like `List<Shape>` example mentioned: you can do `for(Shape sh : shapes) System.out.println(sh.area());` and each shape (Circle, Rectangle, etc.) computes area with its own implementation ([Java OOP(Object Oriented Programming) Concepts | GeeksforGeeks](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/#:~:text=Polymorphism%20in%20Java%20is%20mainly,2%20types%20as%20mentioned%20below)) ([Java OOP(Object Oriented Programming) Concepts | GeeksforGeeks](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/#:~:text=2,in%20the%20method%20already%20written)).
        
    - _Polymorphism through Interfaces:_ If different classes implement the same interface, you can treat them as that interface type. E.g., `Movable m = new Car(); m.move(5,10);` and `m = new Person(); m.move(3,4);` – here `m` is of type Movable, and at runtime it can refer to different implementations.
        

Polymorphism is heavily used in designing flexible systems and also in the Collections API (e.g., a method might take a parameter of type `List` so it can accept `ArrayList` or `LinkedList` or any implementation). For interview algorithm questions, you might not explicitly use polymorphism much, but if you’re asked OOP concepts or to design something like an animal class hierarchy, demonstrate understanding of overriding vs overloading. For instance, you might mention that Java distinguishes overriding (runtime polymorphism) and overloading (compile time), similar to C++ ([Java OOP(Object Oriented Programming) Concepts | GeeksforGeeks](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/#:~:text=1,can%20or%20cannot%20be%20same)). Also note that Java doesn’t allow covariant return types except that a subclass override may return a subtype of the original return (that’s an advanced point, usually not needed unless designing clone() or such).

- **Additional OOP Notes:** Java lacks some C++ features like multiple inheritance of implementation (but interfaces cover the multiple interface case), and it doesn’t have concepts like mixins or templates in the same way. It also has garbage collection, which means you don’t usually implement a destructor for cleanup – if you need to close resources, you use try-with-resources or finally blocks. Java’s philosophy is to avoid undefined behavior; if you do something wrong (null access, out-of-bounds, etc.), it throws exceptions rather than corrupt memory.
    

In summary, **Java’s OOP** for a C++ programmer is fairly familiar: use classes, `extends` for inheritance, `implements` for interfaces, `private/protected/public` for encapsulation. Remember that everything is a reference, so assignment of objects and passing to methods follows reference semantics (like pointers in C++ but without pointer syntax). If you have a strong grasp of OOP in C++, transitioning to Java mainly involves syntax differences and remembering the single inheritance rule and how interfaces work.

When preparing for a Java-based interview, be ready to explain these OOP concepts (interviewers often ask about encapsulation, inheritance, polymorphism, and abstraction). Use simple examples to illustrate (like a base class Shape and subclasses, or an interface example). Given your C++ background, also be prepared for questions like “what’s the difference between Java and C++ in XYZ OOP feature” – for instance, you can mention _“Java doesn’t support multiple inheritance of classes to avoid the diamond problem; instead it uses interfaces to achieve multiple inheritance of type”_, or _“Java is always pass-by-value, even for objects (the reference is passed by value)”_, or _“Java’s methods are virtual by default, whereas in C++ you specify virtual explicitly”_, etc. These show you understand both sides.

**By focusing on these areas – syntax differences, core Java collections, I/O, and OOP principles – a C++ programmer can quickly get up to speed for coding interviews in Java.** Practice a few LeetCode problems in Java to get comfortable with things like array vs ArrayList usage, string handling (`StringBuilder` for heavy concatenation), and using HashMap/HashSet for typical algorithm puzzles. With these essentials in mind, you’ll be able to translate your C++ solutions into Java with minimal friction while following Java’s best practices in an interview setting. Good luck!

**Sources:**

1. GeeksforGeeks – _“C++ vs Java”_ (table of language differences: memory management, inheritance, pointers, etc.) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Memory%20Management%20Memory%20Management%20is,It%20strongly%20supports%20pointers)) ([C++ vs Java | GeeksforGeeks](https://www.geeksforgeeks.org/cpp-vs-java/#:~:text=Input,reference)).
    
2. UpGrad – _“Strings in Java vs C++”_ (immutability of Java strings vs mutability of C++ strings) ([Strings in Java vs. Strings in CPP: A Comparative Analysis](https://www.upgrad.com/tutorials/software-engineering/java-tutorial/strings-in-java-vs-strings-in-cpp/#:~:text=2)).
    
3. GeeksforGeeks – _“Difference Between == and equals() in Java”_ (string content comparison vs reference comparison) ([Difference Between == Operator and equals() Method in Java | GeeksforGeeks](https://www.geeksforgeeks.org/difference-between-and-equals-method-in-java/#:~:text=In%20Java%2C%20the%20equals,the%20same%20location%20or%20not)).
    
4. GeeksforGeeks – _“Collections in Java – ArrayList”_ (dynamic array behavior and need for wrapper types) ([Collections in Java | GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/#:~:text=ArrayList%20provides%20us%20with%20dynamic,130%20for%20such%20cases)).
    
5. GeeksforGeeks – _“LinkedList in Java”_ (linked list structure and usage example) ([Collections in Java | GeeksforGeeks](https://www.geeksforgeeks.org/collections-in-java-2/#:~:text=The%20LinkedList%20class%20is%20an,is%20known%20as%20a%20node)).
    
6. GeeksforGeeks – _“HashMap in Java”_ (hash map operations and complexity) ([HashMap in Java | GeeksforGeeks](https://www.geeksforgeeks.org/java-util-hashmap-in-java/#:~:text=duplicate%20key%2C%20it%20will%20replace,1%29%20time%20complexity)).
    
7. GeeksforGeeks – _“HashSet in Java”_ (set of unique elements, no order) ([Java HashSet | GeeksforGeeks](https://www.geeksforgeeks.org/hashset-in-java/#:~:text=HashSet%20in%20Java%20implements%20the,any%20specific%20order%20of%20elements)).
    
8. Stack Overflow – _Answer on Java PriorityQueue (min-heap by default)_ ([priority queue - How does Java's PriorityQueue differ from a min-heap? - Stack Overflow](https://stackoverflow.com/questions/6065710/how-does-javas-priorityqueue-differ-from-a-min-heap#:~:text=119)).
    
9. GeeksforGeeks – _“Min Heap in Java (PriorityQueue)”_ (Java PriorityQueue defaults to min-heap) ([Min Heap in Java | GeeksforGeeks](https://www.geeksforgeeks.org/min-heap-in-java/#:~:text=,in%20below%20example%20as%20follows)).
    
10. GeeksforGeeks – _“OOP Concepts in Java”_ (definitions of encapsulation, etc.) ([Java OOP(Object Oriented Programming) Concepts | GeeksforGeeks](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/#:~:text=It%20is%20defined%20as%20the,the%20code%20outside%20this%20shield)) ([Java OOP(Object Oriented Programming) Concepts | GeeksforGeeks](https://www.geeksforgeeks.org/object-oriented-programming-oops-concept-in-java/#:~:text=1,can%20or%20cannot%20be%20same)).