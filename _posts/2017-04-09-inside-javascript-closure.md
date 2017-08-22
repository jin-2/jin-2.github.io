---
layout: post
title: "실행 컨텍스트와 클로저"
excerpt: "책요약"
categories: [Book - Inside JavaScript]
comments: false
---

> 인사이드 자바스크립트  
> 송형주, 고현준  
> 한빛미디어(주)  
> 978-89-6848-065-2  

## 5.1 실행 컨텍스트 개념

> "실행 가능한 자바스크립트 코드 블록이 실행되는 환경"

**실행 컨텍스트가 형성되는 경우**
- 전역 코드
- eval() 함수로 실행되는 코드
- 함수 안의 코드를 실행할 경우

이 코드가 실행되면 실행 컨텍스트가 생성되고,
실행 컨텍스트는 스택 안에 하나씩 차곡차곡 쌓이고,
제일 위에 위치하는 실행 컨텍스트가 현재 실행되고 있는 컨텍스트다.

> "현재 실행되는 컨텍스트에서 이 컨텍스트와 관련 없는 실행 코드가 실행되면,
새로운 컨텍스트가 생성되어 스택에 들어가고 제어권이 그 컨텍스트로 이동한다."

## 5.2 실행 컨텍스트 생성 과정

### 5.2.1 활성 객체 생성
실행 컨텍스트가 생성되면 자바스크립트 엔진은 해당 컨텍스트에서 실행에 필요한
여러 가지 정보를 담을 객체를 생성하는데, 이를 활성 객체라고 한다.

### 5.2.2 arguments 객체 생성
앞서 만들어진 활성 객체는 arguments 프로퍼티로 이 arguments 객체를 참조한다.

### 5.2.3 스코프 정보 생성
현재 컨텍스트의 유효 범위를 나타내는 스코프 정보를 생성한다. 이 스코프 정보는
현재 실행 중인 실행 컨텍스트 안에서 연결 리스트와 유사한 형식으로 만들어진다.
현재 컨텍스트에서 특정 변수에 접근해야 할 경우, 이 리스트를 활용한다. 이 리스트를
**스코프 체인** 이라고 하는데, [[scope]] 프로퍼티로 참조된다.

### 5.2.4 변수 생성
현재 실행 컨텍스트 내부에서 사용되는 지역 변수의 생성이 이루어진다. 변수 객체(= 활성 객체)
안에서 호출된 함수 인자는 각각의 프로퍼티가 만들어지고 그 값이 할당된다.  
여기서 주의할 점은 이 과정에서는 변수나 내부 함수를 단지 메모리에 생성하고,
초기화는 각 변수나 함수에 해당하는 표현식이 실행되기 전까지는 이루어지지 않는다는
점이다.

### 5.2.5 this 바인딩
마지막 단계에서는 this 키워드를 사용하는 값이 할당된다.
여기서 this가 참조하는 객체가 없으면 전역 객체를 참조한다.

### 5.2.6 코드 실행
이렇게 하나의 실행 컨텍스트가 생성되고, 변수 객체가 만들어진 후에, 코드에 있는
여러 가지 표현식 실행이 이루어진다. 이렇게 실행되면서 변수의 초기화 및 연산,
또 다른 함수 실행 등이 이루어진다.

## 5.3 스코프 체인
각각의 함수는 [[scope]] 프로퍼티로 자신이 생성된 실행 컨텍스트의 스코프 체인을
참조한다. 함수가 실행되는 순간 실행 컨텍스트가 만들어지고, 이 실행 컨텍스트는 실행된
함수의 [[scope]] 프로퍼티를 기반으로 새로운 스코프 체인을 만든다.

### 5.3.1 전역 실행 컨텍스트의 스코프 체인
전역 실행 컨텍스트는 단 하나만 실행되고 있어 참조할 상위 컨텍스트가 없다. 자신이
최상위에 위치하는 변수 객체인 것이다. 따라서, 이 변수 객체의 스코프 체인은 자기
자신만을 가진다. 다시 말해서, 변수 객체의 [[scope]]는 변수 객체 자신을 가리킨다.

### 5.3.2 함수를 호출한 경우 생성되는 실행 컨텍스트의 스코프 체인
- **각 함수 객체는 [[scope]] 프로퍼티로 현재 컨텍스트의 스코프 체인을 참조한다.**
- 한 함수가 실행되면 새로운 실행 컨텍스트가 만들어지는데, 이 새로운 실행 컨텍스트는
자신이 사용할 스코프 체인을 다음과 같은 방법으로 만든다. **현재 실행되는 함수 객체의
 [[scope]] 프로퍼티를 복사하고, 새롭게 생성된 변수 객체를 해당 체인의 제일 앞에 추가한다.**
- 요약하면 스코프 체인은 다음과 같이 표현할 수 있다.

**스코프 체인 = 현재 실행 컨텍스트의 변수 객체 + 상위 컨텍스트의 스코프 체인**

이렇게 만들어진 스코프 체인으로 식별자 인식이 이루어진다. 식별자 인식은 스코프 체인의
첫번째 변수 객체부터 시작한다. 식별자와 대응되는 이름을 가진 프로퍼티가 있는지를 확인한다.
함수를 호출할 때 스코프 체인의 가장 앞에 있는 객체가 변수 객체이므로, 이 객체에
있는 공식 인자, 내부 함수, 지역 변수에 대응되는지 먼저 확인한다. 첫 번째 대응되는
프로퍼티를 발견하지 못하면, 다음 객체로 이동하여 찾는다. 이런 식으로 대응되는 이름의
프로퍼티를 찾을 때까지 계속된다. 여기서 this는 식별자가 아닌 키워드로 분류되므로,
스코프 체인의 참조 없이 접근할 수 있음을 기억하자.