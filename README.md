# TensorFlowHelp
1. What does batch_size mean?
* Source: https://qna.habr.com/q/733739
```
raw_train_ds = tf.keras.preprocessing.text_dataset_from_directory(
    directory='aclImdb/train',
    batch_size=batch_size,      # Size of the batches of data. Default: 32.
    validation_split=0.2,       # Optional float between 0 and 1, fraction of data to reserve for validation.
    subset='training',          # One of "training" or "validation". Only used if validation_split is set.
    seed=seed)                  # Optional random seed for shuffling and transformations.
```

```
`batch_size` -  - влияет на среднюю ошибку, на которую сеть будет реагировать.
Например если взять batch=1. А "истина" районе 5.
Шаг 1. получим условное смещение весов на +10;
Шаг 2. получим условное смещение весов на -2; Итог +8;
Взять 2.
Шаг 1. получим условное смещение весов на (+10 + -2) / 2=> 4;
Мы приближаемся быстрее.
Если взять мало, то сеть будет туда-сюда "метаться". Если много, то ошибка "средней по больнице" будет очень мала в районе нуля, и обучаться тогда она будет долго.
```
* Source: https://stats.stackexchange.com/questions/153531/what-is-batch-size-in-neural-network
```
Typically when people say online learning they mean batch_size=1. The idea behind online learning is that you update your model as soon as you see the example. With larger batch size it means that first you are looking through the multiple samples before doing update. In RNN size of the batch can have different meanings. Usually, It's common to split training sequence into window of fixed size (like 10 words). In this case including 100 of these windows during the training will mean that you have batch_size=100

In the neural network terminology:
one epoch = one forward pass and one backward pass of all the training examples
batch size = the number of training examples in one forward/backward pass. The higher the batch size, the more memory space you'll need.
number of iterations = number of passes, each pass using [batch size] number of examples. To be clear, one pass = one forward pass + one backward pass (we do not count the forward pass and backward pass as two different passes).
Example: if you have 1000 training examples, and your batch size is 500, then it will take 2 iterations to complete 1 epoch.
```

