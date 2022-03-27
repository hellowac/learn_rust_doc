- [数据类型](#数据类型)
  - [标量类型](#标量类型)
    - [整型](#整型)
    - [浮点型](#浮点型)
    - [数值运算](#数值运算)
    - [布尔型](#布尔型)
    - [字符类型](#字符类型)
  - [复合类型](#复合类型)
    - [元组类型](#元组类型)
    - [数组类型](#数组类型)

# 数据类型

Rust 是 **静态类型**（statically typed）语言，也就是说在编译时就必须知道所有变量的类型。

根据值及其使用方式，编译器通常可以推断出我们想要用的类型。当多种类型均有可能时，必须增加类型注解，例如：

```rust
fn main() {
    let guess: u32 = "42".parse().expect("Not a number!");  // 注解guess的值为 u32 的类型。
}
```

## 标量类型

标量（scalar）类型代表一个单独的值。Rust 有四种基本的标量类型：整型、浮点型、布尔类型和字符类型。

### 整型

整数 是一个没有小数部分的数字。

**Rust 中的整型**:

| 长度    | 有符号 | 无符号 |
| ------- | ------ | ------ |
| 8-bit   | i8     | u8     |
| 16-bit  | i16    | u16    |
| 32-bit  | i32    | u32    |
| 64-bit  | i64    | u64    |
| 128-bit | i128   | u128   |
| arch    | isize  | usize  |

`isize` 和 `usize` 类型依赖运行程序的计算机架构：64 位架构上它们是 64 位的， 32 位架构上它们是 32 位的。

**Rust 中的整型字面值**:

| 数字字面值                  | 例子        |
| --------------------------- | ----------- |
| Decimal (十进制)            | `98_222`      |
| Hex (十六进制)              | `0xff`        |
| Octal (八进制)              | `0o77`        |
| Binary (二进制)             | `0b1111_0000` |
| Byte (单字节字符)(仅限于u8) | `b'A'`        |

1. 允许使用 `_` 做为分隔符以方便读数，例如`1_000`，它的值与你指定的 `1000` 相同。
2. 数字类型默认是 `i32`。
3. `isize` 或 `usize` 主要作为某些集合的索引。

### 浮点型

1. 浮点数类型是 `f32` 和 `f64`，分别占 `32` 位和 `64` 位。
2. 默认类型是 `f64`，因为在现代 CPU 中，它与 `f32` 速度几乎一样，不过精度更高。
3. 所有的浮点型都是有符号的。

```rust
fn main() {
    let x = 2.0; // f64

    let y: f32 = 3.0; // f32
}
```

1. 浮点数采用 `IEEE-754` 标准表示。
2. `f32` 是单精度浮点数，`f64` 是双精度浮点数。

### 数值运算

1. 支持基本数学运算：加法、减法、乘法、除法和取余。
2. 整数除法会向下舍入到最接近的整数。

```rust
fn main() {
    // 加法
    let sum = 5 + 10;

    // 减法
    let difference = 95.5 - 4.3;

    // 乘法
    let product = 4 * 30;

    // 除法
    let quotient = 56.7 / 32.2;  //  浮点数相除
    let floored = 2 / 3; // 结果为 0， 向下舍入。

    // 取余
    let remainder = 43 % 5;
}
```

### 布尔型

1. 布尔类型使用 `bool` 表示。
2. 有两个可能的值：`true` 和 `false`。

```rust
fn main() {
    let t = true;

    let f: bool = false; // 显式指定类型注解
}
```

### 字符类型

1. `char` 类型是语言中最原生的字母类型.

```rust
fn main() {
    let c = 'z';
    let z = 'ℤ';
    let heart_eyed_cat = '😻';
}
```

1. 用单引号声明 `char` 字面量，使用双引号声明字符串字面量。
2. `char` 类型的大小为四个字节(four bytes)，并代表了一个 Unicode 标量值（Unicode Scalar Value），这意味着它可以比 ASCII 表示更多内容。
3. 在 Rust 中，拼音字母（Accented letters），中文、日文、韩文等字符，emoji（绘文字）以及零长度的空白字符都是有效的 char 值。
4. Unicode 标量值包含从 U+0000 到 U+D7FF 和 U+E000 到 U+10FFFF 在内的值。不过，“字符” 并不是一个 Unicode 中的概念，所以人直觉上的 “字符” 可能与 Rust 中的 char 并不符合。

## 复合类型

**复合类型**（Compound types）可以将多个值组合成一个类型。

Rust 有两个原生的复合类型：**元组**（tuple）和 **数组**（array）。

### 元组类型

将多个其他类型的值组合进一个复合类型的主要方式。

1. **长度固定**：一旦声明，其长度不会增大或缩小。
2. 使用包含在圆括号中的逗号分隔的值列表来创建一个元组。
3. 元组中的每一个位置都有一个类型，而且这些不同值的类型也不必是相同的。

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

从元组中获取单个值，可以使用模式匹配（pattern matching）来解构（destructure）元组值, 例如：

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;  // 解构

    println!("The value of y is: {}", y);
}
```

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0; // 也可以用 .索引 来访问值

    let six_point_four = x.1; // 也可以用 .索引 来访问值

    let one = x.2;
}

```

没有任何值的元组 `()` 是一种特殊的类型，只有一个值，也写成 `()` 。该类型被称为 **单元类型**（unit type），而该值被称为 **单元值**（unit value）。如果表达式不返回任何其他值，则会隐式返回单元值。

### 数组类型

1. **数组**（array）。与元组不同，数组中的每个元素的类型必须相同。
2. Rust中的数组长度是固定的。
3. 将数组的值写成在方括号内，用逗号分隔.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```

1. 数组在栈（stack）而不是在堆（heap）上为数据分配空间。
2. 数组并不如 vector 类型灵活。【标准库提供的一个 允许 增长和缩小长度的类似数组的集合类型】

```rust
fn main() {
    // 当你确定元素个数不会改变时，数组会更有用。比如12个月份
    let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
}
```

在方括号中包含每个元素的类型，后跟分号，再后跟数组元素的数量 -- 声明数组的方式2

```rust
fn main() {
    let a: [i32; 5] = [1, 2, 3, 4, 5];  // 
}
```

在方括号中指定初始值加分号再加元素个数的方式来创建一个每个元素都为相同值的数组 -- 声明数组的方式3

```rust
fn main() {
    let a = [3; 5]; // 这种写法与 let a = [3, 3, 3, 3, 3]; 效果相同，但更简洁。
}
```

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];  // 索引方式访问数组
    let second = a[1];
}
```

越界访问数组时会产生 `panic` 【这是 Rust 术语，它用于程序因为错误而退出的情况】

```rust
use std::io;

fn main() {
    let a = [1, 2, 3, 4, 5];

    println!("Please enter an array index.");

    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Failed to read line");

    let index: usize = index
        .trim()
        .parse()
        .expect("Index entered was not a number");

    let element = a[index];

    println!(
        "The value of the element at index {} is: {}",
        index, element
    );
}
```

输出如下：

```text
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is 10', src\main.rs:149:19
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
error: process didn't exit successfully: `target\debug\hello-rust.exe` (exit code: 101)
```
