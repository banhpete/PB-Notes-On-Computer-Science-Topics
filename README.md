# PB-Notes-On-Computer-Science-Topics
My notes while studying the following Computer Science Topics:
- [Big O](#big-o)
- [Recursion](#recursion)
- [Sorting](#sorting)
- [Data Structures](#data-structures)
- [Search](#search)
- [Operating System](#operating-system)
- [Virtualizaition](#virtualization)
- [Containers](#containers)
- [SOLID Principle](#solid-principle)
- [Dependency Injection](#dependency-injection)

## Big O
Big O Notation is a way of describing time and space complexities of our codes/agorithms in terms of general mathematical functions.
-Space complexitiy is described in one of two formats, in place and out of place.
   - In place types do not depend on size of the input and the space it takes is predictable
   - Out of place is the opposite, it needs more space. I suppose we can think of it as it's out of place because it needs more space!
-The time complexity of a complicated can be determined by splitting it up and then multiplying them, think of the Merge Sort, which can be split into two different time complexities. One which is O(log(N)) and one which is O(N), this results in Merge Sort being O(N log(N))

## Recursion
### What is Recursion
Recursion, by definition, is the repetition of a, well, repetitive procedure. In the context of programming and computer science, it's the repetition of some function, by having the function call itself over and over, to solve some problem by breaking it down to smaller problems.

For example, below is an example of solving the problem of finding a the n fibbonacci number in the fibbonacci sequence. See how the function is essentially calling itself up again during the return.
```
int fib(int n) {
   // Base case
   if (n == 0 || n == 1) return n;
 
   // Recursive step
   return fib(n-1) + fib(n-2);
}
```

### When do we use Recursion
So when do we want to use recursion? Initially, to someone who is new, recursion may not seem neccessary at all especially since recursion may use a lot of memory as you fill up the call stack. The thought may be that anything that can be solved using recursion can just be done iteratively with some sort of loop since, as we mentioned above, it's used for problems that requires reptition. This is far from the truth. While it is true that there are recursions solutions which could easily be solved with loops, there are situations where loops would not work at all and recursion would be the best answer.

Now what are these situations? Essentially, any solution where you have one number, or you start at some point, and you need to branch off and check if there is a valid answer and if not go back to an original point and branch off again, essentially when you know that your answer requires checking serveral different values, and these values are all connected to one value. Take for example the Flood Fill function, which can be seen happening in a game like Minesweeper where you can click on an empty square and it uncovers surrounding empty squares up until it reaches a non-empty square. What's happening here is that the first square will be uncovered, and then you have to check the surrounding squares in all directions, if there are any empty squares surrounding it, then you uncover those squares and check the square surrounding those, and then so on and so on until you reach a non-empty square. Based on the example above, you can see that it would be difficult to set up a function with a loop because there several loops occuring at different points, and you don't know how many will need to occur. So to summarize, recursion would be best when:
 - Your solution requires some sort of branching from a singular point
 - The solutions seems like it requires several loops
 - You know when you would like to stop a loop/repitive action but you don't when you will get there.

 
### How do we write recursion?
This is the trickest part, recursion is difficult and requires practice! 

First thing to consider is the base case, essentailly, at what point dp we want to stop the recusions. See for example the solution for the Fibonacci number, the base case is when n=0 or n=1, essentially, when the fibonacci sequence calls fib(0) and fib(1) stop calling fib! The base case is very important for recursion, otherwise, we just have endless recursion.

Next consider what you want to get out of this solution. If the situation calls for a list of all possible combinations, then we need an array returned, and this most likely will call for some global variable we can push to and what is a known as a recusrive helper function. If it just requires one value, our recursive function returns one value everytime.

Also consider how do we get to the base case, what will we do the data that we are following. Whatever we do, we will most likely have it mutate when we call the recursive function again, see the fibbonacci function as an example, each time we call it, we subtract 1 from n.

### Additional Notes on Recursion
- A recursive helper function is essentially a function within another function, why might we do this? To remove the concern for needing for a recursive function to hold onto infomation with parameters, the outer function can be used to hold onto information. These functions are helpful for when we need to return a list of combinations.

## Sorting
In regards to sorting algorithms, below are some notes:
### Insertion and Bubble
- There are stable sorts and and unstable sorts. Stable sorts keep the initial order of a collection after sorting by some other feature/attribute. This is important to consider especially when you are sorting by two different factors, otherwise, you may not get what you want.
- There are two types of sorting, distribution sorting and comparison sorting. The names are self-explanatory, essentially one will sort items in a group of other items, and the other compare items to other items for sorting.
- **Bubble Sort** is one of the least inefficient sorting algorithms but it's going to know about how it's done to give us content. Bubble sorts starts at one end and then compares the first pair of numbers, and swaps the numbers if the first number is greater than the second number. Then it moves to the second and third number and compares and swaps if necessary, and then so on and so on. This way, the largest number bubbles to the very end, and then we start all over again to have the second largest number bubble to the end.
- **Insertion Sort** is when you start at the beginning and then consider the second number and insert it in the right place (considering the two numbers), then move to the next number and insert where it makes sense, and so on and so on. **Bubble Sort and Insertion Sort are the same in terms of their time and space complexity being O(N^2) and O(1) respectively, and both are stable**.
### Divide and Conquer
- Quick Sort and Merge Sort are considered the divide and conquer sorts cause well.. they divide and conquer the collection! Essentially they break down whatever collection we have into multiple smaller pieces (through recursion) and then sort the smaller pieces.
-**Merge Sort** is the sort that first breaks the collection down through recursion in 1 element long, then they combine the elements such that there are several groups of 2, and those sort those, then they comebine again such that there is a group of 4 now, and that is sorted, and so on and so on. If there's an odd number, that's fine too, there can be groups of 3.
-**Quick Sort** is when we pick a pivot in the collection, partition the collection based on that pivot such that all elements lower is one side and all elements higher is on the other side. After this is done, we do it again on the two new sides we created! Partition based on pivot! How can we partition it? Pick a random pivot number, then go through the array to create two new arrays, one where it's larger than the pivot and one where it's smaller than pivot. Then we combine, the array with smaller elements, the pivot, and the array with larger elements together *BUT* only after doing the same thing with the other two elements.
-It's interesting to note that in terms of Big O Notation, merge sort is O(N log(N)) but Quick Sort is O(N^2), however both algorithms are actually considered to be really effective at sorting, how is this possible? Well, recall Big O Notation is only based on worst case scenario, but generally, on average, they're both O(average)(log(N)). Also consider the fact that Quick Sort uses less memory (O(log(N)), remember merge sorts creates an array for every element! Memory can affect the overall speed as well!
### Bucket and Radix Sorting
- Bucket and Radix sorting are distribution sorts as the main concept of the sort algorithim is sorting them into specific groups, rather than comparing to one another.
- For **Bucket Sorting**, you'll need to determine what buckets you have first, and then you sort your items into each bucket. With that in mind, we obivously need to determine what buckets we have, for a collection of numbers, determine the max and min of the numbers, determine the number of buckets we need (usually the square root of the total number of items) and then we can determine our bucket ranges. After this we can create separate arrays for each bucket, and then we can start looping through the array. Using what we know about our min, and bucket sizes (magnitude of their range) we take each item and sort them to their respective bucket. Once all items are sorted into each bucket we can sort each of them which will be faster since we're doing it at a smaller scale, and then we combine them.
- For **Radix Sorting**, it can almost be like layers of distribution sorting, where we sort by the radix of an item, also known as the base of an item. So when it comes to numbers, we're sorting by each base which means we can sort all items by their Least significant digit, then the next significant digit, and then the next significant digit. Now keep in mind, for radix sorting to work, it needs to be a stable sorting such that we don't lose the order of the numbers when we sort multiple times, otherwise if the sorting is not stable it defeats the purpose of the subsequent sorting. So to begin (when we're working with numbers), we need to create buckets, one for each possible digit, essentially we need 10 buckets, representing 0-9. Once we have our buckets, we loop through our collection of items, and sort them to their respective bucket based on their LSD, once we do that, we can combine all arrays and now they're sorted based on the LSD. Then we recreate the buckets, and loop through this new array and distribute them to their respective bucket based on the next significant digit, and then so on and so on.
- Now for these types of sorting methods, the data is prefered to be densed in the sense that we don't have a huge range. For examples if we were sorting 10 numbers and the minimum number was 3 and the maximum numbers was 1000, but all the other numbers were around 1-30, can you imagine how are buckets will look like? Most elements will fall in one bucket, and this really defeats the purpose of distribution sorting because you're not breaking it into smaller groups and sorting them.
### Binary Search
The Binary Search Algorithim is an algorithm for sorted arrays and only sorted arrays and it is extremely fast. Essentially when going through a collection of items that are sorted you start at the very middle of the collection and then you can decide which side of the collection will have the item you're looking for. Once you do, you discard the other side of the array and you look at the middle of the array you picked, is it the item you're look for? If yes, sweet! If no, then again decide which side of the collection you want and which side you'll discard. So this code will require you to repeatedly find the middle of an array and keep track of an upper and lower bound, until you find your item OR if your middle element becomes starts incepting the upper and lower bound.

## Data Structures
### Linked List
- A linked list contains nodes which in the context of a linked list are units that contain data, and potentially two pointers, one pointer to the next item in the list and depending on the type of linked list, a poitner to the previous item in the list. Keep in mind that in other languages besides JavaScript or Python, arrays are static, they're size doesn't grow, this is why linked list are more prevalent in these languages, because it uses pointers to other data, a set size is not required.
  - Why not use a link list over an array all the time? Because it does require more space since each node needs a pointer and a data and it takes more time to read data as you need to go through the linked list where in an array you can just pick which index
  - **Application:** Consider using a linked list when that data that is stored in the linked list needs to be accessed together. Some files are stored as linked list, their data are split into chunks and all the chunks are nodes in a linked list.
### Stack
- A type of data structure that follows a first in last out approach. Think of it as a special type of an array or linked list, where we can only look at the item that was last entered into the stack; if we wanted to look at that other items we need to remove the items on top first. It's very a limited data structure in terms of functionality, but it does provide great efficiency for the actions that  you can do, such as accessing the item pushed on top of the stack, or removing or adding a new item.
- **Application:** With such limited functionality, it might be difficult to understand what we use stacks for, but the best example is to consider the call stack. The call stack is what we use in programming to keep track of what functions we want to execute. There's a specific order we want to follow when we write functions, callback functions and recursions, and the call stack helps us maintain that by ensuring first in, last out.
### Queues
- A type of data structure that follows a first in first out approach. Similiar to a stack, it's a special type of an array or linked list (depends on how you want to implement it) where we can only access the item that was first in, and if we want to access any other items we have to remove all items before that. Again, similiar to a stack, it has very limitted functionality but it's super efficient at what it can do.
- **Application:** Essentially anywhere, where you need to prioritize things by when they come up, for example the printer when it's printing items or CPU schedule.
- Now there are variations of queues, such as: 
  - The priority queue, where we not only consider when an item was entered in the queue, but also it's priority level. With that in mind, when are removing anything priority queue we need to search through it to find the highest priority, this will have a time complexity of O(n) because you don't know which item has it and you need to go through them all.
  - The double ended queue where we don't just remove items from the beginning but from the end. You can imagine that if you do have a double ended queue, you need to have a doubly linked list. 
### Hash Tables
- A hash table is a type of data structure that implements an associative array abstract data type meaning that it maps keys to value but what sets it apart from just your regular associative array (like a javascript object, or a python dictionary) is that when you store data in a hash table, it uses a hash function to decide where the data is stored in the table. 
- The *hash function* takes a key, which can be the data, or parts of a data, and scrambles it with an algorithm to produce an index in the table, and this where the data will be stored. This has function must be consistent meaning that a key must always have the same value.
- A perfect hash function would have be written such that no key value will ever produce the same index, but this is unrealistic, the more data we have the more likely we are to run into the situation where the hash function produces the same index value for the same key - this is what is called a collision. We can approach a collision two ways:
  - We can do probing where if a collision occurs, we just find the next available spot:
    - Linear probing where we just move to the next spot in the table and see if it's available, if it's not we check the next one after.
    - Quadractic probing where we check 1 spot after, then 4 spots after, then 9, and so on and so on.
    - Double Hashing, if a collision occurs, just hash again.
  - We can also do chaining, where if a collision occurs, that new key is still linked to that index; it's just chained to the element that's already there.
  - Which way is better?
    - Probing does not require another data structure, and it allows a table to filled up more efficiently. However, that means a table can be completely filled up, and the addresses of a key is sometimes unpredictable as probing can take a key to some random value
    - Chaining allows allows a table to keep growing since values just keep getting chained on (typically using a linked list), and the values are always predicatable. Chaining does require more memory and processing since we are creating a linked list, AND sometimes certain slots in table will never get filled.
- Why is this better than just an associative array? Because we're using simple indexes to store data, it will use less memory, and we can still find our data.
- **Applications:** It's use is great for storing data and retrieiving it fast from a collection of million/billion entries, think of a spell checker. When you type a word, there will be a problem that takes whatever you typed, but it through a hash funciton and then see if it exists in a hash table containing all the known words. If it's not in the table, we know the word is spelt wrong!
### Sets
- Sets are another type of a list structure, like an array, however it only allows unique values. These are great for determining how many unique values you have let's say in an array.
### Trees
 - A tree is data structure that is a collection of nodes amd edges (the connections between nodes), and there is a visible hierarchy. In a tree:
   - There is a root node which, despite the name, sits at the very top of the tree, it's the root of all the nodes.
   - All nodes only have one parent node (we're not talking about a family tree here, only one parent!)
   - Nodes that have no child nodes are called leaves
   - The length of the longest path from a leat to the root is a tree's height
- **Applications:** Where do we see these types of data strucutres in action? Think of your basic file storage, files are all children of one folder (one parent) and it can go on and on. There is a root folder. Essentially anywhere you need a sort of hierachy. Even the DOM, the document object created by the browser, is a a tree!
- Now, there are specific types of trees, one tree is the binary tree where a node will only have two children max, a left and a right, and the left node will always hold data that is lower than the parent, and the right will hold the higher value.
- How should traverse a tree structure? There are two ways:
  - Breadth-first where you go level by level in a tree. I imageine if you go level by level, you need to store in memory which nodes are on which level, therefore breadth-first is more memory intensive (cause it's bread). We should use breadth first if our tree is very deep, or if the value we're looking for we know is near the top, or, if  you're trying to find the shortest path.
  - For depth-first, it is a more memory efficient method since  you're not holding a node in memory, this method involves going down a branch, then back up, and then down a branch again. Now this is better than breadth-first if we need to get to the bottom of a tree faster, it works better if a tree is wider since it's shorter. We can use depth-first to understand dependencies in data better.
### AVL Tree
- Now think about the situation where we have a tree that only goes to the very right think about the tree 10,11,12,13,14. This is essentially just a linked list, if we were to look for a specific value in this tree, the time complexity is O(n) - it doesn't have the efficiency that comes with a tree! Why is it like this? Because the tree is imbalance (meaning somewhere in the tree one branch is longer than another more than one node)! So, when a tree is imbalance, it becomes less efficient, so we never want a tree to be imbalance *hence* we want to use an AVL tree, it's a self balancing tree! When an AVL tree does an insertion, it checks if there's an imbalance, and if there is, we move the nodes around - this is called rotating.
### Trie
- A trie, pronounced try, is a type tree used for storing alphabetical data, it is not like binary tree where a node has a left or right, a node can have many edges/connections to other nodes. It's **application** for predicting word says a lot about how it looks like, it's essentially a connection of a bunch of connections to form words. Consider google's search bar, if you type "Be",  you've gone down a trie data structure already, and to predict your word it looks all of the other nodes connected to "Be" which could be a lot.
### Graph
- A graph is a collection of nodes and edges, sort of similiar to a tree, *HOWEVER* there isn't really a hierachy, a node in graph can have many edges to other nodes, there isn't a parent/child language involved in a graph. It's a network of nodes and that's what it's used to model, a network of data. 
  - A graph can be directed or undirected. In a directed graph, a edge between nodes go only one way. In a undirected graph, a edge goes both ways,
  - Graphs can be represented with a two dimension array where a row represnts a node each element in the row represnts an edge to another node. Or it can be represented using an object/dictionary where each node has its own array showing us to which node it's connected to.
  - Graphs can be traversed two ways, breadth-frist and depth-first, like a tree.
  
## Search
### Binary Search
- A binary search is an algorithm to search in an array that is sorted which is O (log n). 
- To do this search, we need to use two indexes, one starting at the beginning and the other starting at end. Then we look in the middle.
- If the value we're looking for is not in the middle, we look at the section that will have the value by looking at the value in middle (because it's sorted). Then we look at the middle of that section. If we can't find the value, it'll be a point where the values repeat, or one the left index is higher than the right index.

## Operating Systems
### What is an operating system?
The operating system is the software that acts as the interface between the computer's hardware and other applications that a user might use. It essentially provides three essential capabilities:
 - A UI for a user to interface with, either through a CLI or GUI, which allows a user to use the OS to do things such as set up/troubleshoot the hardware. 
 - Launches and manages applications. The OS will also provide APIs to enable the applications to utilize the OS and hardware functions. For example, the OS allow applications to receive inputs from hardware such as a keyboard or mouse.
 - Manages devices, the OS is responsible for managing devices (identifying and configuring, and providing applications with common access to underlying computer hardware devices)
 
The best way to think of why we need operating system is that it allows software/applications to remain focus on its business logic rather than how it will work with a computer's hardware. Can you imagine if we didn't? Then every application would need its own UI as well as really comprehensive code needed to handle all low-level functionality of the hardware, and that's a lot more code. With OS, these applications just use API's specific to an OS to work with the hardware.

### What is the Kernal?
The Kernal is considered to be the core of the operating system, this is the piece of the code that makes the operating system really the interface between hardware and other applications. It handles memory management (checks out memory space for the proper execustion of application programs), process management, task management and disk management. It may be easier for us to say that the Kernal and OS is exactly the same but that's not true, the OS is more than the Kernal, the OS also includes the shell (or in general a UI) that allows us to interact with the Kernal.

## Virtualization 
Virtualization is the process of creating a virtual version of something (not physically existing as such but made by software to appear to do so). This is commonly done to create virtual computers hence why we have so many virtual machines (essentially computers that exist as a software). To allow for virtualization on a computer, we need to use another software called the hypervisor, this software basically allows us to spin up a virtual computer (virtual OS and virtual hardware) and then allows it to interact with the host's hardware.

The benefits of virtualization are:
 - We can fully take advantage of a server and it's resources, especially if we just have a server to host one app. And the same time we can also have less servers.
 - Threat Isolation, a virtual computer is completely isolated from the host computer.
 - It's easier to backup and recover virtual machines because they're essentialy files. You can also easily create identical machines.
 
## Containers
Containers are essentially a lighter weight, more agile way of handling virtualization, rather than spinning up a virtual machine as we discussed above with the virtual OS and the virtual hardware, it just spins up a virtual operating system which has everything it needs to run a small piece of software and only the software. Because the container consists of the code, dependencies, and operating system, it allows us to run an application any where consistently. 

## SOLID Principle
Remember that OOP is a programming paradigm based on the concept of "objects", everything is an object and each object has their own data and logic (using code of course). Essentially, computer programs are designed by making them out of objects that interact with one another. 

The SOLID Principles are five design principles to help computer programs/softwares more understandable, flexible, extenable, and maintainable. The five principles are
  1. Single Responsibility Principle
  2. Open Closed Principle
  3. Liskov Substitution Principle
  4. Interface Segregation Principle
  5. Dependency Inversion Principle
  
### Single Responsibility Principle
This principle essentially says that any class you create should focus on one responsibility/one job. This one really speaks for itself, the more we limit responsibilites given to a class the better it is because:
 - We know where the logic is for a responsibility
 - More straight forward to check if a class is working
 - Easier to understand a class
 
### Open Closed Principle
This principle states that entities should be extendable without modifying the class itself. For this principle we can think, how can we implement new code without breaking/changing the old code. Think of this as, open to extensibility but closed to modification.

**An example is where:**
 - We have a classes for shapes, a square, a circle, etc. 
 - And then we have we have a class called AreaCalculator. Given a list of the shapes, the AreaCalculator will determine the area of each shape based on what the shape is, so essentially there are a bunch of conditionals in the AreaCalculator with different logic.
 - If we introduce a new shape, say a hexagon, we need to modify the AreaCalculator to include another conditional.
 - The problem here is that this is not really extensible, everytime we add a new shape we need to modify the original code.
 
**The solution here is:**
 - Keep the logic in shape classes so that the Area Calculator just calls the function instead. This sort of plays in the single responsibility principle as we are saying that the shape classes should take the responsibility of shape related methods.
 - How do we ensure all shapes have the function/method that is called in AreaCalculator? Ensure that AreaCalculator uses a interface rather than some object 

### Liskov Substitution Principle
This principle states that anytime a base case is used in the code, it can easily be replaced with a derived class and do the same.

The idea here is that we are extending the base class without changing it's behaviour, if this isn't done, this could lead to issues because we can use children classes to replace parent classes and if for some reason the child class has a completely different behaviour, we may not get what we expected, or we may even have an error.

Bottom line, when extending a class, make sure the derived class can still be in places where the parent class is used. 

### Interface Segregation Principle
This principle states that an interface shouldn't cover too much as we don't want a client to implement an interface where it won't need everything on the contract. This is sort of a single responsibility but for interfaces

### Dependency Inversion Principle
This principle states that high level module must not depend on the low level module, rather both modules should depend on abstractions. So instead of seeing high level classe that are creating the low level classes inside of them (which means there's a depedency on this low level class), these low level classes are being created somewhere else and the high level classes are able to access them.

The idea here is that we are inverting control in the sense that these low level classes are no longer being controlled by a high level class, we have decoupled them. The reason for doing so is because:
 - We can easily replace the low level class or update it without impact the high level class
 - This also allows to test classes in isolation easier since we can replace the low level class with some sort of mock that does exactly what we need it to do
 - It's easier to manage all the dependencies 

## Dependency Injection
This is the method that supports the Dependency Inversion Principle, and is a technique that falls within the idea of Inversion of Control. In C#, essentially, classes that have depedencies no longer create and manage that dependency, instead, it is passed, or injected into it when instantiated. This classes just need to state its dependencies via interfaces.

This way the higher level classs is also decoupled in the sense that it doesn't know what's being passed into it, as long as it call these methods. This is great for testing in isolation.

**Note:** This is a popular technique in .NET to handle dependencies. The reason we don't see this with NodeJS is because we just handle dependencies with require.
