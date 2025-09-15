# Homework#1 Natural Language Processing 700765221

**Student Name:** Sai Siva Shankara Vara Prasad Kopparthi

**Student ID:** 700765221

---

This is my Homework 1 submission along with ReadMe Explanation and Source Code.


## **Q1. Regex**

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

## Q2. Tokenization (Telugu Example)

**Paragraph (Telugu):**

```
నేను హైదరాబాద్ లో చదువుతున్నాను. నా స్నేహితుడు తెలుగు సినిమాలు చూడడం ఇష్టపడతాడు. మేము ప్రతి వారాంతం కలిసి బయటికి వెళ్తాము.
```

**Tokenization:**

* **Naïve split:** Breaks only by spaces, keeps punctuation attached.
* **Manual correction:** Removes punctuation, cleaner tokens.
* **NLTK tokenizer:** Handles Unicode Telugu text, but sometimes splits compound words awkwardly.
* **MWEs (Multiword Expressions):** `"తెలుగు సినిమాలు"`, `"ప్రతి వారాంతం"`, `"హైదరాబాద్ లో"` should be treated as single tokens.

**Reflection:**
 - Tokenization in Telugu is harder than English because of compound words and rich morphology.
 - Naïve splitting by spaces often leaves punctuation attached to words.
 - Manual correction improves results, but still misses some cases.
 - Tools like NLTK handle Unicode but may not fully capture Telugu MWEs, so extra care is needed.
---

## Q3: Manual BPE on a Toy Corpus

### 3.1 Toy Corpus

**Corpus:** `low low low low low lowest lowest newer newer newer newer newer newer wider wider wider new new`

**Initial vocab (with `_` as end-of-word):**

```
l o w _ : 5
l o w e s t _ : 2
n e w e r _ : 6
w i d e r _ : 3
n e w _ : 2
```

**First 3 merges:**

1. `e r` → `er`
2. `er _` → `er_`
3. `n e` → `ne`

**Updated vocab:**

```
l o w _ : 5
l o w e s t _ : 2
ne w er_ : 6
w i d er_ : 3
ne w _ : 2
```

---

### 3.2 Mini-BPE Learner

**Top 10 merges:** `('e','r'), ('er','_'), ('n','e'), ('ne','w'), ('l','o'), ('lo','w'), ('new','er_'), ('low','_'), ('w','i'), ('wi','d')`

**Word segmentation examples:**

```
new → [new, _]
newer → [newer_]
lowest → [low, e, s, t, _]
wider → [wid, er_]
```

**Reflection:** Subword tokens reduce OOV issues, capture common morphemes like `er_`, and allow rare words to be represented using familiar units.

---

### 3.3 BPE on a Paragraph

**Top 5 merges:** `('a','n'), ('e','_'), ('s','_'), ('d','_'), ('o','r')`
**Longest subwords:** `subwor, and_, age_, wor, how`

**Word segmentation examples:**

```
processing → [pr, o, ce, s, si, ng_]
tokenization → [to, k, en, i, z, at, i, on_]
subword → [subwor, d_]
morphological → [m, or, p, ho, l, o, g, i, c, al, _]
coverage → [co, v, er, age_]
```

**Reflection:** BPE captures frequent prefixes, suffixes, and stems, reduces vocab size, handles rare words, and generalizes to unseen words. Drawback: splits can sometimes create meaningless fragments.

---

## Q4. Word Pair: *Sunday → Saturday*

**1. (Model A: Sub=1, Ins=1, Del=1)**

* Edit sequence: Insert `a`, insert `tur`, delete `n`
* The Distance = **3**

**2. (Model B: Sub=2, Ins=1, Del=1)**

* Edit sequence: Insert `a`, insert `tur`, delete `n`
* The Distance = **4**

**3. Reflection**

* Model A = 3 edits, Model B = 4 edits
* Model A uses cheaper substitutions, fewer steps
* Model B avoids expensive substitutions, more insertions/deletions
* Applications:
  - Spell check → cheap substitutions
  - DNA alignment → cheap insertions/deletions

---
