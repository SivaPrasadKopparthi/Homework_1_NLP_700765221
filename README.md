# Homework_1_NLP_700765221
This is my Homework 1 submission along with ReadMe Explanation and Source Code.

# **Q1. Regex**

### **1. U.S. ZIP Codes**

```python
r'\b\d{5}(?:[-\s]\d{4})?\b'
```

👉 Finds ZIP codes like `12345`, `12345-6789`, `12345 6789`.
Only matches whole ZIP codes, not parts of bigger numbers.

---

### **2. Words Not Starting with a Capital Letter**

```python
r'\b(?![A-Z])[A-Za-z’\'-]+\b'
```

👉 Picks up words that do **not** start with a capital letter.
Examples: `apple`, `state-of-the-art`, `don’t`.

---

### **3. Numbers (sign, commas, decimals, scientific notation)**

```python
r'[+-]?\d{1,3}(?:,\d{3})*(?:\.\d+)?(?:[eE][+-]?\d+)?'
```

👉 Matches many kinds of numbers:

* `123`, `+123`, `-99.5`
* `12,345`
* `3.14`
* `1.23e-4`

---

### **4. Variants of “Email”**

```python
r'(?i)e[ -–]?mail'
```

👉 Matches `email`, `e-mail`, `E mail`, `EMAIL`.
Case-insensitive.

---

### **5. “gooo…” with Optional Punctuation**

```python
r'\bgo+[,!?.]?\b'
```

👉 Matches `go`, `goo`, `gooo`, `goooo!`, `go?`.

---

### **6. Lines Ending with ? and Quotes/Brackets**

```python
r'\?['")\]\s]*$'
```

👉 Matches sentences that end with a `?` and may have quotes, brackets, or spaces after.
Examples:

* `Are you okay?`
* `Really?”`
* `This is true?)”   `

---
