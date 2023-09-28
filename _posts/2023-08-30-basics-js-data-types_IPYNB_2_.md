---
title: Javascript Data Types/Lists
hide: True
description: A Tech Talk on javascript data types and how to use with lists
type: ccc
permalink: /basics/datatypes
author: Will Cheng
---

{% include nav_basics.html %}

# string datatype
- We discussed that strings store text
- It is useful to know a few functions that can be used on string manipulation (see example below)
- We can see the type of data using `typeof` operator


```python
%%js

// assign variable
var hello = "Hello World";
console.log("variable: hello")
console.log(hello)

// seeing the type of this data
console.log("variable: hello check typeof")
console.log(typeof hello)

// add strings together
console.log("string concatenation: hello + Rohan!")
console.log(hello + " Rohan!")
```


<script>

// assign variable
var hello = "Hello World";
console.log("variable: hello")
console.log(hello)

// seeing the type of this data
console.log("variable: hello check typeof")
console.log(typeof hello)

// add strings together
console.log("string concatenation: hello + Rohan!")
console.log(hello + " Rohan!")

// getting a certain component of this text
// (here the _ is a standin for the space character)
// H  e  l  l  o  _  W  o  r  l  d
// 0  1  2  3  4  5  6  7  8  9  10
// if we want the hello component, we want characters 0-4, so we use the following function
// (note how we use 0 and 5 as arguments, the last character is NOT INCLUSIVE)
console.log("substring: hello 0, 5")
console.log(hello.substring(0, 5))

// useful functions to make string lowercase or uppercase
console.log("string convert to upper case: hello toUpperCase")
console.log(hello.toUpperCase())
console.log("string convert to lower case: hello toLowerCase")
console.log(hello.toLowerCase())

// useful function to check if one string is contained in another
console.log("string includes: hello includes Rohan")
console.log(hello.includes("Rohan"))
console.log("string includes: hello includes Hello")
console.log(hello.includes("Hello"))
</script>



## .substring()


```python
%%js
var hello = "Hello World";

// getting a certain component of this text
// (here the _ is a standin for the space character)
// H  e  l  l  o  _  W  o  r  l  d
// 0  1  2  3  4  5  6  7  8  9  10
// if we want the hello component, we want characters 0-4, so we use the following function
// (note how we use 0 and 5 as arguments, the last character is NOT INCLUSIVE)
console.log("substring: hello 0, 5")
console.log(hello.substring(0, 5))
```

## .toUpperCase() and .toLowerCase()


```python
%%js
var hello = "Hello World";

// useful functions to make string lowercase or uppercase
console.log("string convert to upper case: hello toUpperCase")
console.log(hello.toUpperCase())
console.log("string convert to lower case: hello toLowerCase")
console.log(hello.toLowerCase())
```

## .includes()


```python
%%js
var hello = "Hello World";

// useful function to check if one string is contained in another
console.log("string includes: hello includes Rohan")
console.log(hello.includes("Rohan"))
console.log("string includes: hello includes Hello")
console.log(hello.includes("Hello"))
```

# number datatype
- we discussed that numbers store numbers
- here are some useful ideas in javascript to deal with numbers


```python
%%js
console.log("Numbers info")

// assign numbers to varialbes
console.log("variable: num1")
var num1 = 9
console.log(num1)
console.log("variable: num2")
var num2 = 6
console.log(num2)


// simple operations with numbers
console.log("Operations")
console.log("subtract: num1 - num2")
console.log(num1 - num2)
console.log("add: num1 + num2")
console.log(num1 + num2)
console.log("divide: num1 / num2")
console.log(num1 / num2)
console.log("multiply: num1 * num2")
console.log(num1 * num2)
console.log("remainder (modulo): num1 % num2")
console.log(num1 % num2)
```


<script>
console.log("Numbers info")

// assign numbers to varialbes
console.log("variable: num1")
var num1 = 9
console.log(num1)
console.log("variable: num2")
var num2 = 6
console.log(num2)


// simple operations with numbers
console.log("Operations")
console.log("subtract: num1 - num2")
console.log(num1 - num2)
console.log("add: num1 + num2")
console.log(num1 + num2)
console.log("divide: num1 / num2")
console.log(num1 / num2)
console.log("multiply: num1 * num2")
console.log(num1 * num2)
console.log("remainder (modulo): num1 % num2")
console.log(num1 % num2)

// converting numbers to text
console.log("number convert string: num1")
console.log(num1.toString())

// rounding a number
console.log("round(num1 / num2)")
console.log(Math.round(num1 / num2))

// rounding a number to decimal palces
console.log("set decimals to 2 places (num1 / num2)")
console.log((num1 / num2).toFixed(2))
</script>



# number formatting


```python
%%js
console.log("variable: num1")
var num1 = 9
console.log(num1)
console.log("variable: num2")
var num2 = 6
console.log(num2)

// converting numbers to text
console.log("number convert string: num1")
console.log(num1.toString())

// rounding a number
console.log("round(num1 / num2)")
console.log(Math.round(num1 / num2))

// rounding a number to decimal palces
console.log("set decimals to 2 places (num1 / num2)")
console.log((num1 / num2).toFixed(2))
```

# Array datatype
- an array is just a list of other datatypes
- put all the items in square brackets
- some useful methods below


```python
%%js
console.log("Array: assigning a list of strings")
var str1 = "1st string"
var arr_data = [str1, "2nd string", "3rd string"]
// seeing what is in the array
console.log(arr_data)

// getting one thing from an array
// "A string" "Other Data" "more data"
//    0           1            2
console.log("Array: referencing a cell #1")
console.log([ arr_data[1] ])  // zero based counting: 1 is 2nd cell

```


<script>
console.log("Array: assigning a list of strings")
var str1 = "1st string"
var arr_data = [str1, "2nd string", "3rd string"]
// seeing what is in the array
console.log(arr_data)

// getting one thing from an array
// "A string" "Other Data" "more data"
//    0           1            2
console.log("Array: referencing a cell #1")
console.log([ arr_data[1] ])  // zero based counting: 1 is 2nd cell

// adding something new to the array
console.log("Array: adding to list")
arr_data.push("4th string")
console.log(arr_data)

// removing the first element of array
console.log("Array: removing from front of list")
arr_data.shift()
console.log(arr_data)

// removing the last element of array
console.log("Array: removing from end of list")
arr_data.pop()
console.log(arr_data)
</script>




# array manipulation


```python
%%js
console.log("Array: assigning a list of strings")
var str1 = "1st string"
var arr_data = [str1, "2nd string", "3rd string"]
// seeing what is in the array
console.log(arr_data)

// adding something new to the array
console.log("Array: adding to list")
arr_data.push("4th string")
console.log(arr_data)

// removing the first element of array
console.log("Array: removing from front of list")
arr_data.shift()
console.log(arr_data)

// removing the last element of array
console.log("Array: removing from end of list")
arr_data.pop()
console.log(arr_data)
```

# Object datatype

- store records as key-value pairs
- are defined by enclosing data in curly braces `{}`
- allow access and modification using dot `.` or square bracket `[]` notation


```python
%%js
console.log("Object: assigning key-value objects")
var obj = {
    name: "Safin",
    age: 13
};

// The following is stored in the object called "obj"
// {
//     name: "Safin",
//     age: 13
// }
//
// The key "name" is associated with the string value "Safin"
// The key "age" is associated with the number value 13
// Notice that keys are of the type "string"

// print obj to the console
console.log(obj);
// -> { name: 'Safin', age: 13 }
// Notice that single quotes ' and double quotes " can be used interchangeably
```


<script>
console.log("Object: assigning key-value objects")
var obj = {
    name: "Safin",
    age: 13
};

// The following is stored in the object called "obj"
// {
//     name: "Safin",
//     age: 13
// }
//
// The key "name" is associated with the string value "Safin"
// The key "age" is associated with the number value 13
// Notice that keys are of the type "string"

// print obj to the console
console.log(obj);
// -> { name: 'Safin', age: 13 }
// Notice that single quotes ' and double quotes " can be used interchangeably

// To access certain values within an object, also known as an object's fields,
// you can use the name of the object suffixed with a dot and the name of the field
// or using the square bracket notation shown below
console.log("Object: using key name to access the name value (key notation)")
console.log(obj["name"]);
console.log("Object: using key name to access the name value (dot notation)")
console.log(obj.name);
// -> Safin

// Fields of an object can be manipulated similar to variables
console.log("Object: mutating the key name from Safin to John")
obj.name = "John"
console.log(obj);
console.log(obj.name);
// -> John

// A key-value pair can be added to the object
console.log("Object: mutating the key name from Safin to John")
obj["ghid"] = "jm1021"
console.log(obj);
// Observe new key
</script>



# object access


```python
%%js
console.log("Object: assigning key-value objects")
var obj = {
    name: "Safin",
    age: 13
    
};

// The following is stored in the object called "obj"
// {
//     name: "Safin",
//     age: 13
// }
//
// The key "name" is associated with the string value "Safin"
// The key "age" is associated with the number value 13
// Notice that keys are of the type "string"

// print obj to the console
console.log(obj);
// -> { name: 'Safin', age: 13 }
// Notice that single quotes ' and double quotes " can be used interchangeably

// To access certain values within an object, also known as an object's fields,
// you can use the name of the object suffixed with a dot and the name of the field
// or using the square bracket notation shown below
console.log("Object: using key name to access the name value (key notation)")
console.log(obj["name"]);
console.log("Object: using key name to access the name value (dot notation)")
console.log(obj.name);
// -> Safin

// Fields of an object can be manipulated similar to variables
console.log("Object: mutating the key name from Safin to John")
obj.name = "John"
console.log(obj);
console.log(obj.name);
// -> John

// A key-value pair can be added to the object
console.log("Object: mutating the key name from Safin to John")
obj["ghid"] = "jm1021"
console.log(obj);
// Observe new key
```


    <IPython.core.display.Javascript object>


# Hacks
Create a JavaScript snippet below with the following requirements:
- Create an object representing yourself as a person. The object should have keys for your name, age, current classes, interests, and two more of your choosing
- Your object must contain keys whose values are arrays. The arrays can be arrays of strings, numbers, or even other objects if you would like
- Print the entire object with console.log after declaring it
- Manipulate the arrays within the object and print the entire object with console.log as well as the specific changed key afterwards
- Perform mathematical operations on fields in your object such as +, -, /, % etc. and print the results with console.log along with a message contextualizing them
- Use typeof to determine the types of at least 3 fields in your object


```python
%%js
// Create an object representing yourself
const person = {
    name: "Will Cheng",
    age: 15,
    currentClasses: ["Calc AB", "World", "Chem", "Photography", "CSP"],
    interests: ["Coding", "Reading", "Gaming"],
    heightInCm: 175,
    weightInKg: 70,
    1: "Afghanistan",
    2: "Albania",
    3: "Algeria",
    4: "Andorra",
    5: "Angola",
    6: "Antigua and Barbuda",
    7: "Argentina",
    8: "Armenia",
    9: "Australia",
    10: "Austria",
    11: "Azerbaijan",
    12: "Bahamas",
    13: "Bahrain",
    14: "Bangladesh",
    15: "Barbados",
    16: "Belarus",
    17: "Belgium",
    18: "Belize",
    19: "Benin",
    20: "Bhutan",
    21: "Bolivia",
    22: "Bosnia and Herzegovina",
    23: "Botswana",
    24: "Brazil",
    25: "Brunei",
    26: "Bulgaria",
    27: "Burkina Faso",
    28: "Burundi",
    29: "Cabo Verde",
    30: "Cambodia",
    31: "Cameroon",
    32: "Canada",
    33: "Central African Republic",
    34: "Chad",
    35: "Chile",
    36: "China",
    37: "Colombia",
    38: "Comoros",
    39: "Congo (Congo-Brazzaville)",
    40: "Costa Rica",
    41: "Croatia",
    42: "Cuba",
    43: "Cyprus",
    44: "Czechia (Czech Republic)",
    45: "Democratic Republic of the Congo (Congo-Kinshasa)",
    46: "Denmark",
    47: "Djibouti",
    48: "Dominica",
    49: "Dominican Republic",
    50: "Ecuador",
    51: "Egypt",
    52: "El Salvador",
    53: "Equatorial Guinea",
    54: "Eritrea",
    55: "Estonia",
    56: "Eswatini",
    57: "Ethiopia",
    58: "Fiji",
    59: "Finland",
    60: "France",
    61: "Gabon",
    62: "Gambia",
    63: "Georgia",
    64: "Germany",
    65: "Ghana",
    66: "Greece",
    67: "Grenada",
    68: "Guatemala",
    69: "Guinea",
    70: "Guinea-Bissau",
    71: "Guyana",
    72: "Haiti",
    73: "Holy See",
    74: "Honduras",
    75: "Hungary",
    76: "Iceland",
    77: "India",
    78: "Indonesia",
    79: "Iran",
    80: "Iraq",
    81: "Ireland",
    82: "Israel",
    83: "Italy",
    84: "Jamaica",
    85: "Japan",
    86: "Jordan",
    87: "Kazakhstan",
    88: "Kenya",
    89: "Kiribati",
    90: "Kuwait",
    91: "Kyrgyzstan",
    92: "Laos",
    93: "Latvia",
    94: "Lebanon",
    95: "Lesotho",
    96: "Liberia",
    97: "Libya",
    98: "Liechtenstein",
    99: "Lithuania",
    100: "Luxembourg",
    101: "Madagascar",
    102: "Malawi",
    103: "Malaysia",
    104: "Maldives",
    105: "Mali",
    106: "Malta",
    107: "Marshall Islands",
    108: "Mauritania",
    109: "Mauritius",
    110: "Mexico",
    111: "Micronesia",
    112: "Moldova",
    113: "Monaco",
    114: "Mongolia",
    115: "Montenegro",
    116: "Morocco",
    117: "Mozambique",
    118: "Myanmar (formerly Burma)",
    119: "Namibia",
    120: "Nauru",
    121: "Nepal",
    122: "Netherlands",
    123: "New Zealand",
    124: "Nicaragua",
    125: "Niger",
    126: "Nigeria",
    127: "North Korea",
    128: "North Macedonia (formerly Macedonia)",
    129: "Norway",
    130: "Oman",
    131: "Pakistan",
    132: "Palau",
    133: "Palestine State",
    134: "Panama",
    135: "Papua New Guinea",
    136: "Paraguay",
    137: "Peru",
    138: "Philippines",
    139: "Poland",
    140: "Portugal",
    141: "Qatar",
    142: "Romania",
    143: "Russia",
    144: "Rwanda",
    145: "Saint Kitts and Nevis",
    146: "Saint Lucia",
    147: "Saint Vincent and the Grenadines",
    148: "Samoa",
    149: "San Marino",
    150: "Sao Tome and Principe",
    151: "Saudi Arabia",
    152: "Senegal",
    153: "Serbia",
    154: "Seychelles",
    155: "Sierra Leone",
    156: "Singapore",
    157: "Slovakia",
    158: "Slovenia",
    159: "Solomon Islands",
    160: "Somalia",
    161: "South Africa",
    162: "South Korea",
    163: "South Sudan",
    164: "Spain",
    165: "Sri Lanka",
    166: "Sudan",
    167: "Suriname",
    168: "Sweden",
    169: "Switzerland",
    170: "Syria",
    171: "Tajikistan",
    172: "Tanzania",
    173: "Thailand",
    174: "Timor-Leste",
    175: "Togo",
    176: "Tonga",
    177: "Trinidad and Tobago",
    178: "Tunisia",
    179: "Turkey",
    180: "Turkmenistan",
    181: "Tuvalu",
    182: "Uganda",
    183: "Ukraine",
    184: "United Arab Emirates",
    185: "United Kingdom",
    186: "United States of America",
    187: "Uruguay",
    188: "Uzbekistan",
    189: "Vanuatu",
    190: "Venezuela",
    191: "Vietnam",
    192: "Yemen",
    193: "Zambia",
    194: "Zimbabwe"
    

  };
  
  // Print the entire object
  console.log("Original Object:");
  console.log(person);
  
  // Manipulate the arrays within the object
  person.currentClasses.push("Art");
  person.interests.splice(1, 1, "Gaming");
  
  // Print the entire object after manipulation
  console.log("\nObject after Manipulation:");
  console.log(person);
  
  // Perform mathematical operations
  const bmi = person.weightInKg / ((person.heightInCm / 100) ** 2);
  const nextYearAge = person.age + 1;
  
  // Print results with contextual messages
  console.log(`\nBMI (Body Mass Index): ${bmi.toFixed(2)}`);
  console.log(`Age next year: ${nextYearAge}`);
  
  // Use typeof to determine types
  console.log(`\nData Types:`);
  console.log(`- name is a ${typeof person.name}`);
  console.log(`- age is a ${typeof person.age}`);
  console.log(`- currentClasses is an ${typeof person.currentClasses}`);
  
```


    <IPython.core.display.Javascript object>

