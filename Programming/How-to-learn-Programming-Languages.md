# How to learn Programming languages?
This is process that I'm learning new languages.

## 1. Print "Hello, World!"
```Python
# Python
print("Hello, World!")
```

```Kotlin
// Kotlin
println("Hello, World!")
```

## 2. Declare Variables
```Python
# Python
a = 1
b = "Hello"
```

```Kotlin
// Kotlin
var a = 1
val b: String = "Hello"
```

## 3. Branches
```Python
# Python
x = 1

if (x == 1):
  print("x is 1!")
else:
  print("x is not 1...")

while x < 10:
  print(x)
  x += 1
```

```Kotlin
// Kotlin
var x = 1

if (x == 1) {
  println("x is 1!")
}
else {
  println("x is not 1...")
}

while (x < 10) {
  println(x)
  x += 1
}
```

## 4. Functions
```Python
# Python
def hello(a):
  print(f"Hello, {a}!")
hello("Python")
```

```Kotlin
// Kotlin
fun hello(a: String) {
  println("Hello, $a!")
}
hello("Kotlin")
```

## 5. Array
```Python
# Python
a = [1, 2, 3]
print(a[0])
a.append(4)
```

```Kotlin
// Kotlin
val a = mutableListOf(1, 2, 3)
println(a[0])
a.add(4)
```

## 6. Classes
```Python
# Python
class Ball:
  def __init__(self, size):
    self.size = size
  
  def printSize(self):
    print(f"Size of this ball is {self.size}!")

a = Ball()
a.printSize()
```

```Kotlin
// Kotlin
class Ball(val size: Int) {
  fun printSize() println("Size of this ball is $size!")
}
```

## 7. Make Fibonacci and BrainF**k compiler, or anything!
```Python
# Python
# Fibonacci with Matrices, using Function, Array, (+ and Classes sometimes)
def mul(mat, other):
  a, b, c, d = mat
  e, f, g, h = other
  return [a*e+b*g, a*f+b*h, c*e+d*g, c*f+d*h]

def pow(mat, n):
  if n == 0: return [1, 0, 0, 1]
  if n == 1: return mat
  return mul(pow(mat, n//2), pow(mat, n//2 + n%2))

def fibo(n):
  mat = [1, 1, 1, 0]
  powered = pow(mat, n)
  return powered[1]
```

```Kotlin
// Kotlin
// BrainF**k language compiler, using Classes, Array, Branches
```
[Kotlin Source code is Here!](https://github.com/pl-Steve28-lq/ProgrammingLanguages/blob/master/Kotlin/BrainFuck.kt)

## 8. Make toy project.
Find out what you need while making your programs! Google, StackOverflow is your best friends :)

Python - [Project Keyboard](https://github.com/pl-Steve28-lq/Project-Keyboard)<br>
Kotlin - [CoronaSearchApp](https://github.com/pl-Steve28-lq/CoronaSearchApp)
