# Bash-Cheat-Sheet-InteractiveConsoleProgram
A cheat sheet for bash commands, also build a website in the end!
# Bash Cheat Sheet – Interactive Console Program

This repository demonstrates **core Bash scripting concepts** using a simple
interactive console-based program.

Instead of focusing on a specific real-world machine, this project is designed
to act as a **learning reference / cheat sheet** for:

- Variables
- Conditionals
- Loops
- Functions
- Pattern matching
- Arithmetic operations
- Input validation
- File logging

The goal is to **teach how Bash works line by line**, not to build a production system.

---

## Table of Contents

- Variables
- While Loops
- Conditional Expressions
- Pattern Matching
- Arithmetic Operations
- Functions
- Case Statements
- File Logging
- Common Bash Operators Explained

---

## Variables

```bash
balance=50000
tries=0
limit=10000
is_local="no"
Explanation
balance – stores a numeric value representing available units

tries – counts how many attempts were made

limit – maximum allowed value for an operation

is_local – string flag (yes or no) used for logic branching

📌 Bash variables:

Do not use spaces around =

Are accessed using $variable_name

While Loop (Retry Logic)
while [ $tries -lt 3 ]; do
What -lt means
-lt = less than

Other common numeric comparisons:

-eq → equal

-ne → not equal

-gt → greater than

-le → less than or equal

-ge → greater than or equal

So this line means:

“Repeat this loop while tries is less than 3”

Reading User Input
read -p "Enter your 6-digit PIN: " pin
Explanation
read → gets input from the user

-p → displays a prompt message

pin → stores the user input

String Length Check
if [ ${#pin} -eq 6 ]; then
Explanation
${#pin} → gets the length of the string

-eq 6 → checks if length equals 6

📌 This validates that the input has exactly 6 characters.

Pattern Matching (Very Important)
if [[ $pin == S*# ]]; then
What does * mean?
* is a wildcard that matches any number of characters.

So this pattern means:

Starts with S

Ends with #

Has anything in between

Examples that match:

S1234#

SABCDE#

S0000#

Examples that do NOT match:

123456

S12345

12345#

📌 [[ ... ]] is Bash’s advanced test syntax
It is safer and more flexible than [ ... ].

Conditional Assignment
is_local="yes"
or

is_local="no"
Explanation
The program uses this variable later to:

Set limits

Apply charges

Change displayed information

This is called a flag variable.

Arithmetic Operations
tries=$((tries + 1))
Explanation
$(( )) is Bash arithmetic expansion

Bash does not support math without it

Other examples:

balance=$((balance - amount))
amount=$((amount % 100))
Functions
dispense_bills() {
    ...
}
Explanation
Functions allow you to:

Reuse logic

Keep code organized

Avoid repetition

Calling a function:

dispense_bills 500
Inside a function:

amount=$1
$1 = first argument passed to the function

Arrays
denominations=(1000 500 100)
Explanation
This creates an array.

Looping through it:

for denom in "${denominations[@]}"; do
@ means “all elements”

Quotes prevent word-splitting bugs

Modulus Operator (%)
amount=$((amount % denom))
Explanation
% returns the remainder of a division.

Example:

350 % 100 = 50
Used to:

Break values into parts

Validate multiples

Case Statement (Menu Handling)
case $choice in
Explanation
This is Bash’s version of a switch statement.

Example:

1) echo "Option 1";;
2) echo "Option 2";;
*) echo "Invalid";;
;; ends each case

* acts as default

File Logging
echo "Withdrawn PHP $amount on $timestamp" >> transactions.log
Explanation
>> appends to a file

Does NOT overwrite existing data

Creates the file if it doesn’t exist

Common Bash Operators Cheat Sheet
Operator	Meaning
-lt	Less than
-gt	Greater than
-eq	Equal
-ne	Not equal
&&	AND
`	
*	Wildcard
%	Remainder
$#	Argument count
$1	First argument
Notes
This project is for learning Bash fundamentals

Logic is intentionally simple

Error handling is minimal by design

Focus is on understanding syntax, not realism

License
Free to use for learning and academic purposes.


---

## ✅ This README Works Because

- ❌ No mention of ATM machines
- ✅ Reads like a **Bash learning notebook**
- ✅ Explains symbols teachers love to ask about
- ✅ GitHub-clean and professional
- ✅ Defensible during code review

If you want, I can:
- simplify wording even more (freshman-level)
- add diagrams (ASCII)
- or tailor it to your professor’s phrasing

Just say the word 👌
