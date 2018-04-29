### 인프런 생활코딩 자바스크립트 함수와 콜백
---

값으로서의 함수     
자바스크립트에서는 함수도 **객체**이다.     
함수는 값이 될 수 있다. 즉, 변수에 담을 수 있다.        그리고 객체의 값으로 포함될 수 있다. 이렇게 객체의 속성 값으로 담겨진 함수를 **메소드(method)**라고 부른다.         


```
function a(){} //함수 a는 변수 a에 담겨진 값이다.

var a = function(){} //이것과 같다


a = {
    b :function(){ // b는 키(속성, property), 함수는 value(메소드)

    }
}
```


함수는 값이기 때문에 **다른 함수의 인자**로 전달이 될 수도 있다.        
```
function cal(func, num){
    return func(num);
}

function increase(num){
    return num+1;
}

function decrease(num) {
    return num -1;
}

alert(cal(increase, 1));
alert(cal(decrease, 1))
```

함수는 **함수의 리턴 값**으로도 사용할 수 있다.

```
function cal(mode){
    var func = {
        'plus' : function(left, right){return left+ right},
        'minus':function(left, right){return left -right}
    }
    return funcs[mode];
}

alert(cal('plus')(2,1)); //3
alert(cal('minus')(2,1)); //1

cal('mode') //여기까지는 cal안에 있는 plus, minus
그 뒤에 (2, 1)은 plus, minus안에 있는 함수 실행
```

함수는 **배열의 값**으로도 사용할 수 있다
```
var process = [
    function(input){return input +10;},
    function(input){return input * input;},
    function(input){return input / 2;}
] // 배열에 함수를 담을 수 있다

var input = 1;
for(var i =0; i <process.length; i++){
    input = process[i](input); // porcess[i]는 배열의 순서, (input)은 실행
}
alert(input); // 11, 121, 최종 alert에는 60.5
```

> 변수, 매개변수, 리턴값으로 사용될 수 있는 데이터를 프로그래밍에서 **first-class citizen(object)**라고 부른다. 자바스크립트의 함수가 바로 first-class citizen이다. 

