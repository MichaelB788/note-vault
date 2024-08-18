

import java.util.Arrays;
import java.util.Comparator;

//CLASSES
class Animal {
    @Override
    public String toString() {
        return "animal";
    }
}

public class AnonymousClassDemo {
    public static void main(String[] args) {
	/*
		We are defining an anonymous class that inherits from Animal,
        and we are simultaneously creating an object of that anonymous class.
        An anonymous class must inherit from a class or interface.
        It's good for a class that you only intend to create a sinlge object of.
	*/      

	  	Animal feline = new Animal() {
            @Override
            public String toString() {
                return "cat " + super.toString();
            }
        };

		// This calls the toString method of the anonymous calss.
        System.out.println(feline.toString()); // cat animal

        String[] stringArray = {"cat", "rabbit", "bird"};

        // We are defining an anonymous class that inherits from Comparator
        // and we are creating an object of that class

        Comparator<String> byLength = new Comparator<String>() {
            @Override
            public int compare(String s1, String s2) {
                return Integer.compare(s1.length(), s2.length());
            }
        };

        Arrays.sort(stringArray, byLength); // sorts the array based on the provided Comparator
        System.out.println(Arrays.toString(stringArray)); // [cat, bird, rabbit]

		// Anonymous classes allow us to utilize interfaces such as Comparator without
		// having to create a standalone class (like StringLengthComparator). 
    }
}

