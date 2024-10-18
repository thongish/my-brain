
Kevin Pham - A01026954
Matilda Kim - A01390906

### Q1.

```bash
if [[ -d ~/bin ]]; then
	PATH=$HOME/bin:$PATH
fi
```
### Q2.

```bash
name="Kevin"

echo "Hello, ${name}!"
```
### Q3.

```bash
echo "Hello, ${1}!"
```
### Q4.

```bash
if [[ ! $# -gt 0 ]]; then
  echo "You need to provide a positional parameter"
  exit 1
else
  echo "Hello, ${1}!"
fi
```
### Q5.

```bash
if [[ ! $# -gt 0 ]]; then
  echo "You need to provide a positional parameter"
  exit 1
else
  for name in $@
  do
    if [[ ${#name} -gt 3 ]]; then
      echo "Hello, ${name}"
    else
      echo "Hi, ${name}"
    fi
  done
fi
```
### Q6.

```bash
for file in $(find -type f)
do
  if [[ ${file} =~ [0-9] ]]; then
    echo ${file}
  fi
done
```


