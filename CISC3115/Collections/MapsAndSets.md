# Maps
> Most of the content here will be covered in Java, though the core ideas and concepts
can be translated to all languages.

**[Documentation of Maps](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html)**

Maps are interfaces within the JDK library and are most known for their **ability to
store key-value pairs**.

A key can be thought of as a sort **tag**, and this tag is mapped to a specified **value**.
This can be extremely useful whenever we want to use an array-like object, where each
element is essentially "bundled" by a particular trait.

## Useful Maps

### TreeMap
**[Documentation of TreeMaps](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)**

TreeMaps inherit from the AbstractMap interface and are useful whenever you want a
natural ordering of its keys. Below is what a TreeMap should look:

```Java
Map<K, V> treeMap = new TreeMap<>();
treeMap.put(key, value);
```

Here's a small program which reads from a file using a Scanner (sc) in order to print
the number of occurances a unique letter has appeared in said file (wherein
each found letter is organized in natural order):

```Java
// Initialize the TreeMap and Scanner

Scanner sc = new Scanner(new File("input.txt"));
Map<Character, Integer> map = new TreeMap<>();

// I'll search through each word and convert the current
// word to a character array.

while (sc.hasNext())
{
    String token = sc.next();
    for (char ch : token.toCharArray())
    {
        // Now I can analyze each individual letter and determine
        // whether this is the first time I have seen this letter
        // or if this letter is already on my map.
        if (Character.isLetter(ch) && !map.containsKey(ch)){
            map.put(ch, 1);
        }else if (map.containsKey(ch)){
            map.replace(ch, (map.get(ch) + 1));
        }
    }
}

// Initialize a character Set by using map.keySet() so I could 
// iterate over each key using Iterator. 

// Since TreeMap automatically sorts my keys, I only need to print out
// the assosciated value to each key in the format "key: value".

Set<Character> keys = map.keySet();
Iterator it = keys.iterator();

while (it.hasNext())
{kkk
    char curr = (char) it.next();
    System.out.println(curr + ": " + map.get(curr));
}
```

# Sets
**[Documentation of Sets](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)**
