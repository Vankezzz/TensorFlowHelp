# TensorFlowHelp
1. What does `batch_size` mean?
 Example code, where `batch_size` is used (python):
 ```
batch_size = 32
seed = 42

raw_train_ds = tf.keras.preprocessing.text_dataset_from_directory(
    directory='aclImdb/train',
    batch_size=batch_size,      # Size of the batches of data. Default: 32.
    validation_split=0.2,       # Optional float between 0 and 1, fraction of data to reserve for validation.
    subset='training',          # One of "training" or "validation". Only used if validation_split is set.
    seed=seed)                  # Optional random seed for shuffling and transformations.
```

Source answer (if you wonder then should read contents in url): 
https://stats.stackexchange.com/questions/153531/what-is-batch-size-in-neural-network
```
Typically when people say online learning they mean batch_size=1. 
The idea behind online learning is that you update your model as soon as you see the example. 
With larger batch size it means that first you are looking through the multiple samples before doing update. 
In RNN size of the batch can have different meanings. 
Usually, It's common to split training sequence into window of fixed size (like 10 words). 
In this case including 100 of these windows during the training will mean that you have batch_size=100

In the neural network terminology:
one epoch = one forward pass and one backward pass of all the training examples
batch size = the number of training examples in one forward/backward pass. 
The higher the batch size, the more memory space you'll need.
number of iterations = number of passes, each pass using [batch size] number of examples. 
To be clear, one pass = one forward pass + one backward pass 
(we don't count the forward pass and backward pass as two different passes).
Example: if you have 1000 training examples, and your batch size is 500, then it will take 2 iterations to complete 1 epoch.
```
2. What does `seed` mean?
 Example code, where `seed` is used (python):
 ```
batch_size = 32
seed = 42

raw_train_ds = tf.keras.preprocessing.text_dataset_from_directory(
    directory='aclImdb/train',
    batch_size=batch_size,      # Size of the batches of data. Default: 32.
    validation_split=0.2,       # Optional float between 0 and 1, fraction of data to reserve for validation.
    subset='training',          # One of "training" or "validation". Only used if validation_split is set.
    seed=seed)                  # Optional random seed for shuffling and transformations.
```
Source answer1: https://stackoverflow.com/questions/38604437/what-is-a-seed-in-tensorflow
```
The term "seed" is an abbreviation of the standard term "random seed". 
TensorFlow operators that produce random results accept an optional seed parameter.
If you pass the same number to two instances of the same operator, they will produce the same sequence of results.
```
Source answer2: https://towardsdatascience.com/how-to-solve-randomness-in-an-artificial-neural-network-3befc4f27d45
```
To make the randomness predictable, we use the concept of seed. Seed helps get predictable, repeatable results every time
```
Properly Setting the Random Seed in ML Experiments. Not as Simple as You Might Imagine: 
https://medium.com/@ODSC/properly-setting-the-random-seed-in-ml-experiments-not-as-simple-as-you-might-imagine-219969c84752

3. How does method of tf.data.Dataset `take(number_of_batch)` work?
Example code, where `take(number_of_batch)` is used (python):
```
# raw_train_ds is dataset
raw_train_ds = tf.keras.preprocessing.text_dataset_from_directory(
    directory='aclImdb/train',
    batch_size=batch_size,  # Size of the batches of data. Default: 32.
    validation_split=0.2,  # Optional float between 0 and 1, fraction of data to reserve for validation.
    subset='training',  # One of "training" or "validation". Only used if validation_split is set.
    seed=seed)  # Optional random seed for shuffling and transformations.

for text_batch, label_batch in raw_train_ds.take(1):
    for i in range(3):
        print("Review", text_batch.numpy()[i])
        print("Label", label_batch.numpy()[i])
```
tf.data.Dataset.take(number_of_batch) - this is a sample, where the size is batch_size. For instance, you have 96 samples and batch_size=32 then it's mean that number_of_batch=96/32=3 (no more)

Source answer:https://stackoverflow.com/questions/64138844/in-tensorflow-understanding-pipeline-what-is-use-of-take1-in-for-feature-batc

## Usefull materials:
1. Tensorflow for Deep Learning Research lectures: https://web.stanford.edu/class/cs20si/2017/lectures/

## Terminalogy
Embeddings - В языковом моделировании отдельные слова и группы слов сопоставляются векторам – некоторым численным представлениям с сохранением семантической связи. Сжатое векторное представление слова называют эмбеддингом.
Мешок слов - это модель представления текста в виде вектора (набора слов). Каждому слову в тексте сопоставляется число его вхождений.
