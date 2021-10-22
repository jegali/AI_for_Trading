# NLP on Financial Statements

This is the project review I got for the project "NLP on Financial Statements" in the "AI for trading" nanodegree


## Meets Specifications

Congratulations on finishing this project successfully  ![:tada:](https://review.udacity.com/assets/images/emojis/tada.png ":tada:")  Most of your python codes are compact and elegant in this project. Great work!  ![:smile:](https://review.udacity.com/assets/images/emojis/smile.png ":smile:")

## 10-Ks

- [x] The function  `get_documents`  extracts the documents from the text.

	Regular expressions are quite useful methods for text matching and extracting.  
Check out this Quick Regex Cheatsheet  [https://www.cheatography.com/mutanclan/cheat-sheets/python-regular-expression-regex/](https://www.cheatography.com/mutanclan/cheat-sheets/python-regular-expression-regex/)

- [x] The function  `get_document_type`  returns the document type lowercased.

## Preprocess the Data

- [x] The function  `lemmatize_words`  lemmatizes verbs.

	Lemmatization is used to bring all the tokens into their base form.

## Analysis on 10ks

- [x] The function  `get_bag_of_words`  generates a bag of words from documents.

	The bag of words (BOW) is used to encode the words into the numerical form. Because the model cannot use the text directly in its matrix computation.

- [x] The function  `get_jaccard_similarity`  calculates the jaccard similarities for neighboring documents.

- [x] The function  `tfidf`  generate TFIDF vectors for each document.

	IDF puts more weightage to the specific words related to the corresponding specific documents. For example, a medical term will be given more weightage in the medical documents.

- [x] The function  `get_cosine_similarity`  calculates the cosine similarities for each neighboring TFIDF vector/document.

	Cosine Similarity is calculated by taking the dot product of the two vectors and the divided by the product of the length of the two vectors to rescale value to the normalized range.
