############################# 
FITTER Documentation 
#############################

.. image:: https://badge.fury.io/py/fitter.svg :target: https://pypi.python.org/pypi/fitter

.. image:: https://github.com/cokelaer/fitter/actions/workflows/main.yml/badge.svg?branch=main :target: https://github.com/cokelaer/fitter/actions/workflows/main.yml

.. image:: https://coveralls.io/repos/cokelaer/fitter/badge.png?branch=main :target: https://coveralls.io/r/cokelaer/fitter?branch=main

.. image:: http://readthedocs.org/projects/fitter/badge/?version=latest :target: http://fitter.readthedocs.org/en/latest/?badge=latest :alt: Documentation Status

.. image:: https://zenodo.org/badge/23078551.svg :target: https://zenodo.org/badge/latestdoi/23078551

**Compatible with Python 3.7, 3.8, 3.9, and 3.10**

# What is it?

The **fitter** package is a Python library used for fitting probability distributions to data. It provides a straightforward and intuitive interface to estimate parameters for various types of distributions, both continuous and discrete.

Using **fitter**, you can easily:

-   Fit a range of distributions to your data
-   Compare their fit quality using multiple metrics (SSE, AIC, BIC, KL divergence)
-   Identify the most suitable distribution for your dataset

The package is designed to be user-friendly and requires minimal setup, making it a useful tool for data scientists and statisticians working with probability distributions.

# Installation

You can install fitter in several ways:

From GitHub::

```
git clone https://github.com/tg12/fitter
cd fitter
pip install .

```

From PyPI::

```
pip install fitter

```

From Conda (bioconda channel)::

```
conda install fitter

```

# Usage

## Standalone Application

A standalone application is provided that works with input CSV files::

```
fitter fitdist data.csv --column-number 1 --distributions gamma,normal

```

This creates:

-   A file called `fitter.png` with the visualization
-   A log file `fitter.log`

## From Python Shell

First, let's create a sample dataset with 10,000 points from a gamma distribution:

```python
from scipy import stats
data = stats.gamma.rvs(2, loc=1.5, scale=2, size=10000)

```

_Note: The fitting process can be computationally intensive, so keep the sample size reasonable._

Now, without any prior knowledge about the distribution or its parameters, we can use **Fitter** to find the best fit:

```python
from fitter import Fitter
f = Fitter(data)
f.fit()
# This may take some time since by default, all distributions are tried
# You can manually provide a smaller set of distributions to speed up the process
f.summary()

```

![Fitter Example](http://pythonhosted.org/fitter/_images/index-1.png)

See the [online documentation](http://fitter.readthedocs.io/) for more details.

# Running Tests

To run the test suite for fitter, follow these steps:

1.  Clone the repository and install development dependencies:

```bash
git clone https://github.com/tg12/fitter
cd fitter
pip3 install -e ".[dev]"

```

2.  Navigate to the tests directory:

```bash
cd tests

```

3.  Run the test suite using the provided test runner:

```bash
python3 run_tests.py

```

### Additional Test Options

The test runner supports several useful options:

-   Run with verbose output:
    
    ```bash
    python3 run_tests.py -v
    
    ```
    
-   Run a specific test file:
    
    ```bash
    python3 run_tests.py -f test_fitter.py
    
    ```
    
-   Run tests matching a specific keyword:
    
    ```bash
    python3 run_tests.py -k "common"
    
    ```
    
-   Specify an alternative test directory:
    
    ```bash
    python3 run_tests.py -d ../other_tests
    
    ```
    

The test runner automatically handles src directory structures and ensures proper import paths are configured.

# Contributors

Setting up and maintaining Fitter has been possible thanks to users and contributors. Thanks to all:

.. image:: https://contrib.rocks/image?repo=cokelaer/fitter :target: https://github.com/cokelaer/fitter/graphs/contributors

# Changelog

Version

Description

1.7.1

* Integrate PR github.com/cokelaer/fitter/pull/100 from @vitorandreazza to speedup multiprocessing run.

1.7.0

* Replace logging with loguru<br>* Main application update to add missing --output-image option and use rich_click<br>* Replace pkg_resources with importlib

1.6.0

* For developers: uses pyproject.toml instead of setup.py<br>* Fix progress bar fixing https://github.com/cokelaer/fitter/pull/74<br>* Fix BIC formula https://github.com/cokelaer/fitter/pull/77

1.5.2

* PR https://github.com/cokelaer/fitter/pull/74 to fix logger

1.5.1

* Fixed regression putting back joblib

1.5.0

* Removed easydev and replaced by tqdm for progress bar<br>* Progressbar from tqdm also allows replacement of joblib need

1.4.1

* Update timeout in docs from 10 to 30 seconds by @mpadge in https://github.com/cokelaer/fitter/pull/47<br>* Add Kolmogorov-Smirnov goodness-of-fit statistic by @lahdjirayhan in https://github.com/cokelaer/fitter/pull/58<br>* Switch branch from master to main

1.4.0

* get_best function now returns the parameters as a dictionary of parameter names and their values rather than just a list of values (https://github.com/cokelaer/fitter/issues/23) thanks to contributor @kabirmdasraful<br>* Accepting PR to fix progress bar issue reported in https://github.com/cokelaer/fitter/pull/37

1.3.0

* Parallel process implemented https://github.com/cokelaer/fitter/pull/25 thanks to @arsenyinfo

1.2.3

* Remove verbose arguments in Fitter class. Using the logging module instead<br>* The Fitter.fit has now a progress bar<br>* Add a standalone application called fitter (see the doc)

1.2.2

Was not released

1.2.1

* Adding new class called histfit (see documentation)

1.2

* Fixed the version. Previous version switched from 1.0.9 to 1.1.11. To start a fresh version, we increase to 1.2.0<br>* Merged pull request required by bioconda<br>* Merged pull request related to implementation of AIC/BIC/KL criteria (https://github.com/cokelaer/fitter/pull/19). This also fixes https://github.com/cokelaer/fitter/issues/9<br>* Implement two functions to get all distributions, or a list of common distributions to help users decreasing computational time (https://github.com/cokelaer/fitter/issues/20). Also added a FAQS section.<br>* Travis tested Python 3.6 and 3.7 (not 3.5 anymore)

1.1

* Fixed deprecated warning<br>* Fitter is now in readthedocs at fitter.readthedocs.io

1.0.9

* https://github.com/cokelaer/fitter/pull/8 and 11<br>* PR https://github.com/cokelaer/fitter/pull/8

1.0.6

* summary() now returns the dataframe (instead of printing it)

1.0.5

* https://github.com/cokelaer/fitter/issues

1.0.2

* Add manifest to fix missing source in the pypi repository.
