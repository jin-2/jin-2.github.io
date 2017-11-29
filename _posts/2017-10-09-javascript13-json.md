---
layout: post
title: "JSON"
excerpt: "책요약"
categories: [Book - JavaScript for Web Developers]
comments: false
---

JSON은 복잡한 데이터 구조를 쉽게 표현하도록 디자인된 경량화된 데이터 형식이다. 크록포드가 자바스크립트에서 구조화된 데이터에 접근하는 수단으로 XML 대신 JSON을 권하는 이유는, JSON은 `eval()`에 직접 넘길 수 있으며 DOM을 따로 생성할 필요가 없기 때문이다.

## 20.1 문법

### 20.1.1 단순한 값
문자열, 숫자, 불리언, null은 모두 자바스크립트와 같은 문법으로 표현

#### 숫자 5를 표현하는 JSON

```json
5
```

#### 문자열을 나타내는 유효한 JSON

```json
"Hello world!"
```
**! 자바스크립트 문자열과 JSON 문자열의 차이는  JSON 문자열은 반드시 큰따옴표로 감싸야만 유효하다는 점이다.**

### 20.1.2 객체
JSON 객체는 객체 리터럴 표기법과 매우 비슷합니다.

#### 자바스크립트 객체 리터럴 표기법
```javascript
var person = {
    name: "amy",
    age: 29
};
```

#### JSON 객체 표기법
```json
{
    "name": "amy",
    "age": 29,
    "school": {
        "name": "Berkeley",
        "location": "California"
    }
}
```

#### 차이점
- 변수 선언이 없다.
- 문장을 마치는 세미콜론이 없다.
- 프로퍼티 이름도 **큰 따옴표**로 감싸야 한다.
- 객체 안에 객체를 쓸 수 있다.

### 20.1.3 배열

#### 자바스크립트 배열 리터럴 표기법
```javascript
var values = [25, "hi", true];
```

#### JSON 배열 표기법
```json
[25, "hi", true]
```

#### 배열과 객체를 조합한 복잡한 데이터 컬렉션
```json
[
    {
        "title": "Professional Javascript",
        "author": [
            "Nicholas C. Zakas"
        ],
        "edition": 3
    },
    {
        "title": "Professional Ajax",
        "author": [
            "Nicholas C. Zakas",
            "Jeremy McPeak",
            "Joe Fawcett"
        ],
        "edition": 2
    }
]
```

## 20.2 파싱과 직렬화

### 20.2.1 JSON 객체
- 오래된 브라우저에서 JSON을 파싱할 때 `eval()`을 쓰면 악의적인 코드를 실행할 위험이 있으므로 `eval()`을 쓰지 말아야 한다.
- [오래된 브라우저에 대한 폴백](https://github.com/douglascrockford/JSON-js)

### 20.2.2 직렬화 옵션

#### JSON.stringify() 메서드는 객체 외에 두 가지 매개변수를 더 받을 수 있습니다.
- 첫 번째 매개변수는 필터이며 배열이나 함수를 쓸 수 있습니다.
- 두 번째 매개변수는 JSON 문자열의 들여쓰기를 조절합니다.

##### 결과 필터링

###### 두번째 매개변수가 배열일 때
`JSON.stringify()`는 해당 배열에 포함된 객체 프로퍼티만 직렬화합니다.

```javascript
var book = {
    title: "Professional Javascript",
    author: [
        "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011
};

var jsonText = JSON.stringify(book, ["title", "edition"]);

// Result
{"title":"Professional Javascript","edition":3}
```

###### 두번째 매개변수가 함수일 때

```javascript
var book = {
    title: "Professional Javascript",
    author: [
        "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011
};

var jsonText = JSON.stringify(book, function(key, value){
    switch (key) {
        case "author":
            return value.join(",");
        case "year":
            return 5000;
        case "edition":
            return undefined;
        default:
            return value;
    }
});

console.log(jsonText );

// Result
{"title":"Professional Javascript","author":"Nicholas C. Zakas","year":5000}
```

##### 문자열 들여쓰기
- `JSON.stringify()`의 세 번째 매개변수는 들여쓰기와 공백을 컨트롤한다.
- 들여쓰기를 지정하면 읽기 쉽도록 줄바꿈도 삽입한다.
- 들여쓰기 최대값으 10이며 이보다 큰 값은 자동으로 10으로 바뀐다.

```javascript
var book = {
    title: "Professional Javascript",
    author: [
        "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011
};

var jsonText = JSON.stringify(book, null, "--");

// Result
{
--"title": "Professional Javascript",
--"author": [
----"Nicholas C. Zakas"
--],
--"edition": 3,
--"year": 2011
}
```

##### `toJSON()` 메서드
JSON 객체를 직렬화할 때 `JSON.stringify()`가 제공하는 기능 이상이 필요할 때도 있다. 이럴 때는 객체에 `toJSON` 메서드를 추가해서 올바른 JSON 표현을 반환한다.

```javascript
var book = {
    title: "Professional Javascript",
    author: [
        "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011,
    toJSON: function() {
      return this.title;
    }
};

var jsonText = JSON.stringify(book);
```

### 20.2.3 파싱 옵션
`JSON.parse()` 메서드 역시 각 키-값 쌍에서 호출될 콜백 함수를 추가적인 매개변수로 받는다. 이 함수는 `JSON.stringify()`에서 사용하는 '리플레이서(필터)' 함수와 구분하기 위해 **'리바이버'** 함수라고 부르지만 형식은 정확히 같아서 매개변수로 키와 값을 받으며 반환 값도 있습니다.

```javascript
var book = {
    title: "Professional Javascript",
    author: [
        "Nicholas C. Zakas"
    ],
    edition: 3,
    year: 2011,
    releaseDate: new Date(2011, 11, 1)
};
var jsonText = JSON.stringify(book);
  
var bookCopy = JSON.parse(jsonText, function(key, value) {
  if (key == "releaseDate") {
    return new Date(value);
  } else {
    return value;
  }
});

// Result
// 2011
```
