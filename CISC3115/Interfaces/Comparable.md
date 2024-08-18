Many unrelated types of objects have the property of being comparable:

Strings are comparable, Integers are comparable, LocalDates are comparable, etc.
These classes all implement an interface named Comparable, which specifies a method named compareTo().

The compareTo method gets invoked like this: a.compareTo(b). It returns:
- a negative int if a is "less than"/"before" b
- a positive int if a is "greater than"/"after" b
- 0 if a and b are equal

*compareTo() is abstract by default in Comparable.

More info:
https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html#compareTo-T- 


***********************************************************************************************


EXAMPLES USING .compareTo(), Arrays.sort(), AND Arrays.toString()


import java.util.Arrays;

public class UsingComparableDemo {
    public static void main(String[] args) {

        System.out.println("a".compareTo("r")); // negative int
        System.out.println("r".compareTo("a")); // positive int
        System.out.println("a".compareTo("a")); // 0
        System.out.println();

        // Arrays.sort(arr) works only if the elements of arr come from a class
        // that implements Comparable

        String[] stringArray = {"r", "a", "y", "h"};
        Arrays.sort(stringArray); // uses String's compareTo method to compare the elements with each other
        System.out.println(Arrays.toString(stringArray)); // [a, h, r, y]
        System.out.println();

        System.out.println(new Student(1111, 23).compareTo(new Student(2222, 20))); // a negative int

        Student[] students = {
            new Student(56789, 19),
            new Student(12345, 21),
            new Student(11111, 20)
        };
        System.out.println(Arrays.toString(students));
        Arrays.sort(students);
        System.out.println(Arrays.toString(students));

        Product[] products = {
            new Product(666, "apple", 1.25),
            new Product(555, "apple", 1.05),
            new Product(444, "bread", 2.25),
            new Product(333, "bread", 2.25),
            new Product(222, "milk", 1.75),
            new Product(111, "almonds", 1.25)
        };

        Arrays.sort(products);

        for (Product product : products) {
            System.out.println(product);
        }

        Date[] dates = {
            Date.parse("9/15/2022"),
            Date.parse("10/13/1999"),
            Date.parse("12/10/1999")
        };
        Arrays.sort(dates);
        System.out.println(Arrays.toString(dates));

    }
}


***********************************************************************************************


EXAMPLE OF IMPLEMENTING THE Comparable INTERFACE:


import java.util.Objects;

public class Date implements Comparable<Date> {
    private int month, dayOfMonth, year;

    public Date(int month, int dayOfMonth, int year) {
        this.month = month;
        this.dayOfMonth = dayOfMonth;
        this.year = year;
    }

    // dateString has the format of month/dayOfMonth/year, for example, "10/25/2023"
    public static Date parse(String dateString) {
        String[] parts = dateString.split("/"); // ["10", "25", "2023"]
        int month = Integer.parseInt(parts[0]);
        int dayOfMonth = Integer.parseInt(parts[1]);
        int year = Integer.parseInt(parts[2]);
        return new Date(month, dayOfMonth, year);
    }

    @Override
    public String toString() {
        return month + "/" + dayOfMonth + "/" + year;
    }

    @Override
    public boolean equals(Object o) {
        if (o instanceof Date) {
            Date other = (Date) o;
            return this.month == other.month && this.dayOfMonth == other.dayOfMonth && this.year == other.year;
        } else {
            return false;
        }
    }

    @Override
    public int hashCode() {
        return Objects.hash(month, dayOfMonth, year);
    }

    // compares dates chronologically
    @Override
    public int compareTo(Date other) {
        int yearComparison = Integer.compare(this.year, other.year);
        if (yearComparison != 0) {
            return yearComparison;
        }

        // at this point, we know that the the years are equal

        int monthComparison = Integer.compare(this.month, other.month);
        if (monthComparison != 0) {
            return monthComparison;
        }

        // at this point, we know that the years are equal and the months are equal

        int dayOfMonthComparison = Integer.compare(this.dayOfMonth, other.dayOfMonth);
        return dayOfMonthComparison;
    }
}
