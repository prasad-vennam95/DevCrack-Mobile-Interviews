# Cheetsheet

## First Kotlin program
```
fun main() {
    println("Hello world")
}
```
## Comments
``` 
// This is an end-of-line comment

/* This is a block comment
   on multiple lines. */

/* The comment starts here
/* contains a nested comment *⁠/
and ends here. */

KDoc

/**
 * Calculates the sum of two integers.
 *
 * @param a The first integer to add.
 * @param b The second integer to add.
 * @return The sum of the two integers.
 */
fun sum(a: Int, b: Int): Int {
    return a + b
} 
```

## Data types
```
val booleanVar: Boolean = true
val byteVar: Byte = 127
val shortVar: Short = 32767
val intVar: Int = 2147483647
val longVar: Long = 9223372036854775807L
val floatVar: Float = 3.14f
val doubleVar: Double = 3.14159265358979323846
val charVar: Char = 'A'
val stringVar: String = "Hello, world!"
```

## Mutability
```
var mutableString: String = "Adam"
val immutableString: String = "Adam"
val inferredString = "Adam"
```

## Numbers
```
val intNum = 10
val doubleNum = 10.0
val longNum = 10L
val floatNum = 10.0F
```

## Static Fields
```
class Person {
    companion object {
        val NAME_KEY = "name_key"
    }
}

val key = Person.NAME_KEY
```
## Strings
```
val name = "Adam"
val greeting = "Hello, " + name
val greetingTemplate = "Hello, $name"
val interpolated = "Hello, ${name.toUpperCase()}"
```
## Booleans
```
val trueBoolean = true
val falseBoolean = false
val andCondition = trueBoolean && falseBoolean
val orCondition = trueBoolean || falseBoolean
```
## Ranges
```
for(i in 0..3) {             
    print(i)
}

for(i in 0 until 3) {       
    print(i)
}

for(i in 2..8 step 2) {     
    print(i)
}

for (i in 3 downTo 0) {     
    print(i)
}

for (c in 'a'..'d') {   
    print(c)
}
```
## Null Safety

### Nullable properties
```
val cannotBeNull: String = null // Invalid
val canBeNull: String? = null // Valid

val cannotBeNull: Int = null // Invalid
val canBeNull: Int? = null // Valid
```
### Safe Operator
```
val nullableStringLength: Int? = nullableString?.length
val nullableDepartmentHead: String? = person?.department?.head?.name
```
### Checking for null
```
val name: String? = "Adam"

if (name != null && name.length > 0) {
    print("String length is ${name.length}")
} else {
    print("String is empty.")
}
```
### Elvis Operator
```
val nonNullStringLength: Int = nullableString?.length ?: 0
val nonNullDepartmentHead: String = person?.department?.head?.name ?: ""
val nonNullDepartmentHead: String = person?.department?.head?.name.orEmpty()
```
### Safe Casts
```
// Will not throw ClassCastException
val nullableCar: Car? = (input as? Car)
```
## Collections
### Creation
```
val numArray = arrayOf(1, 2, 3)
val numList = listOf(1, 2, 3)
val mutableNumList = mutableListOf(1, 2, 3)
```
### Accessing
```
val firstItem = numList[0]
val firstItem = numList.first()
val firstItem = numList.firstOrNull()
```
### Iterating
```
for (item in myList) {
    print(item)
}

myList.forEach {
    print(it)
}

myList.forEachIndexed { index, item -> 
    print("Item at $index is: $item")
}
```
### Maps
```
val faceCards = mutableMapOf("Jack" to 11, "Queen" to 12, "King" to 13)
val jackValue = faceCards["Jack"] // 11
faceCards["Ace"] = 1
```
### Mutability
```
val immutableList = listOf(1, 2, 3)
val mutableList = immutableList.toMutableList()

val immutableMap = mapOf("Jack" to 11, "Queen" to 12, "King" to 13)
val mutableMap = immutableMap.toMutableMap()
```
### Filtering & Searching
```
val evenNumbers = numList.filter { it % 2 == 0 }
val containsEven = numList.any { it % 2 == 0 }
val containsNoEvens = numList.none { it % 2 == 0 }
val containsNoEvens = numList.all { it % 2 == 1 }
val firstEvenNumber: Int = numList.first { it % 2 == 0 }
val firstEvenOrNull: Int? = numList.firstOrNull { it % 2 == 0 }
val fullMenu = objList.map { "${it.name} - $${it.detail}" }
```
## Functions
### Parameters & Return Types
```
fun printName() {
    print("Adam")
}

fun printName(person: Person) {
    print(person.name)
}

fun getGreeting(person: Person): String {
    return "Hello, ${person.name}"
}

fun getGreeting(person: Person): String = "Hello, ${person.name}"
fun getGreeting(person: Person) = "Hello, ${person.name}"
```
### Default Parameters
```
fun getGreeting(person: Person, intro: String = "Hello,"): String {
    return "$intro ${person.name}"
}

// Returns "Hello, Adam"
val hello = getGreeting(Person("Adam"))

// Returns "Welcome, Adam"
val welcome = getGreeting(Person("Adam"), "Welcome,")
```
### Named Parameters
```
class Person(val name: String = "", age: Int = 0)

// All valid
val person = Person()
val person = Person("Adam", 100)
val person = Person(name = "Adam", age = 100)
val person = Person(age = 100)
val person = Person(age = 100, name = "Adam")
```
### Higher Order Functions
```
fun calculate(x: Int, y: Int, operation: (Int, Int) -> Int): Int { 
    return operation(x, y)                                         
}

fun sum(x: Int, y: Int) = x + y                         
```        
### Lambda Expressions
```
val sum = { a: Int, b: Int -> a + b }

val square: (Int) -> Int = { it * it }
```
### Static Functions (Companion Object)
```
class Fragment(val args: Bundle) {
    companion object {
        fun newInstance(args: Bundle): Fragment {
            return Fragment(args)
        }
    }
}

val fragment = Fragment.newInstance(args)
```
### Extension Functions
```
fun Int.timesTwo(): Int {
    return this * 2
}

val four = 2.timesTwo()
```
### Variable number of arguments (varargs)
```
Varargs is a feature that allows you to pass a variable number of arguments of the same type to a function.
fun printNumbers(vararg numbers: Int) {
    for (number in numbers) {
        println(number)
    }
}

fun main() {
    printNumbers(1, 2, 3) // prints 1, 2, 3
    printNumbers(4, 5, 6, 7, 8) // prints 4, 5, 6, 7, 8
}
```
### Infix notation
```
Infix in Kotlin allows you to define functions that can be called using infix notation (i.e., without using parentheses and the dot notation).
infix fun Int.times(str: String) = str.repeat(this)

fun main() {
    val str = 5 times "Hello "
    println(str) // Output: "Hello Hello Hello Hello Hello "
}
```
## Scope Functions
### let
```
let takes the object as an argument and returns the result of the lambda expression.
If you don’t need to modify the original object and just want to perform some operations on it and get a new value, let is a good choice.
val message: String? = "Hello"
message?.let {
    print(it.toUpperCase()) // Output: "HELLO"
}
```
### run
```
run takes the object as the context and returns the result of the lambda expression.
On the other hand, if you need to modify the original object and get the modified object itself as the result, run is a better choice.
val message: String? = "Hello"
message?.run {
    print(this.toUpperCase()) // Output: "HELLO"
}
```
### with 
```
with is a non-extension function that can access members of its argument concisely: you can omit the instance name when referring to its members.
val person = Person("Ali", 24)
val message = with(person) {
    "My name is $name and I'm $age years old."
}
```
### apply
```
val person = Person("Ali", 24)
person.apply {
    name = "Ali"
    age = 24
}
```
### also
```
val message: String? = "Hello"
message?.also {
    print(it.toUpperCase()) // Output: "HELLO"
}
```
## Classes
### Primary Constructor
```
class Person(val name: String, val age: Int)
val adam = Person("Adam", 100)
```
### Secondary Constructors
```
class Person(val name: String) {
    private var age: Int? = null

    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
}

// Above can be replaced with default params
class Person(val name: String, val age: Int? = null)
```
### Inheritance & Implementation
```
open class Vehicle
class Car : Vehicle()

interface Runner {
    fun run()
}

class Machine : Runner {
    override fun run() {
        // ...
    }
}
```
## Control Flow
### If Statements
```
if (someBoolean) {
    doThing()
} else {
    doOtherThing()
}
```
### For Loops
```
for (i in 0..10) { } // 1 - 10
for (i in 0 until 10) // 1 - 9
(0..10).forEach { }
for (i in 0 until 10 step 2) // 0, 2, 4, 6, 8
```
### When Statements
```
when (direction) {
    NORTH -> {
        print("North")
    }
    SOUTH -> print("South")
    EAST, WEST -> print("East or West")
    "N/A" -> print("Unavailable")
    else -> print("Invalid Direction")
}
```
### While Loops
```
while (x > 0) {
    x--
}

do {
    x--
} while (x > 0)
```
## Destructuring Declarations
### Objects & Lists
```
val person = Person("Adam", 100)
val (name, age) = person

val pair = Pair(1, 2)
val (first, second) = pair

val coordinates = arrayOf(1, 2, 3)
val (x, y, z) = coordinates
```
### ComponentN Functions
```
class Person(val name: String, val age: Int) {
    operator fun component1(): String {
        return name
    }

    operator fun component2(): Int {
        return age
    }
}
```
### Visibility Modifiers in Kotlin

Kotlin provides four visibility modifiers for classes, objects, interfaces, constructors, functions, and properties:

| Modifier   | Description                                                                 | Scope                                  |
|------------|-----------------------------------------------------------------------------|----------------------------------------|
| `public`   | Visible everywhere (default if not specified).                              | Any code can access                    |
| `internal` | Visible within the same module.                                             | Same module                            |
| `protected`| Visible to the class and its subclasses.                                    | Subclasses only (not top-level)        |
| `private`  | Visible only within the file or class where it is declared.                 | Same file or class                     |

#### Example

```kotlin
class Example {
    private val privateValue = 1
    protected val protectedValue = 2
    internal val internalValue = 3
    public val publicValue = 4 // 'public' is the default
}
```

- `private`: Only accessible inside `Example`.
- `protected`: Accessible in `Example` and its subclasses.
- `internal`: Accessible anywhere in the same module.
- `public`: Accessible everywhere.

For top-level declarations (outside classes), `protected` is not allowed.

