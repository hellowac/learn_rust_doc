# 示例程序

## 版本1 调用函数

获取以像素为单位的长方形的宽度和高度，并计算出长方形的面积。

```rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(width: u32, height: u32) -> u32 {
    width * height
}
```

## 版本2 使用元组重构

```rust
fn main() {
    let rect1 = (30, 50);

    println!(
        "The area of the rectangle is {} square pixels.",
        area(rect1)
    );
}

// 元组并没有给出元素的名称，所以计算变得更费解了，因为不得不使用索引来获取元组的每一部分：
fn area(dimensions: (u32, u32)) -> u32 {
    dimensions.0 * dimensions.1
}
```

## 使用结构体重构

使用结构体为数据命名来为其赋予意义。

```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

// 明宽高是相互联系的，并为这些值提供了描述性的名称而不是使用元组的索引值 0 和 1 。结构体胜在更清晰明了。
fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```

## 通过派生 trait 增加实用功能

```rust
// 加上外部属性, 使其可以打印
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {}", rect1);
}
```

输出如下：

```shell
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished dev [unoptimized + debuginfo] target(s) in 0.48s
     Running `target/debug/rectangles`
rect1 is Rectangle {
    width: 30,
    height: 50,
}
```

## 使用 Debug 格式打印数值

另一种使用 Debug 格式打印数值的方法是使用 `dbg!` 宏。`dbg!` 宏接收一个表达式的所有权，打印出代码中调用 `dbg!` 宏时所在的文件和行号，以及该表达式的结果值，并返回该值的所有权。

> 注意：调用 `dbg!` 宏会打印到标准错误控制台流（stderr），与 println! 不同，后者会打印到标准输出控制台流（stdout）。

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```

输出如下：

```shell
$ cargo run
   Compiling rectangles v0.1.0 (file:///projects/rectangles)
    Finished dev [unoptimized + debuginfo] target(s) in 0.61s
     Running `target/debug/rectangles`
[src/main.rs:10] 30 * scale = 60
[src/main.rs:14] &rect1 = Rectangle {
    width: 60,
    height: 50,
}
```
