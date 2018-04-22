### 인프런 생활코딩 자바스크립트 정규표현식 강의
---
문자열 안에서 특정한 문자를 찾아내는 도구. 특정한 문자를 다른 문자로 치환해주는 도구.       
이번 수업에서는 자바스크립트 내에서 정규표현식을 조작하는 방법을 배운다.

##### 정규표현식을 통해 하는 주요한 작업들
패턴을 만들고 그 패턴에 맞는 정보를 **추출**
자신이 확인하고자 하는 정보가 있는지 **테스트**
사전에 찾은 정보를 다른 정보로 **치환**하는것


1. 컴파일 - 작업을 하기 위해 필요한 대상(패턴)을 찾는 것
2. 실행 - 찾은 대상에 대해서 어떠한 작업을 구체적으로 하는 것

#### 컴파일
```
//패턴을 만드는 방법
// 1. 정규표현식 리터럴
var pattern = /a/;  //찾고자 하는 대상을 /사이에 넣어준다

//pattern이라는 변수에 담는다.

// 2. 정규표현식 객체 생성자
var pattern = new RegExp('a');

//RegExp = regular expression의 약자 
//new를 사용해 정규표현식 객체를 만든다. 찾고자 하는 대상을 ()에 넣는다

```
#### 정규표현식 메소드 실행
```
var pattern = /a/;
//pattern변수안엔 정규표현식 객체가 들어있다
pattern.exec('abcde'); // ["a"];

// 문자열 a를 찾고 싶다.
// 실행의 대상을 첫번째 인자로 전달
// 두번째 인자에 찾아볼 대상
var pattern = /a./;
pattern.exec('a');// ["ab"]

pattern안에 a.을 넣을 경우에 a뒤에 있는 문자까지 찾아온다

var pattern = /a/;
pattern.exec('devdc'); // null , 찾고자 하는 대상이 없기 때문에
pattern.test('devcd');// false
pattern.test('abdc');//true


//문자열 메소드
var pattern = /a/;
var str = 'abcde';
str.match(pattern); // ["a"]

var str = 'bdcdcd';
str.match(pattern);// null

var str = 'abcdef';
str.replace(pattern, 'A');// "Abcdef"


//정규표현식 메소드
exec //추출
test //존재유무 테스트
match //매칭
replace // 치환

```

#### 정규표현식 옵션(i, g)

```
//i를 붙이면 대소문자를 구분하지 않는다
var xi = /a/; 
"Abcde".match(xi);//null 소문자 a가 없으므로 null이 리턴

var oi = /a/i;//i를 주게 되면 대문자 소문자를 구별하지 않는다
"Abcde".match(xi);//["A"]

//g를 붙이면 검색된 모든 결과를 리턴한다
var xg = /a/;
"abcdea".match(xg); //["a"]  a가 두개지만 하나만 리턴
var og = /a/g;
"abcdea".match(xg); //["a","a"] a가 배열에 두개담김

var ig = /a/ig; //대소문자 구별없이 모든 a를 찾는다
"AabcdAa".match(ig);//["A","a","A","a"] 대문자 소문자 구별없이 모든 a를 찾는다
```

#### 캡쳐
- 정규표현식 시각화 [https://regexper.com/]

```
(\w+)\s(\w+)
문자 공백 문자

() : 그룹
\w : 문자를 의미, 문자란  A~Z, a~z, 0~9
+ : 수량자. 앞에있는 문자가 **하나 이상**인 경우 패턴이 유효해진다
\s : space 공백 
```

- 정규표현식 빌더 [https://regexr.com/]

```
var pattenr = /(\w+)\s(\w+)/;

var str = "conding everybody"

var result = str.replace(pattern,"$2, $1"); 
//문자열 값을 패턴에 해당되는 문자를 두번째 인자의 값으로 치환
// $라는 기호는 그룹을 의미. $2는 두번째 그룹, $1은 첫번째 그룹
//everybody가 첫번째로 공백은 컴마로, 공백뒤에 첫번째 그룹이 뒤로 간다.
console.log(result); // everybody, coding

//그룹을 지정하고 지정된 그룹을 가져와서 사용하는 기능을 캡쳐라고 한다.
```

#### 치환

```
var urlPattern = /\b(?:https?):\/\/[a-z0-9-+&@#\/%?=~_|!:,.;]*/gim; //패턴 정의

var content = '생활코딩 : http://opentutorials.org/course/1 입니다. 네이버 : http://naver.com 입니다. ';

var result = content.replace(urlPattern, function(url){
    return '<a href="'+url+'">'+url+'</a>';
});// 첫번째 인자는 패턴, 두번째 인자로는 함수를 전달.
console.log(result);
```
