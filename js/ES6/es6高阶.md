## ES6高阶

##知识点

- defineProperty；
- Proxy代理
- 数据劫持
- es6模块化、exports 和 import
- AMD /CMD模块化；



### defineProperty

```js
Object.defineProperty(obj,'name',{
        get(){
            return value;
        },
        set(newValue){
            console.log("set...");
            value = newValue;
        }
    })
```



### proxy

- 定义  ：对象用于定义基本操作的自定义行为（如属性查找，赋值，枚举，函数调用等）。

- 基本使用

  ```js
  let obj = new Proxy({
                      name: "张三",
                      age: 20
                },{
                      get(target, name) {
                          return target[name];
                      },
                      set(target,name,value){
                          target[name] = value;
                      }
                 })
  ```

- 相关配置参数

  ```
  has(target, propKey)：拦截propKey in proxy的操作，返回一个布尔值。
  defineProperty(target, propKey, propDesc)：拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。
  ```

  

## es6模块化

- 浏览器默认模块化  script 里加入  "type=module"；

- 导出  关键字  export

  - 导出 方式一  ：

    ```js
    export { a ,b , c}
    ```

  - 导出方式二 关键字  "as"

    ```js
    export { a as aa ,b , c}
    ```

  - 导出方式三

    ```js
    export let c = ()=>{console.log("I am c function...")}
    ```

  - 导出方式四

    ```js
    export default a;
    ```

    - 等同

      ```js
      export {a as default};
      ```

  - 

  export  可以导出多个，export default  只能导出一个；

- 导入方式：关键字 import

  - export导出的,命名要保持一致

    ```js
    import {aa , b , c} from './moduleb.js';
    ```

  - export导出的，命名可以自定义；

    ```js
    import myfn from './moduleb.js';
    ```

  - 通配符 "*"方式导入

    ```js
    import * as obj from './moduleb.js';
    ```



###AMD require.js



- require.js使用

  - 引入require.js

    ```js
    https://cdn.bootcss.com/require.js/2.3.6/require.js
    ```

  - 1.加载模块

    ```js
    require(["a"]);
    ```

  - 2.定义模块

    - 无依赖定义

    ```js
    define({
        method1:function(){
            console.log("a method...");
        },
        method2:function(){
            console.log("b method...");
        }
    });
    ```

    - 模块有依赖

      ```js
      define(["c"],{
          method1:function(){
              console.log("a method...");
          },
          method2:function(){
              console.log("b method...");
          }
      });
      ```

    - 函数式写法

      ```js
      define(["c"],function(){
          obj = {
              name:"张安",
              age:20
          }
          return obj;
      });
      ```


### 模块化优点

- 防止作用域污染 
- 提高代码的复用性
- 维护成本降低
