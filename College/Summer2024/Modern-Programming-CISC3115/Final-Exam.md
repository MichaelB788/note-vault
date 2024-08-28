# Final Exam Review

Link to [Spring 2024 Final](https://drive.google.com/file/d/1-YgEMEYB4v9nl7wul9Tm7bOg2lhqsaQf/view?pli=1)

#### **Question 1 (5 points)** 

1. Suppose we using the Linux command line, working in a newly-created directory. We
write a program consisting of a class named P in a file named P.java. The program,
which contains no errors, is designed to read some data from standard input (the
keyboard) and to print some data to standard output (the screen).
Write the command to compile (but not run) the program.

    `javac P.java`

2. Write what is printed on the screen if we now enter the ls command.

    `P.java P.class`

3.  Suppose we now create two additional files, named in.txt and out.txt, in the current
directory. Write the command to run the program, arranging matters so that the program’s
input comes from in.txt and the program’s output goes to out.txt.

    `java P << in.txt >> out.txt`

4.  Write the command to make a copy of in.txt, naming the copy copy.txt.

    `cp in.txt copy.txt`

5.  Write the command to move copy.txt to the parent of the current directory.

    `mv copy.txt ..`

<br>

#### **Question 2 (6 points)**

Suppose we have the following Point class.

```Java
public class Point {
    private int x , y ;
    public Point (int x , int y ) {
        this.x = x;
        this.y = y;
    }
    public Point ( Point original ) {
        this.x = original.x;
        this.y = original.y;
    }
    public void setX ( int x ) { this.x = x; }
    public void setY ( int y ) { this.y = y; }
    @Override
        public String toString () { return "(" + x + ", " + y + ")"; }
}
```

Write the output of each of the following programs.

Output for a:

```
true
false
true
true
```

Output for b:

```
in m1: (3, 4)
after m1: (1, 2)
in m2: (5, 2)
after m2: (5, 2)
```

Output for c:
```
(3, 2)
(3, 4)
```

<br>

#### Question 3

Complete all parts of the Circle class.

```Java

public class Circle
{
    private Point center;
    private int radius;

    public Circle(Point center, int radius)
    {
        this.center = new Point(center);
        this.radius = radius;
    }

    public Circle(Circle original)
    {
        center = original.getCenter();
        radius = original.getRadius();
    }

    public Point getCenter()
    {
        return new Point(center);
    }

    public int getRadius()
    {
        return radius;
    }

    public void setCenterX(int x)
    {
        center.setX(x);
    }
}

```

<br>

#### Question 4

```Java
import java.util.Objects;
import java.lang.Comparable;

public class TimeSpan implements Comparable<TimeSpan>
{
    private int totalMinutes;

    public TimeSpan(int hours, int minutes)
    {
        totalMinutes = minutes + (hours * 60);
    }

    public TimeSpan(int totalMinutes)
    {
        this.totalMinutes = totalMinutes;
    }

    public int getHours()
    {
        return totalMinutes / 60;
    }

    public int getMinutes()
    {
        return totalMinutes % 60;
    }

    public int getTotalMinutes()
    {
        return totalMinutes;
    }

    @Override
    public String toString()
    {
        return String.format("%dh%dm", getHours(), getMinutes());
    }

    @Override
    public boolean equals(Object o)
    {
        if (o instanceof TimeSpan)
        {
            TimeSpan other = (TimeSpan) o;
            return totalMinutes == other.getTotalMinutes();
        }
        else return false;
    }

    @Override
    public int hashCode()
    {
        return Objects.hash(totalMinutes);
    }

    public TimeSpan plus(TimeSpan other)
    {
        return totalMinutes + other.getTotalMinutes;
    }

    @Override
    public int compareTo(TimeSpan other)
    {
        return totalMinutes - other.getTotalMinutes();
    }
}

```

<br>

#### Question 5

Suppose we ahve the following BankAccount class.

```Java
public class BankAccount {
    private final String accountNumber ;
    private int balance ;
    public BankAccount ( String accountNumber , int balance ) {
        this . accountNumber = accountNumber ;
        this . balance = balance ;
    }
    public boolean deposit ( int amount ) {
        if ( amount < 0) {
            return false ;
        } else {
            balance += amount ;
            return true ;
        }
    }
    public boolean withdraw ( int amount ) {
        if ( amount < 0 || amount > balance ) {
            return false ;
        } else {
            balance -= amount ;
            return true ;
        }
    }
    @Override
        public String toString () {
            return accountNumber + " $" + balance ;
        }
}
```

Write a subclass of BankAccount named WithdrawalLimitedAccount. An object of this
class should work like a BankAccount object, except that it allows only a limited
number of withdrawals to be made.

```Java
public class WithdrawalLimitedAccount implements BankAccount
{
    private int limit;
    private int withdrawal;
    
    public WithdrawalLimiitedAccount(String accountNumber, int balance, int limit)
    {
        super(accountNumber, balance);
        this.limit = limit;
    }

    @Override
    public boolean withdraw(int amount)
    {
        if (withdrawal != limit)
            return super(amount);
        else return false;
    }

    @Override
    public String toString()
    {
        return String.format("%s, %d withdrawals left", super.toString(),
            limit - withdrawal);
    }
}
```
