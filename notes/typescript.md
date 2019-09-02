# typescript 使用

## `declare`:声明

### 作用

-   全局环境声明

    自定义的

    ```typescript
    //global.d.td
    declare const jquery1: any;

    //otherflie.ts
    jquery1("#idName");
    ```

    已有框架

    ```shell
    npm install @type/jquery --save-dev
    ```

    在 `tsconfig.josn` 配置(可选，配置的话：只有配置才能被调用，就算安装了也不会生效)

    ```json
    {
        "compilerOptions": {
            "types": ["jquery"]
        }
    }
    ```


    ```typescript
    // otherfile.ts
    juQery("#idName")
    ```

## `reference` 代码的引入

-   使用`namespace`设置命名空间,使用 export 将内容导出

    ```typescript
    // animal.ts
    namespace animal {
        export class Dog {
            run(): void {
                console.log("run");
            }
            say(): void {
                console.log("say");
            }
        }
    }

    //look.ts
    <reference path="animal.ts" />;
    const dog: animal.Dog = new animal.Dog();
    ```

## `interface`：接口，是类的实现描述

### 使用

-   `implements`:表示对接口实现

    ```typescript
    interface Animal {
        run(): void;
        say(): void;
    }
    class Dog implements Animal {
        run() {
            console.log("run");
        }
        say() {
            console.log("wong wong!");
        }
    }
    ```

-   一个类可是是多个接口的实现

    ```typescript
    interface Animal {
        run(): void;
        say(): void;
    }
    interface Live {
        eat(): void;
    }
    class Dog implements Animal, Live {
        run() {
            console.log("run");
        }
        say() {
            console.log("wong wong!");
        }
        eat() {
            console.log("eat");
        }
    }
    ```

-   接口也可以继承

    ```typescript
    interface Live {
        eat(): void;
    }
    interface Animal extends Live {
        run(): void;
        say(): void;
    }
    ```

-   接口也可以继承类

    ```typescript
    class Live{
        eat(){
            console.log("eat")
        }:
    }

    interface Animal extends Live {
        run(): void;
        say(): void;
    }
    ```

### 作用

-   类的实现

    ```typescript
    interface Animal {
        run(): void;
        say(): void;
    }

    class Dog implements Animal {}
    ```

-   注释函数

    ```typescript
    interface SearchFunc {
        (query: string): string;
    }

    const search: SearchFunc = query => {
        return "resData";
    };

    interface SearchFunc {
        (query: string): string;
        (query: number): number;
    }
    ```

    函数重载

    ```typescript
    interface SearchFunc {
        (query: string): string;
        (query: number): number;
    }

    function searchFun(query: any): any {
        if (typeof query === "number") {
            return query + 1;
        } else if (typeof query === "string") {
            return "sdfsdfsfd";
        }
    }
    const search: SearchFunc = searchFun;
    ```

-   注释对象

    ```typescript
    interface Dog {
        color: "yellow" | "white" | "black";
        say(): void;
        run(): void;
    }

    const whiteDog: Dog = {
        color: "white",
        say() {},
        run() {}
    };
    ```

    构造函数

    ```typescript
    interface Dog {
        new (): Dog;
        color: "yellow" | "white" | "black";
        say(): void;
        run(): void;
    }
    ```

## `in` 和 `is` 类型保护

-   检查熟悉是否存在

    ```typescript
    type a = {
        x:namber
    }
    type b = {
        y:string
    }

    function aa(opt:a|b){
        if(“x” in opt ){
            //do something
        }else{
            //do something
        }
    }
    ```

-   自定义类型保护

    ```typescript
    type a = {
        say();
    };
    type b = {
        run();
    };

    function isA(arg: a | b): arg is a {
        return (arg as a)["say"] !== undefined;
    }

    function aa(opt: a | b) {
        if (isA(opt)) {
            // do something
            opt.say();
        } else {
            opt.run();
        }
    }
    ```

## `readonly`:将标记对象设置为只读

    ```typescript
    function readConfig(config:{readonly name:string, readonly age:number}):string{
        return config.name
    }

    type Dog{
        readonly run():void;
        readonly say():void;
    }

    class People{
        readonly name="xiaoming" //ok
        readonly age:string
        constructor(){
            this.age = "12" //ok
            this.name = "xiaozhang" //error
        }
    }

    ```

## 类型的重用

-   `typof`

    获取变量的类型

    ```typescript
    class Dog {
        run() {}
    }

    const dog = new Dog();

    let white: typeof dog;

    const foo = "Hello World";
    let bar: typeof foo;

    const colors = {
        red: "red",
        blue: "blue"
    };

    //获取键的名称
    type Color = keyof typeof cat;
    let color: Color;

    color = "red"; //ok
    color = "yellow"; //error
    ```
## `enum`   枚举


## 内置类型

```

```
