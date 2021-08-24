---
title: JS：原型、原型链继承
date: 2019-10-15 19:39:17
tags: javascript
category: 技术
---

<meta name="referrer" content="no-referrer"/>

<!--more-->

## 一、构造函数

**构造函数模式的目的就是为了创建一个自定义类，并且创建这个类的实例。构造函数模式中拥有了类和实例的概念，并且实例和实例之间是相互独立的，即实例识别。**


构造函数就是一个普通的函数，创建方式和普通函数没有区别，**不同的是构造函数习惯上首字母大写**。另外就是调用方式的不同，普通函数是直接调用，**而构造函数需要使用 new 关键字来调用**。

```
    function Person(name, age, gender) {
        this.name = name
        this.age = age
        this.gender = gender
        this.sayName = function () {
            alert(this.name);
        }
    }
    var per = new Person("孙悟空", 18, "男");
    function Dog(name, age, gender) {
        this.name = name
        this.age = age
        this.gender = gender
    }
    var dog = new Dog("旺财", 4, "雄")
    console.log(per);//当我们直接在页面中打印一个对象时，事件上是输出的对象的toString()方法的返回值
    console.log(dog);
```

![](https://upload-images.jianshu.io/upload_images/3174701-1a20d86bf6856c95?imageMogr2/auto-orient/strip|imageView2/2/w/587/format/webp)

每创建一个 c`Person 构造函数，在 Person 构造函数中，为每一个对象都添加了一个 sayName 方法，也就是说构造函数每执行一次就会创建一个新的 sayName 方法。这样就导致了构造函数执行一次就会创建一个新的方法，执行 10000 次就会创建 10000 个新的方法，而 10000 个方法都是一摸一样的，为什么不把这个方法单独放到一个地方，并让所有的实例都可以访问到呢?这就需要原型(`prototype`)

## 二、原型

**在 JavaScript 中，每当定义一个函数数据类型(普通函数、类)时候，都会天生自带一个 prototype 属性，这个属性指向函数的原型对象，并且这个属性是一个对象数据类型的值。**

让我们用一张图表示构造函数和实例原型之间的关系：

![](http://upload-images.jianshu.io/upload_images/3174701-2dd95188a8f6b19e?imageMogr2/auto-orient/strip|imageView2/2/w/467/format/webp)

原型对象就相当于一个公共的区域，所有同一个类的实例都可以访问到这个原型对象，我们可以将对象中共有的内容，统一设置到原型对象中。

## 三、原型链

### 1.`__proto__`和`constructor`

**每一个对象数据类型(普通的对象、实例、prototype......)也天生自带一个属性**proto**，属性值是当前实例所属类的原型(prototype)。原型对象中有一个属性 constructor, 它指向函数对象。**

```
    function Person() {}
    var person = new Person()
    console.log(person.__proto__ === Person.prototype)//true
    console.log(Person.prototype.constructor===Person)//true
    //顺便学习一个ES5的方法,可以获得对象的原型
    console.log(Object.getPrototypeOf(person) === Person.prototype) // true

```

![](http://upload-images.jianshu.io/upload_images/3174701-9a3de0b501161c07?imageMogr2/auto-orient/strip|imageView2/2/w/530/format/webp)

### 2.何为原型链

**在 JavaScript 中万物都是对象，对象和对象之间也有关系，并不是孤立存在的。对象之间的继承关系，在 JavaScript 中是通过 prototype 对象指向父类对象，直到指向 Object 对象为止，这样就形成了一个原型指向的链条，专业术语称之为原型链**。

举例说明:person → Person → Object ，普通人继承人类，人类继承对象类

**当我们访问对象的一个属性或方法时，它会先在对象自身中寻找，如果有则直接使用，如果没有则会去原型对象中寻找，如果找到则直接使用。如果没有则去原型的原型中寻找,直到找到 Object 对象的原型，Object 对象的原型没有原型，如果在 Object 原型中依然没有找到，则返回 undefined。**

我们可以使用对象的`hasOwnProperty()`来检查对象自身中是否含有该属性；使用`in`检查对象中是否含有某个属性时，如果对象中没有但是原型中有，也会返回 true

```
    function Person() {}
    Person.prototype.a = 123;
    Person.prototype.sayHello = function () {
      alert("hello");
    };
    var person = new Person()
    console.log(person.a)//123
    console.log(person.hasOwnProperty('a'));//false
    console.log('a'in person)//true

```

person 实例中没有 a 这个属性，从 person 对象中找不到 a 属性就会从 person 的原型也就是 `person.__proto__` ，也就是 Person.prototype 中查找，很幸运地得到 a 的值为 123。那假如 `person.__proto__`中也没有该属性，又该如何查找？

当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层 Object 为止。**Object 是 JS 中所有对象数据类型的基类(最顶层的类)在 Object.prototype 上没有**proto**这个属性。**

```
console.log(Object.prototype.__proto__ === null) // true

```

![img](http://upload-images.jianshu.io/upload_images/3174701-18a76d28c0a9ea1b?imageMogr2/auto-orient/strip|imageView2/2/w/521/format/webp)

## 四、原型链继承

### 1、原型链继承

子类的原型是父类原型的一个实例对象。

```
function Person(name, age){

}

function Student(name, age, sex){

}
Student.prototype = new Person();
```

### 2、借用构造函数

在子类的构造函数中使用 call()调用父类的构造函数。

```
function Person(name, age){

}
function Student(name, age, sex){
    Person.call(this, name, age);
}

```

### 3、原型链继承+借用构造函数=组合继承

通过在子类的构造函数中调用父类型的构造函数，保留传参的优点，此外通过将父类的实例对象作为子类的原型，满足函数复用。

```
function Person(name, age){

}
function Student(name, age, sex){
    Person.call(this, name, age);
}
Student.prototype = new Person();
Student.prototype.constructor = Student();
```

### 4、组合继承优化 1

子类的构造函数中调用父类的构造函数，子类的原型和父类的原型指向同一对象。

```
function Person(name, age){

}
function Student(name, age, sex){
    Person.call(this, name, age);
}
Student.prototype = Person.prototype;
```

### 5、组合继承优化 2

子类的构造函数中调用父类的构造函数，使用 var B = Object.create(A)，以 A 为对象为原型生成 B。这样 B 就继承了 A 的所有属性和方法。

```
function Person(name, age){

}
function Student(name, age, sex){
    Person.call(this, name, age);
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;
```

### 6：ES6 中 class 继承

```
class Person{
    constructor(name, age){

    }
}
class Student extends Person{
    constructor(name, age, sex){
        super(name, age);
    }
}
```

[JavaScript 常见的六种继承方式](https://juejin.im/post/5bb091a7e51d450e8477d9ba)
