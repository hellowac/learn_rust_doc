- [变量与可变性](#变量与可变性)
  - [不可变变量](#不可变变量)
  - [可变变量](#可变变量)
  - [常量](#常量)
  - [隐藏（Shadowing）](#隐藏shadowing)
  - [隐藏版本2](#隐藏版本2)

# 变量与可变性

## 不可变变量

1. 变量默认是不可改变的
2. 默认 let 声明的变量为不可变的。

```rust
fn main() {
    let x = 5; // 声明变量，默认不可变
    println!("The value of x is: {}", x);
    x = 6; // 因为 x 是不可变变量，所以此处会报错
    println!("The value of x is: {}", x);
}
```

## 可变变量

1. 使用 mut 关键字声明为可变的。

```rust
fn main() {
    let mut x = 5; // 使用 mut 声明可变变量
    println!("The value of x is: {}", x);
    x = 6; // 因为x是可变变量，所以不会报错。
    println!("The value of x is: {}", x);
}
```

## 常量

1. 使用 const 关键字声明常量。
2. 不允许对常量 使用 mut。
3. 常量可以在任何作用域中声明，包括全局作用域。
4. 常量只能被设置为常量表达式，而不能是只能在运行时计算出的值。

```rust

fn main() {
    const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
}

```

## 隐藏（Shadowing）

1. 可以定义一个与之前变量同名的新变量。

```rust
fn main() {
    let x = 5;  // 第一次声明的变量 x

    let x = x + 1;  // 第二次声明，隐藏第第一个声明的变量 x

    {
        let x = x * 2;  // 第三次声明在本作用域内隐藏第二次声明的变量x
        println!("The value of x in the inner scope is: {}", x);
    }

    println!("The value of x is: {}", x);  // 使用第二次声明的变量 x
}
```

## 隐藏版本2

1. 使用 let 时，实际上创建了一个新变量，我们可以 **改变值的类型**，并且复用这个名字。

```rust
fn main() {
    let spaces = "   ";  // string类型
    let spaces = spaces.len();  // 隐藏并更改为 u32 类型
}
```

对于 使用 mut 的可变变量， 隐藏上一个变量时，不可改变类型

```rust
fn main() {
    let mut spaces = "   "; // 可变的，string类型变量
    spaces = spaces.len(); // 转化为u32类型，会报错。
}
```
