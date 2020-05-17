
# [Builder pattern](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/builder-pattern/landing.html#builder-pattern)

This pattern is a common way of creating instances in Rust. It will help you write cleaner and more readable code that'll be easy to expand later.

Let's dive straight into everyones favorite toy example, the car:

```rust

#[derive(Debug)]
struct Car {
    number_of_doors: usize,
    color: String,
}

```

Cars have a number of defining properties, let's pretend there's only two for now. (This struct is very simple, so we could of course create an  `impl`  with a  `new()`  in it in this case, but bear with me.)

In Rust, the builder pattern consists of a struct with multiple functions that consume  `self`  mutably and returns it again. It is commonly given the name of the type it builds, followed by the word  `Builder`. In our case, it would be a  `CarBuilder`.

```rust

struct CarBuilder {
    number_of_doors: usize,
    color: Option<String>,
}

```

This  `CarBuilder`  contains data that will later be used to construct the  `Car`. Note that the signature for  `color`  differs from the one in  `Car`.

Let's start by giving the  `CarBuilder`  a  `new()`  and initialize the values.

```rust

impl CarBuilder {
    pub fn new() -> Self {
        Self {
            number_of_doors: 5,
            color: None,
        }
    }
}

```

Here we set the number of doors to 5, as that's a very common number to have. Four actual doors plus one trunk. The color is set to None, because there's no "normal" color for a car to have.

Let's add another function to build a  `Car`. We'll set a rule here that only builds one if we've set a color.

```rust

impl CarBuilder {
    pub fn build(self) -> Result<Car, CarBuilderError> {
        let color = match self.color {
            Some(color) => color,
            None => return Err(CarBuilderError::NoColor),
        };

        Ok(Car {
            number_of_doors: self.number_of_doors,
            color,
        })
    }
}

```

You'll notice that  `build()`  returns  `Result<Car, CarBuilderError>`. We'll get to  `CarBuilderError`  in a bit.

Next we'll add a function that can set the amount of doors.  `number_of_doors is a` usize`, and we don't judge here, so users can have millions of doors if they want. That means that we'll only have one rule; don't set the number to 0.

```rust

impl CarBuilder {
    pub fn number_of_doors(mut self, number_of_doors: usize) -> Result<Self, CarBuilderError> {
        if number_of_doors == 0 {
            Err(CarBuilderError::WrongNumberOfDoors)
        } else {
            self.number_of_doors = number_of_doors;
            Ok(self)
        }
    }
}

```

The rule about the number of doors is enforced by returning an error if the number is wrong.

We will also add a function that lets us set the color. If you look back at the build function, you'll notice that it will fail to build if you don't pick a color.

```rust

impl CarBuilder {
    pub fn color(mut self, color: Color) -> Self {
        self.color = Some(color);
        self
    }
}

```

(As we all know, cars can only be one of two colors).

```rust

#[derive(Debug)]
enum Color {
    Red,
    Green,
}

```

Now all we have left to do is to define those errors we mentioned before.

```rust

#[derive(Debug)]
enum CarBuilderError {
    WrongNumberOfDoors,
    NoColor,
}

impl Error for CarBuilderError {
    fn description(&self) -> &str {
        match self {
            CarBuilderError::WrongNumberOfDoors => "The car must have at least one door.",
            CarBuilderError::NoColor => "The car must have a color.",
        }
    }
}

impl fmt::Display for CarBuilderError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "{}", self.description())
    }
}

```

That's it. Try it out like this:

```rust
fn main() -> Result<(), Box<dyn Error>> {
    let car = CarBuilder::new()
        .number_of_doors(3)?
        .color(Color::Red)
        .build()?;

    println!("car = {:?}", car);

    Ok(())
}

```

If you've discovered a new feature a car might have, like horsepower or a chromed exhaust pipe tip, you can easily add it now.

Good luck.

---

## [Full example](http://segfaultsourcery.s3-website.eu-central-1.amazonaws.com/snippets/rust/builder-pattern/full-example.html#full-example)

```rust
use std::error::Error;
use std::fmt;

fn main() -> Result<(), Box<dyn Error>> {
    let car = CarBuilder::new()
        .number_of_doors(3)?
        .color(Color::Red)
        .has_chromed_exhaust(true)
        .build()?;

    println!("car = {:?}", car);

    Ok(())
}

#[derive(Debug)]
struct Car {
    number_of_doors: usize,
    color: Color,
    horsepower: usize,
    has_chromed_exhaust: bool,
}

struct CarBuilder {
    number_of_doors: usize,
    color: Option<Color>,
    horsepower: usize,
    has_chromed_exhaust: bool,
}

impl CarBuilder {
    pub fn new() -> Self {
        Self {
            number_of_doors: 5,
            color: None,
            horsepower: 45,
            has_chromed_exhaust: false,
        }
    }

    pub fn build(self) -> Result<Car, CarBuilderError> {
        let color = match self.color {
            Some(color) => color,
            None => return Err(CarBuilderError::NoColor),
        };

        Ok(Car {
            number_of_doors: self.number_of_doors,
            color,
            horsepower: self.horsepower,
            has_chromed_exhaust: self.has_chromed_exhaust,
        })
    }

    pub fn number_of_doors(mut self, number_of_doors: usize) -> Result<Self, CarBuilderError> {
        if number_of_doors == 0 {
            Err(CarBuilderError::WrongNumberOfDoors)
        } else {
            self.number_of_doors = number_of_doors;
            Ok(self)
        }
    }

    pub fn color(mut self, color: Color) -> Self {
        self.color = Some(color);
        self
    }

    pub fn horsepower(mut self, value: usize) -> Self {
        self.horsepower = value;
        self
    }

    pub fn has_chromed_exhaust(mut self, value: bool) -> Self {
        self.has_chromed_exhaust = value;
        self
    }
}

#[derive(Debug)]
enum Color {
    Red,
    Green,
}

#[derive(Debug)]
enum CarBuilderError {
    WrongNumberOfDoors,
    NoColor,
}

impl Error for CarBuilderError {
    fn description(&self) -> &str {
        match self {
            CarBuilderError::WrongNumberOfDoors => "A car must have at least one door.",
            CarBuilderError::NoColor => "A car must have a color.",
        }
    }
}

impl fmt::Display for CarBuilderError {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "{}", self.description())
    }
}
```