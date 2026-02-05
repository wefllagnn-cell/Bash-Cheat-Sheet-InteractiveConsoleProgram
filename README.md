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

bash
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

## ✅ This README Works 

Just say the word 👌
------------------------------------


Secure Resource Dispenser Simulator (Bash)

This project is a command‑line resource dispenser simulator written in Bash.
It demonstrates input validation, session limits, role‑based rules, dynamic constraints, modular functions, 
and continuous menu execution in a Unix shell environment.

1. Interpreter Declaration
#!/bin/bash


Tells the operating system to run this script using Bash

Ensures compatibility with Bash‑specific features like [[ ]], arrays, and regex

2. Initial Configuration Section
balance=50000
tries=0
is_local="no"
limit=10000 # Default limit

balance=50000

Represents the available resource units

Stored as an integer for arithmetic operations

tries=0

Counter used to limit authentication attempts

Prevents unlimited retries

is_local="no"

Boolean‑style flag stored as a string

Used to determine rule variations later

limit=10000

Default maximum allowable withdrawal per session

Can be dynamically changed after verification
---------
3. Secure Access Validation Loop
while [ $tries -lt 3 ]; do


Starts a loop that allows a maximum of 3 attempts

Prevents brute‑force input guessing

----------
Interface Header
echo "---------------------------------"
echo "    FILM VIEWING                 "
echo "---------------------------------"


Prints a visual banner for clarity and UX

Purely aesthetic, no logic involved

----------User Input Prompt
read -p "Enter your PIN (Format Sxxxxx#): " pin


read -p displays a prompt and stores input into variable pin

Input is read as plain text

---------
4. Format Validation Using Regex
if [[ $pin =~ ^S[0-9]{5}\#$ ]]; then

Regex Breakdown:
Component	Meaning
^	Start of string
S	Must start with capital S
[0-9]{5}	Exactly 5 digits
\#	Ends with a literal #
$	End of string

✔ Accepts only inputs like: S12345#
--------------
Successful Validation Path
echo "PIN Accepted."


Confirms successful pattern match
-----------------
5. Dynamic Profile Detection
first_digit=${pin:1:1}


Extracts the first digit after S

Uses Bash substring syntax:

${variable:start:length}
------------------
Conditional Rule Assignment
if [ $((first_digit % 2)) -eq 0 ]; then


Converts first_digit into a number

Checks if it is even

Uses arithmetic expansion $(( ))
--------------------
Even Case
is_local="yes"
limit=20000
echo "Local Bank Account Detected (Limit: PHP 20,000)"


Enables higher resource limit

Flags user as internal/privileged
---------------------
Odd Case
is_local="no"
limit=10000
echo "Other Bank Account Detected (Limit: PHP 10,000)"


Applies standard restrictions
--------------------
Exit Authentication Loop
break


Leaves the while loop once validation succeeds
------------------
6. Failed Authentication Handling
else
    echo "Invalid PIN format. Access Denied."
    tries=$((tries + 1))
fi


Displays error message

Increments attempt counter

Maximum Attempt Enforcement
if [ $tries -eq 3 ]; then
    echo "Too many attempts. Card blocked."
    exit
fi


Terminates script after 3 failed attempts

Uses exit to stop execution entirely
---------------------
7. Resource Dispensing Function
dispense_bills() {


Declares a reusable function

Keeps logic modular and readable
-----------
Parameter Handling
amount=$1


Reads the first argument passed to the function

Denomination Array
denominations=(1000 500 100)


Bash array holding allowed unit sizes

Ordered from largest to smallest

Iteration Logic
for denom in "${denominations[@]}"; do


Loops through each denomination

Quantity Calculation
bill_count=$((amount / denom))


Determines how many units of each size are needed

Conditional Output
if [ $bill_count -gt 0 ]; then
    echo "PHP $denom: $bill_count bill(s)"
fi


Prevents printing zero values

Remainder Update
amount=$((amount % denom))


Reduces remaining amount before next iteration

8. Balance Inquiry Function
check_balance() {


Encapsulates balance display logic

Conditional Fee Application
if [ "$is_local" == "no" ]; then
    balance=$((balance - 5))


Applies service cost for non‑privileged users

Output Formatting
echo "Available Balance: PHP $balance.00"


Displays updated balance

Adds .00 for readability

9. Main Control Loop
while true; do


Infinite loop

Runs until explicitly exited

Menu Display
echo "1. Withdraw Money"
echo "2. Balance Inquiry"
echo "3. Exit"


Presents available actions

User Selection Input
read -p "Select option: " choice

10. Option Handling via Case Statement
case $choice in


Cleaner alternative to multiple if statements

11. Resource Withdrawal Flow
Input Validation
if [[ ! "$amount" =~ ^[0-9]+$ ]] || [ $((amount % 100)) -ne 0 ]; then


Ensures numeric input

Enforces denomination compatibility

Limit Enforcement
if [ $amount -gt $limit ]; then


Prevents exceeding profile‑based limit

Balance Check
if [ $amount -gt $balance ]; then


Blocks over‑allocation

Transaction Execution
dispense_bills $amount
balance=$((balance - amount))


Calls dispensing function

Updates remaining balance

Conditional Service Charge
if [ "$is_local" == "no" ]; then
    balance=$((balance - 18))


Applies additional processing cost

12. Session Termination
echo "Thank you for using our ATM. Goodbye!"
break


Gracefully exits the main loop

13. Invalid Input Handling
*)
    echo "Invalid selection."
;;


Catches any unsupported menu input
