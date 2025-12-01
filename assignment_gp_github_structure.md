# Python Intern Assignment — GitHub Project Structure

This repository contains the 12-task Python assignment implemented as a clean, testable, and deployable project. Files are organized for easy maintenance, CI, packaging, and contribution.

---

## Repository tree

```
assignment-gp/
├── .github/
│   └── workflows/
│       └── python-app.yml
├── docs/
│   └── README.md
├── src/
│   └── assignment_gp/
│       ├── __init__.py
│       ├── task1_fizzbuzz.py
│       ├── task2_palindrome.py
│       ├── task3_factorial.py
│       ├── task4_fibonacci.py
│       ├── task5_anagram.py
│       ├── task6_missing_number.py
│       ├── task7_linkedlist.py
│       ├── task8_merge_sort.py
│       ├── task9_longest_unique.py
│       ├── task10_todo.py
│       ├── task11_count_keyword.py
│       └── task12_fetch_api.py
├── tests/
│   ├── test_task1.py
│   ├── test_task2.py
│   └── test_task3.py
├── .gitignore
├── LICENSE
├── README.md
├── pyproject.toml
├── requirements.txt
└── setup.cfg
```

---

## Key files (created for you)

### `README.md` (top-level)
Contains project overview, quick start, running tests, and contribution notes.

### `pyproject.toml`
Simple modern packaging config using `setuptools`.

### `requirements.txt`
Lists runtime/test dependencies (pytest, requests).

### `src/assignment_gp/` modules
Each task is implemented in its own module file. Names follow `taskN_description.py` and export one main function/class with the `_gp` suffix.

### `tests/`
Pytest tests for the core tasks (representative tests are included for Tasks 1-3 and you can add more following the pattern).

### GitHub Actions CI (`.github/workflows/python-app.yml`)
A simple workflow that runs tests on push/pull-request, checks formatting with `ruff` (optional), and runs `pytest` on Python versions 3.9, 3.10, 3.11.

---

## How to use

1. Clone the repo

```bash
git clone https://github.com/<your-username>/assignment-gp.git
cd assignment-gp
```

2. Create a virtual environment and install dev deps

```bash
python -m venv .venv
source .venv/bin/activate  # on Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

3. Run tests

```bash
pytest -q
```

4. Run an example from one module

```bash
python -c "from assignment_gp.task1_fizzbuzz import fizz_buzz_gp; print(fizz_buzz_gp(15))"
```

---

## License
MIT (file included)

---

## Files content (skeletons)

Below are the contents of the most important files. You can copy these into the repo.

### `pyproject.toml`

```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "assignment-gp"
version = "0.1.0"
description = "Solutions for 12 Python internship tasks (unique names with _gp)."
readme = "README.md"
requires-python = ">=3.9"

[project.dependencies]
requests = "*"

[tool.setuptools.packages.find]
where = ["src"]
```

### `requirements.txt`

```
pytest>=7.0
requests>=2.28
```

### `.gitignore`

```
__pycache__/
.venv/
*.pyc
*.pyo
*.pyd
.DS_Store
.idea/
.vscode/
*.egg-info/
dist/
build/
.env
*.sqlite3
```

### `setup.cfg`

```ini
[tool:pytest]
minversion = 6.0
addopts = -ra -q
testpaths = tests
```

### `.github/workflows/python-app.yml`

```yaml
name: Python package

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.9, 3.10, 3.11]
    steps:
      - uses: actions/checkout@v4
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: Run tests
        run: pytest -q
```

### `src/assignment_gp/__init__.py`

```python
from .task1_fizzbuzz import fizz_buzz_gp
from .task2_palindrome import is_palindrome_gp
from .task3_factorial import factorial_gp
from .task4_fibonacci import fibonacci_gp
from .task5_anagram import is_anagram_gp
from .task6_missing_number import find_missing_gp
from .task7_linkedlist import NodeGP, LinkedListGP
from .task8_merge_sort import merge_sort_gp
from .task9_longest_unique import longest_unique_substring_gp
from .task10_todo import ToDoAppGP
from .task11_count_keyword import count_keyword_lines_gp
from .task12_fetch_api import fetch_api_data_gp

__all__ = [
    "fizz_buzz_gp",
    "is_palindrome_gp",
    "factorial_gp",
    "fibonacci_gp",
    "is_anagram_gp",
    "find_missing_gp",
    "NodeGP",
    "LinkedListGP",
    "merge_sort_gp",
    "longest_unique_substring_gp",
    "ToDoAppGP",
    "count_keyword_lines_gp",
    "fetch_api_data_gp",
]
```

### `src/assignment_gp/task1_fizzbuzz.py`

```python
def fizz_buzz_gp(n: int):
    result = []
    for i in range(1, n + 1):
        if i % 15 == 0:
            result.append("FizzBuzz")
        elif i % 3 == 0:
            result.append("Fizz")
        elif i % 5 == 0:
            result.append("Buzz")
        else:
            result.append(str(i))
    return result
```

### `src/assignment_gp/task2_palindrome.py`

```python
def is_palindrome_gp(text: str) -> bool:
    cleaned = ''.join(ch.lower() for ch in text if ch.isalnum())
    return cleaned == cleaned[::-1]
```

### `src/assignment_gp/task3_factorial.py`

```python
def factorial_gp(n: int) -> int:
    if n < 0:
        raise ValueError("Number must be non-negative")
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

### `src/assignment_gp/task4_fibonacci.py`

```python
def fibonacci_gp(n: int):
    if n <= 0:
        return []
    if n == 1:
        return [0]
    seq = [0, 1]
    while len(seq) < n:
        seq.append(seq[-1] + seq[-2])
    return seq
```

### `src/assignment_gp/task5_anagram.py`

```python
def is_anagram_gp(a: str, b: str) -> bool:
    clean = lambda s: ''.join(sorted(ch.lower() for ch in s if ch.isalnum()))
    return clean(a) == clean(b)
```

### `src/assignment_gp/task6_missing_number.py`

```python
def find_missing_gp(arr, n):
    return (n * (n + 1) // 2) - sum(arr)
```

### `src/assignment_gp/task7_linkedlist.py`

```python
class NodeGP:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedListGP:
    def __init__(self):
        self.head = None

    def append_gp(self, value):
        if not self.head:
            self.head = NodeGP(value)
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = NodeGP(value)

    def reverse_gp(self):
        prev = None
        curr = self.head
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
        self.head = prev

    def to_list_gp(self):
        result = []
        temp = self.head
        while temp:
            result.append(temp.value)
            temp = temp.next
        return result
```

### `src/assignment_gp/task8_merge_sort.py`

```python
def merge_sort_gp(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort_gp(arr[:mid])
    right = merge_sort_gp(arr[mid:])
    i = j = 0
    merged = []
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
    merged.extend(left[i:])
    merged.extend(right[j:])
    return merged
```

### `src/assignment_gp/task9_longest_unique.py`

```python
def longest_unique_substring_gp(s: str) -> int:
    last = {}
    start = 0
    longest = 0
    for i, ch in enumerate(s):
        if ch in last and last[ch] >= start:
            start = last[ch] + 1
        last[ch] = i
        longest = max(longest, i - start + 1)
    return longest
```

### `src/assignment_gp/task10_todo.py`

```python
import json
import os

class ToDoAppGP:
    def __init__(self, file="todo_gp.json"):
        self.file = file
        self.tasks = []
        self._load()

    def _load(self):
        if os.path.exists(self.file):
            try:
                with open(self.file, "r", encoding="utf-8") as f:
                    self.tasks = json.load(f)
            except Exception:
                self.tasks = []

    def _save(self):
        with open(self.file, "w", encoding="utf-8") as f:
            json.dump(self.tasks, f, indent=2)

    def add_task_gp(self, name, desc=""):
        next_id = max((t["id"] for t in self.tasks), default=0) + 1
        task = {"id": next_id, "name": name, "desc": desc, "done": False}
        self.tasks.append(task)
        self._save()
        return next_id

    def complete_task_gp(self, task_id):
        for t in self.tasks:
            if t["id"] == task_id:
                t["done"] = True
                self._save()
                return True
        return False

    def list_tasks_gp(self):
        return list(self.tasks)

    def clear_gp(self):
        self.tasks = []
        self._save()
```

### `src/assignment_gp/task11_count_keyword.py`

```python
def count_keyword_lines_gp(filename, keyword="ERROR"):
    count = 0
    with open(filename, "r", encoding="utf-8", errors="ignore") as f:
        for line in f:
            if keyword in line:
                count += 1
    return count
```

### `src/assignment_gp/task12_fetch_api.py`

```python
import requests

def fetch_api_data_gp(url: str, params=None, timeout=10):
    response = requests.get(url, params=params or {}, timeout=timeout)
    response.raise_for_status()
    try:
        return response.json()
    except ValueError:
        return {"text": response.text}
```

### `tests/test_task1.py`

```python
from assignment_gp.task1_fizzbuzz import fizz_buzz_gp


def test_fizz_buzz_basic():
    assert fizz_buzz_gp(5) == ["1", "2", "Fizz", "4", "Buzz"]
```

### `tests/test_task2.py`

```python
from assignment_gp.task2_palindrome import is_palindrome_gp


def test_palindrome_examples():
    assert is_palindrome_gp("Racecar") is True
    assert is_palindrome_gp("Hello") is False
```

### `tests/test_task3.py`

```python
from assignment_gp.task3_factorial import factorial_gp


def test_factorial_small():
    assert factorial_gp(0) == 1
    assert factorial_gp(5) == 120
```

### `LICENSE` (MIT)

```text
MIT License

Copyright (c) 2025 <Your Name>

Permission is hereby granted, free of charge, to any person obtaining a copy
... (standard MIT text)
```

---

If you'd like I can now:

- Create each of these files for you and provide a zip you can download, or
- Create a single combined repository file here and let you copy, or
- Push the structure to your GitHub repo if you provide a repo name and grant access (I cannot perform the push for you, but I can give exact commands).

Tell me which of the three you'd like next and I will proceed.

