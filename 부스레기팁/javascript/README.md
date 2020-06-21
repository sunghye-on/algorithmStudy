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

