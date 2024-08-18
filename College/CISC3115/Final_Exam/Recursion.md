Topics covered:
- [Factorials](#factorials)
- [Fibonacci Sequence](#fibonacci-sequence)

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

## Factorials

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
| main |


`factorial(n)` (and most recursive methods) **push several recursive
methods into the stack in order to achieve the effect of recursion**. 

Now that all these methods are in the stack, the compiler processes each of these
functions and "pops" them out.

Read the above diagram, but now go from top to bottom, passing each result
to the next factorial method in the stack, up until it reaches main.

## Fibonacci Sequence

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
