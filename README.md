**BINARY CLASSIFICATION MODEL FRAMEWORK**

A generic model dispatcher framework for binary classification problems. No need to start from scratch, model can be updated in and chosen from the dispatcher.

1) Open Terminal and clone the directory

```
git clone https://github.com/vinejain/random-forest-classifier-framework.git
```

2) Create a directory INPUT and fetch the categorical data. 
Make sure your Kaggle API key (kaggle.json) is located in your C:\Users\user\.kaggle.
If you're not sure what kaggle.json is, refer below links first and download your key

- https://github.com/Kaggle/kaggle-api
- https://www.kaggle.com/docs/api

or manually download data from below link
- https://www.kaggle.com/c/cat-in-the-dat/data

```
mkdir input
cd /input
pip install kaggle
kaggle competitions download -c cat-in-the-dat
```

3) Unzip the downloaded file and discard zip

```
ls
unzip cat-in-the-dat.zip -d ./
rm *.zip
```

4) Check train.csv

```
head train.csv
```

5) Activate the kaggle environment

```
cd ..
./kaggle-env/Scripts/activate.bat
```

6) Create a directory MODELS where TRAIN.PY will save the model using joblib

```
mkdir models
```

7) Execute the shell script 'run.sh'

```
sh src/run.sh
```

**DISPATCHER**

SRC/DISPATCHER.py dispatches the required model

**K-FOLD Cross Validation**

SRC/CREATE_FOLDS.py creates Stratified Folds with 5 splits on the training dataset, and saves output file in INPUT/TRAIN_FOLDS.csv. See new column 'Fold'

**TRAINING**

SRC/TRAIN.py will train the data and dump the models in MODELS/.

Following will be fetched using os.environ.get:
TRAINING_DATA
TEST_DATA
FOLD
MODEL

METRICS: Since the data is skewed, using ROC_AUC. On current data it gives score of 0.74 with FOLD=4


**PREDICT**

SRC/PREDICT.py will predict_proba() to predict the probability of 1s, and save it in MODELS/rf_output.csv

**RUN.SH**

FOLD=0 python -m src.train
FOLD=1 python -m src.train
FOLD=2 python -m src.train
FOLD=3 python -m src.train
FOLD=4 python -m src.train
python -m src.predict
