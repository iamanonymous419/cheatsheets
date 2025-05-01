# Shell Scripting Cheatsheet (Linux)

Shell scripting allows you to automate tasks in a Unix/Linux system using command-line programs. This cheatsheet covers key concepts, syntax, and commands.

---

## What is SHELL?

- **S** - Shell (Command interpreter)
- **H** - Hardware access through kernel
- **E** - Execution of user commands
- **L** - Linux/Unix OS
- **L** - Layer between user and OS

---

## Types of Shells

| Shell       | Path         | Description                  |
|-------------|--------------|------------------------------|
| sh          | /bin/sh      | Bourne Shell                 |
| bash        | /bin/bash    | Bourne Again Shell (most common) |
| csh         | /bin/csh     | C Shell                      |
| ksh         | /bin/ksh     | Korn Shell                   |
| fish        | /usr/bin/fish| Friendly Interactive Shell   |

---

## Writing Your First Shell Script

1. Create a file with `.sh` extension:
   ```bash
   vim hello.sh
   ```

2. Start with shebang:
   ```bash
   #!/bin/bash
   ```

3. Add your script content.

4. Save and exit:
   - Press `i` to insert
   - Press `ESC`
   - Type `:wq` to save & quit

---

## Running a Shell Script

```bash
chmod +x hello.sh     # Make it executable
./hello.sh            # Execute script
bash hello.sh         # OR run it using bash
```

---

## File to View Users
```bash
cat /etc/passwd      # Shows all system users
```

---

## Variables

```bash
name="Steve"
echo "My name is $name"
```

- No space before/after `=`
- Use `$` to access value

### Environment Variables
```bash
echo $HOME
echo $USER
```

---

## Arguments (Like Function Parameters)

```bash
echo "Script Name: $0"
echo "First Argument: $1"
echo "All Arguments: $@"
echo "Total Arguments: $#"
```

---

## Conditional Statements

```bash
if [ "$name" == "Steve" ]; then
  echo "Welcome Steve"
elif [ "$name" == "Admin" ]; then
  echo "Welcome Admin"
else
  echo "Access Denied"
fi
```

### Test Expressions
- `[ -f file ]` – file exists
- `[ -d dir ]` – directory exists
- `[ -z $var ]` – variable is empty
- `[ $a -eq $b ]` – numeric equality

---

## Loops

### For Loop
```bash
for i in 1 2 3
do
  echo "Number: $i"
done
```

### While Loop
```bash
count=1
while [ $count -le 5 ]
do
  echo "Count: $count"
  ((count++))
done
```

### Until Loop
```bash
count=1
until [ $count -gt 5 ]
do
  echo "Count: $count"
  ((count++))
done
```

---

## Functions

```bash
greet() {
  local name=$1
  echo "Hello $name"
}
greet "Steve"
```

- Use `local` to limit scope to function
- Functions can be declared anywhere in the script

---

## Makefile Integration

- Shell scripts can be run via `Makefile`:
```make
all:
	bash hello.sh
```
Run with:
```bash
make
```

---

## File Handling

### Reading a File Line by Line
```bash
while IFS= read -r line; do
  echo "$line"
done < file.txt
```

### Writing to a File
```bash
echo "Hello World" > output.txt
```

### Appending to a File
```bash
echo "Another Line" >> output.txt
```

---

## Scheduling Jobs with Cron

Edit crontab:
```bash
crontab -e
```
Example job:
```bash
0 * * * * /home/user/script.sh   # Run every hour
```

---

## Debugging Scripts

```bash
bash -x script.sh     # Trace execution
set -e                # Exit on error
```

---

## Useful Commands

| Command             | Description                        |
|---------------------|------------------------------------|
| `echo`              | Print text                         |
| `read`              | Get user input                     |
| `pwd`               | Print current directory            |
| `ls`                | List directory contents            |
| `cd`                | Change directory                   |
| `cat filename`      | View file contents                 |
| `touch file.sh`     | Create new file                    |
| `chmod +x file.sh`  | Make file executable               |

---

## Tips

- Always use `#!/bin/bash` at the top of bash scripts
- Keep your scripts modular and commented
- Use `set -e` to make scripts exit on error
- Use `trap` to catch signals and clean up

```bash
trap "echo 'Script interrupted'; exit" SIGINT
```

---

## Conclusion

Shell scripting is powerful for automation, task scheduling, and system management. With practice, you can streamline many repetitive tasks in your Linux workflow.

