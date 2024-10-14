## Definition

A **falsy** (sometimes written **falsey**) value is a value that is considered false when encountered in a **Boolean** context.

## Complete List of JavaScript Falsy values

| Value          | Type      | Description                                                                                                                     |
| -------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `null`         | Null      | The keyword `null` - the absence of any value                                                                                   |
| `undefined`    | Undefined | `undefined` - the primitive value                                                                                               |
| `false`        | Boolean   | The keyword `false`                                                                                                             |
| `NaN`          | Number    | `NaN` - not a **Number**                                                                                                        |
| `0`            | Number    | The **Number** zero, also including `0.0`, `0x0`, etc.                                                                          |
| `-0`           | Number    | The **Number** negative zero, also including `-0.0`, `-0x0`, etc.                                                               |
| `0n`           | BigInt    | The **BigInt** zero, also including `0x0n`, etc. Note that there is no **BigInt** negative zero — the negation of `0n` is `0n`. |
| ""             | String    | Empty **string** value, also including `''` and ` `` `.                                                                         |
| `document.all` | Object    | The only **falsy** object in JavaScript is the built-in `document.all`                                                          |

The values `null` and `undefined` are also [[#Nullish]].

## Nullish

In [[JavaScript]], a **nullish** value is the value which is either `null` or `undefined`. **Nullish** values are always **falsy**.