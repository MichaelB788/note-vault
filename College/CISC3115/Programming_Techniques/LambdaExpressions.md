Topics Covered:
- Lambda Expressions
- [Functional Interface](#functional-interface)
- [Applications of Lambda Expressions in Java](#application-of-lambda-expressions-with-the-comparator-interface)

# Lamda Expressions

> More on lambda expressions [here](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-expressions).

A Lambda Function, which is fancy for an **anonymous function** (and typically a 
small one), is a self-contained block of functionality that can be passed around
and used in your code.

In essence Lamda functions allows us to avoid boilerplate code with quick
"throw away" functions.

## Functional Interface

> More on functional interfaces [here](https://www.geeksforgeeks.org/functional-interfaces-java/).

> Note: In Java (and seemingly only in Java), a lambda expression must
> inherit from a **functional interface**.

A functional interface is a special kind of interface, in that it contains exactly
one abstract method (though not including the methods of the Object class).

They're most commonly used alongside lambda expressions in Java.

Below is a small example of a functional interface.

```Java
@FunctionalInterface // Not necessary
interface IntBinaryOperator {

    // This is the functional method, the only abstract method
    // in a functional interface.
    int apply(int a, int b);

    String toString();

    static void staticMethod() {}

    default void defaultMethod() {}
}
```

A functional interface *can* have more than one method, though it doesn't mean it
necessarily should, as inheritors wouldn't be able to access it anyway (note how
none of the methods are `public`).

Below is a program which utilizes the functional interface `IntBinaryOperator` in
order to perform some simple arithmetic.

``` Java
public class LambdaExpressionDemo
{
    public static void main(String[] args) 
    {
        // Note: The arrow (->) signifies to you and the compiler that
        // the code is a lambda expression.

        // simplified lambda expressions:
        IntBinaryOperator addition = (a, b) -> a + b;

        IntBinaryOperator multiplication = (a, b) -> a * b;

        // application
        System.out.println(addition.apply(9, 10)); // 21
        System.out.println(multiplication.apply(4, 5)); // 20

        // Utilizing the "high order function" (more info below).
        int[] ints = {5, 2, 3};
        System.out.println(reduce(ints, 0, addition)); // 10
        System.out.println(reduce(ints, 1, multiplication)); // 30
        System.out.println(reduce(ints, Integer.MIN_VALUE, max)); // 5
    }

    /*
    * The method below is an example of a "higher order function"
    * It is a function that takes another function as input OR
    * returns a function.
    * 
    * This function reduces the array to a single int by applying the
    * given Comparator to the local result and each element in ints[].
    */
    public static int reduce(
        int[] ints, 
        int startingPoint, 
        IntBinaryOperator operator
    ){
        int result = startingPoint;

        for (int element : ints) 
        {
            result = operator.apply(result, element);
        }

        return result;
    }
}
```

Note that the lambda expressions shown above were simplified. Take `IntBinaryOperator addition` for example; we could denote it like this:

```Java
IntBinaryOperator addition = (a, b) -> {
    return a + b;
};
```

However, the extra stuff like the curly braces could be omitted if (and only if) the
lambda expression consists of one line, that being a return operation.

<br>

## Application of Lambda Expressions with the Comparator Interface

The Comparator interface is an incredibly versatile tool being that it nor only is
a functional interface (meaning that it is synergetic with lambda expressions), but
it is a very widely used interface and many Java libraries extend it.

In conjunction with lambda's, Comparator's are able to sort array-like objects in
any way we want.

Take a look at the program below, in which we use a Comparator in order to sort
elements of a `String` array alphabetically, and then by natural order:

```Java
import java.util.Arrays;
import java.util.Comparator;

public class ComparatorUsingLambdaExpressionDemo
{
    public static void main(String[] args) 
    {
        String[] stringArray = {"rabbit", "dog", "cat", "bird"};

        // Sort the elements of the array by the length of the String
        // (smallest to largest)
        Comparator<String> byLength = (s1, s2) ->
            Integer.compare(s1.length(), s2.length());

        // Arrays.sort() take Comparators as a second argument
        Arrays.sort(stringArray, byLength); 

        // [cat, dog, bird, rabbit] OR [dog, cat, bird, rabbit]
        System.out.println(Arrays.toString(stringArray));

        // byLength works fine, but its result is ambiguous
        // Below is not so ambiguous Comparator, though we have to
        // sacrifice the "clean" code.
        Comparator<String> byLengthThenAlphabetically = (s1, s2) ->
        {
            if (s1.length() != s2.length())
            {
                return Integer.compare(s1.length(), s2.length());
            }
            else
            {
                return s1.compareTo(s2);
            }
        };

        Arrays.sort(stringArray, byLengthThenAlphabetically);

        // [cat, dog, bird, rabbit]
        System.out.println(Arrays.toString(stringArray)); 
    }
}

```

Since the above example utilized Strings, one could naturally assume that Comparators
are compatible with all types of objects, including objects that we create ourselves.

Below we use a Comparator to sort an array of `Student(id, age)` objects.

```Java
public class AnotherExample
{
    public static void main(String[] args)
    {
        Student[] students =
        {
                new Student(333, 21),
                new Student(222, 19),
                new Student(111, 21)
        };

        Comparator<Student> byAgeThenById = (student1, student2) -> {
            if (student1.getAge() != student2.getAge()) {
                return Integer.compare(student1.getAge(), student2.getAge());
            } else {
                return Integer.compare(student1.getId(), student2.getId());
            }
        };

        // Sort students by age and then (if the ages are equal)
        // sort them by id.
        Arrays.sort(students, byAgeThenById);
        System.out.println(Arrays.toString(students));
    }
}
```
