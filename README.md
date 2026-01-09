# Sentiment Dataset

## Description

This repository contains a sentiment analysis dataset stored in a CSV file: `sentiment_dataset.csv`.

The dataset is intended for experiments, benchmarking, and educational purposes in sentiment analysis and natural language processing (NLP).

Each example in the dataset is labeled with one of three sentiment classes:

* **positive**
* **negative**
* **neutral**

### ⚠️ Important note about ordering

The dataset is **not randomly shuffled**.

All samples are ordered **by class** in the following sequence:

1. Positive samples
2. Negative samples
3. Neutral samples

If you plan to:

* split the dataset into train/test subsets,
* train machine learning models,
* perform cross-validation,

you **must shuffle the dataset first** to avoid biased results.

---

## File format

* **Format:** CSV (Comma-Separated Values)
* **Encoding:** UTF-8
* **Delimiter:** `,`
* **Header:** Yes

Typical columns include:

* text / content (string)
* label (categorical: `positive`, `negative`, `neutral`)

(Please inspect the file to see the exact column names.)

---

## How to load the dataset

### Python (pandas)

```python
import pandas as pd

df = pd.read_csv("sentiment_dataset.csv")
print(df.head())
```

---

### R

```r
df <- read.csv("sentiment_dataset.csv", stringsAsFactors = FALSE)
head(df)
```

---

### Julia (DataFrames.jl)

```julia
using CSV, DataFrames

df = CSV.read("sentiment_dataset.csv", DataFrame)
first(df, 5)
```

---

## How to shuffle the dataset

### Python (pandas)

```python
import pandas as pd

df = pd.read_csv("sentiment_dataset.csv")

# Shuffle the dataset
df_shuffled = df.sample(frac=1, random_state=42).reset_index(drop=True)

# Save shuffled version (optional)
df_shuffled.to_csv("sentiment_dataset_shuffled.csv", index=False)
```

---

### R

```r
set.seed(42)

df <- read.csv("sentiment_dataset.csv", stringsAsFactors = FALSE)

# Shuffle the dataset
df_shuffled <- df[sample(nrow(df)), ]

# Save shuffled version (optional)
write.csv(df_shuffled, "sentiment_dataset_shuffled.csv", row.names = FALSE)
```

---

### Julia

```julia
using CSV, DataFrames, Random

Random.seed!(42)

df = CSV.read("sentiment_dataset.csv", DataFrame)

# Shuffle the dataset
df_shuffled = df[shuffle(1:nrow(df)), :]

# Save shuffled version (optional)
CSV.write("sentiment_dataset_shuffled.csv", df_shuffled)
```

---

## Recommended usage

Before training any model or performing statistical analysis:

1. **Shuffle the dataset**
2. **Split into train / validation / test sets**
3. Ensure class balance if required

Failing to shuffle may result in misleadingly high or low evaluation metrics.

* добавить пример **train/test split**
* оформить README под **Hugging Face datasets**
* написать краткое описание для статьи или отчёта

## License

This dataset is provided for free use for research and educational purposes.

