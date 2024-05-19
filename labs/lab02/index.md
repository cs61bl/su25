---
layout: page
title: "Lab 2: Conditionals, Loops, Arrays"
tags: [Lab, Java]
released: true
searchable: true
---

## [FAQ](faq.md)

Each assignment will have an FAQ linked at the top. You can also access it by
adding "/faq" to the end of the URL. The FAQ for Lab 2 is located
[here](faq.md).


## Before You Begin

Run `git pull skeleton main` in your repo. You should get a `lab02/` folder.
For this, and later labs, we strongly recommend opening up the lab in IntelliJ.

Also, please note that this lab expects exposure to programming similar to that 
obtained in a course like CS 61A. We will begin diving deep into Java, and moving 
fast. If you are not as comfortable with this material, we recommend you take a 
look at this [Java Crash Course](https://cs61bl.org/su23/java/) as supplemental material.

### Learning Goals

First off, this lab will provide an introduction to Java loops and conditionals
(the `if`, `while` and `for` statements), followed by a brief explanation of
Java Arrays. We assume no prior experience with any of these topics in Java,
but we *do* assume some prior knowledge of these concepts from an earlier
course (like Python control flow and lists as taught in CS61A).

Because of this, there is a lot of information presented in this lab, but
hopefully most of it will be review that can be skimmed through quickly.

This course strives to teach you how to "program", and this includes not just
teaching you how to write code, but how to do a variety of activities. Today's
lab includes some exercises that tests your ability not only to write code,
but also to analyze code (to figure out what code does), to test code (to see
if given code is doing what it should do) and to evaluate multiple versions of
code.

## Control Flow Review

### How `if` and `if ... else` Work

Hopefully you've already seen this in another course, so it should be a bit of 
a review — but read on!

An `if` statement starts with the word `if`. It is followed by a *condition*
statement **in parentheses** that is either true or false (a *boolean
expression*). There is then a sequence of statements surrounded by braces,
which is called the *body*. For example:

```java
if (year % 4 == 0) {
    System.out.println (year + " might be a leap year.");
}
```

> Note: like in Python, the `%` symbol above is called *mod*, and it takes the
> remainder after division. The above statement is checking if `year` has no
> remainder when divided by 4). The behavior of the `%` operator in Java
> annoyingly differs slightly from how it functions in Python, particularly
> with respect to negative numbers.
>
> For example in Python `-5 % 4` evaluates to `3` whereas in Java `-5 % 4`
> evaluates to `-1`. If you want the behavior to match what you might expect 
> in Python, you should use the Math.floorMod function in Java. If you do this 
> then Math.floorMod(-5, 4) evaluates to 3.

The braces after an `if` statement aren't technically necessary if there is
only one statement in the sequence; however, it is good practice to always
include them since it makes it easier to add lines to the body later.

Unlike other languages (Python in particular), the condition of the `if`
statement *must* be a boolean statement or a statement that reduces to a
boolean expression. `if (5):` is a legal statement in Python, but `if (5) {`
will not compile in Java.

Boolean expressions often involve comparisons. The comparison operators in Java
are `==` and `!=` for equality and inequality testing, and `>`, `>=`, `<`, and
`<=` for comparison of magnitudes. Multiple comparisons can be chained together
with the logical operators `&&` (and) and `||` (or). If instead you wish to
negate an expression, you can prefix your expression with `!`, the Java
negation operator.

The block of statements following the `if` statement above will not execute if
`year`'s value is not divisible by 4. If you wanted something to happen when
the test fails, use the `else` keyword. Here's an example:

```java
if (year % 4 == 0) {
    System.out.println (year + " might be a leap year.");
} else {
    System.out.println (year + " is definitely not a leap year.");
}
```

You can also add further tests that are executed only if above boolean
expressions evaluate to false, similarly to `elif` in Python. For example:

```java
if (year % 4 != 0) {
    System.out.println (year + " is not a leap year.");
} else if (year % 100 != 0) {
    System.out.println (year + " is a leap year.");
} else if (year % 400 != 0) {
    System.out.println (year + " is not a leap year.");
} else {
    System.out.println (year + " is a leap year.");
}
```

Note that only one body section, the one corresponding to the first true
boolean expression (or `else` if none are true), will execute. After that,
your program will continue on, skipping all the remaining code in this `if`
structure. This implies that none of the conditions below the first true
boolean expression will be evaluated.

One consequence of conditions reveals in non-void methods. Recall that in Java,
you must return something of the return type. Consider the following code snippet:

```java
public int relu(int x) {
    if (x < 0) {
        return 0;
    }
}
```

As the code is, it will not compile. That is because currently, a value is only
returned when `x` is less than 0. What happens when that's not the case? Java
must be assured that `relu()` *always* returns an int, and thus will not allow
you to compile your code.

A correct version looks like this:

```java
public int relu(int x) {
    if (x < 0) {
        return 0;
    } else {
        return x;
    }
}
```

### How `while` Works

The `while` statement is used to repeat a sequence of statements. It consists
of the word `while`, followed by a continuation *test* in parentheses, also
called the *condition*. It is then followed by a sequence of statements to
repeat enclosed in braces, called the *loop body*.

The `while` statement works by evaluating the condition. If the condition is
true (the test succeeds), the entire loop body is executed, and the condition
is checked again. If it succeeds again, the entire loop body is executed again.
This continues, possibly infinitely.

A common mistake when first learning a Java-like language is to think that the
behavior of `while` is to stop as soon as the test becomes false, possibly in
the middle of the loop. This is not the case. The test is checked only at the
end of a complete iteration, and so this is the only time the loop can stop.

Here's an example that implements the remainder operation `dividend % divisor`,
and produces some output. We assume all variables have already been declared,
and that `divisor` and `dividend` have already been assigned positive values.

```java
while (dividend >= divisor) {
    dividend = dividend - divisor;
    System.out.println ("loop is executed");
}
remainder = dividend;
```

All statements of the loop body are executed, even if one of them affects the
truth value of the test. In the example above, values of 9 for `dividend` and
4 for `divisor` result in two lines of output. We show a representation with
values of 13 for `dividend` and 4 for `divisor` and initially 0 for
`remainder`. This results in 3 lines of output.

When debugging `while` loop code, sometimes it's useful to make charts like the
one below to keep track of the value of each variable.

![DividendDivisor](img/DividendDivisor.jpg)

### Exercise: Date Converter

> For this exercise, suppose that the year is 988, before computers were invented and the 
world was better off for it. Also, it is important to remember that we at CS 61BL course staff
> do not believe in leap years, so 988 should have 365 days!
>
> All joking aside, for this question we will not take leap years into account
> and you should assume that the year has 365 days. Thus
> `java DateConverter 60` should print `3/1` not `2/29` as you might expect.

The program `DateConverter.java` in the `lab02` skeleton folder is missing two
assignment statements. The missing statements can either be at the beginning,
the end, or at both the beginning and the end of the loop.

#### Date Converter Tests

In a bit, you'll determine what the statements are and where they go. But
first, you'll come up with a small but comprehensive set of tests for the code
before writing the code itself. This technique is called *test-driven
development*, and we'll be doing it more in subsequent labs.

Create a table with 6 pairs of Input and Output. Ensure you have some edge cases to
test for odd behavior! The input should be in the form of a day number in 2020,
an integer between 1 and 365, and the corresponding date output. An example is 365 is 12/31.

This will not be handed in or graded, but later in the lab you will be using these input and
outputs to verify the correctness of your code.

#### Command Line Arguments in IntelliJ
In order to run your selected inputs against your code, we will need to pass in the test inputs
into the command line. As it turns out, IntelliJ provides just a feature, so we can run it without
having to open up the terminal. The steps to doing so are as follows:

1. Click the green arrow next to the "public static void main(String[] args)" method header. 
    ![StepZero](img/Args0.png)
2. On the menu that pops up, click on "Modify Run Configuration..." 
    ![StepOne](img/Args1.png)
3. Another menu will pop-up. Find the blank labeled "Program arguments" and try typing in a number, like 22.
Then hit ok.
    ![StepTwo](img/Args2.png)
    ![StepThree](img/Args3.png)
4. Now, just try running the program as normal, and you should see the program output 1/22! That means your input
was successfully passed in. 

#### Implement and Test

Testing the code involves supplying a value for `dayOfYear` on the command
line. A few new things about the code:

-   The value for `dayOfYear` is read from `args[0]`, which is a command line
    argument. Review the previous section for instructions.

-   The statement `import java.io.*;` makes Java library methods involving
    file input and output accessible inside the program. You don't have to worry
    about this.

-   The five lines starting with `try {` catches an *exception* that would
    occur if the command line argument isn't an integer. We'll learn about
    exceptions in a couple of weeks.

Complete `DateConverter.java` by putting in two assignment statements as
specified above. Once you're done with that, compile your program and try each
one of your test cases.

Compile and run your code as you did in lab01.

#### Testing

Using the Input and Output table you created earlier, test your program. Does
it provide the expected output for all of your inputs?

## `for` loops

### How `for` Works

The `for` statement provides another way in Java to repeat a sequence of
statements, similar to `while` but slightly different. It starts with `for`,
continues with *loop information* inside parentheses, and ends with the *loop
body* (the segment to be repeated) enclosed in curly braces.

```java
for (loop-information) {
    loop-body;
}
```

<!-- TODO: I know Oracle docs refer to these as "increments",
but that's weird because it's arbitrary. "update" might be better. -->
Loop information consists of *initializations*, a *test* (condition), and
*increments*. If the test succeeds, the loop continues and then increments. These refer to the creation of variables, boolean conditions that dictates when the loop should and should not be entered, 
and the equation we use to update our position between loops. 
These three sections are separated by semicolons, and any of
these may be blank. If there is more than one initialization or increment,
they are separated by commas.
```java
for (initialization; test; increment) {
    loop-body;
}
```

Loop execution proceeds as follows:

1.  Initializations are performed.
2.  The test is evaluated.
    -   If the condition is false, the loop is finished and execution continues
        with the code following the for loop.
    -   If the condition is true, the loop body is executed, increments are
        performed, and we loop back to the top of step 2 where the test is
        evaluated again. (Note: We never re-initialize.)

Note that, in fact, all of these sections of the for loop are optional. The code
`for (;;)` is in fact valid Java code. It never terminates!

![For Loop Execution](img/ForLoopExecution.png)

The following loops are several equivalent ways to compute `n` factorial
(the product of all the positive integers up through `n`).

-   Two initializations in loop-information

    ```java
    for (int k = n, product = 1; k > 0; k = k - 1) {
        product = product * k;
    }
    ```

-   Product initialized outside for loop

    ```java
    int product = 1;
    for (int k = n; k > 0; k = k - 1) {
        product = product * k;
    }
    ```

-   Decrement performed inside the loop-body

    ```java
    int product = 1;
    for (int k = n; k > 0; ) {
        product = product * k;
        k = k - 1;
    }
    ```

-   While loop equivalent

    ```java
    int product = 1;
    int k = n;
    while (k > 0) {
        product = product * k;
        k = k - 1;
    }
    ```

Look over these four options and decide with your partner which is the easiest
to read. Why?

As the last loop demonstrates, the `for` loop is basically a
repackaged `while` loop that puts all the information about how long the
loop should continue in one place. Thus, a `for` loop is generally easier
to understand than an equivalent `while` loop.

### Exercise: A Jigsaw Puzzle - Drawing a Triangle

The file `TriangleDrawer.stuff` contains a collection of statements. Some of
the statements, together with some extra right braces, form the body of a main
method that, when executed, will print the triangle:

    *
    **
    ***
    ****
    *****
    ******
    *******
    ********
    *********
    **********

(Each line has one more asterisk than its predecessor; the number of asterisks
in the last line is the value of the `SIZE` variable. `SIZE` has a hard-coded value,
which you should experiment with. Feel free to make `SIZE` controlled by a command-line argument!
However, when you turn it in, make sure that it will run with `SIZE = 10`!)

First, if you are working with a partner, swap which partner is primarily writing 
the code. For this next part, we are going to need to create a new class, so let's 
learn how to do this!

At the top of IntelliJ, you should see "File". Click on it, and then hover over "New"
and then click on "Java Class". See this reference screenshot:
![New Java Class](img/NewJavaClass.png)

You will then be prompted to give a name, which in this case you should write `TriangleDrawer.java`. 
Now, you've learned how to create a new Java class, and are ready to continue on to the 
next part of the lab! 

Next, let us add a main method to the class. As a reminder, the structure of a main method is as follows:
```java 
public static void main(String[] args) {
    // statements go here
}
```

Copy and paste statements from the `TriangleDrawer.stuff` file into the main method of 
`TriangleDrawer.java`. You'll have to add some right braces in addition to the copied lines 
that you've chosen and rearranged. (You won't need all the statements. You shouldn't need to use 
any statement more than once.)

Many students encounter infinite loops in their first solutions to this
problem. If you get an infinite loop, be sure to hit `CTRL+C` in your terminal to halt
execution.

> Hint: So far, we have mostly used the well-named function System.out.println
> to conduct our printing. However, this function always outputs a new line at the
> end of its provided string. There is a variant of this function, System.out.print,
> which does not output a new line. You may find it helpful in this exercise!

### Exercise: Another Jigsaw Puzzle

Make a new Java file called `TriangleDrawer2.java` (you might want to copy and
paste from `TriangleDrawer.java`). In this file, rewrite the program so that it
produces the exact same output, but using `for` loops and no `while` loops. If
you have having trouble, re-read the parts above describing how to convert a
`while` loop to a `for` loop.

<details markdown="block">
  <summary markdown="block">
#### Hint: When do we define variables?
{: .no_toc}
  </summary>
When working with loops, we have to consider scope. In other words, we have to consider when our variables are being created,
when they are being modified, and when they are inaccessible. Which variables do we want to define within the loop (either in the
header or the body) and which variables do we want to define outside of the loop (either before or after the loop)?

For example, consider the `SIZE` variable. When is it being modified? Based on that, where should it be defined?

</details>

## Arrays

### Array Definition and Use

 An array is an indexed sequence of elements, all of the same type. Real-life
 examples of arrays include the following:

- ducks in a row
- slices of bread
- words in this sentence
- book pages
- egg cartons
- chessboards / checkerboards

We declare an array variable by giving the type of its elements, a pair of
square brackets, and the variable name, for example:

```java
int[] values;
```

Note that we don't specify the length of the array in its declaration.

Arrays are basically objects with some special syntax. To initialize an array,
we use the `new` operator as we do with objects; the argument to `new` is the type
of the array, which includes the length. For example, the statement

```java
values = new int[7];
```

stores a reference to a 7-element integer array in the variable `values`. This
initializes the array variable itself. If we want to declare and initialize the
array at the same time, we can:

```java
int[] values = new int[7];
```

The elements of the array are indexed from `0` to `(array length) - 1` and the
element at a particular index can be changed with an assignment statement. For
example, to set the second element to `4` we write:

```java
values[1] = 4;
```

For an `int` array, Java will (by default) set all of the elements to `0`.
Similarly, `double` arrays will be filled with `0.0`, `boolean` with `false`,
etc. For arrays of references to non-primitive objects (whose precise definition we will
cover in lab 4), the array will be initialized with `null`.

If you know what every value in your array should be at initialization time,
you can use this simplified syntax to directly initialize the array to the
desired values. Note that you don't have to provide the array length because
you're explicitly telling Java how long your array should be.

```java
int[] oneThroughFive = new int[]{1, 2, 3, 4, 5};
// This also works but only if you declare and initialize in the same line
int[] oneThroughFive = {1, 2, 3, 4, 5};
```

To access an array element, we first give the name of the array, and then
supply an index expression for the element we want in square brackets. For
example, if we want to access the `k`th element of values (0-indexed), we can
write:

```java
values[k]
```

If the value of the index expression is negative or greater than/equal to the
length of the array, an exception is thrown (negative indexing is not allowed).

Every array has an instance variable named `length` that stores the number of
elements that array can hold. For the `values` array just defined,
`values.length` is 7. The length variable can't be changed; once we create an
array of a given length, we can't shrink or expand that array.

### `for` Statements with Arrays

`for` statements work well with arrays. Consider, for example, an array named
`values`. It is very common to see code like the following:

```java
for (int k = 0; k < values.length; k += 1) {
    // do something with values[k]
}
```

### Shortcuts for Incrementing / Decrementing

Let `k` be an integer variable. Then the three following statements are
equivalent in that they all increment `k`.

```java
k = k + 1;
k += 1;
k++;
```

Similarly, these three statements all decrement `k` by 1.

```java
k = k - 1;
k -= 1;
k--;
```

Note: The motivation for this shorthand notation is that the operations of
incrementing and decrementing by 1 are very common. While it is legal to
increment or decrement variables within larger expressions like

```java
System.out.println(values[k++]);
```

this is a risky practice very susceptible to off-by-one errors. Discuss a
few settings that could lead to OBO errors with your partner. In general,
we suggest starting with more verbose syntax. Therefore, we ask that you
only use the `++` or `--` operations on lines **by themselves**.

### The `break` Statement

The `break` statement "breaks out of" a loop (both for and while loops). In
other words, it stops the execution of the loop body, and continues with the
statement immediately following the loop. An example of its use would be a
program segment that searches an array named `values` for a given `value`,
setting the variable found to true if the value is found and to false if it
is not in the array.

```java
boolean found = false;
for (int k = 0; k < values.length; k++) {
    if (values[k] == value) {
        found = true;
        break;
    }
}
```

This `break` statement allows us to save computation time. If we find the value within
the array before the end, we don't waste more time looping through the rest
of the array.

However, the `break` statement is not always necessary, and code with a lot
of `break`s can be confusing. Abusing the break statement is often considered
poor style. When using `break`, first consider if instead it would be more
appropriate to put another condition in the test.

### The `continue` Statement

The `continue` statement skips the current iteration of the loop body,
increments the variables in the loop information, then evaluates the loop
test. This example checks how many 0's there are in array `values`:

```java
int count = 0;
for (int i = 0; i < values.length; i++) {
    if (values[i] != 0) {
        continue;
    }
    count += 1;
}
System.out.println("Number of 0s in values array: " + count);
```

Similar to the `break` statement, the `continue` allows us to save time by
skipping sections of the loop. In this case, the `continue` allows us to add
to the `count` only when there is a 0 in the array. Removing continue will
give an incorrect output.

The difference between `break` and `continue` is that `break` immediately stops
the loop and moves on to the code directly following it. In comparison,
`continue` stops going through the current iteration of the loop body and
immediately continues on to the next iteration as given by the loop information.

Like with `break`, abusing `continue` is often considered poor style. Try not
to go crazy with nested `break`s and `continue`s.

Both `break` and `continue` apply to only the closest loop it is enclosed in.
For instance, in the case of the following nested loop, the `break` will only
exit out of the inner for loop, not the outer one.

```java
for (int i = 0; i < values.length; i++) {
    for (int j = i + 1; j < values.length; j++) {
        if (values[i] == value[j]) {
            break;
        }
    }
}
```

### Break!
Speaking of "break" statements, take a second to sip some water, stretch your body, and swap which partner is controlling the keyboard!

### Exercise: An Adding Machine Simulator

Consider a program that simulates an old-fashioned adding machine. The user
types integers as input, one per line. Input should be handled as follows:

-   A nonzero value should be added into a subtotal.

-   A zero value should print the subtotal and reset it to zero.

-   Two consecutive zeroes should print the total of all values inputted, then
    print out every value that was inputted in sequence (*not* including zeroes)
    then terminate the program.

Open the associated file `AddingMachine.java` that holds the implementation of
the above described program. Read through the TODO in the comments provided in the `AddingMachine.java` file.
For this exercise, you will be asked to "complete" AddingMachine so that it executes as specified in this spec.

Here's an example of how the program should behave.

| *User input* | *Printed output* |
|:------------:|:----------------:|
| 0            | subtotal 0       |
| 5            |                  |
| 6            |                  |
| 0            | subtotal 11      |
| -5           |                  |
| 5            |                  |
| 0            | subtotal 0       |
| 13           |                  |
| -8           |                  |
| 0            | subtotal 5       |
| 0            | total 16         |
|              | 5                |
|              | 6                |
|              | -5               |
|              | 5                |
|              | 13               |
|              | -8               |

There are several things to note. First, look at how the project description
leads to the implementation. Try testing the implementation with the inputs and
outputs listed above. Do the steps make sense?

Second, does this program work with all inputs?
In programming, the person who writes the code can, intentionally or not,
introduce their own ideas and assumption in the code, some of which can lead to
problems. Specifically, for the class `AddingMachine.java` we assumed that the
user will never enter more than `MAXIMUM_NUMBER_OF_INPUTS` non-zero values during
any run of the program.

Discuss with your partner: is this usually a fair assumption to make? Try
running the code and supply input that violates this assumption. Does the code
tell you that you have made an error or does it just crash? This touches on a
new idea of programming: **robustness**. This refers to code's ability to
handle incorrect user input. In real life, you'll never have a guarantee like
this, but you haven't been taught the proper Java to handle an arbitrarily long
sequence of inputs (yet!).

A few things to take away from this code:

-   Always consider what will happen if your user interacts incorrectly with
    your data.

-   To exit the `main` method, execute a `return;` statement somewhere inside
    the method. Because the `main` method is of type `void`, it can't return a
    value. Therefore, the appropriate `return` statement doesn't have an
    argument.

-   This code introduces the `Scanner` class. A `Scanner` can be used to read
    user input. Here the `Scanner` is created with `System.in` as an argument,
    which means that it is expecting input from the command line.

    -   You can do a variety of things with a `Scanner`, but in this exercise
        you'll find it most useful to use code like this:

        ```java
        int k;
        k = scanner.nextInt();
        ```

    -   Here, `scanner` reads everything it can from its input and stores the
        result in an integer `k`. Because `scanner`'s input is the command line,
        the program will actually stop and wait at this part of the code until
        the user types in something at the command line and hits enter. For
        example, if the user types `100`, then the program will store the value
        `100` in `k` before continuing on.

### Exercise: `insert` & `delete`

Look at the files `ArrayOperations.java` and `ArrayOperationsTest.java`.

Fill in the blanks in the `ArrayOperations` class. Your methods should pass
the associated tests in `ArrayOperationsTest`.

Note: Before trying to program an algorithm, you should usually try a small
case by hand. For each of the exercises today, work with your partner to do
each algorithm by hand before writing any code.

-   The `insert` method takes three arguments: an `int` array, a position in the
    array, and an `int` to put into that position. All the subsequent elements
    in the array are moved over by one position to make room for the new element.
    The last value in the array is lost.

For example, let `values` be the array {1, 2, 3, 4, 5}. Calling

```java
insert(values, 2, 7)
```

would result in `values` becoming {1, 2, 7, 3, 4}.

-   The `delete` method takes two arguments: an `int` array and a position in
    the array. The subsequent elements are moved down one position, and the
    value 0 is assigned to the last array element.

For example, let `values` be the array {1, 2, 3, 4, 5}. Calling

```java
delete(values, 2)
```

would result in `values` becoming {1, 2, 4, 5, 0}.

For today don't worry about the methods being called with incorrect input.

### Multidimensional Arrays

Having an array of objects is very useful, but often you will want to have an
array *of arrays* of objects. Java does this in a very natural way. We've
already learned that to declare an array, we do:

```java
int[] array;
```

Similarly, to declare an array of arrays, we do:

```java
int[][] arrayOfArrays;
```

When constructing an array of arrays, you *must* declare how many arrays it
contains (because this is the actual array you are constructing), but you don't
have to declare the length of each array. To declare an array of 10 arrays, you
do this:

```java
int[][] arrayOfArrays = new int[10][];
```

To construct the first array in the array of arrays, you could do:

```java
arrayOfArrays[0] = new int[5];
```

And you could access the first index of the first array as:

```java
arrayOfArrays[0][0] = 1;
```

Hopefully this all makes sense. Alternatively, you can fix the length of each
array in the array of arrays as the same length like this:

```java
int[][] tenByTenArray = new int[10][10];
```

You can also directly instantiate an array of arrays with prefilled elements,
such as:

```java
{% raw %}
int[][] oneThroughTen = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
{% endraw %}
```

An array of arrays, when the different sub-arrays can be of different sizes, is
called a *jagged array*. If they are all the same size, it is often convenient
to forget altogether that you have an array of arrays, and instead to simply
imagine you had a multi-dimensional array. For instance, you could create a
3-dimensional array (to represent points in space, for example) like this:

```java
int[][][] threeDimensionalArray = new int[100][100][100];
```

This 3D array has 100x100x100 = 1,000,000 different values. Multidimensional
arrays are extremely useful, and you'll be encountering them a lot.

### Exercise: Catenate

Again, look at the files `ArrayOperations.java` and `ArrayOperationsTest.java`.

Note that, with the provided starter code, the tests specific to this exercise 
will not pass. This is expected! Implement the related method as described below
and in the comments and the tests will pass!

Complete the Java function `catenate` so that it
performs as indicated below and in the comments. Remember that some
arrays can have zero elements!

Note: Again, before trying to program an algorithm, you should usually try a small
case by hand. Walk through the algorithm by hand with your partner.

You may find `System.arraycopy` useful for this problem, but you are not
required to use it. If you are not sure how to use this method, try Googling it!

-   The `catenate` method takes in two arguments: integer arrays `A` and `B`.
    You should return a new array with all of the elements of `A` directly
    followed by all of the elements in `B`.

For example, let `A` be the array `{1, 2, 3}` and `B` be the array `{4, 5}`.
Calling

```java
int[] values = catenate(A, B);
```

would result in `values` becoming `{1, 2, 3, 4, 5}`.

Again, for today, don't worry about the method being called with incorrect input.
When you finish this function, all tests in `ArrayOperationsTest.java` should
compile and pass.

## Conclusion

### Wrap-Up

Today's lab reintroduced a number of concepts in programming (such as loops and
conditionals) which you have likely seen before, and explained to you how they
work in Java. The exercises gave you practice both for writing your own code
from scratch and debugging or interpreting code which has been given to you.

### Deliverables

Here's a short recap of what you need to do to finish this lab.

Ensure you have saved, `git add`ed, `git commit`ed, and `git push`ed all of your files!
Make sure that, if you are working in a partnership, only one of you submits, and adds the 
other to the submission!

-   Submit the following files to Gradescope for grading.
    - `DateConverter.java`
    - `TriangleDrawer.java`
    - `TriangleDrawer2.java`
    - `AddingMachine.java`
    - `ArrayOperations.java`
