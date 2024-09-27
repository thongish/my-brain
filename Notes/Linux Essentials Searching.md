#LINUX/W3 

# File globbing

| wildcard | matches                 | example               | explanation                  |
| -------- | ----------------------- | --------------------- | ---------------------------- |
| ?        | A single character      | `{bash}ls b?b.txt`    | matches bob.txt and bab.txt  |
| *        | Zero or more characters | `{bash}ls bo*.txt`    | matches bob.txt and both.txt |
| \[ ]     | Letters inside bracket  | `{bash}ls [bs]ob.txt` | matches bob.txt and sob.txt  |
- Brackets may also contain ranges:
	- `[a-z]` - matches lowercase alphabetic letters
	- `[0-9]` - matches numbers 0 through 9
	- `[0-9t]` - matches numbers 0 through 0 and the letter 't'

# Find

- `{bash}find` will find directory entries matching criteria
- Can specify by name, date, size, type, and more

![[Pasted image 20240926205540.png]]

![[Pasted image 20240926205935.png]]

# Regular expressions

![[Pasted image 20240926213513.png]]

| \[:alnum:] | Alphanumeric characters, similar to \[0-9A-Za-z] but also includes letters from Locale |
| ---------- | -------------------------------------------------------------------------------------- |
| \[:alpha:] | Alphabetic characters, same as \[A-Za-z]                                               |
| \[:blank:] | Space and tab                                                                          |
| \[:digit:] | Digits, same as \[0-9]                                                                 |
| \[:lower:] | Lowercase letters, same as \[a-z]                                                      |
| \[:upper:] | Uppercase letters, same as \[A-Z]                                                      |
| and more   |                                                                                        |
![[Pasted image 20240926224359.png]]

## Examples

- Match any line where at the beginning of a line is any letter followed by an "o" and has at least one more letter in the line
```
# greetings.txt
Joe, goodday.txt
Sally, remember.txt
Bob, goodjob.txt
Mary, promotion.txt
```
```bash
# grepping
grep "^.o." greetings.txt
Joe, goodday.txt
Bob, goodjob.txt
```

- Match any line where there are zero or more alphabetic characters followed by a comma (notice the comment lines don't match)
	- Comments are not alphanumeric characters
```
# greetings.txt
# This is a simple greetings list with
# comma separated lists of:
# <name> <filename>
Joe, goodday.txt
Sally, remember.txt
Bob, goodjob.txt
Mary, promotion.txt
```
```bash
# grepping
grep "[[:alpha:]]*," greetings.txt
Joe, goodday.txt
Sally, remember.txt
Bob, goodjob.txt
Mary, promotion.txt
```

# Grep

- Used to search for strings by patterns called regular expressions
- Stands for Global Regular Expression and Print

![[Pasted image 20240926225521.png]]

| option   | meaning                                                      |
| -------- | ------------------------------------------------------------ |
| -r       | recursive - search whole directory tree (don't follow links) |
| -R       | recursive - search whole directory tree (follow links)       |
| -i       | ignore case of text                                          |
| -n       | print line numbers                                           |
| -v       | invert match - print lines that do not match                 |
| and more |                                                              |
![[Pasted image 20240926225818.png]]

# Find and grep together

![[Pasted image 20240926230345.png]]