# 부스레기 팁 javascript

기본적인 것들

```javascript
// shift , unshift / push, pop을 이용한 부스레기
// 맨압에 있는 걸 지우고 뒤에 추가 
a.push(a.shift())

// splice의 응용
//하나도 제거하지 않고 2번인덱스에 "test","test2"추가
let newList = list.splice(2,0,"test","test2");
//3번인덱스에서 n개의 요소 제거
let newLis = list.splice(3, n);
//2번인덱스에서 한개의 요소를 제거하고 "test"추가
let newList = list.splice(2,1,"test");
//뒤에서 2번째인덱스에서 한개의 요소를 제거
let newList = list.splice(-2, 1);
//2번 인덱스를 포함해서 이후의 모든 요소 제거
let newList = list.splice(2)
```



## indexOf() 과 search()

### indexOf()

indexOf는 메서드는 배열에서 지정된 요소를 찾을 수 있는 첫 번째 인덱스를 반환하고 존재하지 않으면 -1을 반환합니다.

 ===을 사용하여 검색요소를 배열과 비교한다.

### search()

search는 메서드는 정규 표현식과 String 객체간에 같은 것을 찾기
위한 검색을 실행한다.

즉 매개변수로 정규표현식이 들어가며 그것으로 검색한다.

### 결론

정규식을 사용하는 검색은 search가 빠르고 단순한 검색은 indexOf 가빠르다.