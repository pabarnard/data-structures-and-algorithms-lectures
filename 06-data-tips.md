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