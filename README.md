# Auton Survival Package
<img align="right" width=50% src=https://www.cs.cmu.edu/~chiragn/auton_survival.png>

Repository of reusable code utilities for Survival Analysis projects.

## `auton_survival.datasets`

Helper functions to load various trial data like `ACCORD`, `BARI2D` and `ALLHAT`.
 
```python
# Load the TOPCAT Dataset
from auton_survival import dataset
features, outcomes = datasets.load_topcat()
```

## `auton_survival.preprocessing`
This module provides a flexible API to perform imputation and data normalization for downstream machine learning models. The module has 3 distinct classes, `Scaler`, `Imputer` and `Preprocessor`. The `Preprocessor` class is a composite transform that does both Imputing ***and*** Scaling.

 ```python
# Preprocessing loaded Datasets

from auton_survival import datasets
features, outcomes = datasets.load_topcat()

from auton_survival.preprocessing import Preprocessing
features = Preprocessor().fit_transform(features, cat_feats=['GENDER', 'ETHNICITY', 'SMOKE'], num_feats=['height', 'weight'])

# The `cat_feats` and `num_feats` lists would contain all the categorical and numerical features in the dataset.
```

## `auton_survival.estimators`

This module provids a wrapper to model BioLINNC  datasets with standard survival (time-to-event) analysis methods. The use of the wrapper allows a simple standard interface for multiple different survival models, and also helps standardize experiments across various differents research areas. 

Currently supported Survival Models are: 

- Cox Proportional Hazards Model (`lifelines`): 
- Random Survival Forests (`pysurvival`): 
- Weibull Accelerated Failure Time (`lifelines`) : 
- Deep Survival Machines: **Not Implemented Yet**
- Deep Cox Mixtures: **Not Implemented Yet**


 ```python
# Preprocessing loaded Datasets

from auton_survival import datasets
features, outcomes = datasets.load_topcat()

from auton_survival.estimators import Preprocessing
features = Preprocessing().fit_transform(features)
```


## `auton_survival.experiments` 

Modules to perform standard survival analysis experiments. This module provides a top-level interface to run `auton_survival` Style experiments of survival analysis, involving cross-validation style experiments with multiple different survival analysis models at different horizons of event times. 

The module further eases evaluation by automatically computing the *censoring adjusted* estimates of the Metrics of interest, like **Time Dependent Concordance Index** and **Brier Score** with **IPCW** adjustement. 

 ```python
# auton_survival Style Cross Validation Experiment.

from auton_survival import datasets
features, outcomes = datasets.load_topcat()

from auton_survival.experiments import SurvivalCVRegressionExperiment

# instantiate a auton_survival Experiment by 
# specifying the features and outcomes to use.
experiment = SurvivalCVRegressionExperiment(features, outcomes)

# Fit the `experiment` object with a Cox Model
experiment.fit(model='cph')

# Evaluate the performance at time=1 year horizon.
scores = experiment.evaluate(time=1.)

print(scores)
```




## `auton_survival.reporting`

Helper functions to generate standard reports for popular Survival Analysis problems. 

## Installation

```console
foo@bar:~$ git clone https://github.com/autonlab/auton_survival
foo@bar:~$ pip install -r requirements.txt 
```

## Requirements

 `scikit-learn`, `scikit-survival`, `lifelines`, `matplotlib`, `pandas`, `numpy`, `missingpy`

## License

MIT License

Copyright (c) 2020 Carnegie Mellon University, Auton Lab

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

<img align="right" height ="120px" src="https://www.cs.cmu.edu/~chiragn/cmu_logo.jpeg">
<img align="right" height ="110px" src="https://www.cs.cmu.edu/~chiragn/auton_logo.png"> 
