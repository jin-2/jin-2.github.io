---
layout: post
title: "참조타입(Array)"
excerpt: "책요약"
categories: [Book - JavaScript for Web Developers]
comments: false
---

> 자바스크립트 프로그래밍: 프론트엔드 개발자를 위한   
> 니콜라스 자카스    
> 인사이트 
> 978-89-6626-076-8

## 5장 참조 타입

### 5.2 Array 타입 

배열은 두 가지 방법으로 만듭니다.

**Array 생성자를 쓰는 방법**

    // length 프로퍼티가 20인 배열
    var colors = new Array(20);
    
    // 문자열 값이 세 개 들어 있는 배열
    // new 연산자를 생략 가능
    var colorsOther = Array('red', 'blue', 'green'); 

**'배열 리터럴' 표기법**

    var colors = ['red', 'blue', 'green'];

    // 데이터가 두 개 또는 세 개 들어있는 배열을 만듭니다.
    // 이렇게 하지 마십시오.
    var values = [1, 2, ];

**배열 값 접근**

    var colors = ['red', 'yellow', 'green'];
    alert(colors[0]); // red: 첫 번째 데이터를 표시합니다.
    
    colors[2] = 'black'; // 세 번째 데이터를 바꿉니다.
    alert(colors[2]); // black

**length 프로퍼티의 흥미로운 특징**  
length 프로퍼티의 값을 바꾸면 배열 길이가 그에 맞게 바뀌면서 데이터를 제거하거나 빈 슬롯을 추가합니다.

    var colors = ['red', 'yellow', 'green'];
    colors.length = 1;
    console.log(colors); // ["red"]

**length 프로퍼티: 배열 마지막 테이터 추가할 때**

    var colors = ['red', 'yellow', 'green'];
    colors[colors.length] = 'black';
    console.log(colors); // ["red", "yellow", "green", "black"]

### 5.2.1 배열 감지

#### instanceof
전역 스코프가 **하나뿐인** 단순한 웹 페이지에서는 instanceof 연산자를 쓰면 됩니다.

    if (value of instanceof Array){
        // 배열일 때 실행하는 코드
    }

#### Array.isArray()
웹 페이지에 프레임이 여러 개 있다면 전역 실행 컨텍스트가 두 개 있는 것이고, 따라서 Array 생성자도 두 개 있는 것입니다. 이 문제를 해결하기 위해 ECMAScript5에서는 이 문제를 우회하기 위해 Array.isArray() 메서드를 제공합니다.

    if (Array.isArray(value)){
        // 배열일 때 실행하는 코드
    }

*익스플로러 9 이상, 파이어폭스 4 이상, 사파리 5 이상, 오페라 10.5 이상, 크롬은 모두*

### 5.2.2 변환 메서드
객체에는 모두  **toLocaleString(), toString(), valueOf()** 메서드가 있습니다.  
배열에서 호출했을 때는 toString()과 valueOf() 메서드는 같은 값을 반환합니다. toLocaleString() 메서드는 toString()이나 valueOf()와 같은 값을 반환할 때도 있고 그렇지 않을 때도 있습니다. 그 값은 쉼표로 분리된 문자열입니다.

    var colors = ['red', 'yellow', 'green'];

    // toString: red,yellow,green
    console.log('toString: '+colors.toString());

    // valueOf: red,yellow,green
    console.log('valueOf: '+colors.valueOf());

    // ["red", "yellow", "green"]
    console.log(colors);

    // alert()은 매개변수로 문자열을 받으므로 먼저 배열에서 toString()을 호출
    // red,yellow,green 
    alert(colors); 

#### join()
구분자가 될 문자열을 매개변수로 받고 배열 데이터를 모두 포함한 문자열을 반환합니다.

    var colors = ['red', 'yellow', 'green'];
    console.log(colors.join('~')); // red~yellow~green
    console.log(colors.join('||')); // red||yellow||green
    console.log(colors.join( )); // red,yellow,green

### 5.2.3 스택 메서드

#### 스택은 LIFO(last-in-first-out) 구조라고 불리기도 하는데,  
이 말의 의미는 데이터를 삭제할 때는 마지막에 추가된 데이터가 제일 먼저 삭제된다는 뜻입니다. 

    // 배열 생성
    var colors2 = [];
    
    // 데이터 추가
    var count = colors2.push('red', 'green');
    console.log('1: '+colors2); // 1: red,green
    console.log('1: '+count); // 1: 2

    // 다른 데이터 추가 
    count = colors2.push('black');
    console.log('2: '+colors2); // 2: red,green,black
    console.log('2: '+count); // 2: 3

    // 마지막 데이터 꺼냄 
    var item = colors2.pop();
    console.log('3: '+colors2); // 3: red,green
    console.log('3: '+item); // 3: black

    // 마지막에 다른 데이터 추가
    colors2[colors2.length] = 'orange';
    console.log('4: '+colors2); // 4: red,green,orange
    console.log('4: '+item); // 4: black
    
    // 마지막 데이터 꺼냄
    item = colors2.pop(2);
    console.log('5: '+colors2); // 5: red,green
    console.log('5: '+item); // 5: orange

#### push()
매개변수를 그대로 배열에 추가한 후 이에 맞게 늘어난 **배열 길이**를 반환합니다.

#### pop()
배열의 **마지막 데이터를 제거**하고 length 프로퍼티를 그에 맞게 줄여서 반환합니다.

###  5.2.4 큐 메서드
스택이 데이터 입출력을 LIFO로 제한하는 구조라면 큐는 데이터 입출력을 **FIFO(first-in-first-out)** 로 제한하는 구조입니다. 큐는 목록 마지막에 데이터를 추가하며 **목록 맨 앞에서 데이터를 꺼냅니다.**

#### shift()
배열의 **첫 번째 데이터를 꺼내서 반환**하며 배열 길이는 1만큼 줄어듭니다.

#### unshift()
매개변수로 넘겨받은 데이터를 **배열의 처음에 추가**하며 그에 맞게 변한 배열 길이를 반환합니다.

    // 배열 생성
    var animals = [];
    
    // 배열에 데이터 2개 추가
    var animalCount = animals.push('lion', 'hippo');
    console.log(animals); // ["lion", "hippo"]
    
    // 다른 데이터 추가
    animalCount = animals.push('tiger');
    console.log(animals); // ["lion", "hippo", "tiger"]
    
    // 첫 번째 데이터 꺼냄
    var firstItem = animals.shift();
    console.log(animals); // ["hippo", "tiger"]
    console.log(firstItem); // lion
    
    // 첫 번째에 데이터 추가
    animalCount = animals.unshift('bear');
    console.log(animals); // ["bear", "hippo", "tiger"]
    console.log(animalCount); // 3
    
    // 마지막 데이터 꺼냄
    firstItem = animals.pop();
    console.log(animals);

### 5.2.5 정렬 메서드

#### reverse()
데이터의 순서를 뒤집습니다.

#### sort()
기본적으로 데이터를 정순, 즉 가장 작은 값이 첫 번째에 오고 가장 큰 값이 마지막에 오도록 정렬합니다. **sort() 메서드는 그대로 쓴 결과에 만족할 수 없을 때가 많으므로 '비교 함수'를 넘겨서 순서를 조절할 수 있습니다.**

    var sortValues = [0, 1, 5, 10, 15];
    sortValues.sort();
        
    // [0, 1, 10, 15, 5]  - 결과값이 이상함.
    console.log('only sort(): '+sortValues);
    
    // 비교 함수
    function compare(value1, value2) {
        if (value1 < value2) {
            return -1;
        } else if (value1 > value2) {
            return 1;
        } else {
            return 0;
        }
    }
    
    sortValues.sort(compare);
    
    // [0, 1, 5, 10, 15]
    console.log('with compare function: '+sortValues);
    
    // 역순으로 정렬
    // sortValues.sort(compare).reverse();
    sortValues.reverse();
    
    // [15, 10, 5, 1, 0]
    console.log('result reverse: '+sortValues);

### 5.2.6 조작 메서드

#### concat()
이 메서드는 먼저 **현재 배열을 복사**한 다음 메서드의 매개변수를 새 배열 **마지막에 추가**해서 반환합니다. 매개변수를 넘기지 않으면 단순히 현재 배열의 복사본을 반환합니다.

*concat이란 이름은 합친다는 뜻인 concatenate의 약자입니다.*

#### slice()
이 메서드는 배열에 포함된 데이터 일부를 가진 새 배열을 만듭니다.

- 매개변수를 두 개 받는다.
- 매개변수를 하나만 넘기면 해당 인덱스에서 끝까지 모든 데이터를 가져옵니다.
- 매개변수를 두 개 넘기면 **첫 번째 매개변수에 해당하는 인덱스부터 두 번째 매개변수에 해당하는 인덱스 바로 앞**까지 가져옵니다.

concat() & slice() 예: 

    var coffee = ['star', 'bean', 'hollys'];
    var coffee2 = coffee.concat('back', 'twosome', 'angel');
    
    // ["star", "bean", "hollys"]
    console.log(coffee);
    
    // ["star", "bean", "hollys", "back", "twosome", "angel"]
    console.log(coffee2);
    
    var coffee3 = coffee2.slice(1, 3);
    // ["bean", "hollys"]
    console.log(coffee3);
    
    var coffee4 = coffee2.slice(5);
    // ["angel"]
    console.log(coffee4);

#### splice()
배열 메서드 중 가장 강력한 메서드는 아마 splice()일 겁니다. splice()의 주요 목적은 배열 중간데 데이터를 삽입하는 것인데 이 메서드는 세 가지 방법(**삭제, 삽입, 대체**)으로 사용합니다. 항상 원래 배열에서 삭제한 데이터의 배열을 반환합니다.

    var colors = ['red', 'green', 'blue'];
    
    // 첫 번째 데이터 제거
    var removed = colors.splice(0, 1); 
    
    console.log(colors); // ["green", "blue"]
    console.log(removed); // ["red"]
    
    // 인덱스 1에 삭제하는 데이터 없이 데이터 2개 추가
    removed = colors.splice(1, 0, 'yellow', 'orange');
    
    console.log(colors); // ["green", "yellow", "orange", "blue"]
    console.log(removed); // []
    
    // 인덱스 1부터 데이터 한개 삭제하고 인덱스 1자리에 데이터 2개 추가
    removed =  colors.splice(1, 1, 'red', 'purple');
    console.log(colors); // ["green", "red", "purple", "orange", "blue"]
    console.log(removed); // ["yellow"]

### 5.2.7 위치 메서드

#### indexOf()
배열의 처음(인덱스 0)에서 검색을 시작하여 마지막까지 검색

#### lastIndexOf()
배열의 마지막에서 검색을 시작하여 처음까지 검색

    var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
    
    console.log(numbers.indexOf(4));  // 3
    console.log(numbers.lastIndexOf(4));  // 5
    
    console.log(numbers.indexOf(4, 4));  // 5
    console.log(numbers.lastIndexOf(4, 4));  // 3
    
    var person = { name: 'Nicholas' };
    var people = [{name: 'Nicholas'}];
    var morePeople = [person];
    
    console.log(people.indexOf(person));  // -1
    console.log(morePeople.indexOf(person));  // 0

- 매개변수를 두 개 받는다.
- 첫 번째 매개변수는 검색할 데이터
- **옵션**인 두번째 매개변수는 검색을 시작할 인덱스
- **데이터를 찾지 못했을 때는 -1을 반환**
- 데이터를 검색할 때는 타입까지 일치하는 `===` 연산자로 비교해서 일치하는 데이터를 검색

! Browser Supported
:   인터넷 익스플로러 9 이상, 파이어폭스 2 이상, 사파리 3 이상, 오페라 9.5이상, 크롬

[MDN-Polyfill](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)

### 5.2.8 반복 메서드
- 매개변수를 두 개 받는다.
- 하나는 배열의 각 데이터에서 실행할 함수
- 옵션인 다른 하나는 함수를 실행할 스코프 객체
- 콜백 함수는 모두 데이터, 데이터의 인덱스, 배열 자체의 세 가지 매개변수 받는다.

#### every()
배열의 모든 데이터에서 콜백 함수를 호출하고 반환 값이 전부 true이면 true를 반환한다.

    var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
    
    var everyResult = numbers.every(function (item, index, array) {
        return (item>2);
    });

    console.log(everyResult); // false

#### some()
배열의 모든 데이터에서 콜백 함수를 호출하고 반환 값 중 하나라도 true이면 true를 반환합니다.

    var someResult = numbers.some(function (item, index, array) {
        return (item>2);
    });
    
    console.log(someResult); //true

#### filter()
배열의 모든 데이터에서 콜백 함수를 호출하고 반환 값이 true인 데이터를 새 배열에 저장하여 반환합니다.

    var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
    
    var filterResult = numbers.filter(function (item, index, array) {
        return (item > 2);
    });
    
    console.log(filterResult); // [3, 4, 5, 4, 3]

**특정 조건에 맞는 데이터만 쿼리하려 할 때 매우 유용합니다.**

#### map()
배열의 모든 데이터에서 콜백 함수를 호출하고 그 결과를 새 배열에 저장하여 반환합니다.

    var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
    
    var mapResult = numbers.map(function (item, index, array) {
        return item * 2;
    });
    
    console.log(mapResult); //[2, 4, 6, 8, 10, 8, 6, 4, 2]

**map() 메서드는 원래 배열과 1:1로 대응하는 배열을 만들 때 유용합니다.**

#### forEach()
배열의 모든 데이터에서 콜백 함수를 호출합니다. 이 메서드는 반환 값이 없습니다.

    array.forEach(function (item, index, array) {
        // 코드
    });

! Browser Supported
:   인터넷 익스플로러 9 이상, 파이어폭스 2 이상, 사파리 3 이상, 오페라 9.5이상, 크롬

###  5.2.9 감소 메서드

#### reduce(), reduceRight()
모두 배열을 순회하며 콜백 함수를 실행하고 값을 하나 만들어 반환합니다. **reduce()** 는 첫번째 데이터에서 시작하여 마지막까지 진행하고, **recuceRight()** 는 반대로 배열의 마지막 데이터에서 시작하여 첫번째까지 진행합니다.

- 매개변수를 두 개 받는다.
- 첫 번째 매개변수는 각 데이터에서 실행할 콜백 함수
- 옵션인 두번째 매개변수는 감소 작업을 시작할 초기 값
- 콜백함수가 넘겨받는 매개변수는 이전 값, 현재 값, 현재 값의 인덱스, 현재 배열 네가지

예:

    var values = [1, 2, 3, 4, 5];
    var sum = values.reduce(function (prev, cur, index, array) {
        return prev + cur;
    });
    console.log(sum); // 15

! Browser Supported
:   인터넷 익스플로러 9 이상, 파이어폭스 2 이상, 사파리 3 이상, 오페라 9.5이상, 크롬
