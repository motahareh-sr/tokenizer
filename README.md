# Byte Pair Encoding (BPE) and WordPiece Tokenization Implementation

## Overview
This project implements two widely used subword tokenization algorithms: **Byte Pair Encoding (BPE)** and **WordPiece Tokenization**. These methods are fundamental for modern NLP tasks, especially in training and using models like BERT and GPT.

## Features
- Reads and tokenizes text from a file
- Implements a **custom tokenizer** using regular expressions
- Implements **Byte Pair Encoding (BPE)** with a frequency-based merging process
- Implements **WordPiece Tokenization** with probability-based merging
- Applies the trained vocabularies on new text samples

## How It Works
### 1. Read and Tokenize Text
The program reads a text file and tokenizes it using a custom tokenizer that considers:
- Word boundaries (`\b\w+\b`)
- Dot-separated words (`\b\w+(?:\.\w+)+\b`)

### 2. Byte Pair Encoding (BPE)
BPE merges the most frequent adjacent character pairs iteratively until a predefined threshold is reached.

#### Steps:
1. Convert words into lists of characters, appending `</w>` to mark word endings.
2. Count occurrences of adjacent character pairs.
3. Merge the most frequent pair.
4. Repeat until the threshold is met.
5. Store the final vocabulary.

### 3. WordPiece Tokenization
WordPiece merges subword units based on a probability measure rather than raw frequency.

#### Steps:
1. Convert words into lists of characters with `</w>` markers.
2. Compute co-occurrence counts of adjacent subwords.
3. Calculate merge probabilities based on frequency ratios.
4. Merge the highest probability subword pair.
5. Repeat until the threshold is met.
6. Store the final vocabulary.

## Usage
### Running the Tokenization
Ensure you have a text file to process. Update the `filename` variable accordingly.

```python
from tokenizer import read_txt_as_string, custom_tokenizer, nested_list, BPE, Wordpiece

filename = '/path/to/textfile.txt'
moon = read_txt_as_string(filename)
corpus = custom_tokenizer(moon)

# Apply BPE
list_of_words = nested_list(corpus)
vocab_BPE = BPE(list_of_words, 10)
print(vocab_BPE)

# Apply WordPiece
list2_of_words = nested_list(corpus)
vocab_Wordpiece = Wordpiece(list2_of_words, 10)
print(vocab_Wordpiece)
```

### Testing on Sample Text
To test tokenization on new text, modify the `test` string and run:
```python
test = "This is a tokenization task. Tokenization is the first step in an NLP pipeline."
pretokenize = custom_tokenizer(test)
nest = nested_list(pretokenize)
vocab_test_BPE = BPE(nest, 10)
vocab_test_Wordpiece = Wordpiece(nest, 10)
print(vocab_test_BPE)
print(vocab_test_Wordpiece)
```

## Dependencies
This project requires Python 3 and the following modules:
- `re`
- `collections.Counter`

## Applications
- **Preprocessing text for NLP models**: BPE and WordPiece tokenization are widely used in models like BERT, GPT, and T5.
- **Compression**: BPE is used in text compression tasks.
- **Efficient vocabulary generation**: Helps in reducing out-of-vocabulary (OOV) issues in NLP models.

## Future Improvements
- Support for multi-threading to speed up tokenization.
- Implement a more optimized data structure for handling merges.
- Extend support for additional tokenization strategies like Unigram LM.

## License
This project is open-source and available under the MIT License.

