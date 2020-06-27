# 부스레기 팁 javascript

## 기본적인 부스레기

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

//배열의 값들을 합쳐주는 join
let a = ['바람', '비', '불'];
let myVar1 = a.join();      // myVar1에 '바람,비,불'을 대입
let myVar2 = a.join(', ');  // myVar2에 '바람, 비, 불'을 대입
let myVar3 = a.join(' + '); // myVar3에 '바람 + 비 + 불'을 대입
let myVar4 = a.join('');    // myVar4에 '바람비불'을 대입
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



## 배열을 90도 회전 하기

```javascript
const arr1 = [
  [0, 0, 0, 0, 1],
  [0, 0, 0, 0, 3],
  [0, 0, 0, 0, 4],
  [0, 2, 0, 0, 2],
  [4, 5, 0, 2, 0],
];
// 반시계방향으로 90도 회전
const arr2 = [
  [1, 3, 4, 2, 0],
  [0, 0, 0, 0, 2],
  [0, 0, 0, 0, 0],
  [0, 0, 0, 2, 5],
  [0, 0, 0, 0, 4],
];
```

arr1을 arr2처럼 회전한 값을 resultArr에 저장하기 위한 코드

```javascript
// 배열의 크기 만큼 빈 배열을 선언
for (let i = 0; i < arr1.length; i++) {
  resultArr[i] = new Array(arr1[0].length);
}

for (let i = 0; i < arr1.length; i++) {
  for (let k = 0; k < arr1[0].length; k++) {
    resultArr[i][k] = arr1[k][arr1[0].length - 1 - i];
  }
}
// 확인
console.log(resultArr);
```





# call / apply / bind

## call

함수를 호출하면서 call을 사용하고 this로 사용할 객체를 넘기면 해당 함수가 주어진 객체의 메소드인 것 처럼 사용할 수 있다. 아래의 예시를 확인하자

```javascript
const dongdong = {
  name: "dongdong",
};

const sungsung = {
  name: "sungsung",
};

//이 함수는 어떤 객체에도 연결되지 않았지만 this를 사용함.
function sayHi() {
  return `Hello, I'm ${this.name}`;
}

sayHi(); // 'Hello, I'm undefined' - this는 어디에도 묶이지 않음
sayHi.call(dongdong); // 'Hello, I'm dongdong'     - this는 dongdong
sayHi.call(sungsung); // 'Hello, I'm Madeline'  - this는 sungsung

```



## apply

함수 매개변수를 처리하는 방법을 제외하면 call과 일치한다. 큰 차이점이라면 apply는 매개변수를 배열로 받는다. 흔하게 사용하는 예시로 Math.min/max가 있다.

```javascript
Math.max.apply(null, list);
// 혹은 ES6문법의 spread연산자를 이용해서 아래와 같이 사용할 수 있다.
Math.max/min(...list);
```





## bind

bind를 사용하면 함수의 this 값을 영구히 바꿀 수 있다. 메서드를 이리저리 옮기면서 호출할 때 this 값은 항상 bruce가 되게끔, call이나 apply, 다른 bind와 함께 호출하더라도 this 값이 변경된 값이 되도록 하려면 bind를 사용한다.





# reduce

## 설명

reduce() 메서드는 배열의 각 요소에 대해 주어진 **리듀서**(reducer) **함수**를 실행하고, 하나의 결과값을 반환합니다.

**리듀서** 함수는 네 개의 인자를 가집니다.

1. 누산기accumulator (acc)
2. 현재 값 (cur)
3. 현재 인덱스 (idx)
4. 원본 배열 (src)

리듀서 함수의 반환 값은 누산기에 할당되고, 누산기는 순회 중 유지되므로 결국 최종 결과는 하나의 값이 됩니다.



## 간단한 예시

```javascript
const list = [10, 20, 30, 40, 1, 2, 3, 4, 11, 45];

// 각각의 값을 더하는 함수
const func = (accumulator, currentValue) => {
  console.log(accumulator, currentValue);
  return accumulator + currentValue;
};
console.log(list.reduce(func));

// 중첩된 배열 펼치기
const listlist = [[0, 1],[2, 3],[4, 5]];

const func2 = (accumulator, currentValue) => {
  return accumulator.concat(currentValue);
};
console.log(listlist.reduce(func2));
```

## 활용하기

```javascript
// 객체 속성으로 분류하기
let people = [
  { name: "Alice", age: 21 },
  { name: "Max", age: 20 },
  { name: "Jane", age: 20 },
  { name: "mikle", age: 22 },
  { name: "tuyr", age: 21 },
];

function groupBy(objectArray, property) {
  return objectArray.reduce(function (acc, obj) {
    let key = obj[property];
    if (!acc[key]) {
      acc[key] = [];
    }
    acc[key].push(obj);
    return acc;
  }, {});
}

let groupedPeople = groupBy(people, "age");
console.log(groupedPeople);
```

[더보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)