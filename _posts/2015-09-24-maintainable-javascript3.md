---
layout: post
title: "책요약 - Maintainalble JavaScript 3"
excerpt: "스타일 가이드라인(변수, 함수, 연산)에 대한 내용 정리"
categories: [js]
comments: false
---

> 읽기 좋은 자바스크립트 코딩 기법 Maintainalble JavaScript  
> 니콜라스 카자스  
> O'REILLY 한빛미디어  
> 978-89-7914-988-3

## part1. 스타일 가이드라인(3) ##

### CHAPTER 4 변수, 함수, 연산자

#### 4.1 변수 선언

**호이스트(hoist)**: 모든 변수 선언은 변수가 선언된 위치와 상관없이 함수의 최상단으로 끌어올려 집니다. 이런 이유로 자바스크립트에서는 변수를 함수 이곳 저곳에 선언하지 않고 최상단에서 한꺼번에 선언하는 스타일을 가장 많이 씁니다. 

지역 변수를 함수의 첫 번째 문장에 선언하는 스타일을 추천합니다. (크락포드 코드 컨벤션, SproutCore 스타일 가이드, Dojo 스타일 가이드)

    function doSomethingWithItems(items) {
        
        var i, len;
        var value = 10;
        var result = value + 10;
    
        for (i=0, len=items.length; i<len; i++) {
            doSomething(items[i]);
        };
    }

함수 상단에 하나의 var 문만 사용하는 것을 권장합니다. (크락포드)

    function doSomethingWithItems(items) {
    
        var i, len,
            value = 10,
            result = value + 10;
    
        for (i=0, len=items.length; i<len; i++) {
            doSomething(items[i]);
        }
    }

var 문으로 모든 변수를 선언하고 변수는 한 줄당 하나만 선언하는 스타일을 선호합니다. 그리고 할당 연산자는 열을 맞춥니다. 초기화하지 않을 변수는 변수 선언문 마지막에 선언합니다.

    function doSomethingWithItems(items) {
    
        var value   = 10,
            result  = value + 10,
            i,
            len;
    
        for (i=0, len=items.length; i<len; i++) {
            doSomething(items[i]);
        }
    }

**하나의 var 문을 사용함으로써 코드의 양을 줄일 수 있고 사용자는 그만큼 더 빨리 코드를 내려 받을 수 잇는 장점이 있어 이 방법을 권장합니다.**

#### 4.2 함수 선언
함수 선언도 변수 선언처럼 자바스크립트 엔진에 의해 끌어올려 집니다. 따라서 함수가 선언되기 전에 먼저 사용할 수 있습니다.

    function doSomethingWithItems(items) {
    
        var i, len,
            value  = 10,
            result = value + 10;
    
        function doSomething(item) {
            // 실행할 코드
        }
    
        for (i = 0, len = items.length; i < len; i++) {
            doSomething(items[i]);
        };
    }

크락포드는 이 예제처럼 지역 함수는 변수 선언 이후에 선언할 것을 권장하고 있습니다.

#### 4.3 함수 호출문에 공백 넣기
함수 호출문은 복합문과 쉽게 구분할 수 있도록 함수명과 괄호 사이에 아무런 공백도 입력하지 않는 스타일을 권장합니다.

좋은 예

    doSomething(item);

나쁜 예

    doSomething (item); // 복합문처럼 보임
    
    // 비교를 위해 복합문을 추가했습니다.
    while (item) {
        // 실행할 코드
    }

#### 4.4 함수 선언하고 바로 호출하기

함수 이름이 없는 익명 함수를 선언할 수 있고 다음 예제처럼 선언한 익명함수를 변수나 프로퍼티에 대입할 수도 있습니다.

    var doSomething = function() {
        // 함수 본문
    }

    
나쁜 예

    var value = function () {
    
        // function body
    
        return {
            message: 'Hi'
        }
    }();

좋은 예
이 코드는 첫 번째 줄에 괄호가 열린 것을 보고 함수가 선언과 동시에 호출됨을 알 수 있습니다. (크락포드의 코드 컨벤션 권장)

    var value = (function () {
    
        // function body
    
        return {
            message: 'Hi'
        }
    }());

#### 4.4.1 strict 모드

    "use strict"

ECMAScript5 자바스크립트 엔진은 이 코드를 만나면 strict 모드를 위한 전환 명령어로 인식합니다. 

일반적으로 "use strict"를 **전역**으로 사용하는 건 피해야 합니다. 만약 총 11개의 자바스크립트 파일 중 하나의 파일에라도 전역 strict 모드가 적용되어 있으면 나중에 파일을 합친 후에는 나머지 파일에도 전역 strict 모드가 적용되기 때문입니다. strict 모드에서는 strict 모드가 아닐 때와 연산 방식이 조금 달라져 다른 파일에서 에러가 발생할 수도 있습니다.

좋은 예

    function doSomething() {
        "use strict";
        
        //코드
    }

함수마다 일일이 "use strict"를 입력해야 하는 게 싫다면 다음 예제처럼 선언과 동시에 호출하는 함수를 이용합니다.

좋은 예2

    (function() {
        "use strict";
    
        function doSomething() {
            // 코드
        }
    
        function doSomethingElse() {
            // 코드
        }
    })();

JSLint와 JSHint 모두 "use strict"를 함수 안에서 사용하는 것을 기준으로 하여 검사를 수행합니다.

### 4.5 동등 연산자 
동등 연산자는 자바스크립트에서 사용할 때 타입 강제 변환이 일어나 다루기 까다롭습니다. 주로 ==와 != 연산자를 사용할 때 타입 강제 변환이 일어납니다.

숫자와 문자열을 비교할 때는 먼저 문자열이 숫자로 변환되고 그 후 비교 연산이 수행됩니다.

    console.log(5 == '5'); // true

boolean 값을 숫자와 비교하면 boolean은 비교 연산을 수행하기 전에 먼저 숫자로 변경됩니다. false는 0으로, true는 1이 됩니다.

    console.log(1 == true); // true
    console.log(0 == false); // true

객체를 객체가 아닌 값과 비교하면 객체의 valueOf() 메서드를 호출해서 얻은 기본 데이터 타입값으로 비교 연산을 수행합니다. valueOf() 가 없으면 toString() 을 호출합니다.

    var object = {
        toString: function() {
            return "0*19";
        }
    };
    
    console.log(object == 25); // true

타입 강제 변환이 일어나는 타입 중 마지막으로 다룰 타입은 null과 undefined입니다.

    console.log(null == undefined); // true

**===와 !== 연산자는 타입 강제 변환 없이 비교 연산을 수행합니다.**

    console.log(0 === false); // false
    console.log(1 === true); // false
    console.log(null === undefined); // false

크락포드의 코드 컨벤션과 jQuery 코어 스타일 가이드, SproutCore 스타일 가이드에서는  ===와 !== 사용을 권장합니다.

### 4.6 eval()
eval()은 문자열로 된 자바스크립트 코드를 실행하는 함수입니다. 이 함수를 이용해 자바스크립트 코드를 추가로 내려받거나 실행 중에 자바스크립트 코드를 생성하고 실행할 수 있습니다. 

    eval("alert('hi~')");
    var count = 10;
    var number = eval("5 + count");
    console.log(number);

크락포드의 코드 컨벤션에는 eval()과 Function 사용을 금지하고 있고 문자열을 사용한 setTimeout()과 setInterval()도 금지하고 있습니다. jQuery 코어 스타일 가이드에서는 JSON 파싱을 위한 목적이 아니라면 eval() 사용을 금지하고 있습니다. 구글 자바스크립트 가이드는  Ajax 응답을 자바스크립트에서 사용하는 값으로 변경하는 목적으로 사용할 때를 제외하고는 eval() 사용을 금지하고 있습니다. 

### 4.7 기본 래퍼 타입
기본 래퍼 타입에는 String, Boolean, Number 세 가지가 있습니다.

나쁜 예

    var name = new String('jin');
    var author = new Boolean(true);
    var count = new Number(10);

이 예제처럼 기본 래퍼 타입을 직접 사용하는 방법도 있지만, 개인적으로 이렇게 사용하지 말 것을 권장합니다. 객체를 다루는지 기본 데이터 타입을 다루는지 혼동해서 기본 래퍼 타입을 잘못 사용해 버그가 발생할 수 있습니다. 게다가 객체를 반드시 직접 생성해야 할 이유도 없습니다.