Kevin Pham - A01026954
Noah Thomson - A01276533
Angad Bains - A01371850

```bash
#!/usr/bin/env bash

# Function to handle errors
err() {
        #Handle error message logic here
        exit 1
}

# Check if directory argument is provided
if [[ $# -ne 1 ]]; then
        err"Please provide a directory path as an argument."
fi

# Check if the argument given is a valid directory
if [[ ! -d $1 ]]; then
        err"Not a valid directory."
else

# Creates our counter variables
declare -i txtfiles=0
declare -i otherfiles=0

# Iterates through all the files in the given path argument.
# The iteration ignores all files starting with '.'
for file in $(find $1 -not -path '*/.*'); do
        # extn grabs the extension of the filename if it has one
        extn="${file##*.}"

        case "$extn" in

                # If the file extension is .txt, increment txtfiles
                "txt")
                        txtfiles+=1
                        ;;

                # If the file extension is anything but .txt, increment otherfiles
                *)
                        otherfiles+=1
                        ;;
        esac
done

echo "There are $txtfiles .txt files and $otherfiles other files in this directory."

fi
```