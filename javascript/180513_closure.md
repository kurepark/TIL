### 인프런 생활코딩 자바스크립트 클로저
---

##### 클로저(closure)
외부함수가 내부함수의 컨텍스트에 접근할 수 있는 것      

```
function outter(){//외부함수
        var title = 'coding';//외부함수의 지역변수
    function inner(){//내부함수
        alert(title);//내부함수안에 title이란 변수가 없다. 이럴경우 외부함수의 지역변수에 접근하는 것을 클로저라고 한다
    }
    inner();
}
//위의 함수는 아래와 같다
function outter(){
    var inner = function(){}
}

```

클로저는 외부함수의 실행이 끝나 외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근할 수 있다. 
```
function outter(){
    var title = 'coding';
    return function(){
        alert(title);
    }
}
var inner = outter();//외부함수는 여기서 실행
inner();//외부함수는 실행 후 소멸되었지만 'coding'을 출력한다
```


##### privatae variable
조금 더 실용적인 예제

```
//get_title과 set_title이란 두개의 메소드를 반환하는 객체
//객체안에 함수가 정의되어있음. 메소드들이 내부함수가 된다.
//매개변수는 함수안에서 지역변수로 사용된다. 지역변수는 내부함수에서 접근이 가능하다


function factory_movie(title){
    return{
        get_title : function(){
            return title;
        },
        set_title : function(_title){
            title = _title;
        }
    }
}
ghost = factory_movie('Ghost in the shell');
matrix = factory_movie('Matrix');
alert(ghost.get_title());//Ghost in the shell
alert(matrix.get_title());//Matrix

ghost.set_title('공각기동대'));
alert(ghost.get_title());//공각기동대
alert(matrix.get_title());//Matrix

위와같이 사용하면 title이라는 변수는 외부에선 수정할 수 없고 get_title과 set_title을 이용해서만 변경과 출력이 가능하다. 
대규모의 코드나 협업을 할 경우 변수의 내용이 변경될 위험이 줄어든다.
```

##### 클로저의 응용
```
var arr = [];
for(var i = 0; i < 5; i++){
    arr[i] = function(){
        return i ;//for문에서 정의된 i
    }
}
for(var index in arr) {//arr배열에 담긴 값을 하나씩 꺼낸다
    console.log(arr[index]());//하나씩 꺼낸 것을 함수로 호출
}

//예상 출력은 4, 출력결과는 5 가 다섯번 

for(var i = 0; i < 5; i++){
    arr[i] = function(id){//외부함수
       return function(){//내부함수
             return id ;//for문에서 정의된 i
        }
    }(i);//외부함수의 매개변수로 i를 준다
}

for(var index in arr) {
    console.log(arr[index]());//출력결과는 0,1,2,3,4
}
```