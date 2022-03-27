- [函数](#函数)
  - [参数](#参数)
  - [语句和表达式 【函数体】](#语句和表达式-函数体)
  - [具有返回值的函数](#具有返回值的函数)

# 函数

1. `main` 函数，它是很多程序的入口点。
2. `fn` 关键字，它用来声明新函数。
3. `Rust` 代码中的函数和变量名使用 `snake case` 规范风格。所有字母都是小写并使用下划线分隔单词。
4. Rust 不关心函数定义于何处，在使用函数之前或之后，只要定义了就行

```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```

## 参数

1. 可以定义为拥有 参数（parameters）的函数，参数是特殊变量，是函数签名的一部分。
2. 在函数签名中，**必须** 声明每个参数的类型。【要求在函数定义中提供类型注解，意味着编译器再也不需要你在代码的其他地方注明类型来指出你的意图。】
3. 当定义多个参数时，使用逗号分隔。

```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {  // 参数时函数签名的一部分
    println!("The value of x is: {}", x);
}
```

```rust
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {  // 必须声明每个参数的类型
    println!("The measurement is: {}{}", value, unit_label);
}
```

## 语句和表达式 【函数体】

函数体由一系列的语句和一个可选的结尾表达式构成。

- **语句**（Statements）是执行一些操作但不返回值的指令。
- **表达式**（Expressions）计算并产生一个值。

 Rust 是一门基于 **表达式**（expression-based）的语言。 重点参考：<https://kaisery.github.io/trpl-zh-cn/ch03-03-how-functions-work.html#%E8%AF%AD%E5%8F%A5%E5%92%8C%E8%A1%A8%E8%BE%BE%E5%BC%8F>

```rust
fn main() {
    let y = 6;  // 这是一个语句，不返回值
}
```

```rust
fn main() {
    let x = (let y = 6);  // let y = 6 是一个语句，不返回值，所以将其结果赋值给 x 产生错误。
}
```

```rust
fn main() {
    // 用大括号创建的一个新的块作用域也是一个表达式
    let y = {
        let x = 3;
        x + 1  // 当结尾有 分号 “;” 时就表示是一个语句，而语句不会返回值，所以这里 表示 x + 1 为表达式，会作为这块作用域的返回值
    };

    println!("The value of y is: {}", y);
}
```

## 具有返回值的函数

函数可以向调用它的代码返回值。在函数括号后面使用箭头（->）并在剪头后声明它的类型。

在 Rust 中，函数的返回值等同于函数体最后一个表达式的值。

使用 `return` 关键字和指定值，可从函数中提前返回；但 **大部分函数隐式的返回最后的表达式** 。

```rust
fn five() -> i32 {  // 这里声明了返回值的类型。
    5  // 最后的表达式作为返回值，即便只是一个数字
}

fn main() {
    let x = five();

    println!("The value of x is: {}", x);
}
```

```rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {}", x);
}

fn plus_one(x: i32) -> i32 {  // 同时声明参数类型和返回值类型
    x + 1 // 最后表达式作为返回值 ， 如果此处加上分号“;”则会变成语句，则编译会报错。
}
```
