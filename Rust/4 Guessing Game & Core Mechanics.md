---
tags:
  - rust
  - control-flow
  - syntax
  - error-handling
---
# 1. Variables, References & Mutability

```rust
let mut guess = String::new();
io::stdin().read_line(&mut guess).expect("Failed to read line");
```

* **Immutability by Default**: Variables declared with `let` cannot be rebound or mutated unless prefixed with `let mut`.
* **Associated Functions (`::`)**: `String::new()` calls an associated function implemented on the type itself (analogous to static methods in other languages).
* **References (`&` and `&mut`)**:
  * Passing `&mut guess` passes a **mutable reference** to standard input.
  * References allow accessing data in memory without copying ownership.
  * Like variables, references are **immutable by default** (`&x`), requiring explicit `&mut x` to grant write access to the callee.

---

# 2. Error Handling via `Result` Enum

Rust does not use exceptions. Fallible operations return the `Result` enumeration:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

* **Compiler Warning (`#[warn(unused_must_use)]`)**: Dropping a `Result` without handling emits a compiler warning.
* **Panicking with `.expect()`**:
  * `Ok(val)` $\to$ extracts and returns `val`.
  * `Err(err)` $\to$ terminates the program (`panic`) with the specified message.
* **Idiomatic Pattern Matching**:
  ```rust
  let guess: u32 = match guess.trim().parse() {
      Ok(num) => num,
      Err(_) => continue, // '_' is a catch-all wildcard; ignores invalid input
  };
  ```

---

# 3. Variable Shadowing & Type Conversion

```rust
let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

* **Shadowing**: Re-declaring a variable with `let` reuses the name `guess`.
  * Allows transforming values (e.g., raw `String` $\to$ clean numeric `u32`) without inventing synthetic names like `guess_str`.
  * Can change both **type** and **mutability**.
* **String Parsing**:
  * `.trim()`: Strips leading/trailing whitespace and control chars (`\n`, `\r\n`).
  * `.parse()`: Parses string slices into inferable or explicitly annotated types (`u32`). Returns `Result`.

---

# 4. Comparisons & Flow Control: `match` and `Ordering`

```rust
use std::cmp::Ordering;

match guess.cmp(&secret_number) {
    Ordering::Less => println!("Too small!"),
    Ordering::Greater => println!("Too big!"),
    Ordering::Equal => {
        println!("You win!");
        break; // Exits the enclosing `loop`
    }
}
```

* **`std::cmp::Ordering`**: Enum containing three comparative variants: `Less`, `Greater`, and `Equal`.
* **`match` Arms**: Consist of a `Pattern => Expression` structure. Evaluation stops after the first matching branch.
* **Infinite Loops**: `loop { ... }` runs continuously until terminated by `break` or an exit signal (`Ctrl-C`).

---

# 5. Dependencies, Cargo & SemVer

To add an external crate (such as `rand`):

```toml
[dependencies]
rand = "0.8.5" # Shorthand for ^0.8.5 (compatible up to < 0.9.0)
```

* **Semantic Versioning (`^X.Y.Z`)**: By default, Cargo pulls the latest patch/minor version preserving backward compatibility.
* **`Cargo.lock`**: Locks dependency versions to exact hashes, guaranteeing deterministic and reproducible builds across environments.
* **Crate Traits**: Methods like `gen_range()` require their defining trait to be within lexical scope:
  ```rust
  use rand::Rng; // Brings Rng trait into scope for thread_rng()
  let secret_number = rand::thread_rng().gen_range(1..=100); // 1..=100 is an inclusive range
  ```
* **Offline Crate Documentation**: `cargo doc --open` builds and renders offline HTML manuals for all referenced crates.