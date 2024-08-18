import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

/*
An exception is an error that occurs while a program is running; 
not detected by the compiler beforehand.

There are many kinds of exceptions in Java. 
Each kind of exception is represented by a class.
For example, NullPointerException is a type of exception 
and is the name of a class.

The occurrence of an exception is called "throwing" the exception.
Java can throw various kinds of exceptions. Below are some exmples.

If an exception is thrown anywhere in the program and not handled,
the program terminates (crashes) and prints a message; any subsequent
statements are not executed.
*/

public class CommonExceptionsDemo {
    public static void main(String[] args) throws FileNotFoundException {
        System.out.println("In main, before calling demo method");
        demo();
        System.out.println("In main, after calling demo method");
    }

    // demonstrates some common types of exceptions
    public static void demo() throws FileNotFoundException {
        System.out.println("In demo method, before the exception");

    // causes an ArithmeticException to be thrown
        System.out.println(4 / 0);

    // causes a NumberFormatException to be thrown
        // int x = Integer.parseInt("123g");

    // NullPointerException
        // String[] strings = new String[10]; // the value of each element is null
        // System.out.println(strings[0].length()); // calling instance method on null

        // this is fine
        // Shape s1 = new Circle();
        // Circle c1 = (Circle) s1;
        
    // ClassCastException
        // Shape s2 = new Shape();
        // Circle c2 = (Circle) s2;

    // NoSuchElementException -- typical case is when trying to read from a Scanner
	// past the end of its data
        // Scanner sc = new Scanner("a b");
        // System.out.println(sc.next()); // fine, prints a
        // System.out.println(sc.next()); // fine, prints b
        // System.out.println(sc.next()); // NoSuchElementException

    // InputMismatchException
        // Scanner sc = new Scanner("1 2 c");
        // System.out.println(sc.nextInt()); // 1
        // System.out.println(sc.nextInt()); // 2
        // System.out.println(sc.nextInt()); // throws InputMismatchException

    // ArrayIndexOutOfBoundsException
        // double[] arr = {7, 8, 9};
        // System.out.println(arr[3]); // throws ArrayIndexOutOfBoundsException

    // StringIndexOutOfBoundsException
        // String s = "abc";
        // System.out.println(s.charAt(3)); // throws StringIndexOutOfBoundsException

    // FileNotFoundException
        // File file = new File("nonexistent-file.txt"); // doesn't throw exception
        // Scanner sc = new Scanner(file); // throws FileNotFoundException

    // OutOfMemoryError
        // StringBuilder sb = new StringBuilder();
        // while (true) {
        //     sb.append("a");
        // }
    }
}

class Shape {}
class Circle extends Shape {}



----------------------------------------------------------------------------



public static double averafe (int[] arr) {
	if (arr.length = 0)
		throw new IllegalArgumentException("Cannot have an array with length of 0");
}
