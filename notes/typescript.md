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

## `enum` 枚举

## `namespace` 命名空间

    多个文件的`namespace`相同的话，内部使用，可以像一个页面一样，但是需要引入依赖文件

    ```typescript
    //a.ts
    namespace Validation{
        export interface StringValidator{
            isAcceptable(s:string):boolean
        }
    }


    //b.ts
    /// <reference path="a.ts" />
    namespace Validation{
        export class NumberValiadtor implements StringValidator{
            isAcceptable(s:string):boolean
        }
    }

    ```

## keyof 

遍历


## 内置类型
### Partial
遍历属性置为可选
```typescript
interface AccountInfo{
    name: string 
    email: string 
    age: number 
    vip: 0|1 // 1 是vip ，0 是非vip
}

// 只需部分属性
const xiaoming :Partial<AccountInfo> = {
    name:"xiaoming",
    age:12
}

```
### Require
遍历属性置为必选

### Readonly
遍历属性置为可读

### Record<T,K>
将T（单个或者多个属性）遍历生成 统一一个类 K

```typescript
type Persion = Record<"name"|"age",string> 
// 相当于 
type Persion1 = {
    name:string;
    age:string;
}

```


### Pick<T, K>
在T类型中选择你的K属性（K必须是T里面的属性之一）
```typescript
interface AccountInfo{
    name: string 
    email: string 
    age: number 
    vip: 0|1 // 1 是vip ，0 是非vip
}

const xiaoming:Pick<AccountInfo,"name"|"age">={
    name:"xiaoming",
    age:12
}

```

### Exclude<T,K>
判断T是不是K的子集，是：返回never,否：T
```typescript
interface AccountInfo{
    name: string 
    email: string 
    age: number 
    vip: 0|1 // 1 是vip ，0 是非vip
}

const xiaoming :Exclude<AccountInfo，"vip"|"email">={
    name:"xiaoming",
    age:12
}

```


