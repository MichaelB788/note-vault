COMPARATOR INTERFACE

Link to the Comparator docs:
https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html

Suppose we would like to compare Strings in some other way, such as by length. To do this, we create an object that inherits from the Comparator interface. 

This interface has a method named compare that takes two objects as input,
and returns an int (negative, positive, or 0, like the compareTo method).
Suppose c refers to an object that inherits from Comparator. 

We can say: c.compare(s1, s2);

Essentially, the Comparator interface takes two objects and compares them by an external controllable, rather than by the default natural order of Comparable.

-----------------------------------------------------------------------------------------------

Use Comparable if you want to define a default (natural) ordering behaviour of the object in question, a common practice is to use a technical or natural (database?) identifier of the object for this.

Use Comparator if you want to define an external controllable ordering behaviour, this can override the default ordering behaviour.


***********************************************************************************************


import java.util.Arrays;
import java.util.Comparator;

// CLASSES
class StringLengthComparator implements Comparator<String> {
    @Override
    public int compare(String s1, String s2) {
		
		// Comparing by String length
        return Integer.compare(s1.length(), s2.length());

    }
}

class StudentAgeComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1 , Student s2) {

		// Comparing by age
        return Integer.compare(s1.getAge(), s2.getAge());

    }
}
// END OF CLASSES


// MAIN
public class ComparatorDemo {
    public static void main(String[] args) {
        
		// Comparing by natural order (through the Comparable interface).

		System.out.println("bird".compareTo("cat")); // negative int
        System.out.println("dog".compareTo("cat")); // positive int

		// Using external sorting method via the Comparator interface we implemented.
		// In this case we compare each object by string length.

        Comparator<String> byLength = new StringLengthComparator();
        System.out.println(byLength.compare("bird", "cat")); // positive int
        System.out.println(byLength.compare("dog", "cat")); // 0

        String[] stringArray = {"cat", "rabbit", "bird"};
        Arrays.sort(stringArray, byLength); // sorts the array based on the provided Comparator
        System.out.println(Arrays.toString(stringArray)); // [cat, bird, rabbit]


        Student[] students = {
                new Student(56789, 19),
                new Student(12345, 21),
                new Student(11111, 20)
        };

        Arrays.sort(students); // sorts the students by id
        
        Comparator<Student> byAge = new StudentAgeComparator();

        // sort students based on their ages, from lowest age to highest age

        Arrays.sort(students, byAge);
        System.out.println(Arrays.toString(students));

        Comparator<Student> byAgeReversed = byAge.reversed();

        Student a = new Student(11111, 21);
        Student b = new Student(22222, 20);
        System.out.println(byAge.compare(a, b)); // positive int

        System.out.println(byAgeReversed.compare(a, b)); // negative int

        // sorts the students by age, from highest age to lowest age
        Arrays.sort(students, byAgeReversed);
        System.out.println(Arrays.toString(students));

        Arrays.sort(students); // sorts by natural order, that is, by id from lowest to highest
        
        // create a comparator that compares students by reverse of the natural order
        // one way:
        // Comparator<Student> byId = Comparator.naturalOrder(); // creates a comparator that uses natural order
        // Comparator<Student> byIdReversed = byId.reversed(); // then we get the reverse
        // better way:
        Comparator<Student> byIdReversed = Comparator.reverseOrder();
        
        // sort students by id in reverse order (highest to lowest)
        Arrays.sort(students, byIdReversed);
        System.out.println(Arrays.toString(students));
    }
}

