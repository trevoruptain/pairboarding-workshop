# Partner B

## Improvements
* Tell me about a time you improved a tool, task, or project you were working on. What was the circumstances?
* Why did you do it?  
* Do you have any other examples?

## JS Trivia
* What do the following lines output, and why?

```JavaScript
console.log(1 < 2 < 3);
console.log(3 > 2 > 1);
```

The first statement returns `true` which is as expected.

The second returns `false` because of how the engine works regarding operator associativity for `<` and `>`. It compares left to right, so `3 > 2 > 1` JavaScript translates to `true > 1`. `true` has value `1`, so it then compares `1 > 1`, which is `false`.
