#### Positional variables
- e.g. if we run `./script 5 2 bob`
- From the script we access using $1, $2, $3

#### Quotes
- single quotes are use to preserve the literal value of characters within the quotes
- double quotes are used to preserve the literal values of characters within the quotes
	- exceptions: $ (positional variables still get expanded), ', \
- e.g. `mkdir "John Smith"` --> a directory called John Smith
- otherwise two directories John and Smith