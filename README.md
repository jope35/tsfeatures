
::: {.cell 0=‘h’ 1=‘i’ 2=‘d’ 3=‘e’}

``` python
from tsfeatures import *
```

:::

# tsfeatures

> porting tsfeature to nbdev

This file will become your README and also the index of your
documentation.

## Install

``` sh
pip install tsfeatures
```

## How to use

Fill me in please! Don’t forget code examples:

``` python
1+1
```

    2

[![Build](https://github.com/FedericoGarza/tsfeatures/workflows/Python%20package/badge.svg)](https://github.com/FedericoGarza/tsfeatures/tree/master)
[![PyPI version
fury.io](https://badge.fury.io/py/tsfeatures.svg)](https://pypi.python.org/pypi/tsfeatures/)
[![Downloads](https://pepy.tech/badge/tsfeatures.png)](https://pepy.tech/project/tsfeatures)
[![Python
3.6+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/release/python-370+/)
[![License:
MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://github.com/FedericoGarza/tsfeatures/blob/master/LICENSE)

# tsfeatures

Calculates various features from time series data. Python implementation
of the R package
*[tsfeatures](https://github.com/robjhyndman/tsfeatures)*.

# Installation

You can install the *released* version of `tsfeatures` from the [Python
package index](pypi.org) with:

``` python
pip install tsfeatures
```

# Usage

The `tsfeatures` main function calculates by default the features used
by Montero-Manso, Talagala, Hyndman and Athanasopoulos in [their
implementation of the FFORMA
model](https://htmlpreview.github.io/?https://github.com/robjhyndman/M4metalearning/blob/master/docs/M4_methodology.html#features).

``` python
from tsfeatures import tsfeatures
```

This function receives a panel pandas df with columns `unique_id`, `ds`,
`y` and optionally the frequency of the data.

<img src=https://raw.githubusercontent.com/FedericoGarza/tsfeatures/master/.github/images/y_train.png width="152">

``` python
tsfeatures(panel, freq=7)
```

By default (`freq=None`) the function will try to infer the frequency of
each time series (using `infer_freq` from `pandas` on the `ds` column)
and assign a seasonal period according to the built-in dictionary
`FREQS`:

``` python
FREQS = {'H': 24, 'D': 1,
         'M': 12, 'Q': 4,
         'W':1, 'Y': 1}
```

You can use your own dictionary using the `dict_freqs` argument:

``` python
tsfeatures(panel, dict_freqs={'D': 7, 'W': 52})
```

## List of available features

| Features        |                 |               |
|:----------------|:----------------|:--------------|
| acf_features    | heterogeneity   | series_length |
| arch_stat       | holt_parameters | sparsity      |
| count_entropy   | hurst           | stability     |
| crossing_points | hw_parameters   | stl_features  |
| entropy         | intervals       | unitroot_kpss |
| flat_spots      | lumpiness       | unitroot_pp   |
| frequency       | nonlinearity    |               |
| guerrero        | pacf_features   |               |

See the docs for a description of the features. To use a particular
feature included in the package you need to import it:

``` python
from tsfeatures import acf_features

tsfeatures(panel, freq=7, features=[acf_features])
```

You can also define your own function and use it together with the
included features:

``` python
def number_zeros(x, freq):

    number = (x == 0).sum()
    return {'number_zeros': number}

tsfeatures(panel, freq=7, features=[acf_features, number_zeros])
```

`tsfeatures` can handle functions that receives a numpy array `x` and a
frequency `freq` (this parameter is needed even if you don’t use it) and
returns a dictionary with the feature name as a key and its value.

# Authors

- **Federico Garza** - [FedericoGarza](https://github.com/FedericoGarza)
- **Kin Gutierrez** - [kdgutier](https://github.com/kdgutier)
- **Cristian Challu** -
  [cristianchallu](https://github.com/cristianchallu)
- **Jose Moralez** - [jose-moralez](https://github.com/jose-moralez)
- **Ricardo Olivares** - [rolivaresar](https://github.com/rolivaresar)
- **Max Mergenthaler** - [mergenthaler](https://github.com/mergenthaler)
