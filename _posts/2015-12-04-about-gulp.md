---
layout: post
title: "gulp 시작하기"
excerpt: "자료 정리"
categories: [dev]
comments: false
---

자동화 빌드도구 gulp를 시작하면서 기억할 것 메모!

## [Gulp와 Grunt의 차이점](http://webframeworks.kr/getstarted/grunt-and-gulp/#tocAnchor-1-4)

## [Gulp 입문 - 감성 프로그래밍](http://programmingsummaries.tistory.com/356)
1. npm, gulp 설치 확인
2. 폴더 생성
3. `$ npm init` [package.json 생성](https://docs.npmjs.com/getting-started/using-a-package.json)
3. `$ npm install gulp --save-dev` node-modules 설치
4. 폴더 및 gulpfile.js 생성

### 디렉토리 구조
src: source / dist: distribution(유통)

    node_modules/
    public/
        src/
            index.html
            img/
            js/
            scss/
        dist/
            index.html
            img/
            js/
            css/
        lib/
            vanilla.js
            fancybox.js
    gulpfile.js
    package.json

### [gulpfile.js](https://gist.github.com/jin-2/4685e457ba2021ee7bdf)

`var name = require('plugin');`  
npm으로 --save-dev 옵션을 주어 설치 된 플러그인을 사용할 때 필요

`gulp.task(name, deps, func)`  
name: task 이름
deps: 해당 task가 실행되기 전 선행되어야 하는 것(선택사항)
func: task의 내용 정의

`gulp.src(files)`  
경로들을 포함하는 배열 또는 스트링  
(와일드카드 형태: js/ ** / *.js)

`gulp.pipe()`  
task결과물 전달

`gulp.watch(folder, [actions])`  
특정 폴더를 계속 관찰한다. css파일을 변경했을 때 js파일의 수정은 필요없으므로 각각 작성한다.

`gulp.dest()`  
해당 dask의 결과물이 저장될 경로

### [A Simple Gulp’y Workflow For Sass - Hugo Giraudel](http://www.sitepoint.com/simple-gulpy-workflow-sass/)

#### [gulpfile.js(Sass에 대한 내용)](https://gist.github.com/jin-2/da318dbbe96221a16a81)

### Module
- **gulp-sourcemaps**
- **gulp-autoprefixer**: prefixer를 지원하고 싶은 브라우저만 지정해서 자동으로 생성해 줌
- **sassdoc**: 주석의 내용을 sass 가이드 문서로 만들어 줌
- **del**: 폴더(디렉토리)/파일 제거
- **gulp-if**: 조건 처리
- **gulp-rename**: 파일 이름 변경
- **gulp-jade**: Jade → HTML 변환
- **gulp-sass**: Sass → CSS 변환
- **gulp-ruby-sass**: Sass → CSS 변환(Ruby 기반)
- **gulp-ruby-compass**: Sass → CSS 변환(Ruby 기반)
- **gulp-plumber**: 오류 발생해도 watch 업무 지속
- **gulp-watch**: 변경된 파일만 처리
- **gulp-html-prettify**: HTML 구조 읽기 쉽게 변경
- **gulp-connect-multi**: 웹 서버
- **gulp-webserver**: 웹서버처럼 동작
- **gulp-concat**: js 파일 병합
- **gulp-uglify**: js 파일 압축
- **gulp-mimify-html**: html 파일 압축
- **gulp-livereload**: 웹 브라우저 리로드


