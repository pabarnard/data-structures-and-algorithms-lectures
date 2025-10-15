# Data tips
Working with data is crucial, as you will deal with it all the time.  Knowing where it comes from and what kind of data you're handling will guide you to the right steps in processing it.  This is important not just in real life, but in algorithm challenges as well, as you need to know what kind of inputs and outputs you will work with, and know which methods you can use - and if you need additional data structures (e.g. sets, maps) to help you tackle the problem.  

## Using the right methods for the right data types
Errors often arise because one might use a method that works for one data type but doesn't work for another, and this arises a lot in functional programming.  Here's an example of a common error in JavaScript where we try to extract each non-space character:
```js
const sentence = "Hello everyone!  I love sunny weather!";
let mystery = sentence.split(" "); // split by spaces
mystery.split(""); // ILLEGAL!!
```
There is a method called `split` for strings, but there is no such method for arrays!  The split method returns an array, so when we called `split` for the array, you can't do it!  Let's fix our code to do the following instead:
```js
const sentence = "Hello everyone!  I love sunny weather!";
sentence.split(" ").map(word => word.split("")).flat(); // Now we have an array of non-space characters
```
Now we have an array consisting of only the nonspace characters!  Notice that `split` works for strings, while `map` and `flat` work for arrays.  (Disclaimer: there are better ways to grab all the non-space characters in a string; this example is meant to illustrate the importance of knowing which data type you're handling so that you can utilize the correct methods accordingly.)

## Accessing data
Another source of confusion is when it comes to accessing data, especially if it comes from an API or from a database.  Imagine you have this data from the Pokemon API (written in JavaScript):
```js
const thisPokemon = {
    "name": "mew",
    "stats": [
        {
            "base_stat": 100,
            "effort": 3,
            "stat": {
                "name": "hp",
                "url": "https://pokeapi.co/api/v2/stat/1/"
                }
        },
        {
            "base_stat": 100,
            "effort": 0,
            "stat": {
                "name": "attack",
                "url": "https://pokeapi.co/api/v2/stat/2/"
                }
        },
        {
            "base_stat": 100,
            "effort": 0,
            "stat": {
                "name": "defense",
                "url": "https://pokeapi.co/api/v2/stat/3/"
            }
        },
        {
            "base_stat": 100,
            "effort": 0,
            "stat": {
                "name": "special-attack",
                "url": "https://pokeapi.co/api/v2/stat/4/"
            }
        },
        {
            "base_stat": 100,
            "effort": 0,
            "stat": {
                "name": "special-defense",
                "url": "https://pokeapi.co/api/v2/stat/5/"
            }
        },
        {
            "base_stat": 100,
            "effort": 0,
            "stat": {
                "name": "speed",
                "url": "https://pokeapi.co/api/v2/stat/6/"
            }
        }
    ],
    "types": [
        {
            "slot": 1,
            "type": {
                "name": "psychic",
                "url": "https://pokeapi.co/api/v2/type/14/"
            }
        }
    ],
    "weight": 40
} // Notice that this variable is an object due to the curly braces {}
```
Think of the raw data like an onion that you need to peel.  You ask yourself each time, "What kind of data am I dealing with at this moment?"  In other words, what data type am I looking at right now?  Is it a string, a boolean, a number, an array, an object, an instance of a class, or something else?  Start with the outermost layer and then work your way in, one piece at a time.  You access something inside the item in question, and then repeat the process until you have grabbed the data you want.

For example, if you wanted the name of this Pokemon, you'd do `thisPokemon.name` or `thisPokemon["name"]`.  However, if you wanted its type, you'd do the following:
```js
thisPokemon["types"] // will give:
[
    {
        "slot": 1,
        "type": {
            "name": "psychic",
            "url": "https://pokeapi.co/api/v2/type/14/"
        }
    }
] // Adding ["types"] allows us to grab the value linked to the "types" key in the object called "thisPokemon"!  Now we're looking at an array!

thisPokemon["types"][0] // will give:
{
    "slot": 1,
    "type": {
        "name": "psychic",
        "url": "https://pokeapi.co/api/v2/type/14/"
    }
} // Notice there are no square brackets in the remaining data as we access an item in the array!  Now we have an object!

thisPokemon["types"][0]["type"] // will give:
{
    "name": "psychic",
    "url": "https://pokeapi.co/api/v2/type/14/"
} // This is also an object

thisPokemon["types"][0]["type"]["name"] // will give:
"psychic" // Here's the answer, and it's a string!
```
Know the data type you're dealing with each step of the way!  This allows you to determine the methods you can use - and how to access the data!  How do you access an item from an array?  From an object?  From an instance of a class?  Hopefully these tips will come in handy so you can deal with data much more easily than before!

## Mutable vs. immutable data
Many folks struggle with whether a variable is **mutable** vs. **immutable**.  **Mutable** data is data that can be changed after it's created, while **immutable** data is data that cannot be modified after creation.

Mutable vs. immutable data plays a major role when you deal with functions and methods.  Here are some examples in JavaScript:
```js
const add10 = val => {
    val += 10;
}
let x = 10;
console.log(x); // 10
add10(x);
console.log(x); // Still 10
```

```js
const add10ToArr = arr => {
    arr.push(10);
}
let myArr = [3, 5];
console.log(myArr); // [3, 5]
add10ToArr(myArr);
console.log(myArr); // [3, 5, 10]
```
Notice in the two examples above that when an integer is passed in and its value is changed inside the function, it says changed only within the scope of the function, and then after the function call its value is still unchanged.  But if you pass in an array and change its contents, they stay changed even after the function call is completed, and what is happening is that you're passing in a *reference* to the item in memory, and then you change its contents.  

Thus usually arrays, objects, instances of classes, etc. are usually mutable in many languages, whereas more primitive types (e.g. booleans, numbers) are immutable.

Here are some useful tips when it comes to which data types are mutable vs. immutable:
- Primitive data types are usually immutable, like booleans and numbers
- Strings in most languages are immutable
- Objects and instances of classes are usually mutable

Some languages actually allow you to specify which variables are mutable and immutable (e.g. Rust), so you have some more flexibility.

Mutable data comes in handy with recursion, dynamic programming and anything that requires you to keep track of multiple items at once.  Immutable data is useful when you need it to be predictable and thread-safe.