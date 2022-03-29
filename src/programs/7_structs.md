# 结构体

**struct，或者 structure，是一个自定义数据类型，允许你包装和命名多个相关的值，从而形成一个有意义的组合。**

1. 结构体需要命名各部分数据以便能清楚的表明其值的意义。
2. 不需要依赖顺序来指定或访问实例中的值。
3. 实例中字段的顺序不需要和它们在结构体中声明的顺序一致。
4. 从结构体中获取某个特定的值，可以使用点号；如果结构体的实例是可变的，我们可以使用点号并为对应的字段赋值。【赋值时，注意整个实例必须是可变的，Rust 不允许只将某个字段标记为可变】
5. 结构体可以使用 **字段初始化简写语法**
6. 可以通过 **结构体更新语法**（struct update syntax）实现。使用旧实例的大部分值但改变其部分值来创建一个新的结构体实例.

```rust
// 定义结构体
struct User {
    active: bool,   // 定义字段名 和 类型 
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    
    // 实例化结构体
    // 实例中字段的顺序不需要和它们在结构体中声明的顺序一致。
    let mut user1 = User { // 注意整个实例必须是可变的；Rust 并不允许只将某个字段标记为可变。
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    // 如果结构体的实例是可变的，我们可以使用点号并为对应的字段赋值。
    user1.email = String::from("anotheremail@example.com");
}
```

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    //  字段初始化简写语法
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}

fn main() {
    let user1 = build_user(
        String::from("someone@example.com"),
        String::from("someusername123"),
    );
}

```

## 从其他实例创建实例

```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    // --snip--

    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    // 使用旧实例的大部分值但改变其部分值来创建一个新的结构体实例
    let user2 = User {
        active: user1.active,
        username: user1.username,
        email: String::from("another@example.com"),
        sign_in_count: user1.sign_in_count,
    };

    // .. 语法指定了剩余未显式设置值的字段应有与给定实例对应字段相同的值。
    let user3 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```

## 使用未命名字段的元组结构体来创建不同的类型

可以定义与元组类似的结构体，称为 **元组结构体**（tuple structs）。元组结构体有着结构体名称提供的含义，但没有具体的字段名，只有字段的类型。

```rust
struct Color(i32, i32, i32);  // 元组结构体
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

## 没有任何字段的类单元结构体

可以定义一个没有任何字段的结构体！它们被称为 **类单元结构体**（unit-like structs）因为它们类似于 `()`，即 `unit` 类型。类单元结构体常常在你想要在某个类型上实现 `trait` 但不需要在类型中存储数据的时候发挥作用。

```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```
