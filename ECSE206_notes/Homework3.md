# Comp 206 - Homework 3: file renaming with Bash

In this assignment, you'll be writing a script to rename files in a given directory.

****Your task**** is to create a script called `rename` to be used in the following way:

* `./rename <directory>` -- prepends the current date in `YYYY-MM-DD-` format
  to every file in the given directory, unless the filename already starts with a date.


The script should check whether a filename already starts with a date in the
format `YYYY-MM-DD-` and skip those files.

## Assumptions 

* Only prepend the date once.

* Skip files that already start with a date.

* Keep files in the same directory after renaming.

## Remarks  

The directory that you should be running the script on is called `dummy_data`.

You're given some starter code in the file `rename`. In particular, it contains

a helper function which checks whether a filename starts with the previously

mentioned date format.

****When testing your code locally,**** you should make a copy of the `dummy_data`

first, or else you'll need to go back and rename the files manually when you

want to test again later.

```bash
#!/bin/bash

# usage: start_wih_date()  <filename>

# returns 0 if <filename> starts with YYYY-MM-DD else 1

start_with_date() {
        local input="$1"
        if [[ "$input" =~ ^[0-9]{4}-[0-9]{2}-[0-9]{2}- ]] ; then
                return 0
        else
                return 1
        fi
}

directory="$1"

today=$(date +%Y-%m-%d)

for file in "$directory"/*; do  

        filename=$(basename "$file")

        if start_with_date "$filename"; then
  
                echo "Skipping" > /dev/null 2>&1
        else
                mv "$file" "$directory/${today}-${filename}"
        fi
done
```