# 부스레기 팁 

```python
print([i for i in range(10) if i % 2 == 0])
```

위와같이 [i for i in range] 처럼 쓸 수 있고 

해당 코드를 실행하면 2로 나눴을 때 나머지가 0인 것들의 List를 만들어준다.

예를 들어 구구단을 출력

```python
print([f'{i}X{j}={i*j}' for i in range(2, 9) for j in range(1, 9)])
```



```python
# 문자 리스트를 문자열로 연결시켜준다.
"".join(문자리스트)
# 자리수를 맞춰준다.(default로 0이 채워짐)
"123".zfile(5)
# 결과 00123
```



예를 들어 아래와 같이 있다. 

```python
s=['1001010','1000101','1001010','1010101']
```

그렇다면 위의 리스트를 2진수로바꾼뒤 문자형으로 바꾸는 작업을 2개지 방법으로 해보자

```python
# 람다를 이용
"".join(list(map(lamda x: char(int(s,2)),s)))
# 함수를 이용
def func(x):
    return char(int(s,2))

"".join(list(map(func,s)))
```

