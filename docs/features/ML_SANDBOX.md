# ML Sandbox

Execute Python, JavaScript, Java, and C/C++ code with instant feedback. Perfect for learning, experimentation, and testing algorithms.

---

## 🧪 What Is the ML Sandbox?

The **ML Sandbox** is an integrated code execution environment that lets you:

- ✍️ **Write code** in a professional IDE (CodeMirror)
- ▶️ **Execute instantly** - see results in seconds
- 📊 **Visualize output** - charts, tables, formatted results
- 🐛 **Debug easily** - clear error messages and stack traces
- 💾 **Save & share** - copy code snippets, share with others

No installation needed. All code runs securely on servers.

---

## 🚀 Getting Started

### 1. Open the Sandbox

From the dashboard, click **"Code Sandbox"** or **"ML Sandbox"**

### 2. Select Your Language

```
┌────────────────────────────────┐
│ Choose Language:               │
│ ○ Python                       │
│ ○ JavaScript                   │
│ ○ Java                         │
│ ○ C/C++                        │
└────────────────────────────────┘
```

### 3. Write Code

```python
# Example: Calculate statistics
import numpy as np

data = [1, 2, 3, 4, 5, 10, 20, 50]
mean = np.mean(data)
median = np.median(data)
std = np.std(data)

print(f"Mean: {mean:.2f}")
print(f"Median: {median:.2f}")
print(f"Std Dev: {std:.2f}")
```

### 4. Execute

Click **[RUN]** button or press `Ctrl+Enter`

### 5. See Results

```
Output:
Mean: 11.13
Median: 7.50
Std Dev: 15.29

Execution: 0.23s | Memory: 12 MB
```

---

## 💻 Supported Languages

### Python 3.10

**Perfect for:** Machine Learning, Data Science, Algorithms

```python
# Libraries available:
import numpy as np        # NumPy
import pandas as pd       # Pandas
import matplotlib.pyplot as plt  # Plotting
import requests           # HTTP requests
import json              # JSON parsing
# ... and 100+ more
```

**Features:**
- Full standard library
- Popular ML/DS packages
- File I/O capability
- Multi-file support (imports)

**Limits:**
- 5-second execution timeout
- 256 MB memory
- No file persistence between sessions

### JavaScript (Node.js 18)

**Perfect for:** Algorithms, Web development, Quick scripts

```javascript
// Client-side (browser) execution for instant feedback
// Full ES2020+ support
const arr = [1, 2, 3, 4, 5];
const sum = arr.reduce((a, b) => a + b, 0);
console.log(`Sum: ${sum}`);
// Output: Sum: 15
```

**Features:**
- Runs directly in browser (instant execution)
- No network latency
- Full ES2020+ syntax
- CommonJS & ES6 modules

**Libraries available:**
- Lodash, Moment, axios, and more

### Java 17

**Perfect for:** Data structures, Algorithms, OOP concepts

```java
public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5};
        int sum = 0;
        for (int num : arr) {
            sum += num;
        }
        System.out.println("Sum: " + sum);
    }
}
// Output: Sum: 15
```

**Features:**
- Full Java standard library
- Automatic compilation
- Classes, generics, streams supported
- JUnit for testing

### C/C++ (GCC 11)

**Perfect for:** Performance-critical code, Systems programming

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> arr = {1, 2, 3, 4, 5};
    int sum = 0;
    for (int num : arr) {
        sum += num;
    }
    std::cout << "Sum: " << sum << std::endl;
    return 0;
}
// Output: Sum: 15
```

**Features:**
- `-std=c++17` compilation
- STL (Standard Template Library)
- Optimization flags available
- Fast execution

---

## 📊 Features

### Live Code Editing

```
┌────────────────────────────────────┐
│ Editor (with syntax highlighting) │
│                                    │
│ 1  import numpy as np              │
│ 2  arr = np.array([1,2,3])        │
│ 3  print(arr.mean())              │
│                                    │
│    [▮ Python  Dark theme ▼]       │
│    [RUN]  [SAVE]  [SHARE]        │
└────────────────────────────────────┘
```

**Features:**
- Real-time syntax highlighting
- Auto-indentation
- Line numbers
- Keyboard shortcuts (Ctrl+A, Ctrl+C, etc.)
- Undo/redo support

### Instant Execution

Click **[RUN]** and see results in seconds:

```
┌────────────────────────────────────┐
│ Output                             │
├────────────────────────────────────┤
│ Mean: 11.13                        │
│ Median: 7.50                       │
│ Std Dev: 15.29                     │
│                                    │
│ ⏱️ Execution: 0.23 seconds         │
│ 💾 Memory: 12 MB                   │
│ ✅ Status: Success                 │
└────────────────────────────────────┘
```

### Input Handling

Provide stdin for interactive programs:

```python
# Code:
name = input("Enter your name: ")
print(f"Hello, {name}!")

# Input:
Enter your name: Alice

# Output:
Hello, Alice!
```

### Error Reporting

Clear, helpful error messages:

```
❌ RUNTIME ERROR

File "main.py", line 5
    print(undefined_var)
NameError: name 'undefined_var' is not defined

Suggestion: Define the variable first or import it
```

### Save & Share

```
[💾 SAVE]     Save to My Snippets
[📋 COPY]     Copy code to clipboard
[🔗 SHARE]    Generate shareable link
[📥 DOWNLOAD] Download as .py, .js, .java, .cpp
```

---

## 🎓 Use Cases

### Learning Algorithms

```python
# Test sorting algorithm
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

test = [64, 34, 25, 12, 22, 11, 90]
print("Original:", test)
print("Sorted:", bubble_sort(test.copy()))
```

### Data Analysis

```python
import pandas as pd
import numpy as np

# Quick data exploration
df = pd.DataFrame({
    'Name': ['Alice', 'Bob', 'Charlie'],
    'Score': [92, 87, 95]
})
print(df.describe())
print(f"Average: {df['Score'].mean()}")
```

### Visualization

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.plot(x, y)
plt.title("Sine Wave")
plt.xlabel("X")
plt.ylabel("Y")
plt.show()
```

### Quick Prototyping

```javascript
// Test a function quickly
const fibonacci = (n) => {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
};

console.log("Fib(10):", fibonacci(10));
```

---

## ⚙️ Configuration

### Theme Selection

```
[☀️ Light]  [🌙 Dark]  [🎨 Custom]
```

Supported themes:
- Dracula
- One Dark
- Solarized
- VS Code Dark
- and 10+ more

### Font & Size

```
Font: [Monospace ▼]  Size: [14px ▼]
```

### Auto-save

☑️ Auto-save to cloud (every 5 seconds)
☑️ Auto-run on save

---

## 📝 Advanced Features

### Multi-file Projects

For Python:
```
files/
  main.py (imports from utils)
  utils.py (helper functions)
  data.json (input data)
```

### Custom Input Files

Attach files or paste data for programs to read.

### Debugging

Print intermediate values:

```python
def solve(x):
    result = x * 2
    print(f"Debug: x={x}, result={result}")  # ← For debugging
    return result
```

### Performance Profiling

See timing for different approaches:

```python
import time

# Approach 1: Loop
start = time.time()
# ... code ...
print(f"Time: {time.time() - start:.4f}s")
```

---

## 🚫 Limitations

| Limit | Value |
|-------|-------|
| **Execution time** | 5 seconds max |
| **Memory** | 256 MB max |
| **File size** | 10 MB max |
| **Output size** | 1 MB max |
| **File writes** | Temporary (no persistence) |
| **Network** | No external API calls |

### Blocked Features
- ❌ Network requests (HTTP calls)
- ❌ File persistence (data lost after run)
- ❌ System calls (shell commands)
- ❌ Processes (can't spawn new processes)

---

## 🐛 Common Issues

### "Execution timeout"
**Cause:** Code took > 5 seconds  
**Solution:** Optimize algorithm or break into smaller pieces

```python
# Too slow (timeout):
for i in range(1000000):
    for j in range(1000000):
        pass

# Better:
# Optimize outer loops, avoid nested loops
```

### "Memory exceeded"
**Cause:** Allocated > 256 MB  
**Solution:** Use generators instead of loading all data

```python
# Too much memory:
data = [i for i in range(1000000)]

# Better (generator):
data = (i for i in range(1000000))
```

### "Import error"
**Cause:** Library not installed  
**Solution:** Use only pre-installed packages

```python
# ✅ Works:
import numpy, pandas, matplotlib

# ❌ Doesn't work:
import tensorflow  # Not installed
```

---

## 💡 Tips

1. **Start simple** - Test small pieces before complex code
2. **Use print()** - Debug by printing intermediate values
3. **Check syntax** - Red squiggles indicate errors
4. **Test edge cases** - Empty inputs, large numbers, special cases
5. **Read errors** - Error messages tell you exactly what's wrong
6. **Save good solutions** - Use [SAVE] to bookmark useful snippets

---

## 🔗 Related

- [Adaptive Learning](ADAPTIVE_LEARNING.md)
- [Troubleshooting](../guides/TROUBLESHOOTING.md)
- [Architecture Overview](../ARCHITECTURE.md)

---

Last updated: May 27, 2026
