---
title: "Python 예외 처리"
slug: "Python 예외 처리"
categories: Python
---


- 에러가 났을때 프로그램이 종료된다는 등의 원치 않는 상황을 피하기 위해 사용한다.

```python
try:
	시도할 코드
	
except:
	에러가 발생했을때 실행할 코드
	
else:
	에러가 발생하지 않았을때 실행할 코드
```

##### 여러가지 에러를 구분할 경우

```python
try:
	시도할 코드

except <예외클래스1>:
	<예외클래스1> 경우에 실행할 코드
	
except <예외클래스2>:
	<예외클래스2> 경우에 실행할 코드
	
except <예외클래스3>:
	<예외클래스3> 경우에 실행할 코드
...
else:
	에러가 발생하지 않았을때 실행할 코드
```

##### 예외사항을 변수로 사용할 경우

```pyhton
import random


l = random.sample(range(10), 10)
dic = {'apple': 'red'}


try:
    print(l[20])
    print(dic['yellow'])
    
# 에러의 클래스를 변수 e로 지정
except IndexError as e:
    print('리스트의 범위를 벗어났습니다.')
    print(e)
    
# 위에서 에러가 걸리면 처음 걸린 부분만 실행된다.
except KeyError as e:
    print('입력한 {}는 해당 딕셔너리에 키로 존재하지 않습니다.'.format(e))
    
print('program terminated')
```

### try ~ else

- else는 try 이후 예외가 발생하지 않았을때 사용

```python
try:
	시도할 코드
	
except:
	에러가 발생했을때 실행할 코드
	
else:
	에러가 발생하지 않았을때 실행할 코드
```

### try ~ finally

- finally는 try에서 에러가 발생하든 발생하지 않은 마지막에 실행된다.

```python
try:
	시도할 코드
	
except:
	에러가 발생했을때 실행할 코드
	
else:
	에러가 발생하지 않았을때 실행할 코드
	
finally:
	에러가 발생하든 발생하지 않은 마지막에 실행할 코드

```

### 예외 발생시키기 raise

- 예외를 발생시킬때 `raise`를 사용한다.

```python
"""
1. 정규표현식으로 검사했을때 일치하는 패턴이 없을 경우 발생할 NotMatchedException을 정의
2. 패턴문자열과 소스문자열을 매개변수로 갖는 search_from_source함수를 정의하고, re.search에 소스 문자열을 전달했을때 MatchObject를 찾지 못하면 NotMatchedException을 발생시킴
3. try~except 구문에서 위 함수를 실행해 예외를 발생시킴 (raise NotMatchedException(arg1, arg2))
4. 위 구문에서 else절을 추가해서 예외가 발생하지 않았을 경우 검색결과를 출력
5. 위 구문에 finally절을 추가해서 프로그램이 끝났음을 출력
"""

import re


class NotMatchedException(Exception):
    """
    패턴과 소스를 받아 매치되지 않았음을 알려주는 Exception 클래스
    """
    def __init__(self, pattern_string, source_string):
        self.pattern_string = pattern_string
        self.source_string = source_string
	
	# 스트링을 출력하는 내장함수, 클래스가 호출되면 항상 아래 내용이 출력됨
    def __str__(self):
        return 'Pattern "{}" is not matched in source "{}"'.format(
            self.pattern_string,
            self.source_string,
        )


def search_from_source(pattern_string, source_string):
    # re.search는 찾으면 찾은 문자열을 반환, 못찾으면 None을 반환
    result = re.search(pattern_string, source_string)
    # 결과가 나오면 결과를 반환
    if result:
        return result
    # 결과가 나오지 않으면 예외로 NoMatchedException를 발생시킨다.
    raise NotMatchedException(pattern_string, source_string)

try:
    source = 'Lux, the Lady of ewrwerer'
    pattern = "Man"
    # pattern = r'L\w{3}\b'
    m = search_from_source(pattern, source)
    
    # NotMatchedException 예외가 발생했을 경우
except NotMatchedException as e:
    print(e)
    
    # 에러가 발생하지 않았을 경우
else:
    print('Search result : {}'.format(m.group()))
    
    # 에러가 발생하든 발생하지 않든 아래 내용이 실행
finally:
    print('Program terminated')
```

#### 참고 

##### style guide for python

- 코딩 스타일을 정해놓았음

##### 파이참에서 reformat code 

- 파이참에서 알아서 문서를 정리해줌. 띄어쓰기, 줄 나누기 등...
- 커맨드+알트+L  



