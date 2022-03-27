- [控制流](#控制流)
  - [if 表达式](#if-表达式)
  - [使用 else if 处理多重条件](#使用-else-if-处理多重条件)
  - [在 let 语句中使用 if](#在-let-语句中使用-if)
  - [使用循环重复执行](#使用循环重复执行)
    - [loop 循环](#loop-循环)
    - [从循环返回值](#从循环返回值)
    - [while 条件循环](#while-条件循环)
    - [for 循环](#for-循环)

# 控制流

根据条件是否为真来决定是否执行某些代码，以及根据条件是否为真来重复运行一段代码的能力是大部分编程语言的基本组成部分。

## if 表达式

if 表达式允许根据条件执行不同的代码分支。

```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```

代码中的条件 **必须** 是 `bool` 值。如果条件不是 `bool` 值，我们将得到一个错误。

```rust
fn main() {
    let number = 3;

    if number {  // 必须是bool 值， 这里会报错。
        println!("number was three");
    }
}
```

不像 `Ruby` 或 `JavaScript` 这样的语言，Rust 并 **不会尝试自动地将非布尔值转换为布尔值**。 必须总是显式地使用布尔值作为 `if` 的条件。

## 使用 else if 处理多重条件

```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

只会执行第一个条件为真的代码块，并且一旦它找到一个以后，甚至都不会检查剩下的条件了。

## 在 let 语句中使用 if

因为 `if` 是一个表达式，我们可以在 `let` 语句的右侧使用它

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };  // 代码块的值是其最后一个表达式的值，而数字本身就是一个表达式

    println!("The value of number is: {}", number);
}
```

```rust
fn main() {
    let condition = true;

    let number = if condition { 5 } else { "six" };  // 如果它们的类型不匹配，则会出现一个错误：

    println!("The value of number is: {}", number);
}
```

`if` 代码块中的表达式返回一个整数，而 `else` 代码块中的表达式返回一个字符串。这不可行，因为变量必须只有一个类型。Rust 需要在编译时就确切的知道 `number` 变量的类型，这样它就可以在编译时验证在每处使用的 `number` 变量的类型是有效的。如果`number`的类型仅在运行时确定，则 `Rust` 无法做到这一点；且编译器必须跟踪每一个变量的多种假设类型，那么它就会变得更加复杂，对代码的保证也会减少。

## 使用循环重复执行

Rust 有三种循环：`loop`、`while` 和 `for`。

### loop 循环

`loop` 关键字告诉 Rust 一遍又一遍地执行一段代码直到你明确要求停止。

```rust
fn main() {
    loop {
        println!("again!");
    }
}
```

1. `break` 关键字来告诉程序何时停止循环.
2. `continue` 关键字告诉程序跳过这个循环迭代中的任何剩余代码，并转到下一个迭代。

如果存在嵌套循环，`break` 和 `continue` 应用于此时最内层的循环。你可以选择在一个循环上指定一个 **循环标签**（loop label），然后将标签与 `break` 或 `continue` 一起使用，使这些关键字应用于已标记的循环而不是最内层的循环。

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {  // 定义一个循环标签
        println!("count = {}", count);
        let mut remaining = 10;

        loop {
            println!("remaining = {}", remaining);
            if remaining == 9 {
                break;  // 退出内层循环
            }
            if count == 2 {
                break 'counting_up;  // 退出 循环标签 处的外层循环
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {}", count);
}

```

### 从循环返回值

将返回值加入你用来停止循环的 break 表达式，它会被停止的循环返回.

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;  // 会结束循环并将 结果 返回。
        }
    };

    println!("The result is {}", result);
}

```

### while 条件循环

当条件为真就执行，否则退出循环。

这种结构消除了很多使用 `loop`、`if`、`else` 和 `break` 时所必须的嵌套，这样更加清晰。

```rust
fn main() {
    let mut number = 3;

    while number != 0 { // 当条件不为 真 时，则退出。
        println!("{}!", number);

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

### for 循环

使用 `for` 循环来对一个 **集合** 的每个元素执行一些代码。

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {}", element);
    }
}
```

使用 `for` 循环来倒计时的例子，它还使用了一个方法，`rev`，用来反转 `range`:

```rust
fn main() {
    for number in (1..4).rev() {
        println!("{}!", number);
    }
    println!("LIFTOFF!!!");
}
```
