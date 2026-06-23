# JavaScript Fundamentals for Web Application Security

## Overview

JavaScript (JS) is one of the core technologies of web development, alongside HTML and CSS. HTML provides the structure of a webpage, CSS controls its appearance, and JavaScript adds interactivity and dynamic behavior.

As a cybersecurity student or penetration tester, understanding JavaScript is important because modern web applications heavily rely on it. Many web vulnerabilities such as Cross-Site Scripting (XSS), insecure client-side validation, exposed API keys, and authentication bypasses involve JavaScript.

   

# Variables

Variables are containers used to store data values. They allow developers to save information and reuse it throughout a program.

Think of a variable as a labeled box:

* The box stores data.
* The label (variable name) helps us access the data later.

## Variable Types

JavaScript provides three ways to declare variables:

### var

```javascript
var username = "Sai";
```

**Characteristics:**

* Function-scoped
* Can be redeclared
* Can be reassigned

### let

```javascript
let age = 23;
```

**Characteristics:**

* Block-scoped
* Cannot be redeclared in the same scope
* Can be reassigned

### const

```javascript
const country = "India";
```

**Characteristics:**

* Block-scoped
* Cannot be redeclared
* Cannot be reassigned

## Comparison Table

| Feature            | var      | let   | const |
| ------------------ | -------- | ----- | ----- |
| Scope              | Function | Block | Block |
| Reassign Value     | Yes      | Yes   | No    |
| Redeclare Variable | Yes      | No    | No    |

 

# Data Types

Data types define the kind of value stored inside a variable.

## String

Stores text values.

```javascript
let name = "Jadhav";
```
 

## Number

Stores numeric values.

```javascript
let age = 23;
```

 

## Boolean

Stores either true or false.

```javascript
let isStudent = true;
```

 

## Null

Represents an intentional empty value.

```javascript
let value = null;
```

 

## Undefined

A variable declared without a value.

```javascript
let data;
```

 

## Object

Stores collections of related data.

```javascript
let person = {
    name: "Sai",
    age: 23
};
```

 

## Array

Stores multiple values.

```javascript
let numbers = [10, 20, 30];
```

 

# Functions

A function is a reusable block of code designed to perform a specific task.

Instead of writing the same code repeatedly, developers create functions and call them whenever needed.

## Function Syntax

```javascript
function functionName(parameters) {
    // code
}
```

## Example

```javascript
function greet(name) {
    console.log("Hello " + name);
}

greet("Sai");
```

### Output

```text
Hello Sai
```

 

# Practical Example: Student Result System

```javascript
function PrintResult(rollNum) {
    alert("Student with Roll Number " + rollNum + " has passed.");
}

PrintResult(101);
```

### Explanation

1. Function `PrintResult()` is created.
2. It accepts a roll number as input.
3. An alert message is displayed.
4. Function can be reused for any student.

 

# Loops

Loops execute a block of code repeatedly.

Instead of writing the same statement multiple times, loops automate repetition.

---

## For Loop

Most commonly used loop.

```javascript
for(let i = 1; i <= 5; i++) {
    console.log(i);
}
```

### Output

```text
1
2
3
4
5
```

 

## While Loop

Executes as long as the condition remains true.

```javascript
let i = 1;

while(i <= 5) {
    console.log(i);
    i++;
}
```

 

## Do While Loop

Runs at least once before checking the condition.

```javascript
let i = 1;

do {
    console.log(i);
    i++;
}
while(i <= 5);
```

 

# Request-Response Cycle

Web applications operate using a request-response model.

## Process

### Step 1

User visits a website.

### Step 2

Browser sends a request to the server.

### Step 3

Server processes the request.

### Step 4

Server sends a response.

### Step 5

Browser displays the webpage.

## Diagram

```text
User
 ↓
Browser
 ↓
Request
 ↓
Web Server
 ↓
Response
 ↓
Browser
 ↓
User
```

 

# First JavaScript Program

```javascript
console.log("Hello, World!");
```

### Output

```text
Hello, World!
```

 

# Running JavaScript in Google Chrome

## Method 1

Press:

```text
Ctrl + Shift + I
```

Then select:

```text
Console
```
 

## Example Program

```javascript
let x = 5;
let y = 10;

let result = x + y;

console.log("The result is: " + result);
```

### Output

```text
The result is: 15
```

 

# Internal JavaScript

Internal JavaScript is written directly inside an HTML document using the `<script>` tag.

## Example

```html
<!DOCTYPE html>
<html>
<body>

<p id="result"></p>

<script>
let x = 5;
let y = 10;

document.getElementById("result").innerHTML =
"The result is: " + (x + y);
</script>

</body>
</html>
```

## Advantages

* Easy for beginners
* Suitable for small projects

## Disadvantages

* Difficult to maintain large applications
* HTML becomes cluttered

 

# External JavaScript

External JavaScript stores code in a separate `.js` file.

## script.js

```javascript
let x = 5;
let y = 10;

document.getElementById("result").innerHTML =
"The result is: " + (x + y);
```

## external.html

```html
<script src="script.js"></script>
```

## Advantages

* Cleaner code structure
* Easy maintenance
* Reusable across multiple pages

 

# Identifying Internal and External JavaScript

## Internal JavaScript

```html
<script>
alert("Hello");
</script>
```

## External JavaScript

```html
<script src="script.js"></script>
```

## Verification

1. Open webpage
2. Right-click
3. Select **View Page Source**
4. Inspect `<script>` tags
 

# JavaScript Dialog Boxes

JavaScript provides built-in functions for user interaction.

 

## Alert

Displays a message box.

```javascript
alert("Hello THM");
```

### Purpose

* Notifications
* Warnings
* Information messages

 

## Prompt

Collects user input.

```javascript
let username = prompt("Enter your name");
```

### Example

```javascript
alert("Hello " + username);
```

 

## Confirm

Asks for confirmation.

```javascript
confirm("Do you want to continue?");
```

### Return Values

```javascript
true
```

or

```javascript
false
```

 

# Security Risk: Alert Abuse

Malicious JavaScript can repeatedly display alert boxes.

## Example

```javascript
for(let i = 0; i < 3; i++) {
    alert("Hacked");
}
```

### Result

User must repeatedly close popup windows.

If changed to:

```javascript
for(let i = 0; i < 500; i++)
```

The browser experience becomes extremely disruptive.

## Lesson Learned

Never execute JavaScript files from untrusted sources.

 

# Conditional Statements

Conditional statements allow programs to make decisions.

## If-Else Example

```javascript
let age = prompt("Enter your age");

if(age >= 18) {
    document.write("You are an adult.");
}
else {
    document.write("You are a minor.");
}
```

### Output

```text
Age = 20 → Adult
Age = 15 → Minor
```

 

# JavaScript Minification

Minification reduces file size by removing:

* Spaces
* Comments
* Tabs
* Line breaks

## Original Code

```javascript
function hi() {
    alert("Welcome");
}
```

## Minified Code

```javascript
function hi(){alert("Welcome")}
```

## Benefits

* Faster loading
* Smaller files
* Better performance

 

# JavaScript Obfuscation

Obfuscation intentionally makes code difficult for humans to understand.

## Original Code

```javascript
function hi() {
    alert("Welcome to THM");
}
hi();
```

## Obfuscated Code

```javascript
(function(_0x1234){
...
})();
```

## Benefits

* Hides business logic
* Makes reverse engineering harder
* Increases effort for attackers

 

# JavaScript Obfuscation Tool

Tool:

https://codebeautify.org/javascript-obfuscator

## Purpose

* Minify JavaScript
* Obfuscate JavaScript
* Protect production code

 

# JavaScript Deobfuscation Tool

Tool:

https://obf-io.deobfuscate.io/

## Purpose

* Convert obfuscated code into readable form
* Analyze suspicious scripts
* Assist during penetration testing

 

# Security Best Practices

## 1. Avoid Client-Side Validation Only

### Bad Practice

```javascript
if(password == "admin123")
{
    login();
}
```

Attackers can modify browser-side JavaScript.

### Recommendation

Always perform validation on the server.

 

## 2. Use Trusted Libraries

Before including a JavaScript library:

* Verify the source
* Verify integrity
* Download from official vendors

 

## 3. Never Hardcode Secrets

### Bad Example

```javascript
const apiKey = "pk_TryHackMe-1337";
```

Anyone can view page source and steal the key.

### Recommendation

Store secrets on the server.

 

## 4. Minify and Obfuscate Production Code

Benefits:

* Smaller files
* Faster loading
* Increased difficulty for attackers

 

