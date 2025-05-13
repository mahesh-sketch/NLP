
# 🧠 Encoding in Machine Learning and NLP

When working with **categorical** or **textual** data, machine learning models need the data to be in **numerical format**. Encoding is the process of converting these non-numeric values into numbers so that ML algorithms can process them.

---

## 📊 Why Encoding Is Necessary?

ML and DL models can only understand numbers. Hence, **categorical data** and **text data** must be encoded into numerical vectors.

### 🧠 Example Use Case:

Imagine you're building a **customer support ticket classifier** to categorize tickets into:

- **Billing**, **Technical**, or **General**

You need to encode both the **ticket category** (categorical) and the **ticket description** (text).

---

## 🔢 Categorical Data Encoding

### 1. **Label Encoding**

Assigns a unique number to each category.

**Example:**

```
Billing   → 0  
Technical → 1  
General   → 2
```

#### ✅ Benefits:
- Simple and efficient
- Best for **ordinal data** (Low, Medium, High)

#### ❌ Limitations:
- Introduces **order** which may not be valid for **nominal data**

---

### 2. **One Hot Encoding**

Creates separate binary columns for each category.

**Example:**

| Billing | Technical | General |
|---------|-----------|---------|
|   1     |     0     |    0    |
|   0     |     1     |    0    |
|   0     |     0     |    1    |

#### ✅ Benefits:
- No order assumption
- Best for **nominal data**

#### ❌ Limitations:
- High dimensionality if categories are many
- Not memory-efficient

---

## 📝 Text Data Encoding

### 3. **Bag of Words (BoW)**

Counts the frequency of each word in a document.

**Example:**

Text 1: `"internet not working"`  
Text 2: `"slow internet connection"`

**Vocabulary**: [internet, not, working, slow, connection]

**BoW Matrix:**

| Text | internet | not | working | slow | connection |
|------|----------|-----|---------|------|------------|
| T1   |    1     |  1  |    1    |  0   |     0      |
| T2   |    1     |  0  |    0    |  1   |     1      |

#### ✅ Benefits:
- Easy to implement
- Effective for basic tasks

#### ❌ Limitations:
- Ignores **word order**
- Sparse and high-dimensional
- Cannot capture semantic meaning

---

### 4. **Bag of Words with n-grams**

Extends BoW by including word sequences of `n` length.

**Example:**

Text: `"internet not working"`

- **Unigrams**: internet, not, working  
- **Bigrams**: internet not, not working  
- **Trigrams**: internet not working

**Feature Vector**:  
["internet", "not", "working", "internet not", "not working"]

#### ✅ Benefits:
- Captures **context** and **phrases**
- Better for sentiment and topic analysis

#### ❌ Limitations:
- Higher dimensionality
- More sparse
- Requires more data to be effective

---

### 5. **TF-IDF (Term Frequency–Inverse Document Frequency)**

A more advanced way of encoding text that gives **importance** to words based on their **frequency in a document** and **rarity across documents**.

#### 🔹 Term Frequency (TF)

Measures how often a word occurs in a document.

**Formula:**
TF(word) = (Number of times word appears in a document) / (Total number of words in that document)

#### 🔹 Inverse Document Frequency (IDF)

Measures how **unique** a word is across all documents.

**Formula:**
IDF(word) = log(Total number of documents / Number of documents containing the word)

#### 🔹 TF-IDF

Combines both:
TF-IDF = TF × IDF


---

**Example:**

Documents:
- Doc1: `"the internet is down"`
- Doc2: `"the internet is slow"`

Vocabulary: [the, internet, is, down, slow]

Step-by-step:

| Word     | Doc1 TF | Doc2 TF | IDF                  | TF-IDF (Doc1)        | TF-IDF (Doc2)        |
|----------|---------|---------|----------------------|-----------------------|----------------------|
| the      | 1/4     | 1/4     | log(2/2) = 0         | 0                     | 0                    |
| internet | 1/4     | 1/4     | log(2/2) = 0         | 0                     | 0                    |
| is       | 1/4     | 1/4     | log(2/2) = 0         | 0                     | 0                    |
| down     | 1/4     | 0       | log(2/1) ≈ 0.301     | 0.075                 | 0                    |
| slow     | 0       | 1/4     | log(2/1) ≈ 0.301     | 0                     | 0.075                |

> Words like "the", "internet", and "is" are common in both documents → IDF is low  
> Unique words like "down" and "slow" have higher TF-IDF → more **important**

#### ✅ Benefits:
- Reduces the weight of **common words**
- Highlights **important and unique** terms

#### ❌ Limitations:
- Cannot capture **synonyms or semantic meaning**
- Still produces **sparse vectors**

---

## 🧠 Summary Table

| Encoding Technique     | Best For             | Captures Order? | Dimensionality | Use Case                             |
|------------------------|----------------------|------------------|----------------|--------------------------------------|
| Label Encoding         | Ordinal categories   | ✅ Yes           | Low            | Product ratings: Low, Medium, High   |
| One Hot Encoding       | Nominal categories   | ❌ No            | High           | Gender, Country, Ticket Category     |
| Bag of Words           | Text data            | ❌ No            | High           | Ticket classification                |
| Bag of n-grams         | Text + Context       | ⚠️ Partial       | Very High      | Sentiment analysis, spam detection   |
| TF-IDF                 | Text weighting       | ❌ No            | High           | Document search, keyword extraction  |
