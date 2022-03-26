# 程序1

## hello-world

```rust
fn main() {
    println!("Hello, world!");
}
```

## 猜数版本1

获取用户输入

```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    // 获取用户输入
    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

## 猜数版本2

生成随机数

```rust
use std::io;
use rand::Rng; // 使用rand包的Rng接口定义

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..101);  // 生成

    println!("The secret number is: {}", secret_number);

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

## 猜数版本3

处理比较输入

```rust
use rand::Rng;
use std::cmp::Ordering;  // 要用到标准包里面的比较接口
use std::io;

fn main() {
    println!("猜数!");

    let secret_number = rand::thread_rng().gen_range(1..101);

    // println!("神秘数字是: {}", secret_number.to_string());

    println!("请输入你猜测的数字:");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("读取数据失败");

    println!("你猜测的数是: {}", guess);

    // 针对字符串进行比较
    match guess.cmp(&secret_number.to_string()){
        Ordering::Less => println!("太小了！"),
        Ordering::Greater => println!("太大了!"),
        Ordering::Equal => println!("你赢了!"),
    }
}
```

## 猜数版本4

转换输入为数字

```rust
use rand::Rng;
use std::cmp::Ordering;  // 要用到标准包里面的比较接口
use std::io;

fn main() {
    println!("猜数!");

    let secret_number = rand::thread_rng().gen_range(1..101);

    // println!("神秘数字是: {}", secret_number.to_string());

    loop {
        println!("请输入你猜测的数字:");

        let mut guess = String::new();

        io::stdin().read_line(& mut guess).expect("不能读取行!");

        let guess: u32 = guess.trim().parse().expect("请输入数字！");

        println!("你输入的是： {}", guess);

        match guess.cmp(&secret_number){
            Ordering::Less => println!("太小了"),
            Ordering::Greater => println!("太大了"),
            Ordering::Equal => {
                println!("你赢了");
                break;
            }

        }
    }
}
```

## 猜数版本5

处理程序崩溃情况

```rust
use rand::Rng;
use std::cmp::Ordering;  // 要用到标准包里面的比较接口
use std::io;

fn main() {
    println!("猜数!");

    let secret_number = rand::thread_rng().gen_range(1..101);

    // println!("神秘数字是: {}", secret_number.to_string());

    loop {
        println!("请输入你猜测的数字:");

        let mut guess = String::new();

        io::stdin().read_line(& mut guess).expect("不能读取行!");

        // 是一个Result，有 OK 和 Err 两种情况
        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,         // 可以转化为数字
            Err(_) => continue,     // 进入下一次循环
        };

        println!("你输入的是： {}", guess);

        match guess.cmp(&secret_number){
            Ordering::Less => println!("你输入的是： {} 太小了", guess),
            Ordering::Greater => println!("你输入的是： {} 太大了", guess),
            Ordering::Equal => {
                println!("你输入的是： {} 你赢了", guess);
                break; // 退出循环
            }

        }
    }
}
```
