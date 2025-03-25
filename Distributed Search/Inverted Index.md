## Why call it a Inverted index

An inverted index is called "inverted" because it maps terms (words) to the documents they appear in, which is the reverse of how a traditional "forward" index works (mapping documents to their terms). 

Here's a more detailed explanation:

-   **Traditional (Forward) Index:**
    In a forward index, you would have a list of documents, and for each document, you would have a list of the words it contains. 
- **Inverted Index:**
    An inverted index, on the other hand, flips this relationship. Instead of listing words per document, it lists documents per word. 
-   **Think of it like a dictionary:**
    Imagine a dictionary where each word (term) points to a list of pages (documents) where that word can be found. 
-   **Why it's useful:** 
    This "inverted" mapping allows for very fast full-text searches because you can quickly find all documents containing a specific term by looking up that term in the index. 
-   **Example:**
    If you have 3 documents: "The cat sat on the mat", "The dog sat on the mat", and "The cat is on the table", a forward index would store:

    -   Document 1: ["The", "cat", "sat", "on", "the", "mat"]
    -   Document 2: ["The", "dog", "sat", "on", "the", "mat"]
    -   Document 3: ["The", "cat", "is", "on", "the", "table"]

An inverted index would store: 
"The", "cat", "sat", "on", "mat", "dog", "is", and "table".