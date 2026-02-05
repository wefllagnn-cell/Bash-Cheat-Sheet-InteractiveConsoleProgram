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
