# 解构方法语法

**方法**（method）与函数类似：它们使用 `fn` 关键字和名称声明，可以拥有参数和返回值，同时包含在某处调用该方法时会执行的代码。不过方法与函数是不同的，因为它们在结构体的上下文中被定义（或者是枚举或 trait 对象的上下文），并且它们第一个参数总是 `self`，它代表调用该方法的结构体实例。

## 定义方法

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

// impl 是 implementation 的缩写
impl Rectangle {
    // 定义方法
    // self 代表结构体实例本身
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}

```

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // 我们可以在 Rectangle 上定义一个方法，并命名为 width：
    fn width(&self) -> bool {
        self.width > 0
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    // 在 main 中，
    // 当我们在 rect1.width 后面加上括号时。Rust 知道我们指的是方法 width。
    // 当我们不使用圆括号时，Rust 知道我们指的是字段 width。
    if rect1.width() {
        println!("The rectangle has a nonzero width; it is {}", rect1.width);
    }
}
```

## 带有更多参数的方法

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

// 所有在 impl 块中定义的函数被称为 关联函数（associated functions），
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}

```

## 关联函数

所有在 `impl` 块中定义的函数被称为 **关联函数**（associated functions），因为它们与 `impl` 后面命名的类型相关。

我们可以定义不以 `self` 为第一参数的关联函数（因此不是方法），因为它们并不作用于一个结构体的实例。

在 `String` 类型上定义的 `String::from` 函数 就是这样的一个关联函数

**不是方法的关联函数经常被用作返回一个结构体新实例的构造函数**:

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    // 非方法的关联函数
    fn square(size: u32) -> Rectangle {
        Rectangle {
            width: size,
            height: size,
        }
    }
}

fn main() {
    let sq = Rectangle::square(3);
}
```

## 多个 impl 块

每个结构体都允许拥有多个 impl 块。

```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

// impl 块1
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

// impl 块2
impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```
