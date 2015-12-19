#JavaScript之闭包与高阶函数

JavaScript虽是一门面向对象的编程语言，但同时也有许多函数式编程的特性，如Lambda表达式，闭包，高阶函数等。

> 函数式编程是种编程范式，它将电脑运算视为函数的计算。函数编程语言最重要的基础是 λ 演算（lambda calculus）。而且λ演算的函数可以接受函数当作输入（参数）和输出（返回值

##闭包

何谓闭包？对于闭包众位各有己见，今我试说之，闭包，常指有权访问其外部作用域中变量和参数的函数。最常见的就是在某函数内部创建另一个函数。如：

```

    var count = (function() {
        var item = 0;
        
        return {
            add: function(num) {
                item += typeof num === 'number' ? num : 1;
            },
            value: function() {
                return item;
            }
        }
    })();
```
*此处把函数返回的结果赋值给count，该函数返回一个包含两个方法的对象，对象中的方法均可访问其包含函数中的变量及参数。count中保存的是该对象的一个引用，对象中的方法依然可以访问自执行函数中的变量，而且访问的是变量本身。*

> 闭包 函数可以访问它创建时所处的上下文环境中的变量以及参数，this以及arguments除外。

闭包其实并不是很好阐述，与我而言，自我理解与向他人阐述差别甚大，但也要试着去征服它。闭包的形成与变量息息相关，尤其是变量的作用以及变量生命周期，请看细说：

###闭包与变量

闭包中所保存的是整个变量对象--执行环境（上下文环境）中的一个表示变量的对象，访问执行环境中变量即是访问该变量对象中的变量。

> 变量对象 每个执行环境（上下文环境）中的一个表示所有变量的对象，全局环境的变量对象始终存在，而局部环境的变量对象只在其执行过程中存在。

典型案例如下：
```

    function myNumber() {
        var count = [];
        for (var i = 0; i < 10; i ++) {
            count[i] = function() {
                return i;
            }
        }
        return count;
    }
```
这个函数会返回一个函数数组，这个数组会不会乖乖返回自己的数字呢？当然不会，事实上，每个函数都返回10。为什么呢？细细道来，因为每个函数的作用域链中都保存着myNumber()函数的活动对象（变量对象），他们都引用同一个变量对象，当然也引用同一个变量i,当myNumber()函数返回后i为10。

再看如下代码：
```

    function myNumber() {
        var count = [];
        for (var i = 0; i < 10; i ++) {
            count[i] = （function(num) {
                return function() {
                    return num;
                };
            })(i);
        }
        return count;
    }
```
在此将自执行匿名函数结果赋值给数组，调用每个匿名函数时，传入变量i，而函数参数是**按值传递**，即将变量值复制给参数num，在此匿名函数内部又创建并返回了一个访问num参数的闭包，count数组中的函数均保存有自己的num变量的副本，于是，便返回各自的值了。


