+++
title = "Blog Embedded Machine Learning"
+++

The are just my comments while exploring implementation of machine learning on embedded small micro processors. For this exploration I am specifically looking at small processors with RAM <= 64k and ROM <1M. 

Due to the size restriction, generated C code was first explored.

# Sci-learn with micromlgen 
02-12-2023

[Micromlgen link](https://github.com/eloquentarduino/micromlgen)


## Pros
- easy to use
- training in python
- small number of basic models supported
- compact C code
## Cons
- does not look as if it is still maintained
- no continious linear model support? 

# Sci-learn with m2cgen 
20-12-2023

[M2cgen link](https://github.com/BayesWitnesses/m2cgen)

[M2cgen tutorial](https://www.freecodecamp.org/news/transform-machine-learning-models-into-native-code-with-zero-dependencies/)

## Pros
- easy to use
- training in python
- more models than micromlgen
- generated C code very compact and standalone
- lots of classification modles
## Cons
- not a lot of support for linear continious models, only  LinearRegression supported?

## Example

```python
import m2cgen as m2c
# from micromlgen import port

from sklearn.tree import DecisionTreeClassifier  # -3
from sklearn.svm import SVC         # -4
from sklearn.decomposition import PCA # fail evaluate
from sklearn.tree import DecisionTreeRegressor as DTR # 0-3
from sklearn.ensemble import RandomForestRegressor as RFR 
# from sktime.classification.deep_learning.cnn import CNNClassifier
from sklearn import linear_model
from sklearn.svm import LinearSVR
from sklearn.svm import SVR



from sklearn.model_selection import train_test_split
import numpy as np
# from sklearn.datasets import load_iris as load_dataset
from sklearn.datasets import fetch_california_housing  as load_dataset


X0, y0 = load_dataset(return_X_y=True)

X, Xt, y, yt = train_test_split(X0,y0, test_size=0.3)

clf = linear_model.LinearRegression()
# clf = DecisionTreeClassifier()
# clf = SVC()
# clf = DTR(max_depth=3, min_samples_leaf=5) # 3
# clf = RFR(n_estimators=10, max_depth=10, min_samples_leaf=5) # 2
# clf = RFR(n_estimators=10, max_depth=3, min_samples_leaf=5) # 1
# clf = RFR(n_estimators=4, max_depth=3, min_samples_leaf=5) # 2
# clf = RFR(n_estimators=4, max_depth=3, min_samples_leaf=3) # 1-3
# clf = PCA(n_components=2, whiten=False)
# clf = CNNClassifier()
# clf = LinearSVR()
# clf = SVR()

clf.fit(X, y)

yr = clf.predict(Xt)
# yr = clf.predict(Xt).round()

# --- model export
# print(port(clf))
print(m2c.export_to_c(clf))

# --- verify
print(yt)
print(yr)
err = yr-yt
print(err)
accabserr = np.absolute(err).sum()
print(f'Result: err {accabserr} / {len(err)} = {accabserr/len(err)} ')
```

Result: err 3264.7222304876614 / 6192 = 0.5272484222363795 

## Generated code
```C
double score(double * input) 
{
    return -36.54197620190014 + input[0] * 0.4317289356671669 + input[1] * 0.009424543998233838 + input[2] * -0.09960404669971323 + input[3] * 0.6008075129913518 + input[4] * -0.000003834638439710256 + input[5] * -0.00773774390350655 + input[6] * -0.41892630023873445 + input[7] * -0.430756266127245;
}
```

# uTensor
[Site Link]()
## Pros
-small footprint somewhere between 1 kB and 2 KB (plus ~1KB for the rest uTensor library).
- buildin quantization

## Cons
- C++ which might be a problem if allocating memory

# TVM

# emlearn
20-12-2023

[Site](https://github.com/emlearn/emlearn)
## Pros
- C99
- support small processors: AVR, ESP,ARM M
- Melspectrogram
- can do MLP?
- still maintained

## Cons
- 