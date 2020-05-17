
## [Rust生命周期参数的详细阐述](https://rustcc.cn/article?id=fc87a081-069e-4939-bae2-a9b36c9fbc92)

[acodercat](https://rustcc.cn/blog_with_author?author_id=e29b123f-9113-4fdb-9cd8-609fc451c718)  发表于  2020-05-17 18:00

Tags：生命周期

## Rust生命周期

> 程序中每个变量都有一个固定的作用域，当超出变量的作用域以后，变量就会被销毁。变量在作用域中从初始化到销毁的整个过程称之为生命周期。

rust的每个函数都会有一个作用域，也可以在函数中使用一对花括号再内嵌一个作用域。比如如下代码中就在main函数的函数作用域中又内嵌了一个作用域：

```
fn main() {
  let a;       // --------------+-- a start
  {            //               |
    let b = 5; // -+-- b start  |
  }            // -+-- b over   |
}              // --------------+-- a over

```

上面代码存在两个作用域，一个是`main`函数本身的作用域，另外一个是在`main`函数中使用一对`{}`定义了一个内部作用域。第2行代码声明了变量`a`,它的作用域是整个`main`函数，也可以说它的生命周期是从第2行代码到第6行代码。在第4行代码中声明了变量`b`，它的作用域是第4行到第6行。我们可以发现变量的生命周期是有长短的。

## 生命周期与借用

> rust中的借用是指对一块内存空间的引用。rust有一条借用规则是借用方的生命周期不能比出借方的生命周期还要长。

例如：

```
fn main() {
  let a;                // -------------+-- a start
  {                     //              |
    let b = 5;          // -+-- b start |
    a = &b;             //  |           |
  }                     // -+-- b over  |
  println!("a: {}", a); //              |
}                       // -------------+-- a over

```

上面第5行代码把`变量b`借给了`变量a`，所以a是借用方，b是出借方。可以发现`变量a`（借用方）的生命周期比`变量b`（出借方）的生命周期长，于是这样做违背了rust的借用规则（借用方的生命周期不能比出借方的生命周期还要长）。因为当b在生命周期结束时，a还是保持了对b的借用，就会导致a所指向的那块内存空间已经被释放了，那么变量a就会是一个悬垂引用。

运行上面代码会报如下错误：

```
error[E0597]: `b` does not live long enough
 --> src/main.rs:5:13
  |
5 |         a = &b;
  |             ^^ borrowed value does not live long enough
6 |     };
  |     - `b` dropped here while still borrowed
7 |     println!("a:{}", a);
  |                      - borrow later used here

```

意思就是说变量b的生命周期不够长。变量b已经被销毁了仍然对它进行了借用。

一个正确的例子：

```
fn main() {
  let a = 1;            // -------------+-- a start
  let b = &a;           // -------------+-- b start
  println!("a: {}", a); //              |
}                       // -------------+-- b, a over

```

观察上面代码发现变量b（借用方）的生命周期要比变量a（出借方）的生命周期要短，所以借用检查器会通过。

## 函数中的生命周期参数

> 对于一个参数和返回值都包含引用的函数而言，该函数的参数是出借方，函数返回值所绑定到的那个变量就是借用方。所以这种函数也需要满足借用规则（借用方的生命周期不能比出借方的生命周期还要长）。那么就需要对函数返回值的生命周期进行标注，告知编译器函数返回值的生命周期信息。

我们下面定义一个函数，该函数接收两个`i32`的引用类型，返回大的那个数的引用。

示例：

```
fn max_num(x: &i32, y: &i32) -> &i32 {
  if x > y {
    &x
  } else {
    &y
  }
}

fn main() {
  let x = 1;                // -------------+-- x start
  let max;                  // -------------+-- max start
  {                         //              |
    let y = 8;              // -------------+-- y start
    max = max_num(&x, &y);  //              |
  }                         // -------------+-- y over
  println!("max: {}", max); //              |
}                           // -------------+-- max, x over

```

由于缺少生命周期参数，编译器不知道`max_num`函数返回的引用生命周期是什么，所以运行报错：

```
error[E0106]: missing lifetime specifier
 --> src/main.rs:1:33
  |
1 | fn max_num(x: &i32, y: &i32) -> &i32 {
  |               ----     ----     ^ expected named lifetime parameter
  |
  = help: this function's return type contains a borrowed value, but the signature does not say whether it is borrowed from `x` or `y`

```

函数的生命周期参数声明在函数名后的尖括号`<>`里，然后每个参数名跟在一个单引号`'`后面，多个参数用逗号隔开。如果在参数和返回值的地方需要使用生命周期进行标注时，只需要在`&`符号后面加上一个单引号`'`和之前声明的参数名即可。生命周期参数名可以是任意合法的名称。例如：

```
fn max_num<'a>(x: &'a i32, y: &'a i32) -> &'a i32 {
  if x > y {
    &x
  } else {
    &y
  }
}
fn main() {
  let x = 1;                // -------------+-- x start
  let max;                  // -------------+-- max start
  {                         //              |
    let y = 8;              // -------------+-- y start
    max = max_num(&x, &y);  //              |
  }                         // -------------+-- y over
  println!("max: {}", max); //              |
}                           // -------------+-- max, x over

```

上面代码对函数`max_num`的参数和返回值的生命周期进行了标注，用于告诉编译器函数参数和函数返回值的生命周期一样长。在第13行代码对`max_num`进行调用时，编译器会把变量x的生命周期和变量y的生命周期与`max_num`函数的生命周期参数`'a`建立关联。这里值得注意的是，变量x和变量y的生命周期长短其实是不一样的，那么关联到max_num函数的生命周期参数`'a`的长度是多少呢？实际上编译器会取变量x的生命周期和变量y的生命周期`重叠`的部分，也就是取最短的那个变量的生命周期与`'a`建立关联。这里最短的生命周期是变量`y`，所以`'a`关联的生命周期就是变量y的生命周期。

运行上面代码，会有报错信息：

```
error[E0597]: `y` does not live long enough
  --> src/main.rs:13:27
   |
13 |         max = max_num(&x, &y);
   |                           ^^ borrowed value does not live long enough
14 |     }
   |     - `y` dropped here while still borrowed
15 |     println!("max: {}", max);
   |                         --- borrow later used here

```

报错信息说变量y的生命周期不够长，当y的生命周期结束后，仍然被借用。

我们仔细观察发现`max_num`函数返回值所绑定到的那个变量`max`（借用方）的生命周期是从第10行代码到第16行代码，而`max_num`函数的返回值（出借方）的生命周期是`'a`，`'a`的生命周期又是变量x的生命周期和变量y的生命周期中最短的那个，也就是变量y的生命周期。变量y的生命周期是代码的第12行到第14行。所以这里不满足借用规则（借用方的生命周期不能比出借方的生命周期还要长）。也就是为什么编译器会说变量y的生命周期不够长的原因了。函数的生命周期参数并不会改变生命周期的长短，只是用于编译来判断是否满足借用规则。

将代码做如下调整，使其变量max的生命周期小于变量y的生命周期，编译器就可以正常通过：

```
fn max_num<'a>(x: &'a i32, y: &'a i32) -> &'a i32 {
  if x > y {
    &x
  } else {
    &y
  }
}
fn main() {
  let x = 1;                  // -------------+-- x start
  let y = 8;                  // -------------+-- y start
  let max = max_num(&x, &y);  // -------------+-- max start
  println!("max: {}", max);   //              |
}                             // -------------+-- max, y, x over

```

函数存在多个生命周期参数时，需要标注各个参数之间的关系。例如：

```
fn max_num<'a, 'b: 'a>(x: &'a i32, y: &'b i32) -> &'a i32 {
  if x > y {
    &x
  } else {
    &y
  }
}
fn main() {
  let x = 1;                  // -------------+-- x start
  let y = 8;                  // -------------+-- y start
  let max = max_num(&x, &y);  // -------------+-- max start
  println!("max: {}", max);   //              |
}                             // -------------+-- max, y, x over

```

上面代码使用`'b: 'a`来标注`'a`与`'b`之间的生命周期关系，它表示`'a`的生命周期不能超过`'b`，即函数返回值的生命周期`'a`（借用方）不能超过`'b``（出借方），`'a`也不会超过`'a`（出借方）。

## 结构体中的生命周期参数

> 一个包含`引用成员`的结构体，必须保证结构体本身的生命周期不能超过任何一个`引用成员`的生命周期。否则就会出现成员已经被销毁之后，结构体还保持对那个成员的引用就会产生悬垂引用。所以这依旧是rust的借用规则即借用方（结构体本身）的生命周期不能比出借方（结构体中的引用成员）的生命周期还要长。因此就需要在声明结构体的同时也声明生命周期参数，同时对结构体的引用成员进行生命周期参数标注。

结构体生命周期参数声明在结构体名称后的尖括号`<>`里，每个参数名跟在一个单引号`'`后面，多个参数用逗号隔开。在进行标注时，只需要在引用成员的`&`符号后面加上一个单引号`'`和之前声明的参数名即可。生命周期参数名可以是任意合法的名称。例如：

```
struct Foo<'a> {
  v: &'a i32
}

```

上面代码可以把结构体`Foo`的生命周期与成员`v`的生命周期建立一个关联用于编译器进行借用规则判断。

函数生命周期参数要注意一点的是，如果函数的参数与函数的返回值不建立生命周期关联的话，生命周期参数就毫无用处。

下面是一个违反借用规则的例子：

```
#[derive(Debug)]
struct Foo<'a> {
  v: &'a i32
}

fn main() {
  let foo;                    // -------------+-- foo start
  {                           //              |
    let v = 123;              // -------------+-- v start
    foo = Foo {               //              |
      v: &v                   //              |
    }                         //              |
  }                           // -------------+-- v over
  println!("foo: {:?}", foo); //              |
}                             // -------------+-- foo over

```

上面代码的第14行到15行`foo`的生命周期依然没有结束，但是它所引用的变量`v`已经被销毁了，因此出现了悬垂引用。编译器会给出报错提示：变量`v`的的生命周期不够长。

## 静态生命周期参数

> 有一个特殊的生命周期参数叫`static`，它的生命周期是整个应用程序。跟其他生命周期参数不同的是，它是表示一个具体的生命周期长度，而不是泛指。`static`生命周期的变量存储在静态段中。

所有的字符串字面值都是  `'static`  生命周期，例如：

```
let s: &'static str = "codercat is a static lifetime.";

```

上面代码中的生命周期参数可以省略，就变成如下形式：

```
let s: &str = "codercat is a static lifetime.";

```

还有`static`变量的生命周期也是`'static`。

例如：

```
static V: i32 = 123;

```

下面举一个特殊的例子：

```
fn max_num<'a>(x: &'a i32, y: &'a i32) -> &'a i32 {
  if x > y {
    &x
  } else {
    &y
  }
}
fn main() {
  let x = 1;                // -------------+-- x start
  let max;                  // -------------+-- max start
  {                         //              |
    static Y: i32 = 8;      // -------------+-- Y start
    max = max_num(&x, &Y);  //              |
  }                         //              |
  println!("max: {}", max); //              |
}                           // -------------+-- max, Y, x over

```

还是之前的`max_num`函数。在代码的第12行定义了一个静态变量，它的生命周期是`'static`  。`max_num`函数的生命周期参数`'a`会取变量`x`的生命周期和变量`Y`的生命周期重叠的部分。所以传入`max_num`函数并不会报错。

## 总结

以上内容是我个人在学习rust生命周期参数相关内容时的总结，如有错误欢迎指正。文中的借用和引用实际上是一个东西。