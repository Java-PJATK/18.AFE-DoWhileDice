# 19.AFE-DoWhileDice

Now, let's assume the user inputs numbers until they enter zero. We want to calculate the sum of all these numbers and count how many numbers were entered:

```java
int sum = 0, num = 0, n;
while ( (n = scanner.nextInt()) != 0) {
    sum += n;
    ++num;
}
```

After the loop, we have what we were interested in in variables `sum` and `num`.

## `do-while` loop

Loops of this type are similar to while-loops, but checking a condition is performed after execution of the body of the loop.

```java
do {
    // ...
    if (cond1) break; // optional
    // ...
    if (cond2) continue; // optional
    // ...
} while(condition);
```

Therefore,
1. The body of the loop is executed;
2. The value of `condition` is evaluated; if it is true, flow of control goes to item 1, if it is false, the flow of control jumps out of the loop.

Let us consider an example. We will use here the `random` from class `Math`. The expression `Math.random()` returns a (pseudo) random value from the half-open interval [0, 1). This is sufficient to generate random values from any range, not necessarily [0, 1). Suppose we want a random integer from the interval [a, b]. There are `b - a + 1` consecutive values in this interval. Multiplying `Math.random()` by this number, we get a `double` from the half-open interval [0, b - a + 1). Casting it to `int` will give us a number from the interval [0, b - a] (we will never get `b - a + 1`, as the interval [0, 1) was half-open). Adding `a` to the result, we get an `int` from the closed interval [a, b], as desired. So, to generate a pseudo-random integer from the closed interval [a, b], we can write

```java
a + (int)(Math.random() * (b - a + 1))
```

It is important to use parentheses around the product `Math.random() * (b - a + 1)` because casting has higher precedence than multiplication. Without the parentheses

```java
a + (int)Math.random() * (b - a + 1) // WRONG
```

casting to `int` would be applied to `Math.random()` before multiplication, but this is always zero, as `Math.random()` is always less than 1.

The program below illustrates what we have just said demonstrating also the `do-while` loop: here, we roll two dice until two sixes are thrown.

## Listing 19 AFE-DoWhileDice/Dice.java Page 40

```java
public class Dice {
    public static void main (String[] args) {
        int a, b;
        do {
            a = 1 + (int)(Math.random()*6);
            b = 1 + (int)(Math.random()*6);
            System.out.println("a=" + a + " b=" + b);
        } while (a + b != 12);
    }
}
```

A possible outcome of the program might be

```
a=5 b=6
a=4 b=3
a=6 b=5
a=1 b=2
a=1 b=3
a=1 b=6
a=3 b=6
a=1 b=3
a=2 b=1
a=4 b=5
a=6 b=6
```
