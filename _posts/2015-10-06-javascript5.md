---
layout: post
title: "JavaScript for Web Developers(5) - 변수와 스코프, 메모리"
excerpt: "책요약: 변수의 원시 값과 참조 값, 실행 컨텍스트, 가비지 컬렉션"
categories: [js]
comments: false
---

> 자바스크립트 프로그래밍: 프론트엔드 개발자를 위한   
> 니콜라스 자카스    
> 인사이트
> 978-89-6626-076-8

## 4장 변수와 스코프, 메모리 ##

> 이 장에서 다루는 내용
> - 변수의 원시 값과 참조 값
> - 실행 컨텍스트의 이해
> - 가비지 컬렉션의 이해

### 4.1 원시 값과 참조 값

#### 원시 값
단순한 데이터입니다. 이들 변수는 **'값으로' 접근한다** 고 하는데 변수에 저장된 실제 값을 조작하기 때문에 이렇게 말합니다.

#### 참조 값
여러 값으로 구성되는 객체, 메모리에 저장된 객체입니다. 자바스크립트는 메모리 위치에 직접 접근하는 것을 허용하지 않으므로 객체를 조작할 때는 사실 객체 자체가 아니라 해당 객체에 대한 '참조'를 조작하는 겁니다. 이런 이유로 **'참조로 접근한다'** 고 합니다.

#### 4.1.1 동적 프로퍼티
참조 값을 다를 때는 언제든 프로퍼티와 메서드를 추가하거나 바꾸고 삭제할 수 있습니다.

```javascript
var person = {};
person.name = 'jin';
alert(person.name); // jin
```

아래 코드에서는 문자열 name에 age란 프로퍼티를 정의했고 값으로 27을 할당했지만, 그 프로퍼티는 바로 다음 줄에서 사라졌습니다. **동적으로 프로퍼티를 추가할 수 있는 값으 참조 값 뿐입니다.**

```javascript
var name = 'jin';
name.age = 27;
alert(name.age);
```

#### 4.1.2 값 복사

```javascript
var obj1 = new Object();
var obj2 = obj1;
obj1.name = 'jin';
alert(obj2.name); // jin
```

참조 값을 변수에서 다른 변수로 복사하면 원래 변수에 들어있던 값이 다른 변수에 복사되기는 마찬가지입니다. 차이는 그 값이 객체 자체가 아니라 **힙에 저장된 객체**를 가리키는 포인터라는 점입니다. **조작이 끝나면 두 변수는 정확히 같은 객체를 가리킵니다.**

**힙이란?** 애플리케이션이 운영체제로부터 미리 할당받는 메모리 영역입니다. 힙 메모리는 '브라우저가 쓰는 메모리'라고 생각하시면 됩니다.

#### 4.1.3 매개변수 전달

```javascript
function setName(obj) {
    obj.name = 'jin';
    obj = new Object();
    obj.name = 'greg';
}

var person = new Object();
setName(person);
alert(person.name); // jin
```

`person.name`에 다시 접근하면 그 값은 'jin' 입니다. 함수에 **값을 전달** 했기 때문에 함수 내부에서 매개변수의 값이 바뀌었음에도 불구하고 원래 객체에 대한 참조를 그대로 유지한 것입니다. **함수 내부에서 `obj`를 덮어 쓰면 `obj`는 지역 객체를 가리키는 포인터가 됩니다. 이 지역 객체는 함수가 실행을 마치는 즉시 파괴됩니다.**

#### 4.1.4 타입 판별

##### typeof
원시 값에 대해서는 잘 동작하지만 참조 값에 대해서는별 쓸모가 없습니다.

```javascript
var s = 'jin';
var b = true;
var i = 22;
var u;
var n = null;
var o = new Object();

alert(typeof s); // string
alert(typeof b); // boolean
alert(typeof i); // number
alert(typeof u); // undefined
alert(typeof n); // object
alert(typeof o); // object
```

##### instanceof
변수가 주어진 참조 타입의 인스턴스일 때 true를 반환합니다.

```javascript
'result' = 'variable' instanceof 'constructor'

console.log(o instanceof Object); // true
console.log(b instanceof Array); // false
console.log(i instanceof RegExp); // false
```

### 4.2 실행 컨텍스트와 스코프
실행 컨텍스트는 짧게 **'컨텍스트'** 라고 부르며 자바스크립트에서는 비할 바 없이 중요한 개념입니다.

가장 바깥쪽에 존재하는 실행 컨텍스트는 **전역 컨텍스트** 입니다. 웹 브라우저에서는 이 컨텍스트를 `window`라 부르므로 전역 변수와 함수는 모두 `window` 객체의 프로퍼티 및 메드로 생성됩니다.

실행 컨텍스트는 포함된 코드가 모두 실행될 때 파괴  
전역 컨텍스트는 애플리케이션이 종료될 때까지 계속 유지  

함수를 호출하면 독자적인 실행 컨텍스트가 생성됩니다. 코드 실행이 함수로 들어갈 때마다 함수의 컨텍스트가 컨텍스트 스택에 쌓입니다. 함수 실행이 끝나면 해당 컨텍스트를 스택에서 꺼내고 컨트롤을 이전 컨텍스트에 반환합니다.

컨텍스트에서 코드를 실행하면 변수 객체에 **'스코프 체인'** 이 만들어집니다. 스코프 체인의 목적은 실행 컨텍스트가 접근할 수 있는 모든 변수와 함수에 순서를 정의하는 것입니다.
변수 객체의 다음 순서는 해당 컨텍스트를 포함하는 컨텍스트(부모 컨텍스트)이며 그 다음에는 다시 부모의 부모 컨텍스트입니다. 이런 식으로 계속 진행하여 전역 컨텍스트에 도달할 때까지 계속합니다. **전역 컨텍스트의 변수 객체는 항상 스코프 체인의 마지막에 존재합니다.**

```javascript
var color = 'blue';

function changeColor() {
    var anotherColor = 'red';

    function swapColors() {
        var tempColor = anotherColor;
        anotherColor = color;
        color = tempColor;

        // red, blue, red
        console.log('1: '+tempColor, anotherColor, color);
    }

    swapColors();
    // blue, red
    console.log('2: '+ anotherColor, color);
}

changeColor();

// red
console.log('3: '+ color);
```

- 이 코드에는 실행 컨텍스트 세 개 있습니다.
    - `changeColor()`
    - `swapColors()`
    - 전역 컨텍스트

내부 컨텍스트는 스코프 체인을 통해 외부 컨텍스트 전체에 접근할 수 있지만 **외부 컨텍스트는 내부 컨텍스트에 대해 전혀 알 수 없습니다.**

#### 4.2.1 스코프 체인 확장
특정 문장은 스코프 체인 앞 부분에 임시로 변수 객체를 만들며 해당 변수 객체는 코드 실행이 끝나면 사라집니다. 이렇게 임시 객체가 생성되는 경우는 다음 두 가지입니다.
- `try-catch` 문의 catch 블록
- `with` 문

#### 4.2.2 자바스크립트에는 블록 레벨 스코프가 없습니다.

```javascript
if (true) {
    var color = "blue";
}

alert(color); // blue
```

자바스크립트에서는 변수를 선언할 때 해당 변수를 현재 실행 컨텍스트(위 코드에서는 전역 컨텍스트)에 추가합니다.

##### 변수 선언

```javascript
function add(num1, num2) {
    var sum = num1 + num2;
    return sum;
}

var result = add(10, 20);
console.log(sum); // sum is not defined
```

변수 `sum`이 함수 값으로 반환되긴 하지만 함수 밖에서는 이 변수에 접근할 수 없습니다. 다음과 같이
**`var` 키워드를 생략** 하면 `add()` 함수를 호출한 다음부터는 변수 `sum`에 접근할 수 있습니다.

```javascript
function add(num1, num2) {
    sum = num1 + num2;
    return sum;
}

var result = add(10, 20);
console.log(sum); // 30
```

`add()`를 호출하면 **전역 컨텍스트에서 `sum`이 생성** 되며 함수가 완전히 실행된 뒤에도 남아 있어서 나중에 사용할 수 있습니다.

*Note: 항상 변수를 선언한 다음 초기화하길 권합니다.*

##### 식별자 검색

```javascript
var color = "blue";
function getColor() {
    return color;
}

alert(getColor()); // blue
```

`getColor()`의 변수 객체에서 찾지 못하면 다음(전역 컨텍스트) 변수 객체에서 color 식별자를 검색합니다.

```javascript
var color = "blue";
function getColor() {
    var color = "red";
    return color;
}

alert(getColor()); // red
```

위와 같이 식별자가 로컬 컨텍스트에 정의되어 있으면 부모 컨텍스트에 같은 이름의 식별자가 있다 해도 참조할 수 없습니다. **전역 컨텍스트의 color 변수를 이용하려면 `window.color`라고 명시** 해야 합니다.

### 4.3 가비지 콜렉션
자바스크립트는 **필요한 메모리를 자동으로 할당하고 더 이상 사용하지 않는 메모리는 자동으로 회수** 하므로 개발자가 직접 메모리를 관리하지 않아도 됩니다.
가비지 콜렉터는 어떤 변수가 더 이상 사용되지 않는지, 사용될 가능성이 있는 변수는 무엇인지 추적해야 메모리 회수 대상을 정할 수 있습니다. 더 이상 사용하지 않는 변수를 식별하는 기준은 브라우저마다 다르지만 보통 두 가지 방법을 흔히 채용합니다.

#### 4.3.1 표시하고 지우기(가장 널리 쓰임)
가비지 컬렉터가 작동하면 메모리에 저장된 변수 전체에 표시를 남깁니다. 그 다음 컨텍스트에 있는 변수와, 컨텍스트에 있는 변수가 참조하는 변수에서 표시를 지웁니다. 이 과정을 거친 다음에도 표시가 남아 있는 변수는 컨텍스트에 있는 변수와 무관하므로 삭제해도 안전합니다. 가비지 컬렉터는 '메모리 청소'를 실행해 표시가 남아 있는 값을 모두 파괴하고 메모리를 회수합니다.

#### 4.3.2 참조 카운팅
이 방식의 주안점은 각 값이 얼마나 많이 참조 되었는지 추척한다는 것입니다. 이 알고리즘은 거의 쓰이지 않지만 인터넷 익스플로러에서는 아직 쓰이는데 DOM 요소처럼 네이티브 자바스크립트 객체가 아닌 객체를 자바스크립트에서 접근해야 하기 때문입니다. 순환 참조 문제가 있습니다.

#### 4.3.3 성능
가비지 컬렉터는 주기적으로 실행되며 메모리 내에 할당된 변수가 많다면 상당한 비용이 드는 작업이므로 가비지 컬렉션을 실행하는 타이밍이 중요합니다. 인터넷 익스플로러는 가비지 컬렉터를 너무 자주 실행하여 성능 문제를 일으키는 것으로 악명높습니다.

#### 4.3.4 메모리 관리
웹 브라우저에서 사용할 수 잇는 메모리는 매우 적습니다. 주된 이유는 웹 페이지에서 실행하는 자바스크립트가 시스템 메모리를 전부 사용해서 운영체제를 다운시키는 일을 방지하기 위함입니다.

가능한 한 최소의 메모리만 사용해야 페이지 성능을 올릴 수 있습니다. **메모리 사용을 최적화하는 가장 좋은 방법은 코드 실행에 필요한 데이터만 유지** 하는 것입니다.

```javascript
function creatPerson(name) {
    var localPerson = new Object();
    localPerson.name = nama;
    return localPerson;
}

var globalPerson = creatPerson("jin");

// globalPerson을 사용하는 코드

globalPerson = null;
```

변수에서 참조를 제거한다 해서 할당된 메모리가 자동으로 반화되는 것은 아닙니다. **참조 제거의 요점은 값의 컨텍스트를 없애서 다음에 가비지 콜렉션을 실행할 때 해당 메모리를 회수** 하도록 하는 겁니다.
