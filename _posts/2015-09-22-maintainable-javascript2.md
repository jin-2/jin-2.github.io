---
layout: post
title: "스타일 가이드라인(주석, 문장과 표현식)"
excerpt: "책요약"
categories: [Book - Maintainalble JavaScript]
comments: false
---

> 읽기 좋은 자바스크립트 코딩 기법 Maintainalble JavaScript  
> 니콜라스 카자스  
> O'REILLY 한빛미디어  
> 978-89-7914-988-3

## part1. 스타일 가이드라인(2)

### 주석
적절한 주석이 있으면 코드를 처음부터 일일이 살펴볼 필요 없이 코드의 작성 이유를 바로 파악하고 작업을 시작할 수 있습니다.

#### 2.1 한 줄 주석

    // 좋은 예
    if (condition) {
        
        // 한 줄 비우고 주석 입력, 들여쓰기도 코드에 맞춤
        allowed(); 
    }

    var result = something + somethingElse; // 꼬리 주석은 한 단계 들여쓰기

    // 코드를 주석 처리할 때
    //  if (condition) {
    //      doSomething();
    //  }

#### 2.2 여러 줄 주석

    /* 
     *  자바 스타일 주석
     */

    if (condition) {
    
        /*
         *  한 줄 비우고, 코드의 들여쓰기와 맞춤
         */
        allowed();
    }
    
    var rusult = something + somethingElse; /* 꼬리 주석은 여러 줄 주석으로 사용하지 말 것 */

#### 2.3 주석 쓰기
- 코드 자체로 충분히 설명 가능한 부분에는 주석을 쓰지 않습니다.
- 코드를 명확하게 해야 할 곳에 추가해야 합니다.

##### 2.3.1 이해하기 어려운 코드

##### 2.3.2 오해하기 쉬운 코드

##### 2.3.3 특정 브라우저 핵

주석을 써야 한다.

#### 2.4 문서화 주석
문서화 주석에는 JavaDoc 문서 포맷이 가장 많이 쓰입니다. 

    /**
    인자로 넘어온 객체...
    프로퍼티가...
    
    @method merge
    @param {Object} object* 합치고 싶은 객체들
    **/

- YUIDoc: HTML과 Markdown을 지원
- JSDoc: HTML만 지원

### 3 문장과 표현식
자바스크립트에서 if나 for와 같은 '문장'을 사용하는 방법은 두 가지입니다.
- 여러 줄을 중괄호로 감싸는 방법
- 중괄호를 사용하지 않는 방법(권장함.)

    // 좋은 예
    if (condition) {
        doSomething();
    }

#### 다음의 모든 복합문에서는 중괄호를 반드시 사용해야 합니다.
- if
- for
- while
- do ... while
- try ... catch ... finally

#### 3.1 중괄호 넣기

    // 권장: 자바 프로그래밍 언어 코드 컨벤션
    if (condition) {
        doSomething();
    }
    
    // 권장하지 않음: 비주얼 스튜디오에서 이 방식을 강제화 주로 C#
    if (condition)
    {
        doSomething();
    }

#### 3.2 복합문에서의 공백

    //  Dojo 스타일 가이드에서 권장
    if(condition){
        dosomething();
    }
    
    // 크락포드의 코드 컨벤션, 구글 자바스크립트 스타일 가이드에서 권장
    if (condition) {
        dosomething();
    }
    
    // jQuery 코어 스타일 가이드에서 권장
    if ( condition ) {
        dosomething();
    }

#### 3.3 switch 문

##### 3.3.1 들여쓰기

    switch (condition) {
        case "first":
            // code
            break;
    
        case "second":
            // code
            break;
    
        case "third":
            // code
            break;
    
        default:
            // code
    }

이 포맷이 JSLint에서 경고 메시지를 출력한다면, 'Tolerate messy white sapce(지전분한 여백을 허용)' 옵션을 끄면 여기에 대한 검사를 수행하지 않습니다.

##### 3.3.2 다음 case 문까지 실행하는 switch 문
'다음 case 문까지 실행하는 switch 문 (fass-through) 을 허용할 것인가'

    switch (condition) {
    
        // 어떤 로직도 수행하지 않고 다음 case 문으로 넘깁니다.
        case "first":
        case "second":
            // code
            break;
    
        case "third":
            // code
    
            /* falls through */
        default:
            // code
    }

세 번째  case 문은 default 문으로 연결됩니다. 여기에는 작성자가 의도적으로 default 문으로 넘겼음을 주석을 통해 알리고 있습니다. 이 코드는 실수가 아닌 개발자의 의도라는 것이 명확합니다. JSHint에서는 실수로 break 문을 빠뜨린 게 아니라는 의미로 "falls through"라고 case 문에 주석을 추가하면, 경고 메시지를 출력하지 않습니다.

##### 3.3.3 default 절
논쟁이 될만한 또 다른 요소는 'switch 문에 default 절을 꼭 넣어야 하는가'입니다. 

    switch (condition) {
        case "first":
            // code
            break;
    
        case "second":
            // code
            break;
    
        // no default
    }

이 방법은 default 절은 생략하겠다는 작성자의 의도가 명확하고 필요없는 문법을 사용하지 않아 용량을 절약할 수도 있습니다.

#### 3.4 with 문
with 문은 실행할 로직의 문맥을 변경합니다.

    var book = {
        title: "Maintainable JavaScript",
        author: "Nicholas C. Zakas"
    };
    
    var message = "The book is ";
    
    with (book) {
        message += title;
        message += " by " + author;
    }

title과 author의 주인이 어떤 객체인지 알기 어렵다는 것이 문제입니다.

with 문은 문법 에러가 발생할 확률이 높아 strict 모드에서는 사용할 수 없는데 이는 ECMAScript 위원회도 with 문을 더는 사용하지 말아야 할 구문이라 생각한다는 걸 의미합니다. 크락포드의 코드 컨벤션과 구글 자바스크립트 스타일 가이드는 with 문 사용을 금지하고 있습니다. 개인적으로도 작성한 코드를 strict 모드로 적용할 때 with 문은 큰 방해 요소이므로 **with 문을 사용하지 않기를 강력하게 권고**합니다.

#### 3.5 for 반복문
break 문을 사용하면 배열 끝에 도달하기 전에 반복문을 종료합니다.

    var values = [1, 2, 3, 4, 5, 6, 7],
        i, len;
    
    for (i = 0, len = values.length; i < len; i++) {
        if (i == 2) {
            break; // 반복문이 종료됩니다.
        }
        process(values[i]);
    }

continue 는 반복문 내 로직 수행을 즉시 종료하지만, 다음 예제처럼 다음 요소로 넘어가 순환을 계속합니다.

    var value = [1, 2, 3, 4, 5, 6, 7],
        i, len;
    
    for (i = 0, len = values.length; i < len; i++) {
        if (i == 2) {
            contiune; // 이번 순환은 그냥 넘어갑니다.
        }
    }

크락포드는 contiune를 사용하기보다는 조건문을 사용하는 편이 낫다고 말합니다.

    var values = [1, 2, 3, 4, 5, 6, 7],
        i, len;
    
    for (i = 0, len = values.length; i < len; i++) {
        if (i != 2) {
            process(values[i]);
        }
    }

#### 3.6 for...in 반복문
**for...in 반복문을 사용할 때 문제점은** 객체가 소유한 인스턴스의 프로퍼티만 반환하는 것이 아니라 상속받은 프로토타입의 프로퍼티도 반환한다는 점입니다. 이 때문에 객체의 프로퍼티를 순환하다 보면 예상치 못한 결과가 발생할 수도 있습니다.

    var prop;
    
    for (prop in object) {
        if (object.hasOwnProperty(prop)) {
            console.log("Property name is "+ prop);
            console.log("Property value is "+ objejct[prop]);
        }
    }

**hasOwnProperty()** 메서드를 사용해 현재 인스턴스의 프로퍼티만 걸러서 사용하는 방법이 가장 좋습니다.

나쁜 예: 배열의 요소를 순환하는 데 for...in 반복문을 사용하는 것

    var values = [1, 2, 3, 4, 5, 6, 7],
        i;
    
    for (i in values) {
        process(items[i]);
    }

