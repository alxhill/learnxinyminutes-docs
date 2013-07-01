---
language: javascript
author: Alexander Hill
author_url: http://alxhill.com
filename: learnjavascript.js
---

JavaScript is the only language that can run directly in every browser and make changes to the current page.
It was created in a very short amount of time, so has a few quirks that are worth being aware of, but other than that is a very capable language.

There are multiple versions of JavaScript and multiple different browser implementations, each working with a subset of the full specifications.
I will try to ensure the code in this article works on IE8+, and will mark any features that do not work as expected.

If you'd like to correct bugs or give me any kind of feedback, you can contact me through [twitter](http://twitter.com/alxhill) or email (on my [website](http://alxhill.com)).

```javascript
// Single line comments start with two slashes.
/*
    Multiline comments are exactly the same as C and Java comments.
*/


/*                 A NOTE ABOUT SEMICOLONS.
 * Semicolons in JavaScript are used to separate statements.
 * However, all modern JavaScript interpretters use something
 * called Automatic Semicolon Insertion, or AST for short. Whilst
 * usually reliable, there are a few cases where ommiting semicolons
 * will cause code to break. As such, it is recommended by most JavaScript
 * to use semicolons.
 *
 * However, I will be omiting them from single line statement.
 */

/**********************************
 * Basic Data Types and Operators *
 **********************************/

// Numbers are simple. There's only one type of number - floats and integers are the same.
3 //=> 3
3.0 //=> 3

// Operators work as expected
3 + 2 //=> 5
3 - 2 //=> 1
3 * 2 //=> 6
3 / 2 //=> 1.5

// Brackets can be used to enforce precedence
(3 + 2) * 2 //=> 10

// Boolean values are:
true
false

// they can be negated with !
!true //=> false

// Comparisons can be done with the usual operators
// All of the following statements are true
1 === 1 // equality
1 !== 2 // inequality
1 < 2
1 > 0
1 <= 1
2 >= 2

// Comparisons can be chained with && (and) and || (or)
// The following statements are true
1 > 1 || 1 === 1
2 > 1 && 1 === 1

// NOTE: there is another equality operator that just uses two equals
// signs. However, it performs 'type coercion' which can have some unexpected results.
// It's use is generally discouraged except for a specific cases.

// Mathematical constants and functions are in the global Math object
// It has constants
Math.PI //=> 3.14159...
Math.E //=> 2.718...
// trig functions
Math.sin(Math.PI/2) //=> 1
Math.cos(Math.PI/2) //=> 0
Math.tan(0) //=> 0
// square roots
Math.sqrt(4) //=> 2
// exponents
Math.pow(2, 3) //=> 8
// max and min
Math.max(1, 2, 3, 4) //=> 4
Math.min(1, 2, 3, 4) //=> 1
// rounding functions
Math.ceil(2.1) //=> 3
Math.floor(2.8) //=> 2
Math.round(2.8) //=> 3
// random number generator
Math.random() //=> Any value between 0 and 1 inclusive

// Strings are created with single or double quotes
'This is a boring string'
"This one is even more boring"

// Individual characters can be accessed in two different ways
"string"[0] //=> "s"
"string".charAt(0) //=> "s"

// you can join two strings with the + operator
"Hello" + " " + "World!" //=> "Hello World!"

/*********************************
 * Variables, objects and arrays *
 *********************************/

// Local variables can be declared with the 'var' keyword.
var something;
something = "hi there!";
something; //=> "hi there"

// assignment and declaration can be done on one line
var something_else = "bacon";
something_else; //=> "bacon"

// Declaring a variable without the var keyword will create a global variable.
// This is usually undesirable
global_thing = "hey world";
global_thing; //=> "hey world"

// Variables that have been declared but not assigned to are undefined. This is
// a special type in JavaScript.
var thing;
thing; //=> undefined

// Objects are the most important type in JavaScript - all other types are also objects
// An empty object is created using empty braces
var object = {};

// Values can be added and accessed to the object like so
object["key"] = "value";
object["key"]; //=> "value"

// or directly using
object.another_key = "another value";
object.another_key; //=> "another value"

// objects literals can be created with values already in place
var another_object = {
    thing: "value", // note that strings are not required around the key
    another_thing: "another value"
}
another_object.thing; //=> "value"

// values can be changed after they have been set
another_object.another_thing = "a slightly more interesting value"

// and can be removed with the delete keyword
delete another_object.thing;
another_object.thing; //=> undefined

// objects can also contain other objects, as well as any primitive value
var survival_kit = {
    food: {
        bacon: true,
        eggs: true,
        tomatoes: "rotten"
    },
    bandages: 12,
    water: "14 litres"
};

survival_kit.food.bacon; //=> true

// the in operator can be used to check for the presence of a key in an object
"food" in survival_kit //=> true
12 in survival_kit //=> false

// Arrays are used for storing an ordered list of elements
// They are created using square brackets.
var empty_array = [];

// and like objects can be filled with values of any type.
// However, it's common for them to have only one type.
var lost_numbers = [4, 8, 15, 16, 23, 42];

// elements are accessed using square brackets. The values are indexed
// from 0.
lost_numbers[0]; //=> 4
lost_numbers[3]; //=> 16
lost_numbers[100]; //=> undefined

// you can get the length of an array using the length property
lost_numbers.length; //=> 6

// Adding new values can be done using square brackets
var numbers = [1, 2];
numbers[2] = 3;

// they don't have to be directly after the current values
numbers[5] = 6;
// ...but JavaScript will fill the spaces with undefined
numbers; //=> [1, 2, 3, undefined, undefined, 6]
numbers.length; //=> 6

// You can add values to the end of an existing array using the push function,
// and remove them with the pop function.
var counting = [1, 2];
counting.push(3);
counting; //=> [1, 2, 3]
counting.pop(); //=> 3, because pop returns the last value
counting; //=> [1, 2] the returned value has been removed

// You can also add and remove values from the start of an array using the
// shift and unshift functions
counting.unshift(0);
counting; //=> [0, 1, 2]
counting.shift() //=> 0, because like pop shift returns the removed value
counting; //=> [1, 2]

// removing elements is a lot more painful
// using the delete operator only sets the value to undefined
delete counting[0];
counting; //=> [undefined, 1]
counting.length; //=> 2

// elements can be removed by index using the splice function.
// Its arguments are an index, and the number of elements to remove.
counting.splice(0, 1);
counting; //=> [1]

// In modern browsers, you can remove a something by value using the indexOf function
// alongside the splice function
counting = [1, 2, 3, 200, 4];
counting.splice(counting.indexOf(200), 1);
counting; //=> [1, 2, 3, 4]

// This article shows how to implement indexOf in browsers that don't natively support it:
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf
// Alternatively, you can loop through the array until the correct element is found. This will
// be demonstrated further down.

/****************
 * Control Flow *
 ****************/

// the 'if' statement can be used to conditionally run code depending on the truth of an expression.
// Brackets around the expression are required.
if (1 < 3)
{
    // maths works!
}

// the else statement will executes if the expression is false
var does_maths_work;
if (1 + 2 == 3)
{
    does_maths_work = true;
}
else
{
    does_maths_work = false;
}
does_maths_work; //=> true, thankfully

// the braces around the block can be excluded if there is only one statement following it.
// Be careful with this - the following two things are not equivalent:
var life, happiness;
if (false)
    life = "meaningless";
    happiness = "doubtful";
// in this case, happiness will always equal doubtful, despite the fact it shouldn't.
var life, happiness;
if (false)
{
    life = "meaningless";
    happiness = "doubtful";
}
// whereas here, both life and happiness will remain undefined.

// the else if allows for multiple comparisons to be made
var age = 19;
var age_group;
if (age < 18)
    age_group = "child";
else if (age < 25)
    age_group = "young adult";
else if (age > 50)
    age_group = "elderly";
else
    age_group = "adult";

// in this case, age_group would be "young adult".

// While loops continue to execute a block of so long as a certain condition holds.
var number = 0;
while (number > 10)
{
    number = number + 1;
}
number; //=> 10, because the condition only fails when number is 10


```
