
## javascript 闭包

    官方定义：JavaScript语言采用词法作用域，也就是说函数执行时所依赖的变量是在函数定义时决定的，而非运行时。为了实现词法作用域，JavaScript函数对象内部状态除了包含函数的代码逻辑，还必须包含当前作用域链的引用。函数对象通过作用域链关联起来，函数体内部的所有变量都可以保存在作用域内，这种特性称之为闭包；
    简单来讲，闭包是一个能够访问其他函数内部变量的函数。
### 相关概念  

作用域链：   

词法作用域：指变量的作用域在词法解析的时候确定的，不会改变.  

**eg**
```javascript
const foo = 1;
function static(){
  alert(foo);
  alert(foo2)
}
function test(){
  const foo = 2;
  const foo2 = 3;
  static();
}
test();  //alert(1); foo2 undefined;
```  

foo是一个全局变量，test函数中的foo，foo2作用域仅在test函数内，static函数执行时，从作用域链中查找foo变量（先从函数内部找是否定义了foo变量，有则直接返回，没有则从上一级中查找，在上级中找到foo，则直接返回），值为1；二foo2static函数的作用域链中找不到，则报undefined错误。

闭包可以捕获单个函数调用的局部变量，并将其私有化。

## 闭包的用途
1. 模块化代码，避免全局污染  
**eg**
```javascript
  var name = 'hello';
  (function(){
    var name = 'mrs zhang';
    console.log(name);
  })()
```

2. 模拟对象行为，实现封装与继承  

**eg**
```javascript
  var Set = (function(){
    var  data = [];
    
    
    function add(n){
      data.push(n);
    }
    function remove(){
      data.pop();
    }
    function size(){
      return data.length
    }
    
    return {
      add : add,
      remove : remove,
      size : size
    }
  })()
  
  var set = new Set();
  set.add(1);
```

3. 私有化变量  
  **eg**
  ```javascript
    for(var i = 0; i<domList.length; i++){
      domList[i].onClick = function(){
        function click(){
          var index = i;
          alert(index);
          return index;
        }
        return click
      }
    }
  ```
  




