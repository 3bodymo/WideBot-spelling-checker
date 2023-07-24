# Task 1 - Spelling Checker

## Overview

This project implements a spell checker class that utilizes a suitable data structure to store a dictionary of words. The class provides three main operations:

1. **Store the Dictionary**: The dictionary is stored in a data structure to efficiently retrieve and check the existence of words.

2. **Search for Nearest Words**: If a word is not found in the dictionary, the class returns the nearest four words in lexicographic order. Nearest words are defined as the two words before and after the input word, if they exist.

3. **Add Word to the Dictionary**: The class allows for the addition of new words to the dictionary.

## Data Structure - Trie

Initially, the implementation used a Trie data structure to store the dictionary. A Trie is a tree-like data structure used for efficient retrieval of keys (words in this case) in a dataset of strings. Each node in the Trie represents a character, and by traversing down the Trie, we can reconstruct the entire word. Here is a brief explanation of the Trie algorithm:

A Trie consists of TrieNodes, each having an array of children where each index of the array corresponds to a character (e.g., a-z). A boolean flag, `isEndOfWord`, is used to determine if a node represents the end of a word.

When inserting a word into the Trie, we start at the root and iterate over each character of the word. For each character, we check if the corresponding child node exists. If not, we create a new node for that character and continue the process until the entire word is inserted.

The Trie data structure is efficient for dictionary storage and word retrieval, making it a good initial choice for this spell checker.

```python
class TrieNode:
    def __init__(self):
        self.children = [None] * 26
        self.isEndOfWord = False

class Trie:
    def __init__(self):
        self.root = self.getNode()

    def getNode(self):
        return TrieNode()

    def _charToIndex(self, ch):
        return ord(ch) - ord('a')

    def insert(self, word):
        root = self.root
        length = len(word)
        for level in range(length):
            index = self._charToIndex(word[level])
            if not root.children[index]:
                root.children[index] = self.getNode()
            root = root.children[index]

        root.isEndOfWord = True

def build_dictionary(trie, file_path):
    with open(file_path, "r") as file:
        for line in file:
            word = line.strip().lower()
            trie.insert(word)
```

## Improving the Nearest Word Search

Although the initial Trie implementation was suitable for storing the dictionary, it encountered challenges when searching for the nearest four words in lexicographic order. As a result, an alternative approach was devised to address this problem.

The new approach involves using a simple list to store the dictionary instead of the Trie. This allows for easy indexing and retrieval of words, which simplifies the process of finding the nearest words.

When a word is not found in the dictionary, it is temporarily added to the list. By sorting the list and locating the position of the word, the two words before and after it can be easily identified as the nearest words.

This algorithm proved to be efficient and effective in finding the nearest words in lexicographic order, solving the challenges faced with the original Trie-based approach.

## Conclusion

In conclusion, this spell checker class utilizes a data structure to store a dictionary efficiently. The initial implementation explored the use of the Trie data structure but faced difficulties in finding the nearest words in lexicographic order. As a result, an alternative approach was adopted, employing a simple list to store the dictionary and simplify the nearest word search.

By employing this spell checker class, you can easily store a dictionary of words, check for word existence, retrieve nearest words for misspelled words, and add new words to the dictionary.
