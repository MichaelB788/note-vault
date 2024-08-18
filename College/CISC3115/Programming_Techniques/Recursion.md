**Topics covered:**
- Recursion
- Introductory Recursion
    - [Factorials](#facotrials)
    - [Fibonacci Sequence](#fibonacci-sequence)
- Advanced Recursion
    - [Reversed String](#reversed-string)
- Practical Recursion
    - [Determining the Size of a Directory](#determining-the-size-of-a-directory)

# Recursion
[More on Recursion](https://en.wikipedia.org/wiki/Recursion_(computer_science)#:~:text=In%20computer%20science%2C%20recursion%20is,from%20within%20their%20own%20code.)

Recursion in programming is simply any method that calls itself within its own function.

In a more general sense however; a recursive definition is any definition that relies
on itself -- **it is defined in terms of itself**.

When trying to use recursion to solve a problem, think about:

- What's a good simple **base case**?
- In the recursive case, how can we do a small amount of work, followed by a
**recursive call**?
    - For the recursive call, we want to use a smaller version of the original problem.

Below is a simple program demonstrating a countdown function using recursion.

```Java
public class Palindrome 
{
    public static void main(String[] args) 
    {
        System.out.println(isPalindrome("cat")); // false
        System.out.println(isPalindrome("racecar")); // true
    }

    public static boolean isPalindrome(String s) 
    {
        return palindromeRecursiveHelper(s, 0, s.length() - 1);
    }

    // Determines whether s is a palindrome in the range from 
    // startIndex through endIndex. Ignores the characters 
    // before startIndex and the characters after endIndex.
    private static boolean palindromeRecursiveHelper(String s, int startIndex, int endIndex)
    {
        // if the length of the range is less than or equal to 1
        if (startIndex >= endIndex)
        {
            return true;
        }
        else 
        {
            return s.charAt(startIndex) == s.charAt(endIndex) 
                && betterIsPalindromeRecursiveHelper(s, startIndex + 1, endIndex - 1);
        }
    }
}
```

## Introductory Recursion 

### Factorials

Consider the definition of a factorial:

```
 0! = 1
 n! = n * (n - 1) * (n - 2)* ...
 where n is any positive integer.
```

For example: `5! = 5 * 4 * 3 * 2 * 1` 

So how can the definition of a factorial be translated into a program?
With recursion, the program itself is quite simple. Consider the following:

```Java
public class Factorial
{
    public static void main(String[] args)
    {
        System.out.println(factorial(5));
    }

    public static int factorial(int n) 
    { 
        if (n < 0) 
        {
            throw new IllegalArgumentException(n + " is negative");
        }
    
        if (n == 0) // base case
        { 
            return 1;
        } else // recursive case 
        { 
            return n * factorial(n - 1);
        }
    }
}
```
In the stack, the above program behaves something like this (Read from bottom to top).

| Function Call | n       | return         |
|---------------|---------|----------------|
| factorial(1)  |  n = 1  | return 1       |
| factorial(2)  |  n = 2  | return 2 * ___ |
| factorial(3)  |  n = 3  | return 3 * ___ |
| factorial(4)  |  n = 4  | return 4 * ___ |
| factorial(5)  |  n = 5  | return 5 * ___ |
| main          |   ---   |      ---       |


`factorial(n)` (and most recursive methods) **push several recursive
methods into the stack in order to achieve the effect of recursion**. 

But what is the result? Well, all you have to do is fill in the blanks.

Read the above diagram, but now go from top to bottom, passing each result
to the next method call in the stack, up until you reach back into main.

| Function Call | n       | return         |
|---------------|---------|----------------|
| factorial(1)  |  n = 1  | return 1       |
| factorial(2)  |  n = 2  | return 2 * _1_ |
| factorial(3)  |  n = 3  | return 3 * _2_ |
| factorial(4)  |  n = 4  | return 4 * _6_ |
| factorial(5)  |  n = 5  | return 5 * _24_|
| main          |   ---   | 120            |

> **In other words, take the return value of the current function call 
> (starting from the first from the top, which is facotrial(1) in this
> case), and pass it down to the next!**


And that's it. You found the return value of a recursive function. Not too
difficult really.

<br>

### Fibonacci Sequence

The Fibonacci Sequence is a much more sophisticated example of recursion in action.
First, consider the following `fib(n)` function below.

```Java
public class Fibonacci
{
    public static void main(String[] args)
    {
        System.out.println(fibonacci(5));

        for (int i = 0; i < 100; i++) 
        {
            System.out.println("fibonacci(" + i + ") = " + fibonacci(i));
        }
    }

    public static int fibonacci(int n)  // returns the nth fib number
    {
        if (n < 0) 
        {
            throw new IllegalArgumentException(n + " is negative");
        }

        if (n == 0 || n == 1) 
        {
            return n;
        }
        else 
        {
        /*
           two recursive calls!
           first, the left call is done fully. 
           when the left is complete, then the right call is done fully.
           when the right is complete, the values are added up and the
           sum is returned by the current method call.
         */
            return fibonacci(n - 1) + fibonacci(n - 2); 
        }
    }
}
```

Tracing the Fibonacci sequence isn't quite as simple as tracing `factorial(n)`, 
and this mainly due to the use of two recursive functions.

It's a lot more simple and accurate, to track the stack in the form of a tree-diagram.

![Fibbing Moment](https://files.realpython.com/media/Screen_Shot_2021-06-03_at_10.24.56_PM.dde28642334d.png)

In order to create this diagram, we first start from `F(5)` (which is equivalent to 
`fibonacci(n)`).

Take note of how `fibonacci(n)` returns

`fibonacci(n - 1) + fibonacci(n - 2)`

What this effectively does is create two branches of `fibonacci(n)` functions. In the
case of `F(5)`, this creates branches `F(4)` and `F(3)`

So what's next? Well, we perfom the same process we did to determine the branches of `F(5)`,
but we do so on each child node we create until we reach child nodes `F(1)` and `F(0)`.

Once we're done breaking it down completely, we then work our way back up. This is
best accomplished when we compute the result of each child node from **left to right**.
> This is known as LR notation.

And that's essentially how compilers determine a sequence such as 

`fibonacci(n - 1) + fibonacci(n - 2)`

<br>

## Advanced Recursion

Included in this section are some problems which were relatively difficult to wrap my
head around upon seeing them at first. Taken from HW11 of CISC 3130, it's best if I take
the time to make sense of some of these problems.

### Reversed String

Wanderer, I highly encourage you to check out this [link](https://cscircles.cemc.uwaterloo.ca/java_visualize/#code=import+java.util.Scanner%3B%0Apublic+class+ClassNameHere+%7B%0A+++public+static+void+main(String%5B%5D+args)+%7B%0A++++++String+str+%3D+%22dog+cat+leopard+dachshund%22%3B%0A++++++Scanner+sc+%3D+new+Scanner(str)%3B%0A++++++%0A++++++copy(sc)%3B%0A+++%7D%0A+++public+static+void+copy(Scanner+sc)%0A+++%7B%0A++++if(sc.hasNext())%0A++++%7B%0A++++++++String+str+%3D+sc.next()%3B%0A++++++++copy(sc)%3B%0A++++++++System.out.println(str)%3B%0A++++%7D%0A+++%7D%0A%0A%7D&mode=display&curInstr=0) in order to view the full stack trace of
this program!

This problem was a little difficult to make sense of, but the solution is seemingly sound.
The goal of the function `copy` is to read in a string of words and print them out to the 
system in reverse order. It's simple enough, but it's difficult to make sense of when
recursion comes in to play.

```Java
import java.util.Scanner;

public class ReversedString
{
    public static void main(String[] args)
    {
        String str = "dog cat leopard dachshund";
        Scanner sc = new Scanner(str);

        copy(sc);
    }

    public static void copy(Scanner sc)
    {
        if(sc.hasNext())
        {
            String str = sc.next();
            copy(sc);
            System.out.println(str);
        }
    }
}
```

So how does this work?

`copy` takes a `Scanner` object and begins to read from our input above. So long as the `sc`
has another token to read, we store the current token into a `String` variable.

Now here's where the magic begins.

We call `copy(sc)` within itself. What I believe happens is that this essentially pushes the
`String` we have stored in `str` to the bottom of the "stack," such that now when we enter the
method again via recursion, we keep pushing the next `String` token to the bottom of the stack.

This then creates the effect that the word is reversed, as when we call `System.out.println(str)`,
we print out the `String` objects we have pushed into the stack when we "pop" them out from top
to bottom.

The stack trace should look something like this:

![Image](/home/mike/Pictures/stackload.png)

> Notice that with each call of `copy(sc)`, we push the next string token on to the stack!

After our `Scanner` cannot read anymore tokens, we finally print out all of the `String` objects
we stored in the stack.

Although, what really happens is that we start from the very last recursion
call of `copy(sc)`, the one which contains `str: "dachshund"`.

We essentially "finish up" this method call by executing the `sout` command we wrote after the
recursion call. We continue to do this until we fully work our way down back to main.

<br>

## Practical Recursion

### Determining the Size of a Directory

Many problems which utilize recursion can usually be solved with loops. However, what
if there was a case where loops weren't the easier solution?

Below is a program that asks the user for the name of a file or directory.

If user enters a file name, the program should print the size of the file in bytes. 
Else if the user enters a directory name, the program prints the total size of all files
in that directory, going all the way down to sub-directories, sub-sub-directories,
etc.

```Java
public class DirectorySize
{
    public static void main(String[] args)
    {
        System.out.print("Enter the name of a directory or file: ");    
        Scanner scanner = new Scanner(System.in);
        String name = scanner.next();
        File directoryOrFile = new File(name);
        System.out.println(getSize(directoryOrFile) + " bytes");
    }
    
    public static long getSize(File directoryOrFile) {...}

}
```

In main, we tell the user to print the name of their directory or file. We then
store this info using `Scanner` and `File` classes. Then we call a method called
`getSize()`, which takes a `File` (the directory of the file) and returns a `long`
(which represents the file size in bytes).

Here is the recursive method `getSize()`:

```Java
public static long getSize(File directoryOrFile)
{
    if (directoryOrFile.isFile())    
    {  
        return directoryOrFile.length();
    }
    else // We know by now that we're dealing with a directory
    { 
        long size = 0;

        // all files and subdirectories inside the currect directory
        File[] children = directoryOrFile.listFiles(); 

        // recursive call
        for (File child : children)
        {
            size += getSize(child); 
        }

        return size;
    }
}
```

Had we opted for a loop, we would have to manually check each child of the directory,
and each grandchild of the directory, so on so forth, until we reach the end of the
directory.

We could save a lot of work by simply cally `getSize()` within itself, as the function
already does the work of checking whether the file passed on is a file or directory.

All we have to do is make sure `getSize()` is called on each child of the directory, so
we make an array of files called `children` by calling `listFiles()` on `directoryOrFile`
(which we know is a directory at this point).

Then it's as simple as getting the size of each child node and adding it to `size`.
> and if that child node happens to be a directory, `getSize()` will know and create
> another parent branch containing children of its own.
