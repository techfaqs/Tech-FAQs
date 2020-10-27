# An example in Tensorflow 2.0

<br>
<center><img src="https://i.imgur.com/KXbnThQ.png" width="500px"></center>
<br>

**Hi** reader, this is a small and simple guide to RNNs, we will discuss all the basic requirements that you will need to get started with RNNs from underneath concepts to code implementation. We will be implementing using TensorFlow 2.0.

<br>

# Table of Content:
1. **What is RNNs**
2. **Many to One RNN**
3. **Some thing about the data**
4. **Loading Data Using Pandas**
5. **Some Basic Exploratory Data Analysis**
6. **Data Preprocessing**
7. **Model Building**
8. **Train Test Split**
9. **Model Training**
10. **Model Evaluation**
11. **Conclusion**
<br>

### What are RNNs?

The R in RNN stands for recurrent which literally means repeating. Now you will think what is repeating here? Here repeating refers to the repeating structure of RNNs. There are different kinds of data available, like normal tabular data with different features, image data,time-series data, text data, etc. From the time series, data and text data are the data which has a sequence in it. Let me discuss the meaning of sequence for text data. It's very noticeable that every sentence has a sequence of words, and if you change the sequence of that sentence then the sentence won't have the same meaning. Because of this reason, we can't use MLPs on text data (there are other reasons too like large parameter size,size of i/p word and o/p word can be different, etc.).
Now, an RNN has many structures as per the problem requirements like- one to one, one to many, many to one, many to many as fig 1.


![RNN structure](https://i.imgur.com/AtbnrWR.jpg)

#### Fig: 1


But, here I will be discussing many to one network. But, keep in mind that a single RNN cell is the same everywhere, just they are placed in different ways to satisfy the problem requirements.

###  Many to One RNN: 
The structure of many to many looks like fig2.The application of many to one network is spam detection, sentiment analysis, etc. Now let's dive deep and understand the bare bones of RNN.

![Many to One](https://i.imgur.com/Zz5bcjX.png)
#### Fig: 2

Every vertical block with input and output arrows is called a RNN cell. In the beginning, it uses a vector with zeros which are named here as <strong>O<sub>0</sub></strong>, this is only for showing the repeating structure of RNN. the circles in the blocks are activation functions. And if you check out carefully, you will observe that there are three types of weights.W which are with input word vector, <strong>W'</strong> is with RNN cell o/p and finally <strong>W''</strong> is at the final RNN cell which helps to make the prediction.O/p of RNN cells are taken as an i/p for the next RNN cell, this is to keep the sequence information preserved. 

Now, <strong>O<sub>i</sub></strong> is,


<strong>O<sub>i</sub> = f(X<sub>i</sub> W+O<sub>i</sub> W')</strong>


And at the end, the output of the last RNN cell and the <strong>W''</strong> are taken and passed through an activation function(here sigmoid is taken) to generate the prediction, <strong>Y' = S(O<sub>n</sub> W'')</strong>. And rest of the things are taken care of by backpropagation and gradient descent stuff, normal model training.


> Note, description of all symbols are given in the image itself.

## Utils


```python
import warnings
warnings.filterwarnings("ignore")                     #Ignoring unnecessory warnings

import numpy as np                                  #for large and multi-dimensional arrays
import pandas as pd                                 #for data manipulation and analysis
import nltk                                         #Natural language processing tool-kit

from nltk.corpus import stopwords                   #Stopwords corpus
from nltk.stem import PorterStemmer                 # Stemmer

from sklearn.feature_extraction.text import CountVectorizer          #For Bag of words
from sklearn.feature_extraction.text import TfidfVectorizer          #For TF-IDF
from gensim.models import Word2Vec                                   #For Word2Vec

from tensorflow.keras.layers import Embedding
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.preprocessing.text import one_hot
from tensorflow.keras.layers import SimpleRNN
from tensorflow.keras.layers import Dropout
from tensorflow.keras.layers import Dense


```

## Loading Data Using Pandas:

We are going to use Food reviews data for for this example,

```python
import pandas as pd
pd.pandas.set_option('display.max_columns',None)
pd.pandas.set_option('display.max_rows',None)
df = pd.read_csv('../input/amazon-fine-food-reviews/Reviews.csv')
```



### Some Basic Exploratory Data Analysis:

### Info:

```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 568454 entries, 0 to 568453
    Data columns (total 10 columns):
     #   Column                  Non-Null Count   Dtype 
    ---  ------                  --------------   ----- 
     0   Id                      568454 non-null  int64 
     1   ProductId               568454 non-null  object
     2   UserId                  568454 non-null  object
     3   ProfileName             568438 non-null  object
     4   HelpfulnessNumerator    568454 non-null  int64 
     5   HelpfulnessDenominator  568454 non-null  int64 
     6   Score                   568454 non-null  int64 
     7   Time                    568454 non-null  int64 
     8   Summary                 568427 non-null  object
     9   Text                    568454 non-null  object
    dtypes: int64(5), object(5)
    memory usage: 43.4+ MB
    

### Shape:
```python
df.shape
```

    (568454, 10)



### Check if there is any nan values
```python
df.isna().sum()
```

    Id                         0
    ProductId                  0
    UserId                     0
    ProfileName               16
    HelpfulnessNumerator       0
    HelpfulnessDenominator     0
    Score                      0
    Time                       0
    Summary                   27
    Text                       0
    dtype: int64



### Remove 3 star reviews:
```python
df1 = df[df['Score']!=3]
df1.shape
```




    (525814, 10)



### Data Preprocessing:

Here, we are dropping the data points where `UseId`,`"ProfileName`,`Time`,`Text` are same and keeping the first data point.


```python
df1 = df1.drop_duplicates(subset={"UserId","ProfileName","Time","Text"}, keep='first', inplace=False)
```

Here, we are keeping the values where `HelpfulnessNumerator` <= `HelpfulnessDenominator`.


```python
df1 = df1[df1['HelpfulnessNumerator']<=df1['HelpfulnessDenominator']]
```

As we have taken this dataset as a NLP problem, so we are only considering the text column as the i/p data and `score` as the labels.


```python
list1 = list(df1['Score'])
list2 = list(df1['Text'])

score_df = pd.DataFrame(list1,columns = ['score'])
text_df = pd.DataFrame(list2,columns = ['text'])

df2 = pd.concat([text_df,score_df],axis=1)
df2.head()
```

|  | text | score |
| ----------- | ----------- |----------- |
|0|I have bought several of the Vitality canned d...|5|
|1|Product arrived labeled as Jumbo Salted Peanut...	|1|
|2|This is a confection that has been around a fe...|4|
|3|If you are looking for the secret ingredient i...|2|
|4|Great taffy at a great price. There was a wid...|5|



Checking out some of the text which starts from 500 index and ends at 550 index.


```python
for i in range(500,505):
    print(df2['text'].values[i])
    print('-----------------------------------------------------')
```

### Output:

    ...you can absolutely forget about these. Confirmed by other reviewers, these chips are now total garbage. Like chewing on styrofoam packaging "peanuts". Positively awful, no hyperbole or exaggeration. I'll NEVER buy anything from Kettle brand ever again! From a reportedly once great "premium" brand, literally any mass market chip I've ever tried tastes better than these. Stale and rancid tasting, and virtually no salty taste whatsoever. Completely awful!
    -----------------------------------------------------
    These chips are nasty.  I thought someone had spilled a drink in the bag, no the chips were just soaked with grease.  Nasty!!
    -----------------------------------------------------
    Unless you like salt vinegar chips as salty as eating actual pinches of salt and drinking actual vinegar, i doubt you will like these chips.  These are the saltiest & sourest chips I have ever had, and the only reason stops me from throwing these away is because I paid for 2 full boxes and dont like to waste food.  The brown chips are especially bad, besides being salty and sour, they also taste overcooked and burnt.  Unless you are the rare kind that can take this kind of extreme taste, you will not like these chips.<br /><br />I actually have a high tolerance for sour taste, so I can down a bag of chips with a bit of difficulty.  But normal people, please do not try this at home.
    -----------------------------------------------------
    I bought this brand as a trial since I am tired of the Pingos.<br /><br />It claims that it is natural. I have no argument on this. But the point is that more than 50% in the bag is over-fried and in brown color. I really suffer eating the over-fried chips. I open some other bags and it looks like the same. So I just throw away all of them. I don't know if I was with bad luck or every bag they are selling is the same. But for sure I will never buy this brand any more.
    -----------------------------------------------------
    They are good but wish they were also baked. Have not found baked no salt potato chips anywhere. If there are any I wish someone would post.
    -----------------------------------------------------


### Reduce dataframe to a first 50,000 rows and print head:

```python
df3 = df2.head(50000)
df3.head()
```

|  | text | score |
| ----------- | ----------- |----------- |
|0|I have bought several of the Vitality canned d...|5|
|1|Product arrived labeled as Jumbo Salted Peanut...	|1|
|2|This is a confection that has been around a fe...|4|
|3|If you are looking for the secret ingredient i...|2|
|4|Great taffy at a great price. There was a wid...|5|


Here we have created a function which will mark the score from 1 to 3 as negative and 4 to 5 as positive. A we are going to do binary classification that's why we are keeping the labels to positive and negative.


```python
def partition(x):
    if x < 3:
        return 'negative'
    return 'positive'

score_upd = df3['score']
t = score_upd.map(partition)
df3['score']=t

df3.head()
```


|  | text | score |
| ----------- | ----------- |----------- |
|0|I have bought several of the Vitality canned d...|positive|
|1|Product arrived labeled as Jumbo Salted Peanut...	|negative|
|2|This is a confection that has been around a fe...|positive|
|3|If you are looking for the secret ingredient i...|negative|
|4|Great taffy at a great price. There was a wid...|positive|





```python
df3.isna().sum()
```

    text     0
    score    0
    dtype: int64



Here, df_x is the i/p text data and df_y is the i/p lable.


```python
df_x = df3['text']
df_y = df3['score']
```


```python
stop_words = set(stopwords.words('english'))
len(stop_words) #finding stop words
```

    179



Here we are doing the real pre-processing,which are like- keeping only the alphabets,making all the alphabets lower,removing all the stop word.


```python
import re
from nltk.corpus import stopwords
from nltk.stem.porter import PorterStemmer
snow = nltk.stem.SnowballStemmer('english')

corpus = []
for i in range(0, len(df3)):
    review = re.sub('[^a-zA-Z]', ' ', df3['text'][i])
    review = review.lower()
    review = review.split()
    
    review = [snow.stem(word) for word in review if not word in stopwords.words('english')]
    review = ' '.join(review)
    corpus.append(review)
```


```python
corpus[1]
```

    'product arriv label jumbo salt peanut peanut actual small size unsalt sure error vendor intend repres product jumbo'




```python
df_x = corpus
```


```python
type(df_x)
```

    list



This is an important step, here we are creating word vectors by doing one hot encoding, and we are only taking 5000 words as the dictionary.


```python
voc_size=5000
onehot_repr=[one_hot(words,voc_size)for words in corpus] 
type(onehot_repr)
```
    list



Padding is one of the most important part before feeding the data to the model. In simple way padding is a way to keep the input size same for all i/p text by adding zeros at the front. Here we are considering each i/p text corpus will be of 400 words. 


```python
sent_length=400
embedded_docs=pad_sequences(onehot_repr,padding='pre',maxlen=sent_length)
print(embedded_docs)
```

    [[   0    0    0 ... 4896 3622 1277]
     [   0    0    0 ... 4842 3622 1244]
     [   0    0    0 ...  862 3777 4073]
     ...
     [   0    0    0 ... 2125 2180 4235]
     [   0    0    0 ... 1025 2246 1680]
     [   0    0    0 ...  744 4878  397]]
    

This is the model build using tensorflow 2.0. Think about the whole model like this,

first its a sequencial model starting with a `Embedding` layer (wich is deep learning version of word to vec,or more intuitively WV is an example of `Embedding` and we are use it because we can be trained,it's not static like WV) and input size is 5000x40 and output size of 400x40.Now we created a dropout layer using `Dropout()` which will reduce the chance of overfitting. After that we are taking 100 layers of `RNN` and feeding the output of Embedding leyer to each of the `RNN` layer . Now, each of the `RNN` layer will spit out a scaller value and then we will be stacking them out,because of that the output size after `RNN` layer would be 100. Ten we againg perform a Dropout layer. At the end we have a single activation unit of `sigmoid` (line 8) which will take the 100 sized vector and give a prediction or in general words give a scaler value between 0 to 1. 

Now we are setting the optimixer as `adam` and evaluation matrics as `accurecy` and loss as `binary_crossentropy`(this is because we have taken this as a binary classification problem) using the `model.compile()` method.
At the 10th line we are printing the model architecture using `model.summary()` method.


```python
## Creating model
embedding_vector_features=40
model=Sequential()
model.add(Embedding(voc_size,embedding_vector_features,input_length=sent_length))
model.add(Dropout(0.3))
model.add(SimpleRNN(100))
model.add(Dropout(0.3))
model.add(Dense(1,activation='sigmoid'))
model.compile(loss='binary_crossentropy',optimizer='adam',metrics=['accuracy'])
print(model.summary())
```

    Model: "sequential_1"
    _________________________________________________________________
    Layer (type)                 Output Shape              Param #   
    =================================================================
    embedding_1 (Embedding)      (None, 400, 40)           200000    
    _________________________________________________________________
    dropout_1 (Dropout)          (None, 400, 40)           0         
    _________________________________________________________________
    simple_rnn (SimpleRNN)       (None, 100)               14100     
    _________________________________________________________________
    dropout_2 (Dropout)          (None, 100)               0         
    _________________________________________________________________
    dense (Dense)                (None, 1)                 101       
    =================================================================
    Total params: 214,201
    Trainable params: 214,201
    Non-trainable params: 0
    _________________________________________________________________
    None
    

Some preprocessing before feeding the data. We are doing lable encoding of the `score` column.


```python
from sklearn.preprocessing import LabelEncoder
encode = LabelEncoder()
df_y2 = encode.fit_transform(df_y)
type(df_y2)
```

    numpy.ndarray


This is a important part, where we car converting our data to nd arrays as we cant just input a pandas data frame.


```python
import numpy as np
X_final=np.array(embedded_docs)
y_final=np.array(df_y2)
```

### Train Test Split:


```python
from sklearn.model_selection import train_test_split
X_train, X_test, Y_train, Y_test = train_test_split(X_final, y_final, test_size=0.2, random_state=42)
```


```python
#we are feeding the 
model.fit(X_train,Y_train,validation_data=(X_test,Y_test),epochs=10,batch_size=64)
```

### Output:

    Epoch 1/10
    625/625 [==============================] - 78s 125ms/step - loss: 0.3643 - accuracy: 0.8591 - val_loss: 0.2562 - val_accuracy: 0.8989
    Epoch 2/10
    625/625 [==============================] - 76s 121ms/step - loss: 0.3047 - accuracy: 0.8830 - val_loss: 0.3438 - val_accuracy: 0.8626
    Epoch 3/10
    625/625 [==============================] - 77s 124ms/step - loss: 0.2992 - accuracy: 0.8847 - val_loss: 0.2755 - val_accuracy: 0.8908
    Epoch 4/10
    625/625 [==============================] - 77s 124ms/step - loss: 0.2555 - accuracy: 0.9012 - val_loss: 0.2714 - val_accuracy: 0.8908
    Epoch 5/10
    625/625 [==============================] - 77s 123ms/step - loss: 0.2417 - accuracy: 0.9074 - val_loss: 0.2741 - val_accuracy: 0.8917
    Epoch 6/10
    625/625 [==============================] - 77s 123ms/step - loss: 0.2318 - accuracy: 0.9126 - val_loss: 0.2726 - val_accuracy: 0.8890
    Epoch 7/10
    625/625 [==============================] - 76s 122ms/step - loss: 0.2177 - accuracy: 0.9166 - val_loss: 0.2600 - val_accuracy: 0.8955
    Epoch 8/10
    625/625 [==============================] - 77s 123ms/step - loss: 0.2857 - accuracy: 0.8852 - val_loss: 0.2866 - val_accuracy: 0.8880
    Epoch 9/10
    625/625 [==============================] - 77s 124ms/step - loss: 0.3006 - accuracy: 0.8788 - val_loss: 0.3423 - val_accuracy: 0.8598
    Epoch 10/10
    625/625 [==============================] - 76s 122ms/step - loss: 0.2995 - accuracy: 0.8789 - val_loss: 0.2991 - val_accuracy: 0.8777
    
    <tensorflow.python.keras.callbacks.History at 0x7f3a10485050>




```python
y_pred_rnn = model.predict_classes(X_test)
```


```python
from sklearn.metrics import accuracy_score
accuracy_score(Y_test,y_pred_rnn)
```

    0.8777



### Conclusion:

Our model is giving nera 90% accurecy which is very good.
This is how you train a RNN using tensorflow 2.0
