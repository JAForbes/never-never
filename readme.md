Never
=====

A value that doesn't equal other values.


Quick Start
-----------

```js
const never = require('never-never')

const answer = 
    [NaN, undefined, null, '', 1, false, true]
    .every( x => x != never )

console.assert(answer, 'nothing equals never')
```

Why
---

Some languages and type systems have a concept of a bottom type, or a never type.  It can be used to model unexpected cases in a far more precise way than checking for `null` or `undefined` (which may have appeared for a variety of reasons). 

`never` is a value that will never satisfy an equality check.  It can be useful for discriminated switches (use never as a default case), or for more precisely checking values in testing.

```js
t.throws( 
    , () => getUser(never) //can never be true
    , 'getUser(id) throws if the user id has no match'
)
```

The above will never be satisfied and is semantically clearer than something like:

```js
t.throws(
    , () => getUser(undefined)
    , 'getUser(id) throws if the user id has no match'
)
```

How does it work
----------------

Javascript has a value that has the exact behaviour we want.

> NaN compares unequal (via ==, !=, ===, and !==) to any other value -- including to another NaN value.  Use Number.isNaN() or isNaN() to most clearly determine whether a value is NaN.  Or perform a self-comparison: NaN, and only NaN, will compare unequal to itself.


[NaN - Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)

This library is simply an object with a `valueOf` that returns `NaN` (plus some helpers for debugging like `toString()` )

Here is the complete source code:

```js

module.exports = {
    valueOf: function valueOf(){
        return NaN
    }
    ,toString: function toString(){
        return 'never'
    }
    ,inspect: function inspect(){
        return 'never'
    }
}
```


What's with the name?
====================

Never Never is an Australian term for "the outback" which is an Australian term for "whoop whoop" which is an Australian term for "beyond the black stump" which is an Australian term for ...

[Never Never](https://en.wikipedia.org/wiki/Never_Never_(Australian_outback))
