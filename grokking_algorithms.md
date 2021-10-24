# Grokking Algorithms  

## Chapter 1 : Introduction to Algorithms  
*Page 1-19*

Algorithms is a set of instructions for accomplishing a task. Every 
piece of code could be called an algorithm. We learn about the fast, or 
the ones that proved solving interesting problems.

### Binary Search  
It is an algorithm that takes in a sorted list of elements. If an 
element you're looking for is in that list, binary search returns 
tbe position where it's located, Otherwise binary search returns 
null.

Suppose you are searching for a word in dictionary. The dictionary 
has 240,000 words. In worst case, simple search could take 240,000 
steps. In binary search you go to the middle of the dictionary 
if that's not it (if it's before this point), you go to the first 
middle's middle, then you repeat each time you eliminate half of 
the problem.

So binary search will take 18 steps in worst case.

### Big O Notation  
It tells you how fast an algorithm is. Not in seconds though. 
But it tells you how fast the algorithm grow as the input size 
grows.

Big O establishes worst case runtime.

Common Big O runtimes  
- O(log n) *Logarithmic*  
- O(n) *Linear*  
- O(n log n)  
- O(n^2) *Quadratic*  
- O(n!) *Fractional*  

So algorithms isn't measured in seconds, but in growth of the 
number of operations. Instead, we talk about how quickly the 
runtime of an algorithm increases as the size of the input 
increases.

---

## Chapter 2 : Selection Sort  
*Page 21-36*

### Arrays and Linked Lists  
**Arrays** store elements in a sequential positions somewhere in the 
memory. whenever you want to add a new element, you'll have to 
create a new array to hold all the elements as the next sequential 
position would have been taken.

**Linked Lists** store elements in different positions in the memory. 
Each element holds an address to the next element. So it's easy 
to add elements to a list. But not easy to find ode.

|   |Arrays|Linked Lists|
|---|---|---|
|Reading|O(1)|O(n)|
|Inserting|O(n)|O(1)|
|Deleting|O(n)|O(1)|

- O(1) *Constant*

#### Types of Access  
Random (Arrays) :  
Jump directly to the "n"th element.

Sequential (Linked Lists) :  
Reading the elements one by one, starting at the first element.

### Selection Sort  
In selection sort you iterate over the entire array `n` times to 
find the smallest element in each iteration.

So it takes `O(n^2)` to sort the array.

* Remember constants in Big O is ignored, you might say that each 
iteration you go over fewer elements `(n-1)`. While that's true, yet
Big O ignores constants.

### Example : 
```java
public ArrayList<Integer> sort(ArrayList<Integer> array) {
    ArrayList<Integer> sortedArr = new ArrayList<>();
    int arrayLength = array.size();
    for(int i = 0; i < arrayLength; i++) {
        int smallestIndex = findSmallest(array);
        sortedArr.add(array.remove(smallestIndex));
    }
    return sortedArr;
}

private int findSmallest(ArrayList<Integer> arr) {
    int smallest = arr.get(0);
    int smallest_index = 0;
    for(int i = 0; i < arr.size(); i++) {
        if(arr.get(i) < smallest) {
        smallest = arr.get(i);
        smallest_index = i;
       }
    }
    return smallest_index;
}
```

---

## Chapter 3 : Recursion  
*Page 37-50*

### Recursion  
Recursion is when a method calls itself repeatedly until it reaches 
an exit condition and returns.

Many important algorithms use recursion, so it's important to 
understand the concept.

### Base Case and Recursive Case
Every recursive function has two parts: *the base case and the 
recursive case*. The recursive case is when the function calls itself. 
The base case is when the function doesn't call itself again, 
so it doesn't go into an infinite loop.

Consider the following function that calculates a number's factorial : 
```java
public int factorial(int n) {
    if (n == 1) return n;            //base case
    return (n * factorial(n - 1));   //recursive case
}   
```

### The Stack  
The call stack is an important concept in
general programming.  
In Arrays and lists you could add an item anywhere in the list. 
The stack is much simpler. When you add an item, it gets added 
to the top of the list. When you read an item, you read only 
the top most-item, and it's taken off the list. So your stack 
has only two actions, push (add to the end of the list), and 
pop (remove the top-most item and read it).

Your computer uses a stack internally called the call stack.

Let's demonstrate it.
```java
public static void main(String[] args) {
    System.out.println("Hello!");
    greatUser("User");
    System.out.println("Welcome!");
}
```

In the above example, the main function gets called. Your computer 
allocates a box of memory for the main function. If there's a variable 
the variable gets saved in memory. Every time you make a function call,
your computer saves the values for all the variables for that
call in memory. Next the `greatUser(userName)` function gets called, 
so your computer allocates memory for that function. Using a stack 
of memory boxes the recently called function's memory box gets 
*pushed* on top of that stack. When the function is done and hits 
the `return` statement that box (top-most) gets popped off the stack 
and then the top-most becomes the box becomes the function that called 
the one we just popped off.


---

## Chapter 4 : Quick Sort  
*Page 51-72*

### Divide and Conquer  
Suppose you're a farmer with a plot of land.  
The land is **1680** Meters wide, and the height is **640** Meters.
You want to divide this farm evenly into *square* plots. You want
the plots to be as big as possible.

How to figure out the largest size you can use for a plot of land? 
Use D&C.  
To solve the problem using D&C there are two steps :  
1. Figure out the base case. This should be the simplest possible 
case.  
2. Divide and decrease your problem until it becomes the base case.  

Let’s use D&C to find the solution to this problem. What is the largest
square size you can use?  
First, figure out the base case. The easiest case would be if one side was
a multiple of the other side.  
Suppose one side is 25 meters (m), and the other side is 50 m. Then the
largest box you can use is 25 m × 25 m. You need two of those boxes to
divide up the land.  

Now you need to figure out the recursive case. This is where D&C
comes in. According to D&C, with every recursive call, you have to
reduce your problem. How do you reduce the problem here? Let’s start
by marking out the biggest boxes you can use.

You can fit two 640 * 640 boxes here, and there's some land 
still left to divide. There’s a farm segment left to divide.
Why don’t you apply the same algorithm to this segment?  
You have 400 * 640 left.

So you started out with a 1680 × 640 farm that needed to be split up.
But now you need to split up a smaller segment, 640 × 400. If you find
the biggest box that will work for this size, that will be the biggest box
that will work for the entire farm. You just reduced the problem from
a 1680 × 640 farm to a 640 × 400 farm!

####Euclid’s Algorithm  
“If you find the biggest box that will work for this size,
that will be the biggest box that will work for the entire farm.”

Let’s apply the same algorithm again. Starting
with a 640 × 400 m farm, the biggest box you
can create is 400 × 400 m.

And that leaves you with a smaller segment, 400 × 240 m.
And you can draw a box on that to get an even smaller segment,
240 × 160 m. And then you draw a box on that to get an even 
smaller segment. Hey, you’re at the base case: 80 is a factor
of 160. If you split up this segment using boxes, you don’t 
have anything left over!

So, for the original farm, the biggest plot size you can 
use is 80 × 80 m.

To recap, here’s how D&C works :  
1. Figure out a simple case as the base case.  
2. Figure out how to reduce your problem and 
get to the base case.

Example of a function that calculates the sum of a list of 
numbers.  
The base case is `if the list is empty return 0`.  
Let's reduce the problem to reach the base case. First we 
check if the list is empty (base case). If not we return 
the first element of the array plus the sum of the rest of 
the array. We recursively repeat that until we hit the base 
case.

```java
public int sum(List<Integer> list) {
    if (list.isEmpty()) return 0;
    return list.get(0) + sum(list.subList(1, list.size()));
}
```

### Quick Sort  
Quick sort is a sorting algorithm that's much faster than selection 
sort and is frequently used in real life.  

Let's use it to sort an array. What is the simplest array 
a sorting algorithm can sort? Empty arrays and arrays that 
have one element. So that's our base case (we can return them
as is).  

Here's how quick sort works.  
Find an element from the array, we will call it *pivot*. 
Will see later how to choose good pivot but for now let's 
pick the first element in the array `[33, 15, 10] -> pivot 
is 33`. Now find the elements smaller than the pivot and 
the elements larger than the pivot. This is called partitioning. 

Now you have  
- A sub array of all elements smaller than the pivot.  
- The pivot.  
- A sub array of all elements larger than the pivot.  

The two sub-arrays aren't sorted they are just partitioned.
But if they were sorted, then sorting the whole array would 
be pretty easy. You would then combine the whole thing like
`left array + pivot + right array` and you get a sorted
array.

How do you sort the sub-arrays? If you call quicksort on the two
sub-arrays and then combine the results, you get a sorted array! 
`quicksort([15, 10]) + [33] + quicksort([])`. This will work with 
any pivot.  

Here are the steps :  
1. Pick a pivot.  
2. Partition the array into two sub-arrays: elements less than 
the pivot and elements greater than the pivot.  
3. Call quicksort recursively on the two sub-arrays.  

Here's a code example for quick sort :  
```java
public List<Integer> sort(List<Integer> list) {
    if (list.size() < 2) {
        return list;
    }

    int pivot = list.remove(0);
    List<Integer> smallerThanPivotList = new ArrayList<>();
    List<Integer> greaterThanPivotList = new ArrayList<>();

    for (int element : list) {
        if (element <= pivot) smallerThanPivotList.add(element);
        else greaterThanPivotList.add(element);
    }

    List<Integer> sortedList = Stream.of(sort(smallerThanPivotList), List.of(pivot), sort(greaterThanPivotList))
            .flatMap(Collection::stream)
            .collect(Collectors.toList());

    return sortedList;
}
```

### Big O Notation Revisited  
Quicksort is unique because its speed depends on the pivot 
you choose.

There’s another sorting algorithm called merge sort, which is
O(n log n). Quicksort is a tricky case. In the worst case, 
quicksort takes O(n2) time.

It’s as slow as selection sort! But that’s the worst case. 
In the average case, quicksort takes O(n log n) time. 
So you might be wondering :  
- What do *worst case* and *average case* mean here?  
- If quicksort is O(n log n) on average, but merge sort 
is O(n log n)always, why not use merge sort? Isn’t it faster?  

#### Merge sort vs Quick Sort  
In Big O notation we know that it ignores the constants.
But sometimes the constant can make a difference. Quicksort 
versus merge sort is one example. Quicksort has a smaller 
constant than merge sort. So if they’re both O(n log n) time, 
quicksort is faster. And quicksort is faster in practice 
because it hits the average case way more often than the 
worst case.

So now you’re wondering: what’s the average case versus 
the worst case?

#### Average Case vs Worst Case  
The performance of quicksort heavily depends on the pivot you choose.
Suppose you always choose the first element as the pivot. And you
call quicksort with an array that is already sorted. Quicksort doesn't
check to see whether the input array is already sorted. So it will still try
to sort it.

We’re not splitting the array into two halves. Instead, one
of the sub-arrays is always empty. So the call stack is really long. 
Now instead, suppose you always picked the middle element as the 
pivot.

The first example you saw is the worst-case scenario, and the second
example is the best-case scenario. In the worst case, the stack size is
O(n). In the best case, the stack size is O(log n).

If you always choose a random element in the array as the
pivot, quicksort will complete in O(n log n) time on average. Quicksort
is one of the fastest sorting algorithms out there, and it’s a very good
example of D&C.

So if we alter our quick sort example from before we will change only 
one line :  
```java
//int pivot = list.remove(0);
int pivot = list.remove(list.size() / 2);
```

---

## Chapter 5 : Hash Tables  
*Page 73-94*

Suppose you have a menu, your menu is an array of items, each 
item contains a name, and a price `[(Apple, 3), (Orange, 2.75)]`. 
Now you want to search for an item in the array. If the array 
is unsorted you will have to use simple search and go through 
every item in the array to find your item. If the array is 
sorted you can use binary search. Simple search as we know 
takes O(n), while binary search takes O(log n). But what 
if you have someone that memorizes all the items in the array.
You can just ask him / her about the item, and she / he will 
reply instantly. That will take O(1). Which is instant.
That’s where hash functions come in.

### Hash Functions  
A hash function is a function where you put a string (string here 
means any kind of data - a sequence of bytes), and you get back 
a number.

In technical terminology, we'd say that a hash function maps 
Strings to Numbers. There are some requirement to hash function :  
- It needs to be consistent. For example, suppose you put in "Apple" 
and get back 4. Every time you put in "Apple", you should get 4 back. 
Without this your hash table won't work.  
- It should map different words to different numbers. For example, 
a hash function is no good if it always returns 1 for any word 
you put in. In the best case every word should map to a different 
number.

So what does a hash function good for? Well, you can use it to make 
yourself that "someone" that memorizes everything.

Start up with an empty array. You will store all of your 
prices in the array. Let's add the price of an apple. Put 
"Apple" into the hash function. The hash function outputs 3.
So let's store the price of an apple at index 3 in the array. 
Let's put "Milk" into the hash function. The hash function 
returns 0. Let's store the price of milk at index 0. Keep 
going, and eventually the whole array will be full of prices.

Now if you want to know what's the price of an avocado. You don't 
have to search for it. You just put "Avocado" into the hash function, 
and it tells you that the price of an avocado is stored at index 
4 in the array.

The hash function tells you exactly where the price is stored, so you
don’t have to search at all! This works because :  
- The hash function consistently maps a name to the same index. Every
time you put in "Avocado", you’ll get the same number back. So you
can use it the first time to find where to store the price of an avocado,
and then you can use it to find where you stored that price.  
- The hash function maps different strings to different indexes.
"Avocado" maps to index 4. "Milk" maps to index 0. Everything maps
to a different slot in the array where you can store its price.  
- The hash function knows how big your array is and only returns valid
indexes. So if your array is 5 items, the hash function doesn't return
100 … that wouldn't be a valid index in the array.

### Collisions  
Most languages have hash tables. You don't need to know how to 
write your own. But to understand the performance of hash tables, 
you first need to understand what collisions are.

First, I've been telling you a white lie. I told you that a 
hash function always maps different keys to different slots 
in the array.

In reality, it's almost impossible to write a hash function 
that does this. Let's take a simple example. Suppose your 
array contains 26 slots. And your hash function is really 
simple: it assigns a spot in the array alphabetically.
Now you want to store the price of "Apple" in the hash, you get 
assigned the first slot. Then you want ot store the price of 
"Avocado" in the hash, you get assigned the first slot again. 
This is called a *collision :* two keys have been assigned in 
the same slot. This is a problem. If you store the price of 
avocados at that slot, you'll overwrite the price of apples.

Collisions are bad, and you need to work around them. There 
are many ways to deal with collisions. The simplest one is 
if multiple keys map to the same slot, start a linked list 
at that slot.

If you then want to search for the price of "Apple", 
you have to go to the first slot and search the linked 
list to find it. If the linked list is small, no big deal. 
But suppose all of your items start with "a". The entire hash 
table will be empty except of one slot. And that slot has a 
giant linked list. Every single element in the hash table is 
in that linked list. That's as bad as putting everything in a 
linked list to begin with. It's going to slow down your hash 
table.

There are two things to consider here :  
- Your hash function is really important. Your hash function 
mapped all the keys to a single slot. Ideally, your hash function 
would map keys evenly all over the hash.  
- If those linked lists get long, it slows down your hash 
table a lot. But they won't get long if you use a good hash 
function!

The hash function is very important. How do you choose a good 
hash function. That's in the next section.

### Performance  
In average case, hash tables take O(1) for everything (search, 
insert, delete). O(1) is called constant time. It doesn't mean 
instant. It means the time taken will stay the same, regardless 
of how big the hash table is.

In the worst case, a hash table takes O(n) for everything,
which is really slow. 

Let's compare hash tables to Arrays and lists.

|   |Hash Tables (Average)|Hash Tables (Worst)| Arrays|Linked Lists|
|---|---|---|---|---|
|Reading|O(1)|O(n)|O(1)|O(n)|
|Inserting|O(1)|O(n)|O(n)|O(1)|
|Deleting|O(1)|O(n)|O(n)|O(1)|

It's important that you don't hit the worst-case performance 
with hash tables. And to do that, you need to avoid collisions. 
To avoid collisions, you need :  
- A low loader factor.
- A good hash function.

#### Load Factor  
The load factor of a hash table is easy to calculate `Number of 
items in the hash table / Total number of slot`.

Hash tables use an array for storage, so you count the number of
occupied slots in an array. For example, this hash table has a 
load factor of 2/5, or 0.4.  
`[empty, 1, empty, 0, empty]`.

Load factor measures how many empty slots remain in your 
hash table.

Suppose you need to store the price of 100 produce items in 
your hash table, and your hash table has 100 slots. In the 
best case, each item will get its own slot.

Having a load factor greater than 1 means you have more items 
than slots in your array. 

Once the load factor starts to grow, you need to add more 
slots to your hash table. This is called resizing. With a 
lower load factor, you'll have fewer collisions, and your 
table will perform better. A good rule is, resize when your 
load factor is greater than 0.7.

Resizing is expensive, and you don't want to resize too often. 
But averaged out, hash tables take O(1) even with resizing.

#### A Good Hash Function  
A good hash function distributes values in the array evenly.
A bad hash function groups values together and produces a 
lot of collisions.

What is a good hash function? That's something you'll never 
have to worry about. If you're really curious, look up the SHA 
function (there's a short description of it in the last chapter). 
You could use that as your hash function.

---

## Chapter 6 : Breadth-First Search  
*Page 95-114*

Breadth-first search allows you to find the shortest distance
between two things. Graph algorithms are some of the most 
useful algorithms I know. Make sure you read the next few 
chapters carefully. These are algorithms you’ll be able to 
apply again and again.

### Introduction to Graphs  
Suppose you want to move from a point to another. There isn't 
direct connection between the two. There are some steps or points 
in between. So you want to find the shortest path to move from 
a point to another. This type of problem is called a shortest-path
problem. The algorithm to solve a shortest-path problem is 
called breadth-first search.

To figure out how to get from point `A` to point `B` there are 
two steps :  
1. Model the problem as graph.  
2. Solve the problem using breadth-first search.

### What is a Graph?  
A graph models a set of connections. Each graph is made up of 
nodes and edges.
```text
(Node) ----Edge---- (Node)
```

A node can be directly connected to many other nodes. 
Those nodes are called its neighbors. Graphs are a way to 
model how different things are connected to one another.

### Breadth-First Search  
We already know Binary search. Breadth-first search is a different 
kind of search algorithm, one that runs on graphs. It can answer 
two types of questions :  
1. Is there a path from node `A` to node `B`?  
2. What is the shortest path from node `A` to node `B`?  

#### Finding the Shortest Path  
To find the shortest path from point `A` to point `B`, you need 
to look at every point in the first-degree connections to see if 
that is the point you want before searching any second-degree 
connections. Breadth-first search does this. The way it works 
is that it radiates out from the starting point. So it will check 
first-degree connections before second-degree connections. 
Breadth-first search not only finds a path from `A` to `B`, 
it also finds the shortest path.

Another way to see this is, first-degree connections are added 
to the search list before second-degree connections. So this 
only works if you search nodes (points) in the same order in 
which they're added. What happens if you search second-degree 
before first-degree connections? You end up with a node (point) 
that isn't the closest to you in the graph. So you need to search 
people in the order that they're added. There's a data structure 
for this, it's called a *queue*.

#### Queues  
A queue works exactly like it does in real life. Queues are 
similar to stacks. You can't access random elements in the queue. 
Instead, there are only two operations, enqueue and dequeue.

If you enqueue two items to the list, the first item you added 
will be dequeued before the second item. You can use this for 
your search list! People who are added to the list first will 
be dequeued and searched first.

The queue is called a FIFO data structure, First In, First Out. 
In contrast, a stack is a LIFO data structure, Last In, 
First Out.

### Implementing the Graph  
First, you need to implement the graph in code. A graph consists 
of several nodes. And each node is connected to neighboring nodes.
How do you express a relationship like `you -> bob`?
Luckily, you know a data structure that lets you express
relationships, a hash table!

Remember, a hash table allows you to map a key to a value. 
In this case, you want to map a node to all of its neighbors.

Here's how you'd write it in Java :  
```java
Map<String, List<String>> graph = new HashMap<>();
List<String> firstDegreeConnections = Arrays.asList("Omar", "Sarah", "Aya");
graph.put("You", firstDegreeConnections);
```
- *In Java we have two implementations for hash tables, 
`Hashtable`, and `HashMap`.*

Notice that `"you"` is mapped to an array. So `graph["you"]` will 
give you an array of all the neighbors of `"you"`.

A graph is just a bunch of nodes and edges, so this is all you need to
have a graph in Java. What about a bigger graph?
```java
Map<String, List<String>> graph = new HashMap<String, List<String>>();
List<String> yourConnections = Arrays.asList("Omar", "Sarah", "Aya");
List<String> ayaConnections = Arrays.asList("Ahmed", "Omar");
List<String> ahmedConnections = Arrays.asList("Yara");
List<String> omarConnections = Arrays.asList();
graph.put("You", yourConnections);
graph.put("Aya", ayaConnections);
graph.put("Ahmed", ahmedConnections);
graph.put("Omar", omarConnections);
```

Does it matter what order you add the key/value pairs in?
Does it matter if you write :  
```java
List<String> ahmedConnections = Arrays.asList("Yara");
List<String> omarConnections = Arrays.asList();
graph.put("Ahmed", ahmedConnections);
graph.put("Omar", omarConnections);
```

Instead of :  
```java
List<String> ahmedConnections = Arrays.asList("Yara");
List<String> omarConnections = Arrays.asList();
graph.put("Omar", omarConnections);
graph.put("Ahmed", ahmedConnections);
```

Well it doesn't. Hash tables have no ordering, so it doesn't 
matter what order you add key/value pairs in.

`Omar` has an arrow pointing to him, but from him to someone else. 
This is called a *directed graph*. So `Omar` is `Aya's` neighbor, 
but `Aya` isn't `Omar's` neighbor. An undirected graph doesn't 
have any arrows, and both nodes are each other's neighbors.

### Implementing the Algorithm  
Here's how the implementation will work.  
1. Keep a queue containing the nodes to check.  
2. Pop an item off the queue.  
3. Check if the item matches your criteria.  
4. If yes, that's it. If no, add all the neighbours of that 
item to the queue.  
5. Loop!  
6. If the queue is empty there are no items that match your 
criteria.

Let's implement the algorithm. First we need to create the graph.
```java
Map<String, List<String>> graph = new HashMap<>();
graph.put("You", Arrays.asList("Omar", "Sarah", "Aya"));
graph.put("Aya", Arrays.asList("Ahmed", "Omar"));
graph.put("Ahmed", Arrays.asList("Yara"));
graph.put("Omar", Arrays.asList());
```
Now let's create a queue.
```java
List<String> queue = new LinkedList<String>();
queue.addAll(graph.get("You"));
```
- *A LinkedList in Java can be used as a queue data structure
as it implements the `Deque` interface which extends the `Queue`
interface.*

Remember that `graph.get("You")` will return a list of all of 
your neighbours. And we add them to the search queue.

Next we will keep track of the people we already searched.
```java
List<String> searched = new ArrayList<>();
```
This is used to prevent looking for the same person twice and 
also without this we could end up in an infinite loop (If your 
connection is Adam and Adam's connection is you, and that's all 
in the graph, so you could end up in an infinite loop).

Let's see the rest.
```java
while (!queue.isEmpty()) {
    List<String> person = queue.remove();
    Optional<String> found = searched.stream().filter(p -> p.equals(person)).findFirst();
    if (found.isEmpty()) {
        if (person.equals("Ahmed")) { //just a dummy search criteria for demonstration
            System.out.println(person + " is found");
            break;
        }
        else {
            String c = graph.get(person);
            if (c != null) queue.addAll(c);
            searched.add(person);
        }
    }
}
```

#### Running Time  
If you search your entire network for some criteria, that means you'll
follow each edge (remember, an edge is the arrow or connection from
one person to another). So the running time is at least O(number of
edges).
You also keep a queue of every person to search. Adding one person to
the queue takes constant time: O(1). Doing this for every person will
take O(number of people) total. Breadth-first search takes O(number of
people + number of edges), and it's more commonly written as O(V+E)
(V for number of vertices, E for number of edges).

Suppose you have a family tree. You, your parents, and your 
grandparents. Suppose you have a family tree.
This is a graph, because you have nodes (the people) and edges.
The edges point to the nodes' parents. But all the edges go down—it
wouldn't make sense for a family tree to have an edge pointing 
back up!That would be meaningless—your dad can't be your 
grandfather’s dad!A tree is a special type of graph, 
where no edges ever point back.

This is called a tree. A tree is a special type of graph, where no edges
ever point back.

---

## Chapter 7 : Dijkstra's Algorithm
*Page 115-140*

In the previous chapter we saw graph and used breadth-first 
algorithm to find the shortest path from point `A` to point 
`F`. But suppose we add travel time from any point to another.
Now you see that the shortest path we found using breadth-first 
is not the fastest path. How do we get the fastest path? the 
answer is Dijkstra's algorithm.

### Working with Dijkstra's Algorithm  
Each segment has a travel time in minutes. You'll use 
Dijkstra's algorithm to go from start to finish in the 
shortest possible time.

There are four steps to Dijkstra's algorithm :  
1. Find the "cheapest" node. This is the node that you 
can get to in the least amount of time.  
2. Update the costs of the neighbors of this node. So that if 
from the starting point to node `A` would take 5 minutes, but 
now that you are at node `B` which took you 3 minutes to get 
from the starting point, and you can get to node `A` from node 
`B` in one minute. Then update that from the start to node `A` 
there's a faster path that takes 4 minutes.  
3. Repeat until you have done this for every node in the graph.  
4. Calculate the final path.

### Terminology  
When you work with Dijkstra's algorithm, each edge in the graph 
has a number associated with it. These are called *weights*.
```text
    7 minutes
A ------------- P
```

A graph with weights is called a *weighted graph*. A graph without 
weights is called *unweighted graph*.

Graphs can also have cycles. It means you can start at a node, 
travel around, and end up at the same node. cycles add more 
weight.

Remember our talk earlier about directed and undirected graphs? 
An undirected graph means that both nodes point to each other. 
That's a cycle! Dijkstra's algorithm only works with directed
acyclic graphs, called DAGs for short.

### Trading for a Piano  
Let's see an example. Our friend Rama, is trying to trade a music 
book for a piano. Perfect! With a little bit of money, Rama 
can trade his way from a piano book to a real piano. Now he 
just needs to figure out how to spend the least amount of money 
to make those trades. Let's graph out what he's been offered.

![Rama's trades graph](./07-01.jpg)

In this graph, the nodes are all the items Rama can trade for. The
weights on the edges are the amount of money he would have to pay
to make the trade. How is Rama going to figure out the path from 
the book to the piano where he spends the least amount of money? 
We will apply Dijkstra's algorithm's four steps.

Before you start, you need some setup. Make a table of the cost 
for each node. The cost of a node is how expensive it is to 
get to.

|Parent|Node|Cost|
|---|---|---|
|Book|LP|5$|
|Book|Poster|0|
|______|Guitar|∞|
|______|Drums|∞|
|______|Piano|∞|

We will also keep track of the parent node to calculate the path 
in the end.

#### Step 1  
Find the cheapest node you can get to. In this case the poster 
is the cheapest trade at 0$. Is there a cheaper way to trade for 
the poster? Answer is no. Because the poster is the cheapest node 
Rama can get to, and there's no way to make it any cheaper. 

This is the key idea behind Dijkstra's algorithm : Look at the 
cheapest node on your graph. Make sure there is no cheaper way 
to get to this node.

#### Step 2  
Figure out how long it takes to get to its neighbors (the cost).

|Parent|Node|Cost|
|---|---|---|
|Book|LP|5$|
|Book|Poster|0|
|Poster|Guitar|30$|
|Poster|Drums|35$|
|______|Piano|∞|

Figure out how long it takes to get to its neighbors (the cost).
You have prices for the bass guitar, and the drum set in the table. 
Their value was set when you went through the poster, so the 
poster gets set as their parent. That means, to get to the bass 
guitar, you follow the edge from the poster, and the same for 
the drums.

#### Step 1 Again  
The LP is the next cheapest node at $5.

#### Step 2 Again  
Update the values of all of its neighbors.

|Parent|Node|Cost|
|---|---|---|
|Book|LP|5$|
|Book|Poster|0|
|LP|Guitar|20$|
|LP|Drums|25$|
|______|Piano|∞|

Hey, you updated the price of both the drums and the guitar! 
That means it's cheaper to get to the drums and guitar by 
following the edge from the LP. So you set the LP as the new 
parent for both instruments.

The bass guitar is the next cheapest item. Update its neighbors.

|Parent|Node|Cost|
|---|---|---|
|Book|LP|5$|
|Book|Poster|0|
|LP|Guitar|20$|
|LP|Drums|25$|
|Guitar|Piano|40$|

Ok, you finally have a price for the piano, by trading the guitar 
for the piano. So you set the guitar as the parent. Finally, 
the last node, the drum set.

|Parent|Node|Cost|
|---|---|---|
|Book|LP|5$|
|Book|Poster|0|
|LP|Guitar|20$|
|LP|Drums|25$|
|Drums|Piano|35$|

Rama can get the piano even cheaper by trading the drum set for 
the piano instead. So the cheapest set of trades will cost 
Rama $35.

So far, you know that the shortest path costs $35, but how do 
you figure out the path? To start with, look at the parent for 
piano.

The piano has drums as its parent. That means Rama trades the drums
for the piano. So you follow this edge.

Let's see how you'd follow the edges. Piano has drums as its parent.
And drums has the LP as its parent. So Rama will trade the LP for 
the drums. And of course, he'll trade the book for the LP. By 
following the parents backward, you now have the complete path.

So far, I've been using the term 'shortest path' pretty literally : 
calculating the shortest path between two locations or between 
two people. I hope this example showed you that the shortest path 
doesn't have to be about physical distance. It can be about 
minimizing something. In this case, Rama wanted to minimize 
the amount of money he spent.

### Negative-Weight Edges  
In the trading example, Alex offered to trade the book for
two items. Suppose Sarah offers to trade the LP for the poster, 
and she'll give Rama an additional $7. It doesn't cost Rama
anything to make this trade; instead, he gets $7 back.

If you run Dijkstra's algorithm on a graph with a negative weight,
Rama will take the wrong path. He'll take the longer path. You 
can't use Dijkstra's algorithm if you have negative-weight edges. 
Negative-weight edges break the algorithm.

If you want to find the shortest path in a graph that has 
negative-weight edges, there's an algorithm for that! It's 
called the Bellman-Ford algorithm.

### Implementation  
Let's see how to implement Dijkstra's Algorithm. Here's the graph we will 
use for this example.

![Rama's trades graph](./07-02.png)

To Code this you will need three hash tables `Graph`, `Costs` and `Parents`.
You’ll update the costs and parents hash tables as the algorithm progresses. 
First, you need to implement the graph. You’ll use a hash table like you 
did in chapter 6.
```java
Map<String, List<String>> graph = new HashMap<>();
```

In the last chapter, you stored all the neighbors of a node in the hash table, 
like this : 
```java
graph.put("You", Arrays.asList("Omar", "Sarah", "Aya"));
```

But this time you need to store the neighbor, and the cost for getting to that 
neighbor. You can use another hashmap. We will create a graph class to store 
this data.

Let's create the `Graph` class.
```java
public class Graph {

    private Map<String, Map<String, Integer>> adjVertices;

    public Graph() {
        this.adjVertices = new HashMap<>();
    }

    public void addVertex(String label) {
        adjVertices.putIfAbsent(label, new HashMap<>());
    }

    public void addVertexValue(String vertexLabel, String label, Integer weight) {
        adjVertices.get(vertexLabel).putIfAbsent(label, weight);
    }

    public HashMap<String, Integer> get(String vertexLabel) {
        return adjVertices.get(vertexLabel);
    }
}
```

We can use it like : 
```java
public class Main {

    public static void main(String[] args) {
        Graph graph = new Graph();

        graph.addVertex("start");
        graph.addVertexValue("start", "a", 6);
        graph.addVertexValue("start", "b", 2);

        // And you can get the neighbors of the "start" like this
        Set<String> start = graph.get("start").keySet();
        System.out.println(start); //["a", "b"]
        
        // And To find the weight of the edge from start to a
        Integer aWeight = graph.get("start").get("a");
        System.out.println(aWeight); //6
    }
    
}
```

Let's add the rest of the Vertices.
```java
graph.addVertex("a");
graph.addVertexValue("a", "fin", 1);

graph.addVertex("b");
graph.addVertexValue("b", "a", 3);
graph.addVertexValue("b", "fin", 5);

graph.addVertex("fin"); //The finish vertex has no edges
```

You will need another hash table to store the costs.
```java
Map<String, Double> costs = new HashMap<>();
costs.putIfAbsent("a", 6d);
costs.putIfAbsent("b", 2d);
costs.putIfAbsent("fin", Double.POSITIVE_INFINITY);
```

The final graph hash table looks like this :  
![Rama's trades graph](./07-03.png)

You also need another hash table for the parents.
```java
Map<String, String> parents = new HashMap<>();
parents.putIfAbsent("a", "start");
parents.putIfAbsent("b", "start");
parents.putIfAbsent("fin", null);
```

Finally, you need an array to keep track of all the nodes you've already processed, 
because you don't need to process a node more than once.
```java
List<String> processed = new ArrayList();
```

That’s all the setup. Now let’s look at the algorithm.
```java
// find the lowest cost node that you haven't processed yet
Map.Entry<String, Integer> lowestCostNode = findLowestCostNode(costs, processed);
// while you still have unprocessed nodes
while (lowestCostNode != null) {
    // get the cost and neighbors of the node
    Integer cost = costs.get(lowestCostNode.getKey());
    Map<String, Integer> neighbors = graph.get(lowestCostNode.getKey());
    
    // go through all the neighbors
    for (Map.Entry<String, Integer> neighbor : neighbors.entrySet()) {
        // calculate the cost of that neighbor when going through this node
        Integer newCost = cost + neighbors.get(neighbor.getKey());
        // if it’s cheaper to get to this neighbor by going through this node ...
        if (costs.get(neighbor.getKey()) > newCost) {
            // update the cost and parent of this neighbor
            costs.put(neighbor.getKey(), newCost);
            parents.put(neighbor.getKey(), lowestCostNode.getKey());
        }
    }
    // mark the node as processed 
    processed.add(lowestCostNode.getKey());
    // get next lowest cost node
    lowestCostNode = findLowestCostNode(costs, processed);
}

// lowest cost node
static Map.Entry<String, Integer> findLowestCostNode(Map<String, Integer> costs, List<String> processed) {
    Integer lowestCost = Integer.MAX_VALUE;
    Map.Entry<String, Integer> lowestCostNode = null;

    for (Map.Entry<String, Integer> node : costs.entrySet()) {
        Integer cost = node.getValue();
        if (cost < lowestCost && !processed.contains(node.getKey())) {
            lowestCost = cost;
            lowestCostNode = node;
        }
    }

    return lowestCostNode;
}
```

---

## Chapter 8 : Greedy Algorithms  
*Page 141-160*

### The Classroom Scheduling Problem  
Suppose you have a classroom and want to hold as many classes here as possible. 
You get a list of classes.


|Class|Start|End|
|---|---|---|
|Art|09:00 AM|10:00 AM|
|ENG|09:30 AM|10:30 AM|
|Math|10:00 AM|11:00 AM|
|CS|10:30 AM|11:30 AM|
|Music|11:00 AM|12:00 PM|

You want to hold as many classes as possible in this classroom. 
How do you pick what set of classes to hold, so that you get the 
biggest set of classes possible?

Here’s how you would do it : 

1. Pick the class that ends the soonest. This is the first class you'll hold in 
this classroom.  
2. Now, you have to pick a class that starts after the first class. Again, pick 
the class that ends the soonest. This is the second class you'll hold.

Keep doing this, and you'll end up with the answer!

Art ends the soonest, at 10:00 a.m., so that's one of the classes you pick.
Now you need the next class that starts after 10:00 a.m. and ends the soonest.
English is out because it conflicts with Art, but Math works. Finally, CS conflicts 
with Math, but Music works.
So these are the three classes you'll hold in this classroom.

|Class|Start|End||
|---|---|---|---|
|Art|09:00 AM|10:00 AM|✓|
|ENG|09:30 AM|10:30 AM|☓|
|Math|10:00 AM|11:00 AM|✓|
|CS|10:30 AM|11:30 AM|☓|
|Music|11:00 AM|12:00 PM|✓|

A greedy algorithm is simple: at each step, pick the optimal move. In this case, 
each time you pick a class, you pick the class that ends the soonest. In technical 
terms: at each step you pick the locally optimal solution, and in the end you're 
left with the globally optimal solution.

Obviously, greedy algorithms don't always work. But they're simple to write! Let's 
look at another example.

### The Set-Covering Problem  
Suppose you're starting a radio show. You want to reach listeners in all 50 states. 
You have to decide what stations to play on to reach all these listeners. It costs 
money to be on each station, so you're trying to minimize the number of stations 
you play on. You have a list of stations. Each station covers a region, and there's 
overlap. How do you figure out the smallest set you can play on to cover all 50 states?

|Radio Station|Available In|
|---|---|
|KOne|IN, NV, UT|
|KTwo|WA, ID, MT|
|KThree|OR, MV, CA|
|KFour|NV, UT|
|...|...|

1. List every possible subset of stations. This is called the power set. 
There are 2^n possible subsets.  
2. From these, pick the set with the smallest number of stations that
covers all 50 states.

The problem is, it takes a lot of time to calculate every possible subset of 
stations. It takes `o(2^n)` time, because there are 2^n stations. It's possible to 
do if you have a small set of 5 to 10 stations.But with all the examples here 
think about what will happen if you have a lot of items. It takes much longer 
if you have more stations.

#### Approximation algorithms  
Greedy algorithm to the rescue! Here's a greedy algorithm that comes pretty close : 

1. Pick the station that covers the most states that haven't been covered yet.
It's OK if the station covers some states that have been covered already.  
2. Repeat until all states are covered.

This is called an approximation algorithm. When calculating the exact 
solution will take too much time, an approximation algorithm will work. 
Approximation algorithms are judged by :  
• How fast they are.  
• How close they are to the optimal solution.

Greedy algorithms are a good choice because not only are they simple to come up 
with, but that simplicity means they usually run fast, too. In this case, the 
greedy algorithm runs in `o(n^2)`, where *n* is the number of radio stations.

Let's see how this problem looks in code.

#### Code For Setup  
First make a set of states you want to cover.
```java
Set<String> states_needed = Set.of("mt", "wa", "or", "id", "nv", "ut", "ca", "az");
```

You also need the list of stations that you're choosing from. I chose to use a 
hash for this.
```java
//You also need the list of stations that you're choosing from
Map<String, Set<String>> stations = new HashMap<>();
stations.putIfAbsent("kone", Set.of("id", "nv", "ut"));
stations.putIfAbsent("ktwo", Set.of("wa", "id", "mt"));
stations.putIfAbsent("kthree", Set.of("or", "nv", "ca"));
stations.putIfAbsent("kfour", Set.of("nv", "ut"));
stations.putIfAbsent("kfive", Set.of("ca", "az"));
```

Finally, you need something to hold the final set of stations you'll use.
```java
Set<String> final_stations = new HashSet<>();
```

#### Calculating the Answer  
Now you need to calculate the stations you'll use. Take a look at the below image, 
and see if you can predict what stations you should use.  
![Stations](./08-01.png)

There can be more than one correct solution. You need to go through every station 
and pick the one that covers the most uncovered states.
```java
// while there is still states that needs to be covered
while (!uncovered_needed_states.isEmpty()) {
    String best_station = null;
    // init the states that the best station covers
    Set<String> covered_states = new HashSet<>();
    for (Map.Entry<String, Set<String>> station : all_stations.entrySet()) {
        // states that this station covers that are not covered yet (exist in the station needed)
        Set<String> uncovered_states = uncovered_needed_states.stream()
                .filter(station.getValue()::contains)
                .collect(Collectors.toSet());
    
        // if this station covers more states (that are not covered yet) than the previously set best station
        // then this is the best station. Yet!
        if (uncovered_states.size() > covered_states.size()) {
            best_station = station.getKey();
            covered_states = uncovered_states;
        }
    }

    // remove all the states that the best station covers from the states that are needed and not covered yet
    uncovered_needed_states.removeAll(covered_states);
    // add the best station found in this iteration to the final all_stations that you will use
    final_stations.add(best_station);
}

System.out.println(final_stations); // [kfour, ktwo, kthree, kfive]
```

`covered_states` is a set of all the states this station covers 
that haven't been covered yet. The for loop allows you to loop over every station 
to see which one is the best station.

In the `for` loop we iterate over all the stations and find out the states that are not 
covered yet `uncovered_states`. If those states are more than the states that are 
covered by the currently `best_station`. Then this is better than the `best_station`, 
and it is the new `best_station`.

After the `for` loop is over, we have the `best_station` that covered the most uncovered 
states. Then we remove those states from the `uncovered_needed_states`, and add that 
station to the `final_stations`. We keep on doing this `while` the 
`uncovered_needed_states` is not empty.

### NP-Complete Problems  
To solve the set-covering problem (with the exact algorithm), you had to calculate 
every possible set.

Maybe you were reminded of the traveling salesperson problem from chapter 1. In 
this problem, a salesperson has to visit five different cities.

And he's trying to figure out the shortest route that will take him to all five 
cities. To find the shortest route, you first have to calculate every possible route.

How many routes do you have to calculate for five cities?

#### Traveling Salesperson, Step by Step  
Let's start small. Suppose you only have two cities. There are two routes to 
choose from.

![Possible Routes](./08-02.png)

> #### Same Route or Different?  
> You may think this should be the same route. After all, isn't SF > Marin the same 
distance as Marin > SF? Not necessarily. Some cities (like San Francisco) have a 
lot of one-way streets, so you can't go back the way you came. You might also 
have to go 1 or 2 miles out of the way to find an on- ramp to a highway. So 
these two routes aren't necessarily the same.

You may be wondering, "In the traveling salesperson problem, is there a specific 
city you need to start from?" For example, let's say I'm the traveling salesperson. 
I live in San Francisco, and I need to go to four other cities. San Francisco would
be my start city.

But sometimes the start city isn't set. For example FedEx may deliver a package for 
the Bay Area. The package will be sent to one of 50 FedEx locations in the Bay Area.
Which location should it get flown to? Here the start location is unknown. It's up 
to you to compute the optimal path and start location for the travelling salesperson.

Let's go with the version where the start city is not defined.

When we had two cities there were two possible routes. Suppose you add a new city.
How many routes are there?

There are six total routes, two for each city you can start at. 
So three cities = six possible routes. Let's add another city, Fremont. Now suppose 
you start at Fremont. Four possible start cities, with six possible routes for 
each start city = 4 * 6 = 24 possible routes.

Do you see a pattern? Every time you add a new city, you're increasing the number of 
routes you have to calculate.

This is called the factorial function (remember reading about this in chapter 3?). 
So 5! = 120. Suppose you have 10 cities. How many possible routes are there? 
10! = 3,628,800. You have to calculate over 3 million possible routes for 10 cities. 
As you can see, the number of possible routes becomes big very fast! This is why 
it's impossible to compute the “correct” solution for the traveling-salesperson 
problem if you have a large number of cities.

The traveling-salesperson problem and the set-covering problem both have something 
in common: you calculate every possible solution and pick the smallest/shortest one. 
Both of these problems are NP-complete.

#### Approximating  
What's a good approximation algorithm for the traveling salesperson? Something simple 
that finds a short path. See if you can come up with an answer before reading on.

Here's how I would do it: arbitrarily pick a start city. Then, each time the 
salesperson has to pick the next city to visit, they pick the closest unvisited 
city. Suppose they start in Marin. Total distance: 71 miles. Maybe it’s not the 
shortest path, but it's still pretty short.

Here's the short explanation of NP-completeness: some problems are famously hard 
to solve. The traveling salesperson and the set-covering problem are two examples. 
A lot of smart people think that it's not possible to write an algorithm that will
solve these problems quickly.

#### How Do You Tell If a Problem is NP-Complete?  
NP-Complete problems show up everywhere! It's nice to know if the problem you're trying 
to solve is NP-complete. At that point you can stop trying to solve it perfectly, and 
solve it using approximation algorithm instead. But it's hard to tell if a problem you 
are working on is NP-complete. Usually there's a very small difference between a problem 
that is easy to solve and an NP-complete problem. For example in the previous chapter, 
we learned how to calculate the shortest path to get from point `A` to point `B`. But 
if you want to find the shortest path that connects several points, that's the traveling
-salesperson problem, which is NP-complete.

There's no way to tell if the problem you are working on is NP-complete But here are 
some giveaways :  
- Your algorithm runs quickly with handful of items, but really slows down with more 
items.  
- "All combinations of X" usually point to an NP-complete problem.  
- Do you have to calculate "every possible version" of X because you can't break it 
down into smaller sub-problems? Might be NP-complete problem.  
- If your problem involves a sequence (such as a sequence of cities, like 
traveling-salesperson), and it's hard to solve, it might be NP-complete.  
- Can you restate your problem as the set-covering problem or the traveling-salesperson 
problem? Then your problem is definitely NP-complete.  

So to recap  
- Greedy algorithms optimize locally, hoping to end up with a global optimum.  
- NP-complete problems have no known fast solution.  
- If you have an NP-complete problem your best bet is to use an approximation algorithm.  
- Greedy algorithms are easy to write and fast to run, so they make good approximation 
algorithms.  


## Chapter 9 : Dynamic Programming  
*Page 161-186*

### The Knapsack Problem  
Let's say you're a thief with a knapsack that can carry 4 lb of goods. You have three 
items that you can put into the knapsack.

1. Stereo, 3000$, 4 lbs.  
2. Laptop, 2000$, 3 lbs.  
3. Guitar, 1500$, 1 lbs.  

What items should you steal so that you steal the maximum money's worth of gold?

#### The Simple Solution  
The simplest algorithm is to try every possible set of goods and find the one that
gives you the most value.

Max value is : Guitar and Laptop for 3500$.

This works, but it's really slow. For 3 items, you have to calculate 8 possible sets. 
For 4 items, you have to calculate 16 sets. This algorithm takes `O(2^n)` time, which 
is very, very slow.

That's impractical for any reasonable number of goods. In chapter 8 we calculated an 
approximate solution. That solution will be close to the optimal solution, but it 
may not be the optimal solution. So how do we calculate the optimal solution?

#### Dynamic Programming  
Let's see how the dynamic programming algorithm works here. Dynamic programming 
starts by solving sub-problems and builds up to solving the big problem.

For the knapsack problem, you'll start by solving the problem for smaller knapsacks
(sub-knapsack) and then work up to solving the original problem.

Let's see the algorithm in action first.

Every dynamic-programming algorithm starts with a grid. Here's a grid for the knapsack 
problem.

| |1|2|3|4|
|---|---|---|---|---|
|Guitar| | | | |
|Stereo| | | | |
|Laptop| | | | |

The columns are for the knapsack weights from 1 to 4 pounds. The rows are for each item 
to choose from. You need all of those columns because they will help you calculate the 
values of the sub-knapsacks.

The grid starts out empty. You're going to fill in each cell of the grid. Once the grid 
is filled in, you'll have your answer to this problem!

##### The Guitar Row  
I'll show you the exact formula for calculating this grid later. Let's do a 
walk-through first. Start with the first row.

This is the guitar row, which means you're trying to fit the guitar into the knapsack. 
At each sell there's a simple decision. Do you steal the guitar or not? Remember you're 
trying to fit the items with the most value to steal. The first cell has a knapsack 
capacity of 1 lb. The guitar is also 1 lb, which means it fits into the knapsack! so 
the value of this cell is 1500$, and it contains a guitar.

Like this, each cell in the grid will contain a list of all the items that fit into the 
knapsack at that point. Let's look at the next cell. Here you have a knapsack of 
**capacity 2** lb. Well, the guitar will definitely fit here. The same for the rest 
of the cells. **Remember** this is the first row, so you have only the *guitar* to choose 
from. You're pretending that other items are not available to steal right now.

| |1|2|3|4|
|---|---|---|---|---|
|Guitar|G, 1500$|G, 1500$|G, 1500$|G, 1500$|
|Stereo| | | | |
|Laptop| | | | |

At this point, you're probably confused. Why are you doing this for knapsacks with 
capacity of 1 lb, 2 lb, and so on, when the problem is about 4 lb knapsack? Remember 
that dynamic programming starts with a small problem and builds up to the big problem. 
You're solving sub-problems here that will help you to solve the big problem.

Remember, you're trying to maximize the value of the knapsack. This row represents the 
current best guess for this max. In other words, according to this row, if you had a 
knapsack of capacity of 4 lb, the max value you could put in there would be 1500$.

You know that's not the final solution. As we go through the algorithm, you'll 
refine your estimate.

##### The Stereo Row  
This row is for the stereo. Now that you're on the second row, you can steal the guitar 
or the stereo. At every row, you can steal the item at that row or the items in the 
row above it. Let's start with the first cell, a knapsack of capacity 1 lb. The current 
max value you can fit into a knapsack of 1 lb is 1500$. 

You can't steal the stereo. you have a knapsack (sub-knapsack) with capacity of 1 lb.
And the stereo is too heavy, so 1500$ remains the max guess for a 1 lb knapsack. Same 
thing for the next two cells. These knapsacks have a capacity of 2 lb and 3 lb. The 
old max value for both was 1500$. You cannot fit the stereo as it's 4 lb so your 
guesses remain unchanged.

For the last cell you have capacity of 4 lb. The stereo finally fits. So now if you 
put the stereo the max value is 3000$. 

| |1|2|3|4|
|---|---|---|---|---|
|Guitar|G, 1500$|G, 1500$|G, 1500$|G, 1500$|
|Stereo|G, 1500$|G, 1500$|G, 1500$|S, 3000$|
|Laptop| | | | |

##### The Laptop Row  
The laptop is 3 lb, so for the first two cells the max value remains the guitar. For the 
third cell though you have capacity of 3 lb, and that fits the laptop. So your max value 
for the third cell is now 2000$.

At 4 lb the current max value is 3000$ (from the previous row). You can put the laptop 
in the knapsack, but it's only 3 lb, so you have 1 lb free! You could put something in 
this 1 lb. What is the maximum value you can put in 1 lb? Well, you've been calculating 
it all along.

According to the last best estimate you can fit the guitar into that 1 lb space and 
that's worth 1500$, Which is the max value when combined with the 2000$ from the 
laptop.

You might have been wondering why you were calculating max values for smaller 
knapsacks. I hope now it makes sense! When you have space left over, you can use 
the answers to those sub-problems to figure out what will fit in that space. It's 
better to take the laptop + the guitar for 3500$.

The final grid looks like this.

| |1|2|3|4|
|---|---|---|---|---|
|Guitar|G, 1500$|G, 1500$|G, 1500$|G, 1500$|
|Stereo|G, 1500$|G, 1500$|G, 1500$|S, 3000$|
|Laptop|G, 1500$|G, 1500$|L, 2000$|L+G, 3500$|

Maybe you think that I used a different formula to calculate the value of that last 
cell. That's because I skipped some unnecessary complexity when filling in the values 
of the earlier cells. Each cell's value gets calculated with the same formula. 
Here it is.

![Formula](./09-01.png)

### Knapsack Problem FAQ  

#### What Happens If You Add an Item?  
Suppose that you can also steal an iphone with size of 1 lb and value of 2000$. Do 
you have to recalculate everything to account for this new item? Nope. Remember 
dynamic programming keeps progressively building on your estimate. So far the latest 
grid holds the max values. Let's add a row for iphone.

| |1|2|3|4|
|---|---|---|---|---|
|Guitar|G, 1500$|G, 1500$|G, 1500$|G, 1500$|
|Stereo|G, 1500$|G, 1500$|G, 1500$|S, 3000$|
|Laptop|G, 1500$|G, 1500$|L, 2000$|L+G, 3500$|
|iphone| | | | |

Let's start with the first cell. The iphone fits into the 1 lb knapsack. The old max 
was 1500$, but the iphone is worth 2000$. Let's take the iphone instead.

In the next cell you can fit the iphone and the guitar. For the third cell you can't do 
better than the iphone and the guitar, So leave it as is.

For the last cell, things get interesting. The current max is 3500$. You can steal 
the iPhone instead, and you have 3 lb of space left over. Those 3 lb are worth 
2000$! 2000$ from the iPhone + 2000$ from the old sub-problem: that's 4000$. 
A new max! Here's the new final grid.

| |1|2|3|4|
|---|---|---|---|---|
|Guitar|G, 1500$|G, 1500$|G, 1500$|G, 1500$|
|Stereo|G, 1500$|G, 1500$|G, 1500$|S, 3000$|
|Laptop|G, 1500$|G, 1500$|L, 2000$|L+G, 3500$|
|iphone|I, 2000$|I+G, 3500$|I+G, 3500$|I+L, 4000$|

#### What Happens If You Add a Smaller Item?  
Suppose you can steal a necklace. It weighs 0.5 lb, and it's worth 1000$. So far, 
your grid assumes that all weights are integers. Now you decide to steal the necklace. 
You have 3.5 lb left over. What's the max value you can fit in 3.5 lb? You don't know! 
You only calculated values for 1 lb, 2 lb, 3 lb, and 4 lb knapsacks. You need to know 
the value of a 3.5 lb knapsack.

Because of the necklace, you have to account for finer granularity, so the grid has 
to change.

| |0.5|1|1.5|2|2.5|3|3.5|4|
|---|---|---|---|---|---|---|---|---|
|Guitar| | | | | | | | |
|Stereo| | | | | | | | |
|Laptop| | | | | | | | |
|Necklace| | | | | | | | |

#### Can You Steal Fractions of an Item?  
Answer: You can't. With dynamic-programming solution you either take the item or not. 
There's no way for it to figure out that you should take half an item.

But this case is also easily solved using a greedy algorithm! First take as much as 
you can of the most valuable item. When that runs out, take as much as you can of the 
next most valuable item, and so on.

#### Optimizing Your Travel Itinerary  
Suppose you're going to London for a nice vacation. You have two days there and 
a lot of things you want to do. You can't do everything, so you make a list.

![Itinerary](./09-02.png)

For each thing you want to see, you write down how long it will take and rate how 
much you want to see it. Can you figure out what you should see, based on this list?

Here's the answer.

| |0.5|1|1.5|2|
|---|---|---|---|---|
|WA|WA, 7|WA, 7|WA, 7|WA 7|
|GT|WA, 7|WA+GT, 13|WA+GT, 13|WA+GT, 13|
|NG|WA, 7|WA+GT, 13|WA+NG, 16|WA+NG+GT, 22|
|BM|WA, 7|WA+GT, 13|WA+NG, 16|WA+NG+GT, 22|
|PC|PC, 8|PC+WA, 15|PC+WA+GT, 21|PC+WA+NG, 24|

#### Handling Items That Depend on Each Other  
Suppose you want to go to Paris. So you put a couple of items on the list.

![Itinerary](./09-03.png)

These place take a lot of time, because you have to travel from London to Paris. If 
you want to do all three items, it will take four and a half days.

Wait! That's not right. You don't travel to Paris for each item. Once you're in Paris, 
each item should only take a day. So it should be, one day per item + half a day of 
travel = 3.5 days, not 4.5 days.

If you put the Eiffel Tower in your knapsack, then the Louvre becomes “cheaper”—it 
will only cost you a day instead of 1.5 days. How do you model this in dynamic 
programming?

You can't. Dynamic programming is powerful because it can solve sub-problems and 
use those answers to solve the big problem. Dynamic programming only works when 
each sub-problem is discrete—when it doesn't depend on other sub-problems. That 
means there's no way to account for Paris using the dynamic-programming algorithm.

#### Is It Possible That The Solution Will Require More Than Two Sub-Knapsacks  
It's possible that the best solution involves stealing more than two items. The way 
the algorithm is set up, you're combining two knapsacks at most, you'll never have 
more than two knapsacks. But it's possible for those knapsacks to have their own 
sub-knapsacks.

#### Is It Possible That The Best Solution Doesn't Fill The Knapsack Completely?  
Yes. Suppose you could also steal a diamond.
This is a big diamond: it weighs 3.5 pounds. It's worth a million dollars, way more 
than anything else. You should definitely steal it! But there's half a pound of 
space left, and nothing will fit in that space.

### Longest Common Substring  
You've seen one dynamic programming problem so far. What are the takeaways?

- Dynamic programming is useful when you're trying to optimize something given a 
constraint. In the knapsack problem, you had to maximize the value of goods you stole
constrained by the size of the knapsack.  
- You can use dynamic programming when the problem can be broken into discrete 
sub-problems, and they don't depend on each other.

It can be hard to come up with a dynamic-programming solution. That's what we'll 
focus on in this section. Some general tips follow :  

- Every dynamic-programming solution involves a grid.  
- The values in the cell are usually what you're trying to optimize. For the knapsack 
problem, the values were the value of the goods.  
- Each cell is a sub-problem, so think about how you can divide your problem into 
sub-problems. That will help you figure out what the axes are.

Let's look at another example. Suppose you run `dictionary.com`. Someone types a word, 
and you give them the definition.

But if someone misspells a word, you want to be able to guess what word they meant. 
Alex is searching for Fish, but he put Hish. That's not a word in your dictionary, 
but you have a lost of words that are similar. Fish, Vista.

Alex typed Hish, which word did he mean to type: Fish or Vista.

#### Making The Grid  
What does the grid for this problem look like? You need to answer these questions. 

- What are the values of the cells?  
- How do you divide this problem into sub-problems?  
- What are the axes of the grid?  

In dynamic programming, you're trying to maximize something. In this case, you're 
trying to find the longest substring that two words have in common. What substring 
do Fish and Hish have in common? How about Hish and Vista? That's what you want to 
calculate.

Remember the values of the cells are usually what you are trying to optimize. In 
this case, the values will probably be a number: the length of the longest substring 
that the two words have in common.

How do you divide this problem into sub-problems? You could compare substrings. 
Instead of comparing Fish and Hish, you could compare his and fis first. Each cell 
will contain the length of the longest substring that tow substrings have in common. 
This also gives you a clue that the axes will probably the two words. So the grid 
probably looks like this.

| |H|I|S|H|
|---|---|---|---|---|
|F| | | | |
|I| | | | |
|S| | | | |
|H| | | | |

#### Filling The Grid  
Now you have a good idea of what the grid should look like. What's the formula for 
filling in each cell of the grid? You can cheat a little, because you already know 
what the solution should be, Hish and Fish have a substring of length 3 in common ish.

But that still doesn't tell you the formula to use. Computer scientists sometimes 
joke about using the Feynman algorithm. The Feynman algorithms is named after
physicist Richard Feynman, and it works like this :  

- Write down the problem.  
- Think real hard.  
- Write down the solution.  

The truth is, there's no easy way to calculate the formula here. You have to experiment 
and try to find something that works. Sometimes algorithms aren't an exact recipe. 
They're a framework that you build your idea on top of.

Try to come up with a solution for this problem yourself. I'll give you a hint, part 
of the grid looks like this.

| |H|I|S|H|
|---|---|---|---|---|
|F|0|0| | |
|I| | | | |
|S| | |2|0|
|H| | | |3|

What are the other values? Remember that each cell is the value of a sub-problem. Why 
does cell (3,3) have a value of 2? Why does cell (3,4) have a value of 0?

Read on after you've tried to come up with a formula yourself. Even if you don't get 
it right, my explanation will make a lot more sense.

#### The Solution  
The final grid looks like this.

| |H|I|S|H|
|---|---|---|---|---|
|F|0|0|0|0|
|I|0|1|0|0|
|S|0|0|2|0|
|H|0|0|0|3|

Here's my formula for filling in each cell. If the letters don't match the value is 0. 
If they do match the value is value of the top left neighbour + 1.

Here's the grid for hish vs. vista.

| |V|I|S|T|A|
|---|---|---|---|---|---|
|F|0|0|0|0|0|
|I|0|1|0|0|0|
|S|0|0|2|0|0|
|H|0|0|0|0|0|

One thing to note: for this problem the final solution may not be in the last cell! 
For the knapsack problem, this last cell always had the final solution. But for the 
longest common substring the solution is the larges number in the grid, and it may 
not be the last cell.

Let's go back to the original question: which string has more in common with hish.
It's fish, Alex probably meant to type fish.

#### Longest Common Subsequent  
Suppose Alex accidentally searched for fosh. Which word did he mean: fish or fort?

Let's compare them using the longest common substring formula.

| |F|O|S|H|
|---|---|---|---|---|
|F|1|0|0|0|
|O|0|2|0|0|
|R|0|0|0|0|
|T|0|0|0|0|

| |F|O|S|H|
|---|---|---|---|---|
|F|1|0|0|0|
|I|0|0|0|0|
|S|0|0|1|0|
|H|0|0|0|2|

They're both the same: two letters! But fosh is closer to fish.

You're comparing the longest common substring, but you really need to compare the 
longest common subsequence: the number of letters in a sequence that the two words 
have in common. How do you calculate the longest common subsequence?

The longest common subsequence is very similar to the longest common substring, 
and the formulas are pretty similar, too.

Here's the grid.

![Formula](./09-04.png)

Here's my formula for filling in each cell.

![Formula for each cell](./09-05.png)

Whew—you did it! This is definitely one of the toughest chapters in the book. So is 
dynamic programming ever really used? Yes:

- Biologists use the longest common subsequence to find similarities in DNA strands. 
They can use this to tell how similar two animals or two diseases are. The longest 
common subsequence is being used to find a cure for multiple sclerosis.  
- Have you ever used diff (like git diff)? Diff tells you the differences between 
two files, and it uses dynamic programming to do so.  
- We talked about string similarity. Levenshtein distance measures how similar two 
strings are, and it uses dynamic programming. Levenshtein distance is used for 
everything from spell-check to figuring out whether a user is uploading 
copyrighted data.  
- Have you ever used an app that does word wrap, like Microsoft Word? How does it 
figure out where to wrap so that the line length stays consistent? Dynamic 
programming!  


