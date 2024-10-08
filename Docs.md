# Syntax of NEV programming language 

let's start with default project settings which is in `program.yaml`
```yaml
Name: moon_app
Type: App
Backend: TCC
OS: windows
OptimizationPreference: Speed
OutJournal: RPF
ModulesHiring: ByFolder
GlobalOpen:
 - Pixel
 - Http
 - Pigeon
CompilerLibraries:
 - AutoFree
 - SpaghettiMaker
 - MathOptimizer
Parser:
 XMLDeclaration: true
 SyntaxChecks: FormalChecks
```
We'll know what is every property equal but every thing we'll know in it's time

at first i should say the Extension of nevlang is nev/nv.
<details>
<summary>Variables</summary>

## Variables and Data types
nev supports a big range of variables types let's learn it



### Read-Only variables
Nevlang is immutable by default so let's start with immutable variables
To declare an immutable variable you should use `:=` operator
And not '=' to make difference between change calue and declare a variable
For example:
```nev
fingers := 5  // There are 5 finger in every hand
legs := 2     // Every human has 2 legs
```



### Mutable variables
You should declare any variables immutable but only if necessary use `vmut` keyword to make it mutable
For example:
```nev
mut customers := 77   // There are mutable number of customers
mut contributors := 2   // There are mutable number of contributors
```


#### Nullable variables
Nev is null safety programming language to declare nullable mutable variable u should use `Option`
For example:
```nev
age := Option(45) // Declare n Option variabel to number
mut name := ?"ahmed" // Declare an Option variabel
```



### Datatypes
Nev support a range of types of variables.

So let's start with easy and simple types that the compiler will specify the type of variables to it if u didn't
| Type   | Length |
| ------ | ------ |
| `num`  | auto   |
| `str`  | auto   |
| `char` | 1-byte |
| `bool` | 1-bit  |

`num` type isn't performance choice and it makes calculations slow and `FormalChecks` mode will warn you if you used it so let's start with static-length numeric types
| Signed | Unsigned | Float  | Complex      | Length  |
| ------ | -------- | ------ | ------------ | ------- |
| `i8`   | `u8`     | ...... | ............ | 1-byte  |
| `i16`  | `u16`    | `f16`  | ............ | 2-byte  |
| `i32`  | `u32`    | `f32`  | `complex32`  | 4-byte  |
| `i64`  | `u64`    | `f64`  | `complex64`  | 8-byte  |


To specify the type of the variable you should write it after color that is after the variable's name.
For examples:
```nev
mut intger := i32(256)
mut float := f64(256)
```



### Array
Nev supports arrays.
An array is a data structure that stores a collection of elements. These elements can be of the same type and are accessed using an index. Arrays are commonly used to store lists of data and enable efficient access to individual elements.

#### Creating an Array
```nev
// Creating an array of numbers
numbers := [1, 2, 3, 4, 5]

// Creating an array of strings with type specified
fruits := [str](["apple", "banana", "cherry"])
```



<details>
<summary>String</summary>

### str and its functions

</details>

</details>


<details>
<summary>Functional Programming</summary>

## Functions and FP
Nev supports a range of FP features lets know it together!




### Functions
Functions in Nev is a block of code that performs a specific task. Functions are used to modularize and reuse code, as well as to improve the readability and structure of a program.
Declare functions is easy like datatypes declaration but the different u use `fun` keyword instead of `val`/`var` and after name or type of function you don't use equal sign and just write function value or `scope`


#### How to declare a scope
There is a 2 types of scope in nev the first one wich is curly-brackets scope and the second one is single-line scope using `=>` and if you using that scope in function that return a value you will write a value directly after `=>` without `return` keyword. 


#### How to declare a function
The syntax of declare a function is 
fun `keyword` + name of function + scope
and you can specify arguments and type of function using type color after function name than type than arguments between brackets like
`function_name + :: + function_type + ( + arguments + ) + scope`
For Example:
```nev
info :: nul() => cli.write("here is the info...": line) // that is a void function returns nul
double :: i32(x: i32) => x * 2
sum :: i32(x, y: i32) => x + y
main :: { // U can don't care about 'nul()' and compiler'll handle it 
    info()
    print_line(double(50): line)
    print_line(sum(double(50), 50): line)
}
```
output:
```
here is the info...
100
150
```
Note that `::` means equals like := for variables but for functions `function type + ( + arguments + )` is like variable type but for function and scope is the value.




### Anonymous functions & Closures
Anonymous functions: that is normal functions that can be declared in another functions.
Closures: This means that anonymous functions can inherit variables from the scope they were created in.
For example:
```nev
use cli {*}
main :: {
    mut arr := [1, 2, 3]
    add_number :: (x: i32, arr) => arr << x
    len := arr.len
    repeat 10 - len, i {
        add_number(i + len)
    }
    arr.for_each(write(it: Word))
}
```
output:
``` 1 2 3 4 5 6 7 8 9 10 ```




### Higher-order functions
In functional programming, a higher-order function is a function that can accept other functions as arguments, return functions, or both. They enable abstraction, composition, and the creation of more flexible and reusable code.


#### Function as an Argument
This approach involves passing a function (callback) as an argument to another function.The receiving function can then execute the callback, enabling flexible and customizable behavior.
For example:
```nev
print_output :: (fn: i32(i32), val: i32) {
    cli.write('The output is: ${fn(val)}'); 
} 
  
square :: i32(x: i32) => x * x

main :: => print_output(square, 5)
```
output:
```
25
```


#### Functions as Return Values
Higher-order functions can also return new functions. This is often used for creating specialized functions or closures. For instance, you can create a function factory that generates functions with specific behavior.
For example:
```nev
use cli {*}

multiplier :: (f: i32) =>
	(x: i32) => x * f

main :: {
    double :: multiplier(2)
    triple :: multiplier(3)

    write(double(5): Line)
    write(triple(5): Line)
}
```
output:
```
10
15
```
</details>

<details>
<summary>Enum & Param</summary>

## Enum
Enum is

</details>

Window :: Kind {} // struct - class
Action :: Enum {} // enum - union
Widget :: Role {} // interface - trait
WriteC :: Case {} // param - tag
