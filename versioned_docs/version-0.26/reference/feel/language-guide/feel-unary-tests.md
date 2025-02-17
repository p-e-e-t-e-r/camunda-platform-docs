---
id: feel-unary-tests
title: Unary tests
---

Unary tests can be used only for input entries of a decision table. They are a special kind of expression with additional operators. The operators get the value of the input expression implicitly as the first argument.

The result of the expression must be either `true` or `false`.

A unary test expression is `true` if one of the following conditions is fulfilled:
* the expression evaluates to `true` when the input value is applied to it
* the expression evaluates to a list and the input value is equal to at least one of the values in that list
* the expression evaluates to a value and the input value is equal to that value

### Comparison

Compare the input value to `x`.

| operator | symbol | example |
|----------|-----------------|---------|
| equal to | (none) | `"valid"` |
| less than | `<`  | `< 10` |
| less than or equal | `<=` | `<= 10` |
| greater than | `>` | `> 10` |
| greater than or equal | `>=` | `>= 10` |

* less than/greater than are only supported for:
  * number
  * date
  * time
  * date-time
  * year-month-duration
  * day-time-duration

### Interval

Test if the input value is within the interval `x` and `y`.

An interval can be open `(x..y)` / `]x..y[` or closed `[x..y]`. If the interval is open then the value is not included.

```js
(2..5)
// input > 2 and input < 5

[2..5]
// input >= 2 and input <= 5

(2..5]
// input > 2 and input <= 5
```

### Disjunction

Test if at least of the expressions is `true`.

```js
2, 3, 4
// input = 2 or input = 3 or input = 4

< 10, > 50
// input < 10 or input > 50
```

### Negation

Test if the expression is `false`.

```js
not("valid")
// input != "valid"

not(2, 3)
// input != 2 and input != 3
```

### Expression

It is also possible to use a boolean [expression](../feel-expression) instead of an operator. For example, invoking a built-in function.

The input value can be accessed by the special variable `?`.

```js
ends with(?, "@camunda.com")
// test if the input value (string) ends with "@camunda.com"

list contains(?, "invalid")
// test if the input value (list) contains "invalid"
```
