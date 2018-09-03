# Partner A

## Time to innovate
* Give me an example of a time you used customer feedback to drive improvement or innovation.
* What was the situation and what action did you take?

## Floating Point Precision

* What will the code below output? Explain your answer.

```JavaScript
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);
```

### Answer
An educated answer to this question would simply be: “You can’t be sure. it might print out `0.3` and `true`, or it might not. Numbers in JavaScript are all treated with floating point precision, and as such, may not always yield the expected results.”

The example provided above is classic case that demonstrates this issue. Surprisingly, it will print out:

```JavaScript
0.30000000000000004
false
```

A typical solution is to compare the absolute difference between two numbers with the special constant `Number.EPSILON`:

```JavaScript
function areTheNumbersAlmostEqual(num1, num2) {
	return Math.abs( num1 - num2 ) < Number.EPSILON;
}
console.log(areTheNumbersAlmostEqual(0.1 + 0.2, 0.3));
```
