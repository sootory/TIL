# 수업 내용 복습
## 통계 분석
1. tableone
> tableone은 환자군을 대상으로 하는 통계치의 요약인 "Table 1"을 만들기 위한 패키지임

```python
# Import libraries(라이브러리 호출)
from tableone import TableOne, load_dataset
import pandas as pd

# Load sample data into a pandas dataframe(샘플 데이터를 데이터프레임화)
data=load_dataset('pn2012')

# Optionally, a list of columns to be included in Table 1 (컬럼 리스트 생성)
columns = ['Age', 'SysABP', 'Height', 'Weight', 'ICU', 'death']

# Optionally, a list of columns containing categorical variables (범주형 변수 명시)
categorical = ['ICU', 'death']

# Optionally, a categorical variable for stratification(집단 간 차이를 검정할 때의 기준이 되는 집단), a list of non-normal variables(비정규성 데이터_정규 분포인 데이터도 nonnormal로 지정해도 큰 문제 없다고 함. non-normal을 normal로 취급하는 것이 더 문제가 될 수 있기 때문에 numeric variable은 전부 non-normal로 해도 된다 함), and a dictionary of alternative labels (열"death"를 이름 변경)

groupby = ['death']
nonnormal = ['Age']
labels={'death': 'mortality'}

# Create an instance of TableOne with the input arguments
mytable = TableOne(data, columns=columns, categorical=categorical, groupby=groupby, nonnormal=nonnormal, rename=labels, pval=False #True로 p-value 나타나게 할 수 있음)

# Display the table using the tabulate method
print(mytable.tabulate(tablefmt = "fancy_grid"))
```

참고 자료:
[tableone_pypi](https://pypi.org/project/tableone/),   
[tableone_colab](https://colab.research.google.com/github/tompollard/tableone/blob/master/tableone.ipynb#scrollTo=unzTcc5mH4d8), 수업 자료