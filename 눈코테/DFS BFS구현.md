# DFS구현

## 깊이우선탐색

stack을 이용하여 탐색

아래와 같은 노드들이 생성된다고 하자

```javascript
const graph = {
  100: new Set([67, 66]),
  67: new Set([100, 82, 63]),
  66: new Set([100, 73, 69]),
  82: new Set([67, 61, 79]),
  63: new Set([67]),
  73: new Set([66]),
  69: new Set([66, 65, 81]),
  61: new Set([82]),
  79: new Set([82, 87, 77]),
  65: new Set([69, 84, 99]),
  81: new Set([69]),
  87: new Set([79, 31, 78]),
  77: new Set([79]),
  84: new Set([65]),
  99: new Set([65]),
  31: new Set([87]),
  78: new Set([87]),
};
```

```javascript
const DFS = (graph, start) => {
  // 스택
  let stack = [start];
  // 방문 기록을 저장할 배열
  let path = [];

  while (stack) {
    // 다음 방문 노트
    let node = 0;
    node = stack.pop();
    // 방문할 노드가 방문기록에 없으면 방문했다고 저장
    if (!path.includes(node)) {
      path.push(node);
      // 다음 노드들은 현재 노드를 제외한 나머지 노드들을 nextNodes에 저장
      let nextNodes = new Set(
        //그래프에 현재노드에서 filter를 이용해서 path에 없는 것으로만 새로운 집합 생성
        [...graph[node]].filter((s) => !new Set(path).has(s))
      );
      for (const i of nextNodes) {
        // 다음 노드들을 스택에 넣어준다.
        stack.push(i);
      }
      // console.log("방문", path);
      // console.log("stack", stack);
    }
    // stack이 비었으면 그만 하고 경로를 출력.
    if (stack.length == 0) {
      return path;
    }
  }
};
console.log("답 : ", DFS(graph, 100));
```



# 깊이우선탐색의 최대/최소값

위와같은 graph를 가질때 아래와 같은 코드로 구현이 가능하다 

우의 코드와 비슷하지만 달라지는 부분이 있다.

```javascript
const DFS = (graph, start) => {
  // 스택
  let stack = [start];
  // 방문 기록을 저장할 배열
  let path = [];

  while (stack) {
    // 다음 방문 노트
    let node = 0;
    node = stack.pop();
    // 방문할 노드가 방문기록에 없으면 방문했다고 저장
    if (!path.includes(node)) {
      path.push(node);
      // 다음 노드들은 현재 노드를 제외한 나머지 노드들을 nextNodes에 저장
      let nextNodes = new Set(
        //그래프에 현재노드에서 filter를 이용해서 path에 없는 것으로만 새로운 집합 생성
        [...graph[node]].filter((s) => !new Set(path).has(s))
      );
	  // 다음 노드가 없으면 끝난다.
      if (nextNodes.size == 0) {
        break;
      }
      // 다음 노드들 중 가장 큰/작은 값만을 push해줌으로 큰/작은 값을 따라간다.
      stack.push(Math.min(...nextNodes));
      stack.push(Math.max(...nextNodes));
        
      // 이제 이 구문은 필요없다
      // for (const i of nextNodes) {
      //   // 다음 노드들을 스택에 넣어준다.
      //   stack.push(i);
      // }
      console.log("방문", path);
      console.log("stack", stack);
    }
    // 여기도 필요없다.
    // stack이 비었으면 그만 하고 경로를 출력.
    // if (stack.length == 0) {
    //   break;
    // }
  }
  return path;
};
console.log("답 : ", DFS(graph, 100));
```



# BFS구현

## 너비우선탐색

위와 비슷한 원리로 탐색을 진행한다. stack을 사용하는 DFS에 비해 BFS는 queue를 사용한다.

위와 같은 graph를 사용할때  코드는 아래와 같다.

```javascript
const BFS = (graph, start) => {
  let q = [start];
  let path = [];

  while (q) {
    let node = 0;
    node = q.pop();

    if (!path.includes(node)) {
      path.push(node);
    }
    let nextNodes = new Set(
      [...graph[node]].filter((s) => !new Set(path).has(s))
    );

    for (const g of nextNodes) {
      // 큐이기 때문에 unshift를 해줌
      q.unshift(g);
    }
    console.log("방문", path);
    console.log("q", q);
    if (q.length == 0) {
      break;
    }
  }
  return path;
};
console.log("답 : ", BFS(graph, 100));
```

