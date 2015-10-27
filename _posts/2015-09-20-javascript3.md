---
layout: post
date: 2015-09-20
title: "책요약 - JavaScript for Web Developers 3"
categories: js
author_name : jmaking
author_url : /author/jmaking
author_avatar: jmaking
show_avatar : false
read_time : 10
feature_image: feature-reed
show_related_posts: true
square_related: recommend-reed
---

언의어 기초(연산자) 내용 정리

> 자바스크립트 프로그래밍: 프론트엔드 개발자를 위한   
> 니콜라스 자카스    
> 인사이트 
> 978-89-6626-076-8

## 3장 언어의 기초 ##

### 3.5 연산자

#### 3.5.1 단항 연산자
단 하나의 값에만 적용되는 연산자

##### 증감 연산자

    var s1 = "2";
    var s2 = "z";
    var b = false;
    var f = 1.1;
    var o = {
    			valueOf: function(){
                	return -1;
                }
    		};
    
    
    console.log(++s1);    // 3 
    console.log(++s2);    // NaN
    console.log(++b);     // 1
    console.log(--f);     
            // 0.10000000000000009(부동소수점의 부정확성)
    
    console.log(--o);     // -2 

   
##### 단항 플러스와 단항 마이너스
   
    var s1 = "01";
    var s2 = "1.1";
    var s3 = "z";
    var b = false;
    var f = 1.1;
    var o = {
    			valueOf: function(){
                	return -1;
                }
    		};
    
    
    console.log(+s1);   // 숫자 1
    console.log(+s2);   // 숫자 1.1
    console.log(+s3);   // NaN
    console.log(+b);    // 숫자 0
    console.log(+f);    // 변함 없이 1.1
    console.log(+o);    // 숫자 -1

#### 3.5.3 불리언 연산자
불리언 연산자는 == 연산자 만큼이나 중요하며 프로그래밍 언어가 제 구실을 하는 데 꼭 필요합니다.

##### 논리 NOT(!)
논리 NOT 연산자는 먼저 피연산자를 불리언 값으로 변환한 다음 그 결과를 부정하며 다음과 같이 동작합니다.
- 피연산자가 객체이면 false
- 피연산자가 빈 문자열이면 true
- 피연산자가 비어 있지 않은 문자열 false
- 피연산자가 숫자 0이면 true
- 피연산자가 0이 아닌 숫자라면 false
- 피연산자가 null이면 true
- 피연산자가 NaN이면 true
- 피연산자가 undefined이면 true

    console.log(!false);          // true
    console.log(!!false);        // false
    console.log(!'blue');         // false
    console.log(!0);               // true
    console.log(!NaN);          // true
    console.log(!'');               // true
    console.log(!12345);      // false
    console.log(!undefined);     // true
    console.log(!null);         //true

**NOT연산자를 연달아 두 개 쓰면 Boolean() 함수를 쓴 것과 마찬가지 효과가 있습니다.** 첫 번째 NOT은 피연산자의 타입에 관계 없이 불리언 값을 반환합니다. 두 번째 NOT은 첫 번째 NOT이 반환한 불리언 값을 부정합니다.

##### 논리 AND(&&)

| 피연산자 1 | 피연산자 2 |  결과 |
|:----------:|:----------:|:-----:|
|    true    |    true    |  true |
|    true    |    false   | false |
|    false   |    true    | false |
|    false   |    false   | false |

첫 번째 피연산자에서 결과를 결정할 수 있다면 논리 AND 연산자는 두 번째 피연산자를 결코 평가하지 않습니다. **논리 AND에서 첫 번째 피연산자가 false라면 두 번째 피연산자의 값과는 무관하게 결과는 절대 true일 수 없습니다.** 즉 결과가 반드시 false이므로 절대 &&의 오른쪽을 평가할 이유는 전혀 없습니다.

    var found = true;
    var found2 = false;
    
    var result = (found2 && someUndeclaredVariable);
    console.log(result); // false
    
    var result2 = (found && someUndeclaredVariable);
    console.log(result2); // Uncaught ReferenceError: someUndeclaredVariable is not defined

##### 논리 OR(||)

| 피연산자 1 | 피연산자 2 |  결과 |
|:----------:|:----------:|:-----:|
|    true    |    true    |  true |
|    true    |    false   |  true |
|    false   |    true    |  true |
|    false   |    false   | false |

첫 번째 피연산자가 true로 평가된다면 두 번째 피연산자는 결코 평가하지 않습니다. 

    var found = true;
    var found2 = false;
    var result = (found || someUndeclaredVariable);
    console.log(result); // true
    
    var result2 = (found2 || someUndeclaredVariable);
    console.log(result2); // someUndeclaredVariable is not defined

**논리 OR 연산자의 행동을 이용해서 변수에 null나 undefined가 저장되지 않게 할 수 있습니다.** 

    var preferredObject = "yes";
    var backupObject = "no";
    var myObject = preferredObject || backupObject;
    console.log(myObject);

#### 3.5.4 곱셈 관련 연산자
숫자가 아닌 값에 적용할 때는 이면에서 Number() 함수를 이용해 타입을 바꿉니다. 즉 빈 문자열은 0으로 취급되고 불리언 true는 1로 취급됩니다.

##### 곱셈(*)

##### 나눗셈(/)
- 0을 0으로 나눈 결과는 NaN

##### 나머지(%)

#### 3.5.5 덧셈 관련 연산자

##### 덧셈
    var num1 = 5;
    var num2 = 10;
    var message = "The sum of 5 and 10 is "+ num1 + num2;
    console.log(message); // The sum of 5 and 10 is 510
    
    // 인터프리터에서 괄호 안을 먼저 계산한 후 그 결과를 문자열에 합침
    var message2 = "The sum of 5 and 10 is "+ (num1 + num2);
    console.log(message2); // The sum of 5 and 10 is 15

- 피연산자가 모두 문자열이라면 두 번째 문자열을 첫 번째 문자열에 합칩니다.
- 피연산자 중 하나가 문자열이라면 다른 피연산자를 문자열로 변환하고 두 문자열을 합칩니다.

##### 뺄셈(-)

    console.log( 5 - true ); // 4
    console.log( NaN - 1 ); // NaN
    console.log( 5 - 3 ); // 2
    console.log( 5 - "" ); // 5
    console.log( 5 - "2" ); // 3
    console.log( 5 - null ); // 5
    console.log( 5 + null ); // 5
    console.log( undefined - undefined ); // NaN

#### 3.5.6 관계 연산자
- 미만(<)
- 초과(>)
- 이하(<=)
- 이상(>=)

관계 연산자의 피연산자가 모두 문자열이면,
첫 번째 문자열의 문자 코드와 두 번째 문자열의 문자 코드를 대응하며 비교합니다.

    console.log("23" < "3"); // true
    console.log("23" < 3); // false
    console.log("a" < 3); // false
    console.log(NaN >= 3); // false

- 숫자와 문자열을 비교할 때는 문자열을 숫자로 바꾼 다음 비교
- "a"는 의미를 유지한 채 숫자로 변환할 수는 없으므로 NaN
- NaN과의 비교는 항상 false

#### 3.5.7 동일 연산자
ECMAScript 에서는 연산자를 두 벌로 분리해서 '동일'과 '비동일' 연산자는 비교하기 전에 타입을 변환하며 **'일치'와 '불일치' 연산자는 타입 변환 없이 비교**하는 것으로 정했습니다.

##### 동일(==)과 비동일(!=)
두 연산자 모두 피연산자를 비교하기 전에 변환합니다. 이런 변환을 종종 '타입 강제'라 부릅니다.

| 표현식            | 값    |
|-------------------|-------|
| null == undefined | true  |
| "NaN" == NaN      | false |
| 5 == NaN          | false |
| NaN == NaN        | false |
| NaN != NaN        | false |
| false == 0        | true  |
| true == 1         | true  |
| true == 2         | false |
| undefined == 0    | false |
| null == 0         | false |
| "5" == 5          | true  |

##### 일치(===)와 불일치(!==)
**null === undefined // false**

#### 3.5.8 3항 연산자

    variable = boolean_expression ? true_value : false_value;

    var num1 = 10;
    var num2 = 100;
    var max = (num1 > num2) ? num1 : num2;
    console.log(max); // 100

#### 3.5.9 할당 연산자(=)

#### 3.5.10 쉼표 연산자
변수 선언에 가장 많이 사용

    var num1=1, num2=2, num3=3;

값을 할당할 때도 쓸 수 있다.

    var num = (5, 1, 4, 8, 0); // num에는 0이 저장됩니다.