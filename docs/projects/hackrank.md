---
sidebar_label: "Hackerank"
sidebar_position: 3
tags: [C#, javascript, Algorithms]
---
## Sum point from Matches

Dado dos arreglos compara cada indixe si a>b suma un punto, si b>a b suma un punto si son iguales ninguno

```js
function checkPoints(a, b) {
  let i = 0;
  const points = [0, 0];
  while (i < a.length) {
    if (a[i] > b[i]) {
      points[0] += 1;
    } else if (b[i] > a[i]) {
      points[1] += 1;
    }
    i++;
  }
  console.log(points[0] + "" + points[1]);
}
checkPoints([5, 6, 7], [3, 6, 10]);
```

## Diagonal difference

Given a square matrix, calculate the absolute difference between the sums of its diagonals.

For example, the square matrix is shown below:

1 2 3
4 5 6
9 8 9  
The left-to-right diagonal = . The right to left diagonal = . Their absolute difference is .

Function description

Complete the function in the editor below.

diagonalDifference takes the following parameter:

int arr[n][m]: an array of integers
Return

int: the absolute diagonal difference
Input Format

The first line contains a single integer, , the number of rows and columns in the square matrix .
Each of the next lines describes a row, , and consists of space-separated integers .

Constraints

Output Format

Return the absolute difference between the sums of the matrix's two diagonals as a single integer.

Sample Input

3
11 2 4
4 5 6
10 8 -12
Sample Output

15
Explanation

The primary diagonal is:

11
5
-12
Sum across the primary diagonal: 11 + 5 - 12 = 4

The secondary diagonal is:

     4

5
10
Sum across the secondary diagonal: 4 + 5 + 10 = 19
Difference: |4 - 19| = 15

Note: |x| is the absolute value of x

### Javascript result

```js
function diagonalDifference(arr) {
  let avarageLenght = 0;
  arr.map((x) => {
    const childZise = x.length;
    if (childZise > avarageLenght) {
      avarageLenght = childZise;
    }
    return avarageLenght;
  });

  let diagonalLetftR = 0;
  let sumLeftR = 0;
  let diagonalRightL = avarageLenght - 1;
  let sumRightL = 0;
  for (let i = 0; i < arr.length; i++) {
    if (arr[i].length == avarageLenght) {
      sumLeftR += arr[i][diagonalLetftR];
      diagonalLetftR++;
      sumRightL += arr[i][diagonalRightL];
      diagonalRightL--;
    }
  }
  return Math.abs(sumLeftR - sumRightL);
}
const result = diagonalDifference([[3], [11, 2, 4], [4, 5, 6], [10, 8, -12]]);
console.log(`${result} : ${result == 15}`);
```

```csharp
static int diagonalDifference(List<List<int>> arr){
  int sizeChild = 0;

  for(int i =0 ; i < arr.Count; i++){
    if(sizeChild < arr[i].Count){
      sizeChild = arr[i].Count;
    }
  }
  Console.WriteLine(sizeChild)

}
```

### C# Solve

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static int diff(List<List<int>> arr)
    {
        int sizeChild = 0;

        for (int i = 0; i < arr.Count; i++)
        {
            if (sizeChild < arr[i].Count)
            {
                sizeChild = arr[i].Count;
            }
        }

        int counterDR = 0;
        int sumDR = 0;
        int counterDL = sizeChild - 1;
        int sumDL = 0;
        for (int i = 0; i < arr.Count; i++)
        {

            if (arr[i].Count == sizeChild)
            {
                sumDR += arr[i][counterDR];
                counterDR++;
                sumDL += arr[i][counterDL];
                counterDL--;
            }
        }
        return Math.Abs(sumDR - sumDL);
    }

    static void Main(string[] args)
    {
        List<List<int>> a = new List<List<int>>();
        a.Add(new List<int> { 3 });
        a.Add(new List<int> { 11, 2, 4 });
        a.Add(new List<int> { 4, 5, 6 });
        a.Add(new List<int> { 10, 8, -12 });
        int result = diff(a);
        Console.WriteLine($"{result} {(result == 15)}");
    }
}
```

## Calculate the ratios of its elements that are positive, negative, and zero

Given an array of integers, calculate the ratios of its elements that are positive, negative, and zero. Print the decimal value of each fraction on a new line with places after the decimal.

Note: This challenge introduces precision problems. The test cases are scaled to six decimal places, though answers with absolute error of up to are acceptable.

Example

There are elements, two positive, two negative and one zero. Their ratios are
2/5 , 2/5 , 1/5. Results are printed as:

0.400000
0.400000
0.200000

### SCharp

```csharp
using System;
using System.Collections.Generic;

class Program
{
    public static void radioCal(List<int> arr)
    {
        int[] deltaRadio = new int[] { 0, 0, 0 };
        int size = arr.Count;
        for (int i = 0; i < arr.Count; i++)
        {
            if (arr[i] > 0)
            {
                deltaRadio[0]++;
            }
            else if (arr[i] < 0)
            {
                deltaRadio[1]++;
            }
            else if (arr[i] == 0)
            {
                deltaRadio[2]++;
            }
        }
        Action<int> print = (x) => Console.WriteLine($"{((float)x / size).ToString("F4")}");
        print(deltaRadio[0]);
        print(deltaRadio[1]);
        print(deltaRadio[2]);
    }

    static void Main(string[] args)
    {
        List<int> a = new List<int> { -1, -2, 3, 0, 5 };
        radioCal(a);
    }
}
/*
0.4000
0.4000
0.2000
*/
```

### Javascript

```js
function radioCal(arr) {
  const radios = [0, 0, 0];
  arr.map((val) => {
    if (val > 0) {
      radios[0]++;
    } else if (val < 0) {
      radios[1]++;
    } else {
      radios[2]++;
    }
  });

  console.log((radios[0] / arr.length).toFixed(4));
  console.log((radios[1] / arr.length).toFixed(4));
  console.log((radios[2] / arr.length).toFixed(4));
}
radioCal([1, 1, -1, -1, 0]);
```

## Staircase detail

This is a staircase of size :

### CSharp Solution

````csharp
/*
   #
  ##
 ###
####
*/
using System;
using System.Collections.Generic;

class Program
{
    public static void radioCal(int n)
    {
        for (int i = 0; i < n ; i++)
        {
            string line = "";
            for (int j = 0; j < n ; j++)
            {
                if (j < n-1-i)
                {
                    line += " ";
                }
                else
                {
                    line += "#";
                }
            }
            Console.WriteLine(line);
        }
    }

    static void Main(string[] args)
    {
        radioCal(6);
    }
}```
````
