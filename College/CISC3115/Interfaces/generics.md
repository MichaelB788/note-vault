GENERICS


An old-style (pre-2004 Java) generic class. 
Generic class: a class that can work with various kinds of data.

public class ObjectBox {
    private Object item;

    public ObjectBox(Object item) {
        this.item = item;
    }

    public Object getItem() {
        return item;
    }

    public void setItem(Object item) {
        this.item = item;
    }
}


There are some problems with this approach:
    One issue with the old approach: we need to cast:
        String temp = (String) oldStringBox.getItem();
        
    Another issue; no type safety:
        oldStringBox.setItem(LocalDate.now());
        // There is nothing to prevent this:
        temp = (String) oldStringBox.getItem(); // Throws a ClassCastException
            

********************************************************************************************


A modern Java generic class.

public class Box<T> { 
    
/*
    T is a type parameter of the Box class
    now T can be used with any instance fields, instance methods, and constructors of Box
    T represents a type that will be specified by client code each time a Box object is
    initialized. 
        For example, one could say:
        Box<String> stringBox = new Box<String>("a");
    T can only represent a reference type, not a primitive type.
*/
    
    private T item;

    public Box(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }

    public void setItem(T item) {
        this.item = item;
    }

    @Override
    public String toString() {
        return "Box{" + item + "}";
    }

/*
    T, the type parameter of the class, cannot be used in static fields and methods.
    There are ways to circumvent this:

    Generic static method - this method can work with data of any reference type
    We define the type paramter right before the return type of the static method
        
        public static <E> void printArray(E[] arr) {
            for (E element : arr) {
                System.out.print(element + " ");
            }
        }
*/

}

Now when we create an object of the Box class, we pass a type argument to the class indicating that T represents for the new object

    Box<String> stringBox = new Box<>("String"); // for this object, T represents String
    String s = stringBox.getItem(); // no cast necessary, getItem returns String
    System.out.println(s); // String
    stringBox.setItem("another String");
    // stringBox.setItem(LocalDate.now()); // Won't compile, preserving safety
    System.out.println(stringBox); // Box{another String}


