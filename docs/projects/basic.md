---
sidebar_label: "Basic concepts"
sidebar_position: 1
tags: [C#]
---

# Basic

## `Vocabulary new`

```bash
- {} - Curl brackets
- [] - Squared brackets
- <> - Angular brackets
- ">" - Greather Than
- ? - Ternary Operator like var result = a > b ? true: false;
- ?? - Null Coalescsing Operator
- PEMDAS - Parentesis, Exponence, Multiplication , Division, Addition, Substraction
- Expresions % + - / \*
- \ - back slash mac option+?
- computational expencive on convertions boxing and unboxings
```

## Encapsulation Basic

```csharp
var s = 1;

class Class1{
  public string firstName;
  public string lastName;

  public Class1(string name, string last){
    firtsName = name;
    lastName = last;
  }

  string displayFullName(){
    return firstName +" "+ lastName;
  }
}
struct Struct1 {

  public string firstName;
  public string lastName;

  public Struct1(string name, string last){
    firstName = name;
    lastName = last;

  }

  public string displayFullName(){
    return firstName + " "+ lastName;
  }

}
var struct = new Struct1("Luis", "Alvarado");
Console.WriteLine(struct.displayFullName());

var class1 = new Class1("John", "Smith");

Console.WriteLine(class1.displayFullName());
// struct is allocated on a stack memory
  // inherence between class and struct
// class is allocated on a heap memory

```

## `typeof on C# using is`

```csharp
//is
bool typeInput = "string text " is string; // True
bool typeInput2 = "string text " is int; // False

class A{}  // Should be out of the Class
class B : A{} // Should be out of the Class

bool typeClass = new B() is A;
Console.WriteLine(typeClass);

```

## `Cast with 'as' operator`

```csharp
var stringText = "text demo";

object objectTest = new Object(); // Logic Error, because this cast with be empty
object objectTest = stringText;

string castObjectToString = objectTest as string;
```

## `Cast int and string, Cast int and float using`

```csharp

object objectTest = 32
string castObjectToString = objectTest.ToString();

int number = 12;
string castNumberToString = number.ToString();
string castNumberToString = (string)number; // Logic Error


string stringNumber = "12";
int number = (int) stringNumber; // Logic Error
int number = int.Parse(stringNumber);
Console.WriteLine($"{number}");


string stringNumber = "12s";
try
{
    int number = int.Parse(stringNumber);
    Console.WriteLine($"{number}");
}
catch (Exception e)
{
    Console.WriteLine($"{e.Message}");

}

// float.Parse
// double.Parse
// decimal.Parse

//Cast int and float using
int intN = 1;
float floatN = 5.9f;
float floatEx = (float)intN;
int intEx = (int)floatN;
Console.WriteLine($"{intEx},{floatEx}");

```

## ` Math`

```csharp

Math.Abs(-1); // 1
Math.Abs(-1.2f) // 1.2

Math.Round(3.2f) // 3
Math.Round(3.6f) // 4

Math.Celling(3.2f) // 4
Math.Floor(3.2) // 3
Math.Truncate(3.9) // 3
Math.Min(1,3); // 1
Math.Max(1,3); // 3

```

## `Null Coalescing Operator ??`

```csharp
var stringText = "123";
var whatValueIsNotNull = stringText ?? "1";

string stringText = null;
var whatValueIsNotNull = stringText ?? "1";
Console.WriteLine($"{whatValueIsNotNull}");
```

## `Strings`

```csharp
/*
Lenght
IndexOf
ToUpper
ToLowCase
Substring
Insert (position, "character")
Remove(position)
Trim('a')
Replace("_", "*")
Sprit(' ')

*/
// Contain
string a = "012345";
string b = "23";
a.Contains(b);

// Equal
a == b
string.Equals(a,b);

// Substring

a.Subtring(0)// = 0;
a.Substring(0,3) //012

// $ ans @

Console.WriteLine($"{a}");
string @if = "@text";
//or
string textEx = @"1\n2"; // 1\n2
string textEx = "1\n2"; // 1 espace 2


// Scape secuense
/*
\n - space
\a - sound
\r - indend word ******* I like for logs
\t - tab space
\" - "
*/


// Formats
// C $ current
// P %
string.Format("{0:C}",12); // $12.00
string.Format("{0:P}",12); // 12.00 %

// String Builder Class
  // String are immutable
  StringBuilder stringEx = new StringBuilder();

  stringEx.Replace(" ","_");
  stringEx.Remove(1,2);
// NullString definition a validation
string s = null
string ss = string.Empty;

string.AsNullOrEmpty(s) // True
string.AsNullOrEmpty(ss) // True

```

## `Boxing and Unboxing on Obj convertion `

In C#, the concepts of boxing and unboxing are important to understand, especially when it comes to performance considerations. These operations can be computationally expensive, and it's crucial to know how and when they occur to write efficient code.

### What is Boxing?

**Boxing** is the process of converting a value type (such as `int`, `float`, etc.) to a reference type (usually `object`). When a value type is boxed, it is wrapped inside an `object` and stored on the heap instead of the stack.

#### Example of Boxing:

```csharp
int intValue = 42;       // Value type
object boxedValue = intValue; // Boxing
```

### What is Unboxing?

**Unboxing** is the reverse process of boxing. It involves converting a boxed value back to a value type. During unboxing, the runtime checks the object to ensure it contains a value of the correct type.

#### Example of Unboxing:

```csharp
object boxedValue = 42; // Boxing
int intValue = (int)boxedValue; // Unboxing
```

### Computational Expense of Boxing and Unboxing

Boxing and unboxing operations are computationally expensive for several reasons:

1. **Heap Allocation**: Boxing involves allocating memory on the heap for the boxed value. Heap allocations are generally more expensive than stack allocations due to the overhead of managing the heap.
2. **Garbage Collection**: Boxed objects are subject to garbage collection, adding additional overhead. Frequent boxing can lead to more frequent garbage collections, which can degrade performance.
3. **Type Checking**: Unboxing requires type checking to ensure the object contains the correct type before converting it back to a value type. This type checking adds runtime overhead.
4. **Copying Data**: Boxing involves copying the value type data into the newly allocated heap space, and unboxing involves copying the data back from the heap to the stack.

### Example of Computational Cost

```csharp
public void BoxingUnboxingExample()
{
    int intValue = 42;

    // Boxing: intValue is copied to the heap
    object boxedValue = intValue;

    // Unboxing: boxedValue is type-checked and copied back to int
    int unboxedValue = (int)boxedValue;
}
```

### Performance Impact

Let's consider a scenario where boxing and unboxing occur inside a loop:

```csharp
public void PerformanceImpactExample()
{
    int sum = 0;
    for (int i = 0; i < 1000000; i++)
    {
        object boxedValue = i; // Boxing
        sum += (int)boxedValue; // Unboxing
    }
}
```

In this example, there are 1,000,000 boxing and unboxing operations, which can significantly impact performance due to the reasons mentioned above.

### Avoiding Boxing and Unboxing

To avoid the performance hit from boxing and unboxing, consider the following strategies:

1. **Use Generic Collections**: Use generic collections like `List<T>`, `Dictionary<TKey, TValue>`, etc., which work with value types without boxing.

   ```csharp
   List<int> intList = new List<int>();
   intList.Add(42); // No boxing
   int value = intList[0]; // No unboxing
   ```

2. **Avoid `object` for Value Types**: Avoid using `object` to store value types. Use specific types or generics to maintain type safety and avoid boxing.

   ```csharp
   void ProcessValue(int value) { /* ... */ }
   ```

3. **Minimize Usage of Non-Generic Interfaces**: Non-generic interfaces like `IComparable` and `IEnumerable` can cause boxing. Use generic versions like `IComparable<T>` and `IEnumerable<T>` to avoid boxing.

### Summary

- **Boxing** converts a value type to a reference type, incurring the cost of heap allocation and garbage collection.
- **Unboxing** converts a boxed reference type back to a value type, incurring the cost of type checking and data copying.
- Frequent boxing and unboxing can significantly impact performance.
- Use generic collections and avoid storing value types in `object` variables to minimize the need for boxing and unboxing.

## Dynamic Types & References

```csharp
/*
var
dynamic
// value type , int float, bool char, enum long ...
int num = 500 ;
int i = 200;

// Reference type, pointer

//string, classes,array , delegates ...
*/

 public class Class1
    {
        public string name = null;

    }

    static void ChangeName(Class1 objClass)
    {
        objClass.name = "New change reference ";
    }


    public static void Main(string[] args)
    {

        // Main()
        var classEx = new Class1();
        classEx.name = "Luis";
        ChangeName(classEx);
        Console.WriteLine(classEx.name);

    }

```

## DateTime & TimeSpan

```csharp
DateTime.Now
DateTime date = new DateTime(year, moth, day);

TimeSpan time = new TimeSpan(DateTime.Now.Hour, DateTime.Now.Minute, 0);
Console.WriteLine(time);

// Format date

Console.WriteLine(DateTime.Now.ToString("dd"));
Console.WriteLine(DateTime.Now.ToString("ddd"));
Console.WriteLine(DateTime.Now.ToString("dddd"));

Console.WriteLine(DateTime.Now.ToString("MM"));
Console.WriteLine(DateTime.Now.ToString("MMM"));
Console.WriteLine(DateTime.Now.ToString("MMMM"));
Console.WriteLine(DateTime.Now.ToString("yy"));
Console.WriteLine(DateTime.Now.ToString("yyy"));
Console.WriteLine(DateTime.Now.ToString("yyyy"));
Console.WriteLine("\r");
Console.WriteLine(DateTime.Now.ToString("D"));
Console.WriteLine(DateTime.Now.ToString("d"));
Console.WriteLine("\r");

Console.WriteLine(DateTime.Now.ToString("yyyy mm dd"));
Console.WriteLine(DateTime.Now.ToString("MM/dd/yyyy hh:mm:ss tt"));

// Timezone
Console.WriteLine(DateTime.Now.ToString("yyyy-MM-dd HH:mm:ss.fff tt"));
Console.WriteLine(DateTime.UtcNow.ToString("yyyy-MM-dd HH:mm:ss.fff tt"));
Console.WriteLine(DateTime.Now.ToUniversalTime().ToString("yyyy-MM-dd HH:mm:ss.fff tt"));
Console.WriteLine(DateTime.UtcNow.ToLocalTime().ToString("yyyy-MM-dd HH:mm:ss.fff tt"));
```

## Control flow statement and loops

```csharp

// if else
if(){

}else{

}
if(){}else if(){}

// switch many values, break is needed always
var day = 2;
switch(day){
  case 1:
  break;
  default:
  break;
}

// for loops
for(var i = 0; i <10 ; i++){ // 0 - 9
  Console.WriteLine(i);
}
for(var i = 10; i >0 ; i--){ // 10 - 1 if (i>=0)-> 10 - 0
  Console.WriteLine(i);
}

// will print 0
int i = 0;
for(;;){
  Console.WriteLine(i);
  i++;
  break;
}

// not appropate to update the collection
// one direction ->
foreach(char c in "Luis"){
  Console.WriteLine(c);
}

// while
int i = 0;
while (i<10){
Console.WriteLine(i);
i++;
}

int x = 3;
while(x > 0 ){
    Console.WriteLine(x);
    x--;
}

// At leastr once
// do while
int i = 0;
do{
  Console.WriteLine(i);
    i++;
}
while (i<10)


```

## User Inpt

```csharp
// Inut
var input = Console.ReadLine();
var input = Console.Read(); // loop
var input = Console.ReadKey(); // nombre de la tecla ConsoleKey.Escape

```

## Tic Tac Toc Best approach

```csharp
using System;

class Program
{
   static char[] board = new char[]{ '1', '2', '3', '4', '5', '6', '7', '8', '9' };
   static char player = 'X';

   static void Main(string[] args)
   {
       int move;
       int turnCount = 0;
       bool isGameOver = false;

       while (!isGameOver && turnCount < 9)
       {
           DisplayBoard();
           Console.WriteLine($"Player {player}, enter your move (1-9): ");
           move = int.Parse(Console.ReadLine());

           if (IsValidMove(move))
           {
               MakeMove(move);
               turnCount++;

               if (CheckWin())
               {
                   DisplayBoard();
                   Console.WriteLine($"Player {player} wins!");
                   isGameOver = true;
               }
               else
               {
                   player = (player == 'X') ? 'O' : 'X'; // Switch player
               }
           }
           else
           {
               Console.WriteLine("Invalid move, try again.");
           }
       }

       if (!isGameOver)
       {
           DisplayBoard();
           Console.WriteLine("It's a draw!");
       }
   }

   static void DisplayBoard()
   {
       Console.Clear();
       Console.WriteLine(" {0} | {1} | {2} ", board[0], board[1], board[2]);
       Console.WriteLine("---+---+---");
       Console.WriteLine(" {0} | {1} | {2} ", board[3], board[4], board[5]);
       Console.WriteLine("---+---+---");
       Console.WriteLine(" {0} | {1} | {2} ", board[6], board[7], board[8]);
   }

   static bool IsValidMove(int move)
   {
       return move >= 1 && move <= 9 && board[move - 1] == move.ToString()[0];
   }

   static void MakeMove(int move)
   {
       board[move - 1] = player;
   }

   static bool CheckWin()
   {
       // Check rows, columns, and diagonals
       return (board[0] == player && board[1] == player && board[2] == player) ||
              (board[3] == player && board[4] == player && board[5] == player) ||
              (board[6] == player && board[7] == player && board[8] == player) ||
              (board[0] == player && board[3] == player && board[6] == player) ||
              (board[1] == player && board[4] == player && board[7] == player) ||
              (board[2] == player && board[5] == player && board[8] == player) ||
              (board[0] == player && board[4] == player && board[8] == player) ||
              (board[2] == player && board[4] == player && board[6] == player);
   }

}

```

## Building Tic Tac Toc With errors

```csharp
class Program
{
    static char[] board = new char[]{ '1', '2', '3', '4', '5', '6', '7', '8', '9' };
    public static void Main(string[] args)
    {


        char userTurn = 'X';
        int turn = 0;
        int move;
        while (turn != -1) // error becaus so
        {
            PrintBoard();
            Console.WriteLine($"{userTurn} Choose?");
            var userChose = Console.ReadLine(); // 1
            move = int.Parse(Console.ReadLine());
            Replace(move, userTurn);
            userTurn = turn % 2 == 0 ? 'X' : 'O';
            turn++;

        }



    }

    static int Win(){

      /*
      000 012
      000 345
      000 678
      */

       /*
      000 036
      000 147
      000 258
      */

       /*
      000 048
      000 246
      */
      if(
      board[0] == player && board[1] == player && board[2] == player ||
      board[3] == player && board[4] == player && board[5] == player ||
      board[6] == player && board[7] == player && board[8] == player ||
      board[0] == player && board[3] == player && board[6] == player ||
      board[0] == player && board[3] == player && board[6] == player ||
      board[1] == player && board[4] == player && board[7] == player ||
      board[0] == player && board[4] == player && board[8] == player ||
      board[2] == player && board[4] == player && board[6] == player ||
      ){

      }
    }



    static void PrintBoard()
    {
      Console.Clear();
       Console.WriteLine(" {0} | {1} | {2} ", board[0], board[1], board[2]);
       Console.WriteLine("---+---+---");
       Console.WriteLine(" {0} | {1} | {2} ", board[3], board[4], board[5]);
       Console.WriteLine("---+---+---");
       Console.WriteLine(" {0} | {1} | {2} ", board[6], board[7], board[8]);
   }
    }

    static void Replace(int userChose, char option)
    {
        Console.WriteLine(userChose.ToString(),option);
        board[8] = 'x';
    }

}
```

## Contrutor and Finalazer

```csharp
// Constructos N with overwriting , params o
class A{
  public A(){

  }
  public A(string a, string b){}

}

// Finalizers
class B{
  ~B(){} // Only call for Garbash collencion
}


```

## Read Only set {} get{}

```csharp
// take a look the Main
class A{
  private string conectionString ;
  public string ConectionString{ // this should not have () because make reference to a propeties
    // set{
    //  conectionString = value;
    // }
    get{

      return conectionString;
    }

  }

  public static void Main(string[] arg){
    A a = new A();
    a.ConectionString;
    //a.ConectionString = "";
  }
}

```

## Attributes Meta Data [Selializer]

Modulariadad gerarquica en C#
// assembly, module, field event, method, param.

```csharp
//[Serializable] Class;

// Obsolete
class A{
  [Obsolte("Take a look the ne vertion")]
  public void OldMethid(){}
  [Conditional("ABC")]
  public void NewMethod(){}
}

[AttributeUsage(AttributeTargets.All)]
class BExAtributte :Attributes{}
```

## `Anonimus and Lambda, Func<TResult> delegate`

```csharp
// Expresion Lambda
Action x = ()=> Console.WriteLine("");
// Statement Lamdba
Action x = ()=>{Console.WriteLine("");};
x();

// Expresion Lambda with paramethers
Action<string> x = (s)=> Console.WriteLine($"{s}");
x("hi");

//Func<TResut> delegate  functions as parameters
Func<int, int, int> sum = (a, b) => a + b;
sum(1, 2); // return 3

Func<int, int, string> sumString = (a, b) => (a + b).ToString();
Type s = sumString(1, 4).GetType(); // return "5"
Console.WriteLine($"{sum(1, 2)}, {s}");
```

## Overriting, Overloading, Infinite Params, Optional Parameters

```csharp
// Overloading, rules: same return type, add more parameters, same name
// Enfoque: reutilizar el mismo nombre de la funcion para hacer mas cosas con las misma
int sum(int a){return a;}
int sum(int a, int b){ return a+b;}//...

// Overloading, child class from Parent, change de definition of the method

class ParentClass{
  int sum(int a, int b){
    return a+b;
  }
}

class ChildX : ParentClass{
  int sum(){
    return 5;
  }
}

// Infinite 6000 parametes allow
//params; is the keyworkd on c#
public void Ex(params string[] words){
foreach(string x in words){
  Console.WriteLine(x);
}
}

// Optional parameters

public int multiply(int s = 0, int a, int b ){
return a+b;
}

```

## IEnumerable to iterate an Obbject Class array

```csharp

using System;
using System.Collections;

class Character : IEnumerable
{
    Powers[] powersList = new Powers[5];
    int indexPowerList = 0;
    public void AddPower(Powers name)
    {
        powersList[indexPowerList] = name;
        indexPowerList++;
    }
    // Take a look here
    public IEnumerator GetEnumerator()
    {
        foreach (Powers p in powersList)
        {
            if (powersList == null)
            {
                break;
            }
            yield return p;
        }
    }

}
class Powers
{
    public string name;
}
class Program
{
    static void Main(string[] args)
    {
        Character one = new Character();
        one.AddPower(new Powers { name = "fly" });
        one.AddPower(new Powers { name = "fly2" });
        foreach (Powers p in one) // Not allowe if one Character has implemet the IEnumerable
        {
            Console.WriteLine(p.name);
        }
    }
}
```

## Interfaces, Abstract Class, Virtual method

### Interfaces

- Are used to definir methods que seran utilizados en sus implementacions
- Syntacincia mas clara
- C# las clases no puden heredar mas de una, es una solucion para definir los methodos
- all should be public

### Abtract

- Solo se pude heredar de una clase
- se debe usar overwrite para sobrescribir y todos los
- se debe usar abrovechar las propiedades, de la clase
- puedo tener una methodos private, protected-
- puede tener definiciones y declaraciones de los method sin usar 'base'
- contructors
- access modifides

### Virtual method

- can be or not overwrited
- debe usar base para acceder al method del padre

```csharp
using System;
using System.Collections;

class BaseAnimal
{

    virtual public string GetName()
    {
        return "BaseAnimal";
    }
}
interface IAnimal
{
    string getName();
}
abstract class Animal
{
    public int maxLife;
    public string name;
    abstract public void animalSound();
    abstract public string animalName();
    public string food(){
      return "all";
    }
}

class Dog : Animal, IAnimal

{
    public override string animalName()
    {
        return "Dog";
    }

    public override void animalSound()
    {
    }

    public string getName()
    {

        sleep();
        return "Dog"+maxLife;
    }
}

class Cat : BaseAnimal
{
    public override string GetName()
    {
        return base.GetName();
        //return "Cat";
    }
}

class Program
{
    static void Main(string[] args)
    {
        BaseAnimal animal = new Cat();
        Console.WriteLine(animal.GetName());// Cat

         Dog d = new Dog();
        Console.WriteLine(d.getName()); // Dog 10
    }
}
```

## Data Structures

### Arrays

```csharp
string[] n = new string[2];
string[] n2 = { "2", "3" };
string[] n3 = new string[] { "22","1", "2" };

Array.Sort(n3);
n3.Length
foreach (string i in n3)
{
    Console.WriteLine(i);
};
```

### List

```csharp
List<int> list = new List<int>();
list.Add(1);
list.Add(2);
list.Contains(1); // True or False
list.AddRange(new List<int>(){10,21});
list.Sort();
 var s = list.Count;
foreach (int i in list){
    Console.WriteLine(i);
};

list.Insert(0,9);
list.InsertRage(1,new List<int>(){12,12,3});
/*
9
12
12
3
1
2
10
21
*/
list.Remove(3);
list.RemoveAt(0);
list.RemoveRange(2,1);
list.Capacity = 2;
list.TrimExcess();// actualiza la lista con la capacidad
  List<int> list = new List<int>(){1,2,3};
  Console.WriteLine(list.Count);
  list.AddRange(new int[]{4,5,6});
  Console.WriteLine(list.Count);
  list.Capacity = 15;
  list.TrimExcess();
  Console.WriteLine(list.Capacity);
// Check values
list.TruForAll((a)=>a<100);
//Reverse
list.Reverse();
// Foreach
List<int> list = new List<int>() { 100, 2, 3 };
  void Print(int a)
  {
    Console.WriteLine(a);
  }
  list.ForEach(Print);

// IndexOf
List<int> list = new List<int>() { 100, 2, 3, 2,  3 };
Console.WriteLine(list.IndexOf(2));
Console.WriteLine(list.LastIndexOf(3));

```

### Stack or Last in Firt Out

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine(isBalanced("[{[]}]"));
        Console.WriteLine(isBalanced("[{[{]}]"));
    }
    static public bool isBalance(string word)
    {
        string part1 = "";
        string part2 = "";
        string part3 = "";
        for (int i = 0; i < word.Length; i++)
        {
            if (i < word.Length / 2)
            {
                part1 = part1 + word[i];

            }
            else
            {
                part2 = part2 + word[i];

            }
        }
        if (part1.Length != part2.Length)
        {
            return false;
        }
        for (int i = 0; i < part2.Length; i++)
        {
            Console.WriteLine(part2[i]);
            switch (part2[i])
            {
                case ')':
                    part3 = part3 + '(';
                    break;
                case '}':
                    part3 = part3 + '{';
                    break;
                case ']':
                    part3 = part3 + '[';
                    break;
                case '<':
                    part3 = part3 + '>';
                    break;
                default:
                    part3 = part3 + '?';
                    break;
            }

        }
        Console.WriteLine($"1:{part1} 2{part3}");
        return part1 == part3;
    }
    static public bool isBalanced(string word)
    {
        Stack<char> stackP1 = new Stack<char>();
        Stack<char> stackP2 = new Stack<char>();

        foreach(var w in word)
        {
            if (w == '{' || w == '[' || w == '<' || w == '(')
            {
                stackP1.Push(w);
            }
            if (w == '}' || w == ']' || w == '>' || w == ')')
            {
                stackP2.Push(w);
            }
        }

        if (stackP1.Count != word.Length / 2)
        {
            return false;
        }
        foreach(var a in stackP1){
            Console.WriteLine($"{a}");
        }
        foreach(var a in stackP2){
            Console.WriteLine($"{a}");
        }
        while (stackP2.Count != 0)
        {
            char s = stackP1.Pop();
            char s2 = stackP2.Pop();
            if (
                (s == '{' && s2 == '}') ||
                (s == '[' && s2 == ']') ||
                (s == '<' && s2 == '>') ||
                (s == '(' && s2 == ')'))
            {
                continue;
            }
            else
            {
                return false;
            }
        }

        return true;
    }
}
```

### Ques First In First Out

```csharp
Queue<string> x = new Queue<string>();
x.Enqueue("A");
x.Enqueue("b");
x.Enqueue("c");
x.Dequeue();
// return b
Console.WriteLine(x.Peek());

```

### Struct

This is very similar to a class

- no constructor
- not contain finalazers
- can implement interfaces

```csharp
interface IExample{
  string getName();
}
struct A:IExample{
  string name;
  int es;
}
```

### Enum

```csharp
enum Days { Monday, Tuesday, Wednesday, Thurday, Friday, Saturday, Sunday };
static void Main(string[] args)
{
  Console.WriteLine(Days.Monday);
  // Iterate
  var iterator = Enum.GetNames(typeof(Days));// Monday ....
  var iterator = Enum.GetValues(typeof(Days)); // 1, ....
  foreach (var s in iterator)
  {
      Console.WriteLine(s);
  }
}
```

### Dictionaries

- Not order methods

```csharp
Dictionary<string, string> dictionary = new Dictionary<string, string>();
Dictionary<int, string> dictionaryIndexNum = new Dictionary<int, string>();

dictionaryIndexNumber.Add(1,"uno");

dictionary.Add("1","uno");
dictionary.Add("1","uno");
dictionary.Add("1","uno");
// use this validation always
if(!dictionary.ContainKey('4')){
  dictionary.Add("1","uno");
}

if(!dictionary.ContainKey('4')){
  dictionary["1"];
}

foreach(var i in dictionary.Values){
  Console.WriteLine(i)
}

foreach(var i in dictionary.Keys){
  Console.WriteLine(i);
}

dictionary.Remove("1");
dictionary.Clean();

```

## Prepocesor directives

Sure! Here is a list of C# preprocessor directives along with small examples for each:

1. **`#define` and `#undef`**

   - Used to define and undefine conditional compilation symbols.

   ```csharp
   #define DEBUG
   // #undef DEBUG

   using System;

   class Program
   {
       static void Main()
       {
           #if DEBUG
           Console.WriteLine("Debug mode is on.");
           #endif

           Console.WriteLine("Program running.");
       }
   }
   ```

2. **`#if`, `#elif`, `#else`, and `#endif`**

   - Used to conditionally include or exclude parts of the code.

   ```csharp
   #define DEBUG

   using System;

   class Program
   {
       static void Main()
       {
           #if DEBUG
           Console.WriteLine("Debug mode is on.");
           #elif RELEASE
           Console.WriteLine("Release mode is on.");
           #else
           Console.WriteLine("Unknown mode.");
           #endif
       }
   }
   ```

3. **`#region` and `#endregion`**

   - Used to mark a block of code that can be collapsed or expanded in the editor.

   ```csharp
   using System;

   class Program
   {
       static void Main()
       {
           Console.WriteLine("Program running.");

           #region Helper Methods

           DisplayMessage();

           #endregion
       }

       static void DisplayMessage()
       {
           Console.WriteLine("Hello from the helper method!");
       }
   }
   ```

4. **`#error` and `#warning`**

   - Used to generate a compile-time error or warning.

   ```csharp
   #define DEBUG

   #if DEBUG
   #error "Debug mode is enabled. Disable it before production build."
   #endif

   using System;

   class Program
   {
       static void Main()
       {
           Console.WriteLine("Program running.");
       }
   }
   ```

5. **`#line`**

   - Used to change the line number and (optionally) the file name for error and warning messages.

   ```csharp
   using System;

   class Program
   {
       static void Main()
       {
           #line 100 "CustomFileName.cs"
           Console.WriteLine("This line is reported as line 100 in CustomFileName.cs");
       }
   }
   ```

6. **`#pragma`**

   - Used to specify compiler directives.

   ```csharp
   using System;

   class Program
   {
       #pragma warning disable 414 // Disable a specific warning

       private static int unusedVariable;

       static void Main()
       {
           Console.WriteLine("Program running.");
           #pragma warning restore 414 // Restore the specific warning
       }
   }
   ```

7. **`#nullable`**

   - Used to enable or disable nullable annotations and warnings.

   ```csharp
   #nullable enable

   using System;

   class Program
   {
       static void Main()
       {
           string? nullableString = null; // No warning due to nullable enable
           string nonNullableString = "Hello"; // No warning
           Console.WriteLine(nonNullableString);
       }
   }
   ```

These preprocessor directives provide powerful ways to manage code compilation and organization, especially for complex or configurable applications.

## Delegate

```csharp
delegate void PrintMeggage();
//PrintMeggage message = printA;
//PrintMeggage message = printB; // referenfe to the method

PrintMeggage message = null;
message += printA;
message += printB;
message();

message();
static void printA(){
  //Do somethong
  Console.WriteLine("Sol");
}
static void printB(){
  //Do somethong
  Console.WriteLine("Soles");
}
```

## Events

### Example

```csharp
  private static event EventHandler evt;
    static void Main(string[] args)
    {
        evt += (sender, evtArg) =>
        {
            // do something
            Console.WriteLine("A");
        };
        evt += (sender, evtArg) =>
        {
            // do something
            Console.WriteLine("B");
        };
        evt.Invoke(null, new EventArgs());

    }
// If is not used lamda expresions
  // ~ClasName(){
  // evt-=Handle
  // }
```

## Action

```csharp
private static Action action;
static void Handle(int a , int b){
  Console.WriteLine($"{a+b}"); // 5

}

action += Handle;
action.Invoke(2,3); // 5
```

## Recursion

- call same funtion until confotion
- bigger that a loop allocatin memory

### Example Fibonacci

- 0,1,2,3,5,8,13,21...

```csharp

using System;
using System.Collections.Generic;

class Program
{

    // 0,  1 ,1
    static public int fib(int number)
    {
        if (number == 0 || number == 1)
        {
            return number;
        }
        return fib(number - 1) + fib(number - 2);


    }

    static public int fib2(int targetNumber)
    {
        int p1 = 0;
        int p2 = 1;
        int counter = 0;
        int result = 0;
        Console.Write(p1);
        Console.Write(p2);
        while (counter < targetNumber - 1)
        {
            result = p1 + p2;
            p1 = p2;
            p2 = result;
            if (counter > 0)
            {
                Console.Write(p1);
            }
            counter++;
        }

        return result;
    }
    static void Main(string[] args)
    {
        Console.WriteLine("\t" + fib2(11));
    }
}

```

### Tower of Hanoi Undertanding

```csharp

Stack<int> t1 = new Stack<int>(){3,2,1};
Stack<int> t2 = new Stack<int>();
Stack<int> t3 = new Stack<int>();
t3.Push(t1.Pop());
Console.WtriteLine($"t1:{t1.Peek()} t2:{t3}");
/*
t1 321
t2
t3

t1 32
t2
t3 1

t1 3
t2 2
t3 1

t1 3
t2 21
t3

t1
t2 21
t3 3

t1 1
t2 2
t3 3

t1 1
t2
t3 32

t1
t2
t3 321
*/

using System;
using System.Collections.Generic;

class Program
{
    static void PrintCountPeek(Stack<int> t1, Stack<int> t2, Stack<int> t3)
    {
        try
        {
            Console.WriteLine("T1");
            foreach (var item in t1)
            {
                Console.WriteLine($"{item}");
            }

        }
        catch (Exception ex)
        {
            Console.WriteLine($" {t1.Count}");
        }

        try
        {
            Console.WriteLine("T2");
            foreach (var item in t2)
            {
                Console.WriteLine($"{item}");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"T2 COUNT {t2.Count}");
        }

        try
        {
            Console.WriteLine("T3");
            foreach (var item in t3)
            {
                Console.WriteLine($"{item}");

            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"T3 COUNT{t3.Count}");
        }

        Console.WriteLine("----------------------");

    }

    static void Main(string[] args)
    {
        Stack<int> t1 = new Stack<int>();
        Stack<int> t2 = new Stack<int>();
        Stack<int> t3 = new Stack<int>();
        t1.Push(3);
        t1.Push(2);
        t1.Push(1);
        PrintCountPeek(t1, t2, t3);
        // Condiciones para efectuar
            // primera iteracion  t1 321 t2 _ t3 _
                // Cual es la torre que  no tiene elementos
                    //  Torre 2 Y torre 3
                    //   Cual seleccionar ? forzar al 3
                    // mover

            // segunda iteracion  t1 32 t2 _ t3 1
                // Cual es la torre que  no tiene elementos t2
                // Mover
            // tercera iteracion t1 3 t2 2 t3 1
                // Cual es la torre que  no tiene elementos niguna
                    // Cual es la torre es menor numero  y que no tenga mas  t3
                    // Cual es la torre con intermedio  y que no tenga mas  t2
                    // mover
            // cuarta iteracion t3 3 t2 21 t3 _
               // Cual es la torre que  no tiene elementos t3

            // tercera iteracion  t1 3 t2 1 t3 2
                // cual es el menor t2 :1
                    // donde lo muevo t3> entoce t1 3 t2 _ t3 2 1 }
                // Cual es la torre que  no tiene elementos
                    // t2
                // Cual es el menor o mayor ?
                    // t3 1
                // Muevo t3 1 t2

        t3.Push(t1.Pop());
        PrintCountPeek(t1, t2, t3);

        t2.Push(t1.Pop());
        PrintCountPeek(t1, t2, t3);

        t2.Push(t3.Pop());
        PrintCountPeek(t1, t2, t3);

        t3.Push(t1.Pop());
        PrintCountPeek(t1, t2, t3);

        t1.Push(t2.Pop());
        PrintCountPeek(t1, t2, t3);

        t3.Push(t2.Pop());
        PrintCountPeek(t1, t2, t3);

        t3.Push(t1.Pop());
        PrintCountPeek(t1, t2, t3);

    }
}

```

### Towe of Hanoi Chat

```csharp
using System;
using System.Collections.Generic;

class Program
{
    // Método recursivo para resolver las Torres de Hanoi
    static void Hanoi(int n, char fromRod, char toRod, char auxRod, Stack<int> t1, Stack<int> t2, Stack<int> t3)
    {
        if (n == 1)
        {
            t3.Push(t1.Pop());
            Console.WriteLine($"Mueve el disco 1 desde {fromRod} hasta {toRod}");
            return;
        }
        Hanoi(n - 1, fromRod, auxRod, toRod, t1, t3, t2);
        t3.Push(t1.Pop());
        Console.WriteLine($"Mueve el disco {n} desde {fromRod} hasta {toRod}");
        Hanoi(n - 1, auxRod, toRod, fromRod, t3, t2, t1);
    }


    static void Main(string[] args)
    {
        int n = 3; // Número de discos
        Stack<int> t1 = new Stack<int>();
        Stack<int> t2 = new Stack<int>();
        Stack<int> t3 = new Stack<int>();
        t1.Push(3);
        t1.Push(2);
        t1.Push(1);
        Hanoi(n, 'A', 'C', 'B', t1, t3, t2);

    }
}
```

## Namespace , Aliases

### Namespace

- reduce naming clonflict
- Organize our code
- interfaces, delegaces , classes, enums, events
-

```csharp

namespace Example{
    class A{

    }
}

class B{
    A a = new A(); // error
    Example.A a = new Example.A(); // or add using Example
}

```

### Aliases

Son nombres que hacen recerencia a librerias

```csharp
using Log = System.Diagnostics.Debug;
// Main o class into
 Log.WriteLine("Working with net7.0");
```

## Programacion Orientada a Objecto

Hay 4 pilares en la programacion a objetos,

- Encapculacion
  - public , protected, private y internal
- Abstraccion
  - abstract class y interfaces
  - la clase abtracta no puede ser intanciada
  - solo se implementan los publicos y proteced
- Herencia
  - compartir method public y protected
  - pero si la clase es seald no puede ser instanciada
- Polimorformo
  - una clase base puede comportarse de otras formas con diferentes methods
  - se debe usar virtual y overwrite para modificar los methods en el padre e hijo

```csharp
class A {
   virtual public void getName (){
    Console.WriteLine("Name");
   }
}

class B:A{

}

class P(){
    public static void Main(string[]args){
        A classeB = new B(); // polimorfismo
        classeB.getNameB();
    }
}


```

## Generic

Los genericons son tipo de dato que se usan para tener libertad de que se definan como dinamicos

```csharp
// Example 1
class Name<T>{
    public string getFullName(T name){
        return name.ToString();
    }
}

Name name = new Name();
name.getName(2);
name.getName("john");
// Exxample 2
// highlight-next-line
//class DinamicClass<U> same like T
class DinamicClass<T>
{
    // highlight-next-line
    //public static void PrintX(U message)
    public static void PrintX(T message)
    {
        Console.WriteLine(message.ToString());
    }
}

class Program
{
    static void Main(string[] args)
    {
        DinamicClass<string>.PrintX("This is a string"); ;
        DinamicClass<int>.PrintX(1000); ;
        DinamicClass<float>.PrintX(1000f); ;
        DinamicClass<bool>.PrintX(false); ;
    }
}
```
## .Net Design Principles

- Interoperability, Build apps on old version, allows to use old version of .Net and mix them with the lastest
- Portability, .Net Apps are design to be use on many platforms  like Mac, Windows and Linux.
- Garbage collections, Manage the memory when some components are not used.
- Security, validation and verification 
- Easy deploymnet , use VScode to deploy apps.
- CLR Commans Language Run Time 

## Threading 

Parral execute a same function