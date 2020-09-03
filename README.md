# CS6513-CP: Neural Machine Translation

Also available at https://colab.research.google.com/drive/1sO5uVCEFASZuffcLdLkQxOF2wSXbUlFB?usp=sharing

This was my class project for NYU Tandon's Summer 2020 Big Data course taught by Raman Kannan. 

## Introduction
### Summary
Recurrent neural networks are used to translate between Spanish and English and French and English (and vice versa). PySpark and distributed Tensorflow used to parallelize and distibute processing, respectively.

### Supported Translations
*   Spanish to English
*   English to Spanish
*   French to English
*   English to French

### Libraries Used
* Spark/PySpark
* Tensorflow/Keras 
* Numpy
* Pandas
* Scikit-learn

### Overview
I used a sequence to sequence language translation model where, a sequence of words in one language goes into the model, and then the model outputs a sequence of words in a different language, as seen below.

![seq2seq](https://app.lucidchart.com/publicSegments/view/0783d692-52e8-44b0-8b37-31b0e8cfaa9f/image.png)

The sequence to sequence model is implemented via a neural network compromised of two recurrent neural networks. The first recurrent neural network is the encoder, and the second is the decoder. A sequence of words is fed into the encoder, and then its output is fed into the decoder. The result is the translated sequence of words.

![encoder-decoder](https://app.lucidchart.com/publicSegments/view/66c06ed4-69a5-4261-9ae6-dbb57b80ff5e/image.png)

Before the text is fed into the encoder, we have to process the text and convert it into a format the neural network can use. First, we clean the text by removing punctuation and converting it to lowercase. Then, we use a tokenizer to map each word to an integer. Each language has its own tokenizer. After each sequence of words is converted into a sequence of integers, we pad the ends with zeros to ensure each sequence is of the same length. Finally, we can run the sequence through the neural network.

Our resulting output is also a sequence of integers. However, we can't immediately use our tokenizer to convert it into a sequence of words. The neural network took each word from the input sequence and determined the probability it's equivalent to any of the word-integers in our output language vocabulary. The word-integer with the highest probability is what we choose as our translation. We can now use the output language's tokenizer to map the integer back to the word and get our full translation.

![full-model](https://app.lucidchart.com/publicSegments/view/a8b90a51-797d-43f4-87b0-dd27119cf9bc/image.png)
