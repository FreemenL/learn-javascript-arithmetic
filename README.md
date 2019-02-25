# learn-javascript-arithmetic

> 数组 
        
>1 ,求斐波那契额数列的前20个数字 已知斐波那契额数列中的第一个数字是1 第二个是二 ，从第三项开始，每一项都等于前两项之和:

```javascript 
let fibonacci = []; 
fibonacci [0] = 1;
fibonacci [1] = 2;
for(let i = 2;i<=20;i++){
    fibonacci[i] = fibonacci[i-2]+fibonacci[i-1];
}
console.log(fibonacci);
//[1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181, 6765, 10946, 17711]
```
> 输入索引返回对应的值 

```javascript
//解法一 
function fibonacci(index){
    if(index===1||index===2){
        return 1;
    }
    return fibonacci(index-2)+fibonacci(index-1);
}
console.log(fibonacci(7));
//13
```

```javascript
//利用数组缓存进行优化
let fibonacci = function() {
    let temp = [0, 1];
    return function(n) {
        let result = temp[n];
        if(typeof result != 'number') {
            result = fibonacci(n - 1) + fibonacci(n - 2);
            temp[n] = result; // 将每次 fibonacci(n) 的值都缓存下来
        }
        return result;
    }
}(); 
```

```javascript
//动态规划
function fibonacci(n) {
    let current = 0;
    let next = 1;
    let temp;
    for(let i = 0; i < n; i++) {
        temp = current;
        current = next;
        next += temp;
    }
    console.log(`fibonacci(${n}, ${next}, ${current + next})`);
    return current;
}
```
>二维和多维数组   (矩阵) 

* 创建一个矩阵
 ```javascript
    var averageTemp = [];
    //day 1
    averageTemp[0] = [];
    averageTemp[0][0] = 72;
    averageTemp[0][1] = 75;
    averageTemp[0][2] = 79;
    averageTemp[0][3] = 79;
    averageTemp[0][4] = 81;
    averageTemp[0][5] = 81;
    //day 2
    averageTemp[1] = [];
    averageTemp[1][0] = 81;
    averageTemp[1][1] = 79;
    averageTemp[1][2] = 75;
    averageTemp[1][3] = 75;
    averageTemp[1][4] = 73;
    averageTemp[1][5] = 72;
 ```
        
>输出矩阵内容具体方法
```js
function printMatrix(myMatrix) {
    for (var i=0; i<myMatrix.length; i++){
        for (var j=0; j<myMatrix[i].length; j++){
            console.log(myMatrix[i][j]);
        } 
    }
}
printMatrix(averageTemp);
```
>假如我们要创建一个3×3的矩阵，每一格里 包含矩阵的i(行)、j(列)及z(深度)之和:
```js
 var matrix3x3x3 = [];
    for (var i=0; i<3; i++){
        matrix3x3x3[i] = [];
        for (var j=0; j<3; j++){ 
            matrix3x3x3[i][j] = [];
            for (var z=0; z<3; z++){
                matrix3x3x3[i][j][z] = i+j+z;
            }
        }
    }
    //输出矩阵内容 
    for (var i=0; i<matrix3x3x3.length; i++){
        for (var j=0; j<matrix3x3x3[i].length; j++){
            for (var z=0; z<matrix3x3x3[i][j].length; z++){
                console.log(matrix3x3x3[i][j][z]);
            } 
        }
    }
```
               
>sort 对象类型的数组 排序
```js
var friends = [
    {name: 'John', age: 30},
    {name: 'Ana', age: 20},
    {name: 'Chris', age: 25}
];
friends.sort((a,b)=>a.age-b.age)
```
        
> 2. 字符串排序
```js
var names =['Ana', 'ana', 'john', 'John'];
console.log(names.sort()); 

//["Ana", "John", "ana", "john"]

//JavaScript在做字符比较 的时候，是根据字符对应的ASCII值来比较的。例如，A、J、a、j对应的ASCII值分别是65、75、 7、106。
//虽然在字母表里a是最靠前的，但J的ASCII值比a的小，所以排在a前面
```
         

>栈是一种遵从后进先出(LIFO)原则的有序集合。新添加的或待删除的元素都保存在栈的 末尾，称作栈顶，另一端就叫栈底。在栈里，新元素都靠近栈顶，旧元素都接近栈底。
```js
function Stack() {
    var items = [];
    this.push = function(element){
        items.push(element);
    };
    this.pop = function(){
        return items.pop();
    };
    this.peek = function(){
        return items[items.length-1];
    };
    this.isEmpty = function(){
        return items.length == 0;
    };
    this.size = function(){
        return items.length;
    };
    this.clear = function(){
        items = [];
    };
    this.print = function(){
        console.log(items.toString());
    }
}
```
        
>要把十进制转化成二进制，我们可以将该十进制数字和2整除(二进制是满二进一)，直到结 果是0为止。举个例子，把十进制的数字10转化成二进制的数字，过程大概是这样:
```js
function divideBy2(decNumber){
    var remStack = new Stack(),
        rem,
        binaryString = '';
    while (decNumber > 0){ 
        rem = Math.floor(decNumber % 2);
        remStack.push(rem); 
        decNumber = Math.floor(decNumber / 2); 
    }
    while (!remStack.isEmpty()){ 
        binaryString += remStack.pop().toString();
    }
    return binaryString;
}
console.log(divideBy2(10));  //1010
console.log(divideBy2(100));  //1100100
```

```js
//把数字转成任何进制
function baseConverter(decNumber,baseNumber){
    var remStack = new Stack(),
    rem,
    baseDtring="",
    digits="0123456789ABCDEF";
    while(decNumber>0){
        rem = Math.floor(decNumber%baseNumber);
        remStack.push(rem);
        decNumber = Math.floor(decNumber/baseNumber);
    }
    while(!remStack.isEmpty()){
        baseDtring += digits[remStack.pop()]
    }
    return baseDtring;
}
console.log(baseConverter(100,2));  //1100100
```  
        