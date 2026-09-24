by using a pipe, we can fee the output of a command to such a while loop, enabling us to loop over the lines of output produced by a program
```bash
ls | while read -r file; do
#Read without escape the next line input from the output of `ls` and store in variable file
	if [ -d "file" ]; then
		echo "Is a directory: $file"
	else
		echo "Is not a directory: $file"
	fi
done
```

This program asks the user if hey want to proceed before either doing the thing or exiting
```bash
read -p "Are you sure? [y/N] " answer
if ["$answer" != "y"]; then
	exit 0
fi
```

shift example
```bash
while [ $# -gt 0 ]; do
	echo "$1"
	shift # shift $2 up and so on
		  # it will also remove the argument everytime
done
```

Evaluating arithmetic expressions
```bash
echo $((5+3))

result=$(($1+$2))

echo $((var++)) #post increment
```

```bash
i=1
weekdays="Mon Tue Wed Thu Fri"
for day in $weekdays
do
	echo "Weekday $((i++)): $day"
done
```

Case statement
```bash
animal=$1
case $animal in
	cat)
		echo "You entered 'cat'"
	;;
	
```

Functions: use like command 
- `local` defines local variables otherwise the variables are global by default even defined in a function
- returns an exit status, cannot return a value

Text stream processing commands