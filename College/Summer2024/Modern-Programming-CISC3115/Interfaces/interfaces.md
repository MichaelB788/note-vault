Interface:

Similar to an abstract class, but no instance fields and no constructors, 
and methods are abstract by default. 

Significantly, a class cannot directly extend multiple classes.

For example, we CANNOT have class Customer extends Friend, Person.
But a class can directly inherit from multiple interfaces, and also from a single class.

So we can have:

class Subclass extends Superclass implements Interface1, Interface2, Interface3 {}

The main differences between abstract classes and interfaces are:
1. Interface cconnot have instance fields; an abtract class can.
2. A class cannot directly extend multiple abstract classes, but a calss can directly inherit from miultiple interfaces.


***********************************************************************************************


Why use interfaces?

The purpose of an interface is to build a common trait into multiple classes without much in common.

For example, consider:

class Animal {}
class Chicken extends Animal {}
class Apple {}

It doesn't make sense for Chicken and Apple to have a common superclass, since they don't 
have much in common. However, they both have the property of being edible. 

[!] We can have both Chicken and Apple implement an Edible interface.
 
If Edible would be a class, then Chicken wouldn't be able to inherit from both Animal and Edible.

And it wouldn't be good to have Animal inherit from Edible, since not all animals are edible.


***********************************************************************************************


Interface                                             Class
- Cannot be instantiated with new                     - Can be instantiated with new 
                                                        (unless class is abstract)
- Cannot contain any constructors                     - Can contain constructors
- No state (instance fields)                          - Can have state (instance fields)
- Fields are automatically public static final        - By default, fields are package-private, 
                                                        non-static, and non-final.
                                                        They can be made public, private, or protected; 
                                                        static; final.
- By default, instance methods are abstract           - Methods are not abstract (expect for 
                                                        explicitly-marked abstract methods in abstract class)
- By default, methods are public                      - By default, methods are package-private
- A class "implements" an interface                   - A class "extends" another class
- A class can directly implement multiple interfaces  - A class cannot directly extend multiple classes
  And a class can extend another class and
  implements an interface at the same time.
- An interface can extend another interface.          - An interface cannot extend a class.


***********************************************************************************************


Class: data type with behavior (methods) and state (instance fields).
Interface: data type with behavior but no state. 

A class:
- specifies a type (the class name) and its operations (instance method headers)
- implements the type by including instance fields and the bodies of instance methods
- a class combines specification with implementation
- can also contain static methods and fields

Interface:
- specifies a type (the interface name) and its operations (instance method headers)
- does not contain full implementation
    - implementation is deferred to classes that inherit from ("implement") the interface
- typically contains abstract methods, which are simply instance method headers;
  non-abstract instance methods must be marked as "default"
- can also contain static fields and methods.


***********************************************************************************************


When a class implements an interface, 
it must override all abstract methods inherited from the interface
(unless the class is itself an abstract class).

Main use of interfaces: as a means of classifying common properties or behaviors that
are exhibited by many non-related types of objects.
For example, although a Chicken and an Apple have very little in common,
and it doesn't make sense for them to directly inherit from the same superclass,
they do share the common property of being Edible, so we can make them both inherit 
from the Edible interface. 

As another example, many unrelated types of objects have the property of being comparable:
Strings are comparable, Integers are comparable, LocalDates are comparable, etc.
These classes all implement an interface named Comparable, 
which specifies a method named compareTo.
The compareTo method gets invoked like this: a.compareTo(b). It returns:
- a negative int if a is "less than"/"before" b
- a positive int if a is "greater than"/"after" b
- 0 if a and b are equal


***********************************************************************************************


/*
Both Apple and Chicken will inherit from the Edible interface. 
Apple s and Chickens are very differnt kinds of things, but they 
both share the property of being edible. 

Contrast this with the Shape class, where Circles and Rectangles
are both the same kind thing: Shapes. 
*/

interface Edible { // data type named Edible
    // interface fields are automatically public static final
    String message = "this is edible";

    // interfaces cannot have constructors.

    // by default, interface methods are public

    // an abstract instance method. will be completed by classes that implement this interface
    // abstract method = just method header with semicolon, no body
    String howToPrepare();

    // a non-abstract instance method
    default void printMessage() {
        System.out.println(message);
    }

    // a static method (never abstract)
    static void printMessageStatic() {
        System.out.println(message);
    }
}

interface Soundable {
    void makeSound(); 
}

class Animal {}

// this class must override howToPrepare (from  Edible) and makeSound (from Soundable)
class Chicken extends Animal implements Edible, Soundable {
    @Override
    public String howToPrepare() {
        return "fry it";
    }

    @Override
    public void makeSound() {
        System.out.println("cluck-cluck");
    }
}

class Apple implements Edible {
    @Override
    public String howToPrepare() {
        return "cut it up";
    }
}

class Tiger extends Animal implements Soundable {
    @Override
    public void makeSound() {
        System.out.println("ROAR");
    }
}

public class Demo {
    public static void main(String[] args) {
        // interface cannot be directly instantiated; this won't compile
        // Edible e = new Edible();

        Edible e = new Chicken(); // allowed

        Soundable[] soundables = {new Chicken(), new Tiger()};

        for (Soundable s : soundables) {
            s.makeSound();
        }
        // cluck-cluck
        // ROAR

        Edible[] edibles = {new Chicken(), new Apple()};

        for (Edible e : edibles) {
            System.out.println(e.howToPrepare());
        }
        // fry it
        // cut it up
    }
}
