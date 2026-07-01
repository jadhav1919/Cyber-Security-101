# CyberChef - Beginner Notes

## What is CyberChef?

**CyberChef** is a **free, web-based tool** that helps perform many cybersecurity-related operations on data without writing code.

It is often called the **"Cyber Swiss Army Knife"** because it contains hundreds of tools in one place.

CyberChef is commonly used by:

* Security Analysts
* Penetration Testers
* DFIR Analysts
* SOC Analysts
* Malware Analysts
* CTF Players

# Why Use CyberChef?

Instead of writing scripts, CyberChef lets you:

* Encode and decode data
* Encrypt and decrypt text
* Convert data formats
* Analyze files
* Work with hashes
* Extract information
* Manipulate text

All through a simple drag-and-drop interface.

# Main Components of CyberChef

CyberChef has **4 main areas**:

```text
+-----------------------+
| Operations            |
+-----------------------+

+-----------------------+
| Recipe                |
+-----------------------+

+-----------------------+
| Input                 |
+-----------------------+

+-----------------------+
| Output                |
+-----------------------+
```

# 1. Operations Area

The **Operations** panel contains all available tools.

Operations are grouped into categories and can also be searched.

Examples include:

* Base64
* XOR
* ROT13
* URL Encode
* URL Decode
* Hex
* AES
* RSA
* Hashing
* Compression
* File Operations

Simply search for an operation and drag it into the Recipe area.


## Common Operations

| Operation       | Purpose                                    | Example                             |
| --------------- | ------------------------------------------ | ----------------------------------- |
| From Morse Code | Decode Morse code                          | `.... . .-.. .-.. ---` → `HELLO`    |
| URL Encode      | Convert special characters into URL format | `https://example.com` → Encoded URL |
| To Base64       | Encode text to Base64                      | `Hello` → `SGVsbG8=`                |
| From Base64     | Decode Base64 text                         | `SGVsbG8=` → `Hello`                |
| To Hex          | Convert text to hexadecimal                | `ABC` → `41 42 43`                  |
| From Hex        | Convert hexadecimal to text                | `41 42 43` → `ABC`                  |
| To Decimal      | Convert characters into decimal values     | `ABC` → `65 66 67`                  |
| ROT13           | Caesar cipher (+13 shift)                  | `Hello` → `Uryyb`                   |


# 2. Recipe Area

The **Recipe** is the heart of CyberChef.

A recipe is simply a **sequence of operations**.

Example:

```text
Input
   │
   ▼
From Base64
   │
   ▼
From Hex
   │
   ▼
ROT13
   │
   ▼
Output
```

CyberChef performs each operation **from top to bottom**.


## Recipe Features

### Save Recipe

Save frequently used recipes.


### Load Recipe

Open previously saved recipes.

### Clear Recipe

Remove all operations.


### BAKE!

Processes the input using the current recipe.


### Auto Bake

Automatically updates the output whenever the input changes.

Recommended for most tasks.


# 3. Input Area

The **Input** panel is where data is entered.

You can:

* Type text
* Paste text
* Upload a file
* Upload a folder


## Input Features

### New Input Tab

Create another input tab.

Useful for working with multiple inputs.


### Open File

Upload a file.

### Open Folder

Upload an entire folder.


### Clear Input

Removes both input and output.


### Reset Layout

Restores the default interface layout.


# 4. Output Area

The **Output** panel displays the processed result.


## Output Features

### Save Output

Save results to a file.


### Copy Output

Copy processed data to the clipboard.

### Replace Input

Replace the original input with the output.

Useful when applying multiple transformations.

### Maximize Output

Expand the output panel for easier viewing.

----------





