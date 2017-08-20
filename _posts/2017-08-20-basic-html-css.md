---
layout: post
title: "HTML"
excerpt: "기초"
categories: [html]
comments: false
---

## 블록 레벨 요소
- 한 개의 독립된 덩어리
- 포함할 수 있는 요소: 인라인요소, 텍스트, 블록 레벨 요소

## 인라인 요소
- 행 안에 일부
- 포함할 수 있는 요소: 인라인요소, 텍스트

---

## 섹션

### section
heading 태그와 함께 사용하여 컨텐츠의 의미적 그룹을 나타낸다.

### article
독립적인 부분을 구성하는 섹션을 나타낸다.

### aside
주요 문맥을 담은 요소와 어떤 관련성을 지니고 있지만, 어떤 부연 설명 표시 영역이나 광고처럼 문맥의 주요 흐름 줄기엔 속하지 않는 섹션을 나타낸다.

### header
페이지의 도입부로서 보통 로고나 사이트 이름 그리고 수평메뉴를 포함한다.
꼭 페이지 처음에 있을 필요는 없다.

### footer
페이지의 종결부로서 보통 저작권이나 법률적 고지 혹은 약간의 링크들을 포함하고 있다. 꼭 페이지 끝에 있을 필요는 없다.

### nav(Group of navigation links)
주된 navigation 블럭을 형성하는 섹션이 nav 요소에 적합하다.

### h1 ~ h6(header 1 to header 6)
섹션의 제목을 나타낸다. 계층구조에 주의하여 사용한다.

### address
가장 가까운 조상 요소인 article 요소나 body 요소의 작성자(연락처) 정보를 나타낸다. adress 요소는 임의의 주소를 담는데 사용되어서는 안되는데 그 주소가 실제 연락처인 경우는 예외로 한다..(우편 주소를 마크업하기에 적합한 요소는 p 요소이다.)

---

## 그룹 컨텐츠

### p(paragraphy)
단락 즉 문장의 한 덩어리를 나타낸다.

### pre(preformatted text)
정형화된 텍스트(소스 안에서의 행바꿈과 스페이스가 그대로 브라우저에 표시되는 텍스트)를 표현한다. code 요소와 조합하여 프로그래밍 언어 소스코드를 표시하는데 일반적으로 사용한다.

### ul(unordered list)
순서가 중요하지 않은 목록을 나타낸다.

### ol(ordered list)
순서가 중요한 목록을 나타낸다.

### li(list item)
목록의 아이템을 나타낸다.

### dl(description list)
이름 - 값 그룹을 나타낸다. 단어와 정의일 수도 있고, 메타데이터 주제와 값일 수도 있다. 

### dt(definition term or name)
단어나 이름을 나타낸다.

### dd(definition description or value)
설명, 정의, 값을 나타낸다.

### figure(figure with optional caption)
figure 요소는 일러스트레이션, 다이어그램, 사진, 코드 등과 같은 플로우 컨텐츠를 문서에 포함한다. 이 요소는 보통 문서의 흐름에서 단일 요소로 참조되어 제거되더라도 문서의 주된 흐름에 영향을 미치지 않는다.

### figcaption
figure 요소 내용에 대한 캡션을 나타낸다.

### div(division)
블록 레벨 요소를 그룹화 한다.

---

## 표 형태의 데이터

### [table](http://html5.clearboth.org/tabular-data.html#the-table-element)

``` html
<table>
  <caption>제목</caption>
  <colgroup>
    <col width="20%">
    <col width="*">
  </colgroup>
  <thead>
    <tr>
      <th scope="col">table header cell 1</th>
      <th scope="col">table header cell 2</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>result 1</td>
      <td>result 2</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>table data cell</td>
      <td>table data cell</td>
    </tr>
  </tbody>
</table>
```

### caption
table의 제목을 표현한다.

### colgroup(table column group)
하나 이상의 열의 구조적인 그룹을 나타낸다.

### col(table column)
속성값과 스타일의 공유목적으로 열을 그룹화 한다.

### tbody(table row group) / thead(table heading group) /tfoot(table footer row group)
표의 행을 그룹하기 위한 요소이다.

### scope
th 요소로 제목정보를 제공하는 td 요소의 범위를 지정한다.
col / row / rowgroup / colgroup

---

## 텍스트 레벨 의미론

### [a(anchor)](http://html5.clearboth.org/text-level-semantics.html#the-a-element)
링크를 나타낸다. a 요소는 문단과 목록, 테이블 심지어는 섹션 전체를 둘러쌀 수도 있다. 단 내부에 버튼이나 다른 링크가 있어서는 안된다.

### [em(emphatic stress)](http://html5.clearboth.org/text-level-semantics.html#the-em-element)
특정 내용의 강조를 나타냅니다. 주변의 문장과 다른 의미나 느낌을 표현하기 위해 사용한다.

``` html
<p><em>Cats</em> are cute animals.</p>
```

"Cats"를 강조하여 어떤 동물에 대해 이야기하고 있다는 뉘앙스가 생겼다. ("dog"가 귀엽다고 주장하는 사람이 있을 수도 있습니니다.)

### strong
그 내용이 중요함을 나타낸다. 중요한 내용을 강조하여 쉬운 이해를 돕기 위한 요소이다.

### b(bold)
시각적인 강조를 위해 사용한다.

### i
문장 안에서 특정 단어에 스타일링이나 언어를 지정해 줄 때 사용한다.

### span
인라인 요소를 그룹화 한다.

---

## 포함된 컨텐츠

### img
[alt 속성](http://html5ref.clearboth.org/doku.php?id=html5:attribute:alt_img)

``` html
<img src="" alt="">
```

---

## Forms

### form

``` html
<form action="#">
    <fieldset>
        <legend>title</legend>
    </fieldset>
</form>
```

### fieldset(set of related form controls)
공통 이름(legend)으로 그룹화 된 폼 컨트롤 집합을 나타냅니다.

### legend(title or explanatory caption)
상위 부모 요소(fieldset, figure, details)에 내용이 있는 경우 해당 영역의 title 또는 설명을 나타낸다.

### label

#### 명시적 라벨 부여
for와 id에 같은 값을 지정하는 방법
``` html
<label for="name">Name</label>
<input type="text" id="name">
```

#### 암묵적 라벨 부여
label 요소의 범위에 텍스트와 컨트롤을 포함하는 방법
``` html
<label>
    Name
    <input type="text">
</label>
```

### [input type](http://html5.clearboth.org/the-input-element.html)

## 참조
- [HTML5 Open Reference - clearboth](http://html5ref.clearboth.org/)
- [문서의 섹션과 아웃라인 - MDN](https://developer.mozilla.org/ko/docs/Web/HTML/HTML5_%EB%AC%B8%EC%84%9C%EC%9D%98_%EC%84%B9%EC%85%98%EA%B3%BC_%EC%9C%A4%EA%B3%BD)
- [본문 : 문단(Paragraph) 요소 - EM, I, STRONG, B, MARK, DFN, CODE, SAMP, KBD, VAR](http://webdir.tistory.com/315)
- [html5 Doctor(HTML을 어떻게 구성하였는지 살펴보자.)](http://html5doctor.com/)