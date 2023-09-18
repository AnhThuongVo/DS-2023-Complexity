# 02/07 Worksheet: Complexity & Recursion
## Initial due date: 02/11 @ 5pm
#### accepted as on time until 02/13 @11:59pm
Collaborators:

Answer the below questions, and make sure that you commit to your own branch.
When done, make a pull request and tag @irabkina.
Respond to my comments by making new commits to the same branch.

## Review
1. In your own words, what is computational complexity? Why is it important to consider?
2. In your own words, what is the difference between run-time complexity and memory complexity?
3. Put the following big-O's in order from fastest runtime/smallest memory use to slowest runtime/most memory use: O(n<sup>2</sup>), O(3<sup>n</sup>), O(n!), O(2<sup>n</sup>), O(n<sup>3</sup>), O(n), O(log(n))
4. What are each of the following big-O's called in English (e.g., O(log n) is "logarithmic"): O(n<sup>2</sup>), O(n<sup>3</sup>), O(n), O(n!), O(2<sup>n</sup>), O(1)?
5. In your own words, what is a recursion algorithm? Note that this is *not* (necessarily) the same thing as a recursive function (i.e. a function that calls itself).
6. In your own words, what is the base case of a recursive algorithm? What is the recursive case?
7. The textbook uses the phrase "smaller subproblems" in their definition of a recursive algorithm.

    a. What is this "smaller subproblem" when a recursive algorithm is used to calculate a factorial? The factorial of a number n is written as n!, and is defined as n * (n-1) * (n-2) * ... * 3 * 2 * 1.

    b. How do you detect the base case, and what should you do in the base case?

    c. How do you detect the recursive case, and what do you do then?
8. The textbook also shows a recursive algorithm/function that works on a singly-linked list. (We will only focus on the "forward" version.)

    a. What is the "smaller subproblem" in a recursive algorithm that operates on a singly-linked list?

    b. How do you detect the base case?

    c. How do you detect the recursive case?


## Exploration
1. For each of the following functions, say whether it has computational complexity O(1), O(n), O(n<sup>2</sup>), or O(n<sup>3</sup>). Give a two-sentence justification of your answer. Your justification should *not* be based on actually running the code.     
a.  
    ```java
    public int f1(int n) {
     int x = 0;
     for (int i = 0; i < n*n*n; i++){
      x++;
     }
     return x;
    }
    ```  
    b.  
    ```java
    public int f2(int n){
     int x = 0;
     for (int i = 0; i < n; i++){
      x++;
      continue;
     }
     return x;
    }
    ```    
    c.  
    ```java
    public int f3(int n){
     int x = 0;
     for (int i = 0; i < n; i++){
      x++;
      break;
     {
     return x;
    }
    ```  
    d.  
    ```java
    public int f4(int n){
     int x = 0;
     for (int i = 0; i < n; i++){
      for (int j = 0; j < i; j++){
       x++;
      }
     }
     return x;
    }
    ```  
    e.  
    ```java
    public int f5(int n){
     int x = 0;
     int y = 10;
     for (int i = 0; i < n; i++){
      for (int j = 0; j < y; j++){
       x++;
      }
     }
     return x;
    }
    ```  
    f.  
    ```java
    public int f6(int n){
     int x = 0;
     for (int i = 0; i < n; i++){
      x++;
     }
     for (int j = n; j >= 0; j--){
      x++;
     }
     return x;
    }
    ```  

2. This question guides you through how to convert code with a while loop into a recursive function. We will use a function that sums up a singly-linked list of integers as the example.

    Consider the following method in a `LinkedList` class, in particular, a class that does *not* store its size. A working example is given to you in `RecursiveList.java`. Although the solution to this question are in that file (commented out at the bottom), I encourage you to work through the questions yourself without referring to it.    

    ```java
    int sum() {
        Node currNode = this.head;
        int total = 0;
        for (int i = 0; i < this.size; i++) {
            total += currNode.data;
            currNode = currNode.next;
        }
    }
    ```

    This code doesn't work because we are assuming `this.size` is not defined. We will fix that first, then convert this method into a recursive one.    
   
   a. First, we will have to get rid of `this.size`. How can we check whether we are at the end of the list just by looking at `currNode`? Why does that work?
        (Note: There are two ways to do this, by checking whether `currNode` points to the last node, and by checking whether `currNode` has gone *past* the last node. The latter makes the code cleaner, and is what we'll use below.)
        Use that fact and re-write the loop into a while loop.   
        
    b. Now that we have a while loop, we can start the conversion to make the function recursive. The first step is to identify all the variables that are changed in the while loop. What are they?  
    
    c. Most recursive list functions have a "wrapper" function that calls the recursive function with the appropriate initial arguments. Two *function stubs* (empty templates) following this pattern are below. Modify the wrapper function so that it calls the recursive function, using the initial value(s) of the variable(s) you identified in the previous question. You do not need to explicitly answer this question.

    ```java
    public void recurSum() {
        // FIXME
    }

    public void recurSum(Node currNode, int total) {
        // FIXME
    }
    ```  
    
    d. Think back to Review Q8 - you'll notice that the recursive case is the same as the condition to the while loop from part b. In the recursive function, write an if-else statement that checks for the recursive case (with the base case being the else).   
    
    e. What happens in the base case is the same as what happens *after* the loop in the original function. Fill out the base case of the if-else statement.  
    
    f. Finally, copy the loop body into the recursive case of the if-else statement. There is one change we need to make here: instead of *changing* the variables, we want to call the recursive function *with their new values*, and return its result. Fill out the recursive case of the if-else statement.  

   At this point, you should have a recursive function that sums up the list. Stare at it to make sure you understand how it works, and test it to make sure that it works. The process we went through to convert a while-loop function to a recursive function can be summarized in the following steps:

    > 1. Create the wrapper function and the recursive function stubs.
    > 2. Turn all local variables into arguments to the recursive function.
    > 3. Replace the `while` with an `if`, and add an `else`. These are the recursive and base cases.
    > 4. Copy the return value (or whatever is after the loop) to the base case (the `else`).
    > 5. Copy the loop body to the recursive case (the `if`), and replace the variable updates with a recursive call.
    > 6. Call the recursive function from the wrapper function using the initial values of the variables. 

3. Convert the following iterative `print()` function to be recursive.

    ```java
    void print() {
        Node currNode = this.head;
        while (currNode != null) {
            System.out.println(currNode.data);
            currNode = currNode.next;
        }
    }

## Challenge
One time when we consider computational complexity is when trying to pick the most efficient data structure for a project. For questions 1-3 in this section, you will compare LinkedLists and ArrayLists for this purpose.

1. 
    a. What is the best and worst case complexity of the `add()` method for ArrayLists? Give a brief justification of each answer. 
   
    b. What is the best and worst case complexity of the `add()` method in a LinkedList? Give a brief justification of each answer.   
   
    c. Is `add()` more efficient in ArrayLists or LinkedLists overall? Explain your reasoning.   

2. 
    a. What is the best and worst case complexity of the `get()` method for ArrayLists? Give a brief justification of each answer.    
    (Something to keep in mind here is that array indexing (i.e., `array[i]`) is constant time. Why? Every element in an array takes up the same amount of space in memory. The starting location in memory is known. Thus, we can find the exact location of any element in the array by plugging into the formula: `start + index * size`. Because this does not depend on the size of the overall array, and each individual computation is constant, we consider array indexing to be constant time overall.)   
   
    b. What is the best and worst case complexity of the `get()` method in a LinkedList? Give a brief justification of each answer.   
   
    c. Is `get()` more efficient in ArrayLists or LinkedLists overall? Explain your reasoning.   

3. Suppose that you are asked to implement a project wherein you add all the Oxy CS majors to a list (we'll learn about better data structures for this task later in the semester). Every year thereafter, you will be asked to update the list by adding new majors (don't worry about deleting people who have graduated).    
    a. Suppose that, when it comes time to update, you are only given the names of new majors. Is it better to use an ArrayList or a LinkedList for this implementation? Why?  
    
    b. Suppose, instead, that you are always given the names of all majors who are currently enrolled. You still only want to add new majors to your list. Is it better to use an ArrayList or a LinkedList for this implementation? Why?  
  
    c. Now suppose you are asked to create a new list every year, rather than updating the old one. Is it better to use an ArrayList or a LinkedList for this implementation? Why? Does your answer change depending on whether you receive a list of only new majors or all enrolled majors change? 
   
4. In a general sense, when is it better to use an ArrayList vs a LinkedList?

5. There is a special kind of recursion called *tail recursion*. You should Google it for more details, but in short, when a tail-recursive function is called, instead of *creating* a new stack frame, it *replaces* the existing one. This is only possible if nothing needs to be done after the recursive call. That is, if the function is called `XXXX`, then *all recursive calls* must look like `return XXXX(...);`. Based on this explanation, is the following code tail-recursive? Why/Why not?
    ```java
        int recurSum(Node currNode) {
            if (currNode != null) {
                return 1 + recurSum(currNode.next);
            } else {
                return currNode.data;
            }
        }
    ```
   
6. Is the function below tail-recursive? Why/Why not?
    ```java
    int factorial(int n, int product) {
        if (n == 1) {
            // DRAW MEMORY HERE FOR C8
            return product;
        } else {
            return factorial(n - 1, product * n);
        }
    }
    ```
   
7.  a. How would you call the above function if you wanted to find the factorial of 4?     
    b. Draw what memory looks like at the indicated location in the `factorial()` function, when computing the factorial of 4.


