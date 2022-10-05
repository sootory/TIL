# 세미프로젝트
## 데이터 전처리 및 단어 빈도 분석
- 트위터 api를 활용하여 수집한 데이터에 대한 전처리(colab)
  
1. 한글모음자음 및 특수문자 제거
```python
import pandas as pd
import numpy as np
import re

df = pd.read_excel('./파일명.xlsx')
df.head()
df.info()

# 한글 모음 자음 제거
df["comments"] = df["comments"].apply(lambda x : re.sub(pattern = '([ㄱ-ㅎ ㅏ-ㅣ]+)',repl= " ", string = str(x)))

# 특수문자 제거
df["comments"] = df["comments"].str.replace(pat=r'[^\w]', repl=r'', regex=True)

# 엑셀 파일 저장
df.to_excel('./파일명.xlsx', index=False)
```

2. 명사 추출 및 빈도 분석

```python

from konlpy.tag import Twitter
twt = Twitter()

all_word = []

for n in range(len(df)):
  text = df["comments"].iloc[n]
  words = twt.pos(text)

  for i, j in words:
    if j == 'Noun' : # 명사로 분류된 단어만 all_word에 추가
      all_word.append(i)

print(all_word)

# 각 단어당 숫자 1 count
all_word_df = pd.DataFrame({'words': all_word, 'count': len(all_word)*[1]})

# 단어별 count(등장 횟수)
all_word_df = all_word_df.groupby('words').count()

# 빈도수 높은 것부터 정렬
all_word_df.sort_values('count', ascending = False).head()
```

참고 자료:   
[블로그] [[BOAZ 프로젝트]크롤링 리뷰 데이터 전처리/벡터화](https://taek98.tistory.com/38)   
[블로그] [[데이터 전처리]. pandas Dataframe, Series 특수문자](https://acdongpgm.tistory.com/166)   
[블로그] [파이썬 자연어 처리(NLP)-konlpy를 활용한 형태소 분석/파이썬 데이터 분석 실무 테크닉 100](https://suy379.tistory.com/98)


