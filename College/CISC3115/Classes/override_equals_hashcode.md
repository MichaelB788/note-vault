Overriding equals method in Object class
________________________________________

Whenever you override the equals method (which is native to the Object class), you must also override the hashCode method. This is so objects such as HashMap are more efficient (They would be slow otherwise).

public boolean equals(Object obj){
    if (obj instanceof otherObj){
        otherObj other = (otherObj) obj;
        return this.field == other.field ...;
    } else {
        return false
    }
}

public int hashCode(){
    return Objects.hash(field1, field2, field3, ...);
}


Below is a more detailed example using the Name class.

******************************************************************************************
import java.util.Objects; // Must import this in order to use Objects hash method.

public class Name {
    private String first, last;

    public Name(String first, String last) {
        this.first = first;
        this.last = last;
    }

    @Override
    public String toString() {
        return first + " " + last;
    }

    @Override
/*
    Note that the paramater is of type Object. This is to override the original equals function. It seems obvious but it's easy to mistakenly OVERLOAD this function rather than to OVERRIDE it.
*/

    public boolean equals(Object obj) {
        if (obj instanceof Name){
            Name other = (Name) obj;
            return first.equals(other.first) && last.equals(other.last);
        } else return false; 
    }

    @Override
    public int hashCode() {
        return Objects.hash(first, last);
    }
}


In summary, import java.util.Objects and properly override equals and hashCode.

