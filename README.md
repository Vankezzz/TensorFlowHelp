# TensorFlowHelp
1. Что значит batch_size?
```
raw_train_ds = tf.keras.preprocessing.text_dataset_from_directory(
    directory='aclImdb/train',
    batch_size=batch_size,      # Size of the batches of data. Default: 32.
    validation_split=0.2,       # Optional float between 0 and 1, fraction of data to reserve for validation.
    subset='training',          # One of "training" or "validation". Only used if validation_split is set.
    seed=seed)                  # Optional random seed for shuffling and transformations.
```
`batch_size` -  - влияет на среднюю ошибку, на которую сеть будет реагировать.
Например если взять batch=1. А "истина" районе 5.
```
Шаг 1. получим условное смещение весов на +10;
Шаг 2. получим условное смещение весов на -2; Итог +8;
Взять 2.
Шаг 1. получим условное смещение весов на (+10 + -2) / 2=> 4;
Мы приближаемся быстрее.
Если взять мало, то сеть будет туда-сюда "метаться". Если много, то ошибка "средней по больнице" будет очень мала в районе нуля, и обучаться тогда она будет долго.
https://qna.habr.com/q/733739
```
https://stats.stackexchange.com/questions/153531/what-is-batch-size-in-neural-network
