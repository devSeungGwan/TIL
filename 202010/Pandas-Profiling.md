# 개요

Kaggle에서 EDA(Exploratory Data Analysis) 연습을 하다가 pandas-profiling이라는 라이브러리를 발견할 수 있었다. 해당 라이브러리는 DataFrame인 데이터를 EDA를 할 수 있도록 여러방면으로 데이터를 나타내준다. 

`ProfileReport(pd.DataFrame)`를 실행하여 DataFrame을 분석할 수 있다. 해당 자료에는 다음과 같은 내용이 포함되어 있다.

- **Type inference**: detect the [types](https://github.com/pandas-profiling/pandas-profiling#types) of columns in a dataframe.
- **Essentials**: type, unique values, missing values
- **Quantile statistics** like minimum value, Q1, median, Q3, maximum, range, interquartile range
- **Descriptive statistics** like mean, mode, standard deviation, sum, median absolute deviation, coefficient of variation, kurtosis, skewness
- **Most frequent values**
- **Histogram**
- **Correlations** highlighting of highly correlated variables, Spearman, Pearson and Kendall matrices
- **Missing values** matrix, count, heatmap and dendrogram of missing values
- **Text analysis** learn about categories (Uppercase, Space), scripts (Latin, Cyrillic) and blocks (ASCII) of text data.
- **File and Image analysis** extract file sizes, creation dates and dimensions and scan for truncated images or those containing EXIF information.

# 설치

### pip

```sh
pip install pandas-profiling
```

### Conda

```sh
conda install -c conda-forge pandas-profiling
```

# 사용

```python
import pandas as pd
from pandas_profiling import ProfileReport

df = pd.read_csv("csv_src")
profile = ProfileReport(df, title="Desired Title")
```

# 예시

- [Census Income](https://pandas-profiling.github.io/pandas-profiling/examples/master/census/census_report.html) (US Adult Census data relating income)
- [NASA Meteorites](https://pandas-profiling.github.io/pandas-profiling/examples/master/meteorites/meteorites_report.html) (comprehensive set of meteorite landings) [![Open In Colab](https://camo.githubusercontent.com/52feade06f2fecbf006889a904d221e6a730c194/68747470733a2f2f636f6c61622e72657365617263682e676f6f676c652e636f6d2f6173736574732f636f6c61622d62616467652e737667)](https://colab.research.google.com/github/pandas-profiling/pandas-profiling/blob/master/examples/meteorites/meteorites.ipynb) [![Binder](https://camo.githubusercontent.com/483bae47a175c24dfbfc57390edd8b6982ac5fb3/68747470733a2f2f6d7962696e6465722e6f72672f62616467655f6c6f676f2e737667)](https://mybinder.org/v2/gh/pandas-profiling/pandas-profiling/master?filepath=examples%2Fmeteorites%2Fmeteorites.ipynb)
- [Titanic](https://pandas-profiling.github.io/pandas-profiling/examples/master/titanic/titanic_report.html) (the "Wonderwall" of datasets) [![Open In Colab](https://camo.githubusercontent.com/52feade06f2fecbf006889a904d221e6a730c194/68747470733a2f2f636f6c61622e72657365617263682e676f6f676c652e636f6d2f6173736574732f636f6c61622d62616467652e737667)](https://colab.research.google.com/github/pandas-profiling/pandas-profiling/blob/master/examples/titanic/titanic.ipynb) [![Binder](https://camo.githubusercontent.com/483bae47a175c24dfbfc57390edd8b6982ac5fb3/68747470733a2f2f6d7962696e6465722e6f72672f62616467655f6c6f676f2e737667)](https://mybinder.org/v2/gh/pandas-profiling/pandas-profiling/master?filepath=examples%2Ftitanic%2Ftitanic.ipynb)
- [NZA](https://pandas-profiling.github.io/pandas-profiling/examples/master/nza/nza_report.html) (open data from the Dutch Healthcare Authority)
- [Stata Auto](https://pandas-profiling.github.io/pandas-profiling/examples/master/stata_auto/stata_auto_report.html) (1978 Automobile data)
- [Vektis](https://pandas-profiling.github.io/pandas-profiling/examples/master/vektis/vektis_report.html) (Vektis Dutch Healthcare data)
- [Colors](https://pandas-profiling.github.io/pandas-profiling/examples/master/colors/colors_report.html) (a simple colors dataset)

# 결론

사람마다 데이터를 통해 보고 싶은 내용은 다르다. 그렇기 때문에 다방면으로 데이터를 수집하고 분석하는 업무가 필요한데 해당 라이브러리는 이에 대한 업무를 어느정도는 신속하게 진행해줄 수 있다. 하지만 해당 라이브러리는 모든 데이터에 대한 전반적인 분석을 해주기 때문에 비지니스 워크플로에 맞춘 데이터 분석은 해주지 못한다. 그러므로 해당 라이브러리를 너무 맹신하진 말고, 분석 자료 중 하나라 생각하면 좋겠다고 생각한다. 데이터를 보는 시각의 견해를 늘리는 것이 중요하다.

# Reference

Pandas-Profiling GitHub([Link](https://github.com/pandas-profiling/pandas-profiling))

Document([Link](https://pandas-profiling.github.io/pandas-profiling/docs/master/rtd/pages/introduction.html))

판다스 프로파일링(Pandas-Profiling)([Link](https://wikidocs.net/47193))