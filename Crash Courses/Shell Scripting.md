## 1. Introduction to Shell Scripting

- **What Is a Shell?**  
    A _shell_ is a command‐line interpreter that provides an interface between you (the user) and the operating system kernel. Common shells include **Bash**, **Z-sh**, **KornShell (ksh)**, and **BusyBox ash**.
    
- **Why Script?**
    
    - Automate repetitive tasks
        
    - Glue together commands and programs
        
    - Build lightweight utilities
        
    - Configure environments and startup routines
        

---

## 2. Getting Started

### 2.1 Shebang (`#!`)

- Placed at the very top of the script:
    
    ```bash
    #!/usr/bin/env bash
    ```
    
- Tells the OS which interpreter to use.
    

### 2.2 File Permissions

- Make executable:
    
    ```bash
    chmod +x script.sh
    ```
    
- Then run by path:
    
    ```bash
    ./script.sh
    ```
    

### 2.3 Running Scripts

- **Directly** (`./script.sh`) if executable and has shebang.
    
- **Explicitly** (`bash script.sh` or `sh script.sh`).
    
- **Sourcing** (`. script.sh` or `source script.sh`) runs in current shell, not a subshell.
    

---

## 3. Basic Syntax & Structure

### 3.1 Comments

```bash
# This is a comment
```

### 3.2 Whitespace & Line Continuation

- Commands separated by newlines or `;`.
    
- Line continuation with backslash:
    
    ```bash
    echo "This is a very long command" \
         "that spans two lines"
    ```
    

### 3.3 Variables

- **Assignment (no spaces around `=`)**:
    
    ```bash
    NAME="Alice"
    COUNT=42
    ```
    
- **Access**:
    
    ```bash
    echo "$NAME"
    ```
    
- **Environment vs. Local**:
    
    ```bash
    export PATH      # makes it available to child processes
    ```
    

### 3.4 Quoting

- **Double quotes** `"..."`: allow expansion of `$vars` and command substitution.
    
- **Single quotes** `'...'`: literal, no expansion.
    
- **Backslash** `\`: escape next character.
    

### 3.5 Command Substitution

```bash
DATE=$(date +%Y-%m-%d)
# or older syntax: `date +%Y-%m-%d`
```

### 3.6 Arithmetic Expansion

```bash
SUM=$(( a + b * 2 ))
```

---

## 4. Control Structures

### 4.1 Conditional Execution

#### 4.1.1 `if` / `then` / `else`

```bash
if [ -f "$FILE" ]; then
  echo "File exists"
elif [ -d "$FILE" ]; then
  echo "It's a directory"
else
  echo "Not found"
fi
```

- `[` is a command (alias for `test`); always space‐delimited.
    
- For numeric comparisons: `-eq`, `-ne`, `-lt`, `-le`, `-gt`, `-ge`.
    
- For string comparisons: `=` or `==`, `!=`.
    
- File tests: `-f`, `-d`, `-s`, `-r`, `-w`, `-x`, etc.
    

#### 4.1.2 `case` / `esac`

```bash
case "$1" in
  start)   echo "Starting";;
  stop)    echo "Stopping";;
  restart) echo "Restarting";;
  *)       echo "Usage: $0 {start|stop|restart}"; exit 1;;
esac
```

### 4.2 Loops

#### 4.2.1 `for`

```bash
for file in *.txt; do
  echo "Processing $file"
done
```

#### 4.2.2 C-style `for`

```bash
for (( i=0; i<10; i++ )); do
  echo "$i"
done
```

#### 4.2.3 `while`

```bash
while read -r line; do
  echo "Line: $line"
done < input.txt
```

#### 4.2.4 `until`

```bash
until [ "$COUNT" -ge 5 ]; do
  echo "Count is $COUNT"
  (( COUNT++ ))
done
```

---

## 5. Functions & Modularization

```bash
function greet() {
  local name="$1"
  echo "Hello, $name!"
}

# or
greet() { 
  echo "Hi, $1"; 
}

# Call
greet "Bob"
```

- Use `local` for function‐scoped variables.
    
- Functions return an exit status (0 = success; non-zero = failure).
    

---

## 6. Arrays

```bash
# Declare
fruits=(apple banana cherry)

# Access
echo "${fruits[1]}"         # banana

# All elements
echo "${fruits[@]}"

# Length
echo "${#fruits[@]}"

# Loop
for fruit in "${fruits[@]}"; do
  echo "$fruit"
done
```

---

## 7. I/O Redirection & Pipes

### 7.1 Standard Streams

- **stdin** = fd 0
    
- **stdout** = fd 1
    
- **stderr** = fd 2
    

### 7.2 Redirection

```bash
command > out.txt       # stdout only
command 2> err.txt      # stderr only
command &> all.txt      # both stdout and stderr (Bash)
command >> append.log   # append
```

### 7.3 Here-Documents

```bash
cat <<EOF > file.txt
Line one
Line two
EOF
```

### 7.4 Here-Strings

```bash
grep "foo" <<< "$TEXT"
```

### 7.5 Pipes

```bash
ps aux | grep httpd | awk '{print $2}'
```

### 7.6 Process Substitution

```bash
diff <(sort file1) <(sort file2)
```

---

## 8. Exit Codes & Error Handling

- **Every command** returns an exit status: `$?`.
    
- **Immediate exit on error** (set -e):
    
    ```bash
    set -e
    ```
    
- **Error trapping**:
    
    ```bash
    trap 'echo "Error on line $LINENO"; exit 1' ERR
    ```
    
- **Clean-up on exit**:
    
    ```bash
    trap 'rm -f /tmp/mytemp.$$' EXIT
    ```
    

---

## 9. Shell Built-ins & Useful Commands

- `read` — read input
    
- `test` — evaluate expressions (`[` is same)
    
- `type` — locate built-ins vs. external
    
- `getopts` — parse options in a `while getopts` loop
    
- `kill`, `jobs`, `fg`, `bg` — job control
    

---

## 10. Script Debugging & Best Practices

### 10.1 Debug Modes

- **`-x`**: print each command before execution
    
    ```bash
    bash -x script.sh
    ```
    
- **`-v`**: print shell input lines as read
    

### 10.2 Linting & Style

- Use **shellcheck** (`shellcheck script.sh`).
    
- Consistent indentation (2 or 4 spaces).
    
- Quote variables (`"$var"`).
    
- Always check for unset or empty variables using `-z`/`-n`.
    
- Document functions with comments.
    

### 10.3 Portability

- Use `#!/usr/bin/env bash` instead of hard-coding `/bin/bash`.
    
- Avoid Bash-only features if targeting `/bin/sh`.
    
- Test on multiple environments.
    

---

## 11. Advanced Topics

### 11.1 Signal Handling

```bash
trap 'echo "SIGINT received"; exit 0' INT
```

### 11.2 Coprocesses (Bash 4+)

```bash
coproc myproc { long_running_cmd; }
echo "input" >&"${myproc[1]}"
read -r response <&"${myproc[0]}"
```

### 11.3 Associative Arrays (Bash 4+)

```bash
declare -A userinfo
userinfo[name]="Alice"
userinfo[uid]=1001
echo "${userinfo[name]}"
```

### 11.4 Here-Strings vs. Here-Documents

- **Here-String**: single string to stdin.
    
- **Here-Document**: multi-line block.
    

---

## 12. Performance Tips

- Prefer built-ins over external commands (`[[ ]]` vs. `grep -q`).
    
- Minimize invoking subshells.
    
- Use `read -r` instead of `cat | while`.
    
- Batch operations where possible.
    

---

## 13. Putting It All Together: Sample Script

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

# Usage: ./backup.sh /source/ /dest/
SRC=${1:-}
DST=${2:-}

if [[ -z "$SRC" || -z "$DST" ]]; then
  echo "Usage: $0 SOURCE DESTINATION"
  exit 1
fi

timestamp=$(date +%Y%m%d_%H%M%S)
archive="${DST}/backup_${timestamp}.tar.gz"

echo "Backing up $SRC to $archive..."
tar -czf "$archive" -C "$SRC" .
echo "Done."
```

- **`set -euo pipefail`**:
    
    - `-e`: exit on error
        
    - `-u`: error on unset variables
        
    - `-o pipefail`: catch failures in pipelines
        
- **`IFS`**: safe handling of word splitting
    
- Detailed checks, clear output, timestamped backups.
    

---

### That concludes your in-depth crash course on Linux shell scripting!

With these building blocks—from basics through advanced features—you’re equipped to automate, streamline, and empower your Linux workflows.