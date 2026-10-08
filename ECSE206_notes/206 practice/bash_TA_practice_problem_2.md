<!-- Written by TA Sabrina -->
Practice Question: 

A developer wants to create a basic calculator using Bash. This calculator should support four basic operations: addition, subtraction, multiplication, and division. It will take in as input 4 arguments: 2 integers, a string , and a boolean. The integers represent the numbers used to perform the operation, in that order. The string indicates if the operation is "add", "sub", "mult", or "div". For example, if this calculator is run as "./basic-calculator 2 1 'div' False", the calculator should print the result of 2 divided by 1.

This calculator should take into account certain edge-cases: 
- Division by zero: if the user attempts to divide any number by zero, exit with an error code 1
- Unsupported operation: if the user attempts to provide an operation other than the four listed, exit with an error code 2

It is also possible that the user will want to save their calculation and its results. This program also takes as input a fourth variable which will be a True/False Boolean. If it is True, the program should create a file in the directory "~/results" and write the results of the calculation into this file as a string. If the directory does not exist, the program should create it. 

The result files in this directory should be saved in sequential order, starting from 1, in the format "results-1", based on the number of files already present in the results directory. For example, if it is the first file saved in the directory, it should be named "results-1". If it there is already one file present in the directory, it should be named "results-2". The program should do this by using a for loop to loop through every file in the directory to count them.

The program should write the operation in the file in the format "2 / 1 = 2". It should do this by redirecting the output of the basic command "echo" into the results file.

```bash
num1=$1 
num2=$2 
op=$3 
save=$4 
# Pick the operation (exit 2 on unsupported operation, exit 1 on division by zero) 
case "$op" in 
	add) symbol="+"; result=$((num1 + num2)) ;; 
	sub) symbol="-"; result=$((num1 - num2)) ;; 
	mult) symbol="*"; result=$((num1 * num2)) ;; 
	div) 
		if [ "$num2" -eq 0 ]; then 
			echo "Error: division by zero" >&2 
			exit 1 
		fi 
		symbol="/" 
		result=$((num1 / num2)) 
	;; 
	*) 
		echo "Error: unsupported operation '$op'" >&2 
		exit 2 
	;; 
esac 

echo "$result" 

# Optionally save the calculation 
if [ "$save" = "True" ]; then 
	dir="$HOME/results" 
	mkdir -p "$dir" # Count existing files with a for loop 
	count=0 
	for file in "$dir"/*; do 
		if [ -f "$file" ]; then
			count=$((count + 1))
		fi 
	done 
	echo "$num1 $symbol $num2 = $result" > "$dir/results-$((count + 1))" 
fi
```