---
title:  "Data Structure (자료 구조) - 1"
excerpt: "Stack / Queue / Linked List / Hash Table"

categories:
  - studynote
tags:
  - Javascript
  - Data Structure
last_modified_at: 2020-05-06
---

<br>
  
---

<br>

&nbsp;'Data Structure (자료 구조)'란, 어떤 데이터(자료)들을 효율적으로 사용할 수 있도록 일정한 방식으로 구성하는 방식을 말합니다.  

&nbsp;쉬운 예로는 어떤 자료들을 한데 묶어 나열해 둔 "배열"이 있습니다.  

&nbsp;이하에서는 다음 네 가지의 자료구조에 관하여 공부하려고 합니다.

1. Stack  
2. Queue          
3. Linked List  
4. Hash Table  

<br>
&nbsp;다음과 같은 내용에 중점을 두며 공부하도록 하겠습니다.  

  &nbsp;&nbsp;(a) 개념의 이해 뿐만 아니라 직접 자료구조를 구현해야 한다면 어떻게 코드를 작성해야 할지 생각하기  
  &nbsp;&nbsp;(b) 자료 구조의 모양 추상적으로 그림 그리기  
  &nbsp;&nbsp;(c) 해당 자료구조가 가지고 있는 property 와 method 찾아보기  
  &nbsp;&nbsp;(d) 각 method는 어떻게 동작되는 것인지 알아보고 의사 코드 직접 작성해보기  
  &nbsp;&nbsp;(e) 블로그 플랫폼 등에 TIL 형식으로 기록하기  

<br>
  
---

<br>

# 1. Stack  

## &nbsp;&nbsp;(1) 개념  
&nbsp;'Stack'은, 영어 단어의 뜻 그대로, 데이터가 쌓여 나가는 선형 구조의 Data Structure 입니다.  
&nbsp;데이터의 입/출력이 모두 한 지점에서만 일어나므로, 데이터가 새로 생길 때에는 순서에 따라 다음, 그 다음 순서로 차곡차곡 쌓여가며 구성되며, 데이터가 사라질 때에는 역순으로 가장 나중의 것부터 사라지게 됩니다.  
&nbsp;이러한 순서를 '선출선입' / 'LIFO(Last In First Out)' / 'FILO(First In Last Out)' 이라고 표현합니다.  
<br>
&nbsp;실생활에서 볼 수 있는 Stack의 쉬운 예시가 바로 '접시 쌓기' 입니다.  
새로운 접시를 밑 또는 중간에서 끼워넣을 수는 없으며, 새로운 접시를 추가하고 싶다면 언제나 가장 위에 올려놓게 됩니다.  
&nbsp;쌓여있는 점시를 밑 또는 중간에서 빼낼 수는 없으며, 접시를 빼내고 싶다면 가장 위의 접시를 빼내야만 합니다.  
&nbsp;이렇게, 접시(자료)를 올려놓거나 빼내는 것(입력과 출력)이 가장 위(하나의 지점)에서만 가능하다는 점에서, Stack과의 유사성을 찾을 수 있습니다.  

## &nbsp;&nbsp;(2) methods  

 - `.size()` : 스택 전체에 몇 개의 요소가 존재하는지를 반환합니다.  
 - `.push()` : 배열과 마찬가지로, 스택의 가장 마지막(위)에 새로운 요소를 추가합니다.  
 - `.pop()` : 배열과 마찬가지로, 스택의 가장 마지막(위)의 요소를 제거하고, 그 제거한 요소를 반환합니다.   
 - `.top()` / `.peek()` : 현재 스택의 가장 마지막(위)의 요소를, 삭제하지 않고 그대로 반환합니다. 


## &nbsp;&nbsp;(3) 예시  

&nbsp;이후의 새로운 스택을 생성할 때마다 사용할 수 있도록, 생성자 함수 형식으로 기본 틀을 작성합니다.  
```js
// Stack class 
class Stack {   
    // Array can be used to implement stack 
    constructor() { 
      this.storage = {}; 
      this.top = 0;
    } 
    // Functions to be implemented 
      // push(element) 
      // pop() 
      // peek() 
      // isEmpty() 
      // printStack() 
} 
```  

&nbsp;위 코드에서는 `this.storage` 부분이 빈 객체로 선언되었지만, 배열로 선언해주는 방법 역시 가능합니다.  
&nbsp;`constructor() {  }` 안쪽에다가, 스택에서 사용할 메소드들을 선언해 줍니다.  
<br>

&nbsp;(1) `.size()` / `.push()` / `.pop()` / `.peek()` 메소드는 각각 다음과 같이 작성할 수 있습니다.  
```js
size() {
  return Object.keys(this.storage).length;
}

push(element) { 
  this.storage[this.top + 1] = element;
  this.top += 1;
}

pop() { 
  if (this.size() === 0) {
    return "Underflow";
  } // Underflow if stack is empty
  
  let result = this.storage[this.top];
  delete this.storage[this.top];
  this.size() -= 1
  return result;
} 

peek() {  
  return this.storage[this.top]; 
} 
```  
<br>

&nbsp;(2) 위와 같은 기본 메소드 외에, 아래와 같은 메소드를 고려할 수 있습니다.  
```js
isEmpty() {  // return true if stack is empty     
  return this.top === 0; 
} 

printStack() {  // This method returns a string in which all the element of an stack is concatenated.
    let str = ""; 
    for (let i = 0; i < this.top; i++) 
        str += this.storage[i] + " "; 
    return str; 
}
```  
<br>

&nbsp;(3) 이 외에도, 필요에 따라 다른 메소드를 더 작성할 수 있지 않을까 합니다. 추가할 수 있는 다른 메소드를 고려해 보도록 하겠습니다.  

&nbsp;예를 들면, 'clear() : (함수) 스택의 모든 요소 삭제하기' 등의 기능을 구현할 수 있을 것 같습니다.  


## &nbsp;&nbsp;(4) 참고자료
 - [Stack Data Structure](https://www.geeksforgeeks.org/stack-data-structure/)  
 - [Implementing Javascript Stack Using an Array](https://www.javascripttutorial.net/javascript-stack/)  
 - [Implementation of Stack in JavaScript](https://www.geeksforgeeks.org/implementation-stack-javascript/)  
 - [[Immersive_Sprint.js] Stack & Queue](https://medium.com/@lyhlg0201/immersive-sprint-js-stack-queue-426ccfbdb602)  
 - [큐, 스택, 트리](https://helloworldjavascript.net/pages/282-data-structures.html)  
 - [JavaScript 자료구조 - Stack (스택) - Queue 2개로 Stack 구현하기](https://velog.io/@ryu/JavaScript-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Stack-%EC%8A%A4%ED%83%9D)  
 - [[자료구조] 자바스크립트로 스택(Stack) 구현](https://blog.naver.com/PostView.nhn?blogId=javaking75&logNo=220226369586&categoryNo=71&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView)  
 - [[Immersive_Sprint.js] Stack & Queue](https://medium.com/@lyhlg0201/immersive-sprint-js-stack-queue-426ccfbdb602)  

<br>
  
---

<br>

# 2. Queue 

## &nbsp;&nbsp;(1) 개념  
&nbsp;'Queue'는, 역시 영어 단어의 뜻 그대로, 데이터가 '줄을 선' 형태라고 볼 수 있습니다.  
&nbsp;'Stack'과는 달리, 데이터의 입력이 일어나는 지점과 출력이 일어나는 지점이 다릅니다.  
&nbsp;그래서 입력에서는, 먼저 입력된 데이터(A)가 존재하고, 그 이후에 존재하는 데이터(B, C, D)는 들어온 순서대로 줄을 서게 됩니다.  
&nbsp;이후 출력시에는, 출력은 입력과는 다른 지점에서 이루어지므로, 먼저 입력된 데이터(A)가 먼저 출력되고, 그 다음에는 B, C, D 순서로, 즉 데이터가 입력되어 줄을 서 있는 바로 그 순서 그대로, 출력되게 됩니다.  
&nbsp;이러한 순서를 '선입선출' / 'FIFO(First In First Out)' / 'LILO(Last In Last Out)' 이라고 표현합니다.  
<br>
&nbsp;실생활에서 볼 수 있는 Queue의 쉬운 예시가 바로 '줄 세우기' 입니다.  
&nbsp;먼저 줄에 들어선(입력) 사람(자료)만이 먼저 줄에서 나갈 수 있고(출력), 나중에 줄에 선 사람은 먼저 선 사람의 뒤에만 서게 됩니다.  
&nbsp;줄을 서면 끼어들기를 하지 못하듯이, Queue 역시 입력과 출력이 한 곳에서만 일어날 수 있으므로, 새로운 데이터를 기존의 Queue 안의 어느 지점에 끼워넣을 수가 없습니다.  


## &nbsp;&nbsp;(2) methods  

 - `.size()` : Queue의 현재 요소 개수를 반환합니다.  
 - `enqueue(element)` : 요소를 Queue의 뒤에 추가합니다.     
 - `dequeue()` : 요소를 Queue의 앞에서 제거하고 반환합니다.  

## &nbsp;&nbsp;(3) 예시  

&nbsp;다음과 같이 작성하여, 생성자 함수를 만들었습니다.  

```js
class Queue {
  constructor() {
    this.storage = {};
    this.front = 0; // 맨 앞
    this.rear = 0;  // 맨 뒤
  }
}
```  

&nbsp;이제, `let q = new Queue();` 라는 코드를 통해, q 라는 새로운 queue 자료구조를 생성할 수 있습니다.  

&nbsp;`this.storage` 항목은 queue 안에 포함된 각 요소들의 집합입니다.  

&nbsp;`this.front` 항목은 가장 앞에 있는 요소의 인덱스(?), `this.rear` 항목은 가장 뒤에 있는 요소의 인덱스(?)입니다.  
&nbsp;  

&nbsp;이러한 생성자 함수 안에, 여러 메소드를 구현해 보았습니다.

&nbsp;(1) `.size()` / `enqueue(element)` / `dequeue()` 메소드는 다음과 같이 작성하였습니다.  

```js
  size() {  // 전체 요소들의 수를 반환합니다.  
      return Object.keys(this.storage).length;
    }

  enqueue(element) {  // 가장 뒷자리에 새로운 요소를 추가합니다.  
    this.storage[this.rear] = element;
    this.rear += 1;
  }

  dequeue() {  // 가장 앞에 존재하는 요소를 삭제하고 이를 반환합니다.
    let answer = this.storage[this.front];
    delete this.storage[this.front];
    this.front += 1;
    return answer;
  }
```  

&nbsp;이 외에도 다른 메소드들을 생각할 수 있겠습니다. 구현할 수 있는 방법을 고민하여 코드를 추가하려 합니다.  

&nbsp;가령 `front()`, `isEmpty()`, `printQueue()` 등의 메소드를 구현해 보려 합니다.  


## &nbsp;&nbsp;(4) 참고자료 
 - [Implementation of Queue in Javascript](https://www.geeksforgeeks.org/implementation-queue-javascript/)  
 - [[자료구조][Javascript] Queue 란?](https://medium.com/@songjaeyoung92/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-javascript-queue-%EB%9E%80-dbd8b2fffeac)  
 - [JavaScript Queue](https://www.javascripttutorial.net/javascript-queue/)  
 - [JavaScript 자료구조 - Stack (스택) - Stack 2개로 Queue 구현하기](https://velog.io/@ryu/JavaScript-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Stack-%EC%8A%A4%ED%83%9D)  
 - [[Immersive_Sprint.js] Stack & Queue](https://medium.com/@lyhlg0201/immersive-sprint-js-stack-queue-426ccfbdb602)  

<br>
  
---

<br>

# 3. Linked List  

## &nbsp;&nbsp;(1) 개념  
연결 리스트는 일련의 원소를 배열처럼 차례대로 저장하지만, 원소들이 메모리상에 연속적으로 위치하지 않는다 (배열과의 차이점) - 소년코딩

배열에 비해 데이터의 추가/삽입 및 삭제가 용이하나 순차적으로 탐색하지 않으면 특정 위치의 요소에 접근할 수 없어 일반적으로 탐색 속도가 떨어진다.

즉 탐색 또는 정렬을 자주 하면 배열을, 추가/삭제가 많으면 연결 리스트를 사용하는 것이 유리하다. 


'데이터를 저장할 장소(this.value)'와 '다른 변수를 가리키기 위한 장소(this.next)'가 구분되어 있다

```js
class Node {            
  constructor(value) {
    this.value = value;
    this.next = null;  
  }
}
```

## &nbsp;&nbsp;(2) methods  

 - `.addToTail(value)` : 주어진 값을 Linked List의 끝에 추가합니다.
 - `remove(value)` : 주어진 값을 찾아서 연결을 해제(삭제)합니다. (구현을 위해 `shift()` / `pop()` 메소드를 추가로 작성했습니다.)
 - `getNodeAt(index)` : 주어진 인덱스의 노드를 찾아서 반환합니다. (값이 아니라 노드를 반환해야 합니다. 해당 인덱스에 노드가 없다면 undefined를 반환합니다.)  
 - `contains(value)` : Linked List에 주어진 값을 가지는 노드의 존재 여부를 반환합니다.  
 - `indexOf(value)` : 주어진 값의 인덱스를 반환합니다. 없을 경우 -1을 반환합니다.  
 - `size()` : Linked List의 현재 요소 개수를 반환합니다.  


## &nbsp;&nbsp;(3) 예시  

&nbsp;역시 생성자 함수를 먼저 작성하였습니다.  

&nbsp;LinkedList 에서 활용할 개개의 Node 역시 아래와 같이 함께 작성하였습니다.  

```js
class Node {            // the Doubly Linked List consists of nodes
  constructor(value) {
    this.value = value; // each node has a value
    this.next = null;   // each node has a pointer to the next node (or null at the end of the list)
    // previous 가 없으니까, 이 문제는 singly linked list.   
    // Doubly Linked 에서는, each node has a pointer to the previous node (or null at the beginning of the list)
  }
}


class LinkedList {
  constructor() {
    this.head = null; // (= beginning)
    this.tail = null; // (= end)
    this._size = 0;   // '이 부분이 length를 대신하나?'  /  'index'는 대신하지 못하는 듯?
  }
}
```  

&nbsp;위의 'methods'에서 나열한 내용들을 아래와 같이 구현하였습니다.

```js
  addToTail(value) {  // 주어진 값을 연결 리스트의 끝에 추가합니다.
    let newNode = new Node(value);
    if (this._size === 0) {
      this.head = newNode;
      this.tail = newNode;
    }
    if (this._size > 0) {
      this.tail.next = newNode;
      this.tail = newNode;
    }
    this._size = this._size + 1;
    return newNode;
  }


  shift() {
    if (!this._size) {
      return null;
    } else {
      let nodeToRemove = this.head;
      this.head = this.head.next;
      this._size -= 1;
      if (!this._size) {
        this.tail = null;
      }
      return nodeToRemove;
    }
  }


  pop() {
    if (!this._size) {
      return null;
    } else {
      let nodeToRemove = this.tail;
      this.tail = this.getNodeAt(this._size - 1)
      this._size -= 1;
      if (!this._size) {
        this.tail = null;
      }
      return nodeToRemove;
    }

  }


  remove(value) { //  주어진 값을 찾아서 연결을 해제(삭제)합니다 : 인덱스 기준이 아니라, 값을 기준으로 삭제함
    if (this.head.value === value) {
      this.shift();
    }
    else if (this.tail.value === value) {
      this.pop();
    }
    
    else{
      let valIndex = this.indexOf(value);
      let removeNode = this.getNodeAt(valIndex);
      this.getNodeAt(valIndex).next = null;
      let exNode = this.getNodeAt(valIndex-1);
      exNode.next = this.getNodeAt(valIndex+1);
      this._size -= 1;
      return removeNode;
    }
  }


  getNodeAt(index) {  // 주어진 인덱스의 노드를 찾아서 반환합니다. 값이 아니라 노드를 반환해야 하는 것에 주의하세요. 
      // index번째의 Node 얻기 - 이 문제는 해결한듯
    if (index < 0 || index > this._size) {
      return undefined;
    }

    else {
      let currentNode = this.head;
      let count = 0;
      while (count < index) { // 궁금한 점 : for문으로 하면 안되는 이유는 이게 '배열이 아니어서'인가?
        currentNode = currentNode.next;
        count = count + 1;
      }
      return currentNode;
    }
  }


  contains(value) {   // 연결리스트에 주어진 값을 가지는 노드의 존재 여부를 반환합니다.
      // Node가 현재 존재하는지 확인 : true / false
    let answer = false;
    if (this.indexOf(value) !== -1) {
      answer = true;
    }
    return answer;
  }


  indexOf(value) {  // 주어진 값의 인덱스를 반환합니다. 없을 경우 -1을 반환합니다.
    let currentNode = this.head;
    let count = 0;
    let answer = -1;
      while (count < this._size) {
        if (currentNode.value !== value) {
          currentNode = currentNode.next;
          count = count + 1
        }
        else if (currentNode.value === value) {
          answer = count;
          count = count +1;
        }
      }
    return answer;
  }


  size() { // 데이터 개수를 반환한다. 배열의 length 프로퍼티와 비슷하다.
    return this._size;
  }

```  

&nbsp;이 외에도 여러 메소드를 더 생각해 볼 수 있겠습니다.  

&nbsp;또한, linked list 는 'Doubly linked list'와 'Singly Linked List'라는 별개의 형태가 존재할 수 있습니다.  

&nbsp;이에 따라 추가되는 개념과 메소드 역시 더 공부하여 추가하도록 하겠습니다.  



## &nbsp;&nbsp;(4) 참고자료
 - [Doubly linked list (이중 연결 리스트)](https://opentutorials.org/module/1335/8940)  
 - [JavaScript Data Structures: Singly Linked List](https://dev.to/miku86/javascript-data-structures-singly-linked-list-2og)  
 - [JavaScript Data Structures: Doubly Linked List: Intro and Setup](https://dev.to/miku86/javascript-data-structures-doubly-linked-list-intro-and-setup-275b)  
 - [자바스크립트 자료구조 연결 리스트(Linked List)](https://boycoding.tistory.com/33)
 - [Where are linked lists used in real life?](https://www.quora.com/Where-are-linked-lists-used-in-real-life)  

<br>
  
---

<br>

# 4. Hash Table 

## &nbsp;&nbsp;(1) 개념  
&nbsp;'Hash Table'은 쌍으로 구성된 자료들의 모음에 보다 쉽고 빠르게 접근하기 위해 사용되는 자료구조 입니다.  
&nbsp;각 쌍의 자료의 이름(key)을 일정한 함수(hash function)를 사용하여 새롭게 구성된 숫자로 이루어진 hash index로 변경한 뒤, 기존 key에 대응하는 value를 연결하여 새롭게 저장하게 됩니다.  

## &nbsp;&nbsp;(2) 배열 및 객체와의 비교  
&nbsp;이렇게 자료를 저장할 수 있는 형태에는 배열과 (좁은 의미의)객체도 있습니다.  

&nbsp;배열은 index에 대응하는 값이 나열되는 묶음이라고 할 수 있습니다.  
&nbsp;개개의 값에 접근하거나, 어떤 위치의 값에 일정한 처리를 가하고 싶다면, index를 활용하여 배열 전체를 탐색하여야 합니다.  
<br>
&nbsp;객체는 key에 대응하는 값이 나열되는 묶음이라고 할 수 있습니다.  
&nbsp;개개의 값에 접근하기 위해 어떤 key를 탐색하는 경우, 객체의 key는 문자열이므로, key 문자열의 매 각각의 자리를 하나하나 비교하여 찿아내야 합니다.  가령 key가 1000자리의 문자열로 구성된 단어라면, 원하는 key와 객체 안의 key가 일치하는지 비교하려면 그 'key의 1000자리 문자열을 하나하나 비교'하는 연산이 필요해집니다.  
&nbsp;그러나, key를 hash function으로 처리하여 임의의 숫자로 만든다면, 훨씬 간단한 연산인 '숫자끼리의 비교'만으로도 그 값에 접근할 수 있게 됩니다. 이런 점 덕분에 Hash Table은 속도 면에서 상당한 장점을 가지고 있습니다.  

<br>

## &nbsp;&nbsp;(3) methods  

 - `insert(key, value)` : 주어진 키와 값을 저장합니다. 이미 해당 키가 저장되어 있다면 값을 덮어씌웁니다.  
 - `retrieve(key)` : 주어진 키에 해당하는 값을 반환합니다. 없다면 undefined를 반환합니다.  
 - `remove(key)` : 주어진 키에 해당하는 값을 삭제하고 값을 반환합니다. 없다면 undefined를 반환합니다.    
 - `_resize(newLimit)` : 해시 테이블의 스토리지 배열을 newLimit으로 리사이징하는 함수입니다. (리사이징 후 저장되어 있던 값을 전부 다시 해싱을 해주어야 합니다. 구현 후 HashTable 내부에서 사용합니다.)  

## &nbsp;&nbsp;(4) 예시  

&nbsp;이번에도 생성자 함수를 다음과 같이 작성하였습니다.  

```js
class HashTable {
  constructor() {
    this._size = 0;
    this._limit = 8;
    this._storage = LimitedArray(this._limit); // LimitedArray 함수는 객체 {} 형태를 리턴한다(?)
        // 그러므로 this._storage 는, {get: ƒ, set: ƒ, each: ƒ} 라는 객체 형태임.
  }

```  

&nbsp;그리고, 이를 위해 아래와 같이 메소드를 구현하였습니다.  

```js
  insert(key, value) { // 주어진 키와 값을 저장합니다. 이미 해당 키가 저장되어 있다면 값을 덮어씌웁니다.
    const index = hashFunction(key, this._limit);
      // this._storage[index] = value;  이것만 넣으면 에러 나옴. 아래와 같은 코드들이 필요함...

    const bucket = this._storage.get(index) || [];  // bucket은 어떤 경우이든 배열임. //  (1) || [] 이거는 왜 하는걸까?

    for (let i = 0; i < bucket.length; i += 1) { //하나의 index 안에서 연결되어 있는 bucket세트 모두를 탐색하여,
      const tuple = bucket[i];    // 하나의 bucket(세트) 안에서, i번째 값은 [ key , val ] 형태로, 그 안에 key와 val 2가지 값이 있다.  //  (2) 굳이 tuple에 넣어서 써야되나?
      if (tuple[0] === key) {     // 만약 key 와 i번째 값의 key가 같으면 : 이미 bucket(세트) 안의 i번째 세트에 같은 명칭의 key가 이미 존재하면,
        const oldValue = tuple[1];  // 일단 지금 있는 val 값을 저장해 두고,   (3) (왜?????)
        tuple[1] = value;   // 새로운 value 값으로 tuple[1] 을 대체하고,
        return oldValue;  // 이걸 왜 리턴하는건지 도대체 모르겠음   (4) (왜????? - 대체한 것을 리턴하는것도 아니고)
      }
    }   // 그래서, bucket을 다 뒤졌는데 (tuple[0] === key) 가 성립하지 않으면(새로 입력한 key가 현재 bucket에 존재하지 않으면), 아래 코드를 실행한다.

    bucket.push([key, value]);  // 위에서 뒤져봤는데 목록안에 없는 새로운 key니까, bucket에 추가(push)함.
    this._storage.set(index, bucket); // 스토리지의 index(hash) 위치에, 새롭게 push처리한 bucket을 입력(추가)한다.
    this._size += 1;  // 하나 늘었으니, 숫자도 하나 늘린다.

    if (this._size > this._limit * 0.75) {  // 새로운 키값 쌍을 추가한 뒤, 채워져 있는 정도를 확인하여, 점유율이 0.75 이상이면,
      this._resize(this._limit * 2);  // resize 함수를 실행하여 전체 리미트(해시 테이블의 공간)를 2배 증가시킨다.
    }

    return undefined; // (5) 왜 이걸 리턴할까 : 위 코드를 다 지났는데 아무것도 걸리지 않았으면 이걸 리턴?
  }


  // (6) 해시 충돌을 해결해 주는 코드는 어디에 있는 것인가?
    // 체이닝 방식을 취하고 있는건가? 코드 어디에서 그렇게 정의해 주고 있는지 모르겠음
      // 위의  "for (let i = 0; i < bucket.length; i += 1)"  이하 부분이 이에 해당함. : '체이닝 방식' -> 추가 공부 필요.


  retrieve(key) { // 주어진 키에 해당하는 값을 반환합니다. 없다면 undefined를 반환합니다.
    let index = hashFunction(key, this._limit);
    
    let bucket = this._storage.get(index);   // (7) || []  여기서도 이걸 쓰도록 되어있는데, 이거는 왜 하는걸까?
      // index(hash) 안에 값이 몇개있는지 확인하려면, 일단 index에 대응하는 bucket 세트에 접근할 수 있어야 함.

    for (let i = 0; i < bucket.length; i++) {
      //let tuple = bucket[i];  // 이렇게 별도로 선언 안해줘도 돌아가는것을 확인함. // (8) 뭐하러 tuple 을 선언하지?
      if (bucket[i][0] === key) {
        return bucket[i][1];
      }
    }
    return undefined;    // (9) 이 부분이 없어도 통과는 됨. 문제에서 요구하니까 적어둬야 할 것 같은데, 없어도 통과는 됨. 왜필요하지?


    // 내가 짠 코드 2 : 역시 안됨. for let i=0 / for in 차이밖에 없는 것 같은데..
      // for (let element in bucket) {
      //   if (element[0] === key) {
      //     return element[1];
      //   }
      // }
      // return undefined;


    // 내가 짠 코드 1 : 당연히 안됨 - 해시 충돌 생기는 듯.
      // if (bucket.length === 1) {  // bucket 안에 다른거 없이 딱 1개의 세트만 있으면, ( === 이 index에서는 과거에 충돌이 없었다면,)
      //   if (bucket[0][0] === key) {
      //     return bucket[0][1];
      //   }
      //   else {
      //     return undefined;
      //   }
      // }
      // if (bucket.length > 1) {  // bucket 안에 1개보다 많은 세트가 존재하면, ( === 이 index에서는 과거에 충돌이 있어서, 한 index 안에 여러개의 키값 세트가 연결되어서 존재한다면,)
      //   for (let i = 0; i < bucket.length; i++) {
      //     if (bucket[i][0] === key) {
      //       return bucket[i][1];
      //     }
      //     else {
      //       return undefined;
      //     }
      //   }
      // }


      // 내가 짠 코드 0 : 이거 한 줄만 넣으면 해시 충돌이 생기는 듯. 해결할 코드를 추가해야 함
        // return this._storage[index];  
      
  }


  remove(key) { // 주어진 키에 해당하는 값을 삭제하고 값을 반환합니다. 없다면 undefined를 반환합니다.
    const index = hashFunction(key, this._limit);
    let bucket = this._storage.get(index); 
      // index(hash) 안에 값에 접근하려면, 일단 index에 대응하는 bucket 세트에 접근할 수 있어야 함.

    // 코드스테이츠 답을 보고, 내가 혼자 짜 본 코드 : 통과는 되는 것 같은데, 많이 간소화해야 함.
      // 코드스테이츠 답은 1인 경우와 1 초과인 경우를 나누지 않고 한번에 처리했음
      // 난 충돌이 없는 경우와 충돌이 있는 경우로 나눠보고 싶어서 이렇게 작성함 (그러나, 같은걸 두번 쓰니 비효율이 생기는 듯.)
    if (bucket.length === 1) {  
      // bucket 이 1개인 경우 ( : 충돌이 없는 경우(?))
      if (bucket[0][0] === key) { // bucket 세트 안의 key가, 주어진 key와 동일하다면,
        bucket.splice(0, 1);   // 0번째부터 1개를 지우니까, key 자체를 지우므로, 한 세트를 통째로 지우게 됨
          // .splice(a, b) : 배열 중 a번째 값부터 시작해서, b개만큼 삭제하고, 배열을 변화시키고 b를 리턴
        this._size -= 1;
      }
      // else {   // (10) 역시 있으나 없으나 통과됨.
      //   return undefined;
      // }
    }
    if (bucket.length > 1) {  
      // bucket 이 1개보다 많은 경우
      // (하나의 index 안에 여러개의 값이 존재하는 것이므로, 충돌이 생긴 경우로 보아야 할 듯(?))
      for (let i = 0; i < bucket.length; i++) {
        if (bucket[i][0] === key) {
          bucket.splice(i, 1);
          this._size -= 1;
          // if (this._size / this._limit < 0.25) {   // 레퍼런스는 여기에서 실행하지만, 아래로 옮겨봄
          //   this._resize(Math.floor(this._limit / 2));
          // }
        }
        // else {   // (11) 역시 있으나 없으나 통과됨.
        //   return undefined;
        // }
      }
    }
    if (this._size / this._limit < 0.25) { // 위의 같은 코드의 위치를 옮겨 봤는데, 동작함.
      this._resize(Math.floor(this._limit / 2)); // Math.floor : 소수점 이하 '버림' 기능
    }
    return undefined;  // 위의 else { return undefined; } 부분을 모아서 간소화함.
      // 위 undefined 부분을 주석처리해도 돌아는 감. (12) 왜필요하지?
  }


  _resize(newLimit) { // 해시 테이블의 스토리지 배열을 newLimit으로 리사이징하는 함수입니다.
    // 리사이징 후 저장되어 있던 값을 전부 다시 해싱을 해주어야 합니다. 
    // 구현 후 HashTable 내부에서 사용하시면 됩니다.


      // '동적 해싱 (Dynamic resizing)' - 이 개념 공부하기

    // 내가 처음에 짠 코드인데, - 아래 코드 부분은 각 함수에서 미리 조건을 걸었으므로, 있을 필요가 없는 부분이 됨.
      // if (this._size / this._limit >= 0.75 && newLimit > this._limit) {
      //   this._limit = this._limit * 2;
      // }
      // if (this._size / this._limit <= 0.25 && newLimit <= this._limit) {
      //   this._limit = this._limit / 2;
      // }

    let oldStorage = this._storage; // 밑에서 써먹기 위해, 기존 해시테이블의 스토리지를 옮겨담고,

    newLimit = Math.max(newLimit, 8); // newLimit 과 (기존 리미트인) 8을 비교하여, 더 큰것을 newLimit에 넣고,
    if (newLimit === this._limit) { // 둘이 동일하다면,
      return;   // 아래의 처리를 하지 말고, 이 함수를 끝내라. (newLimit의 최소값을 8로 만들기 위함.)
    } // 아래로 내려가려면 위 조건이 틀려야 하므로, newLimit > this._limit 인 경우에만 밑으로 내려감.

    this._limit = newLimit; // 새롭게 생긴 한계선인 newLimit 을, 다른 코드에서 사용할 this._limit 에 넣고,
    this._storage = LimitedArray(this._limit); //  새롭게 만든 해시테이블을, 다른 코드에서 사용할 this._storage에 넣고, (여기서는 빈 LimitedArray 상태로 들어가는 듯)
    this._size = 0; // 새 스토리지니까 사이즈는 다시 0부터 시작해야 하고,

    // 내가 짠 코드인데, 이렇게 작성하면 동작하지 않음
      // for (let bucket in oldStorage) {   
      //   if (!bucket) {  // bucket 이 false 이면, : oldStorage 안에 bucket이 비어 있으면,
      //     return; // 아래 처리로 가지 말고, 함수를 끝내라.
      //   }
      //   if (bucket) {
      //     for (let i = 0; i < bucket.length; i++) {
      //       this.insert(bucket[i][0], bucket[i][1]); 
      //         // 여기서 this : new HashTable 처리한 새로운 해시테이블

      //       // let index = hashFunction(bucket[i][0], this._limit);
      //       // let newElement = this._storage[index];
      //       // if (newElement) {
      //       //   newElement.push(bucket[i][0], bucket[i][1]);
      //       // }
      //       // else {
      //       //   newElement = [];
      //       //   newElement.push(bucket[i][0], bucket[i][1]);
      //       // }
      //     }
      //   }
      // }

    oldStorage.each(bucket => {  
      // oldStorage.each(function (bucket) {  이렇게 바꾸면 안돌아감

        // MDN : "화살표 함수 표현(arrow function expression)은 function 표현에 비해 구문이 짧고
        //  자신의 this, arguments, super 또는 new.target을 바인딩 하지 않습니다."
          // -> '화살표 함수로 할 때랑 익명함수로 할 때랑, this값이 달라지기 때문에 그런 것인가?'

            // MDN : "화살표 함수는 전역 컨텍스트에서 실행될 때 this를 새로 정의하지 않습니다. 
              // 대신 코드에서 바로 바깥의 함수(혹은 class)의 this값이 사용됩니다. 
              // 이것은 this를 클로저 값으로 처리하는 것과 같습니다."

          // console.log(this); // 실험을 위한 코드 -> 
      if (!bucket) {  // bucket 이 false 이면, : oldStorage 안에 bucket이 비어 있으면,
        return; // 아래 처리로 가지 말고, 함수를 끝내라.
      }
        for (let i = 0; i < bucket.length; i += 1) {
          //const tuple = bucket[i]; // 이 부분을 없애도 돌아감
          this.insert(bucket[i][0], bucket[i][1]);  // 여기의 this 가 무엇을 가리키는지가 중요.
        }
    });

    // [화살표 함수](https://poiemaweb.com/es6-arrow-function) : this 값과 관련하여 공부해야 함!!!

  }
```  

&nbsp;Hash Table 은 hash 값을 만들어 내는 'hash function' 의 기능 및 구조에 대한 이해 역시 필요합니다.  

&nbsp;또한, hash function를 거쳐 나온 hash 값이 일치하는 경우에 발생하는 'hash collision(해시 충돌)' 문제를 해결하는 방법 역시 고려하여야 합니다.  

&nbsp;그 외에도 코드 작성중에 생기는 궁금증을 주석으로 모두 기록해 두었습니다.  

&nbsp;이런 점을 추가 공부하여 반영하도록 하겠습니다.  


## &nbsp;&nbsp;(5) 참고자료
 - [Hash Tables (MDN)](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSPR/Reference/Hash_Tables)  
 - [Hash, Hashing, Hash Table(해시, 해싱 해시테이블) 자료구조의 이해](https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o)  
 - [[자료 구조] Data Structure - (2) Hash Table](https://im-developer.tistory.com/124)  
 - [Hashing Data Structure](https://www.geeksforgeeks.org/hashing-data-structure/)  
 - [Resizing a hash table](http://rvbsanjose.github.io/hash-table-resizing/)  
 - [화살표 함수](https://poiemaweb.com/es6-arrow-function)


<br>
---
<br>

&nbsp;이렇게 하여, Stack / Queue / Linked List / Hash Table 의 4가지 자료구조에 관하여 간단하게 정리하였습니다.  

&nbsp;공부할때마다 내용을 보충해 나가려고 합니다.  

&nbsp;'Tree / Graph / Binary Search Tree' 자료구조에 관하여, 별도의 포스팅을 작성하도록 하겠습니다.  