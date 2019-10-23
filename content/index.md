class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Why Rust?

.grey[Nick Cameron]

.grey[.smaller[PingCAP, Rust core team]]

.grey[.smaller[adapted from slides by Santiago Pastorino]]

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# What is Rust?

- Safe systems programming language
  - Sponsored by Mozilla Research
  - v1.0 released in 2015
  - 2018 edition launched at the end of 2018
- Multiparadigm
  - Imperative, structured, functional, concurrent, generic, compiled
- Static strong typing
  - Inference
- Safe, fast, ergonomic
- Free and open-source software, MIT License or Apache License 2.0

---

# Who is using Rust?

- **PingCAP** - TiKV, Raft, gRPC
- **Mozilla** - Firefox (Stylo, WebRender), Servo.
- **Google** - Fuchsia operating system.
- **Facebook** - Mononoke, Libra.
- **Amazon** - Firecracker.
- **Microsoft** - Azure IoT work.
- **Dropbox** - Storage system.

You can see even more familiar names like **Twitter**, **npm**, **Red Hat**, **Reddit**, **Samsung**, **Cloudflare**, **Yelp**, **Gnome**, **Chef**, **Canonical**, **Coursera**, **Tor** and many more.

---

# Who is using Rust?

> "My biggest compliment to Rust is that it's boring, and this is an amazing compliment."

###### Chris Dickinson, npm

> "All the documentation, the tooling, the community is great - you have all the tools to succeed in writing Rust code."

###### Antonio Verardi, Yelp

---

<img src="content/images/technology-radar.png" alt="Thoughtworks Radar">

"Lot of interest in Rust, some of our clients are already using it."

---

# People love Rust (2016)

<img src="content/images/most-loved-2016.png" alt="Stackoverflow Survey">

---

# People love Rust (2017)

<img src="content/images/most-loved-2017.png" alt="Stackoverflow Survey">

---

# People love Rust (2018)

<img src="content/images/most-loved-2018.png" alt="Stackoverflow Survey">

---

# People love Rust (2019)

<img src="content/images/most-loved-2019.png" alt="Stackoverflow Survey">

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- **Performance**
  - **Zero-cost abstractions**

---

# Performance

<img src="content/images/performance.png" alt="Performance Rust/C/C++">

---

# Qualities Rust shares with C(++)

- **Zero-cost abstractions:**
  - inline memory layout
  - static dispatch
  - no garbage collector or other runtime
- Anywhere you use C(++), you can use Rust:
  - Want to write a plugin for Python or Ruby? You can do it in Rust.
  - Want to write a **kernel**? You can do it in Rust.

---

# Why not just use C(++) then?

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- **Memory safety without GC**
  - **Concurrency without dataraces**

---

# Memory safety

<img alt="Linux CVEs in 2018" src="content/images/Linux CVEs in 2018.svg" style="margin-top: 0rem; margin-bottom: -2rem;">

<img src="content/images/Tux.svg" alt="Linux logo" width="120rem" height="auto" style="display:block; position: absolute; top: 1rem; right: 3rem;">

.grey[.smaller[Source: https://www.cvedetails.com/vulnerability-list/vendor_id-33/product_id-47/year-2018/Linux-Linux-Kernel.html]]

---

# Memory safety

<img alt="Microsoft Memory Safety" src="content/images/microsoft-memory-safety-trends.png" style="margin-top: 0rem; margin-bottom: -2rem;">

.grey[.smaller[Source: https://www.zdnet.com/article/microsoft-70-percent-of-all-security-bugs-are-memory-safety-issues/]]


---

# Memory safety

|                       | C/C++ |
| --------------------- | ----- |
| Control, flexibility  | 🎉    |
| Minimal to no runtime | 🎉    |
| Double free           | 😢    |
| Use after free        | 😢    |
| Data race             | 😢    |

---

# Memory safety

|                       | C/C++ | GC    |
| --------------------- | ----- | ----- |
| Control, flexibility  | 🎉    | 🤷‍♀️ |
| Minimal to no runtime | 🎉    | 🤷‍♀️ |
| Double free           | 😢    | 🎉    |
| Use after free        | 😢    | 🎉    |
| Data race             | 😢    | 😢    |

---

# Memory safety

|                       | C/C++ | GC    | Rust |
| --------------------- | ----- | ----- | ---- |
| Control, flexibility  | 🎉    | 🤷‍♀️ | 😎   |
| Minimal to no runtime | 🎉    | 🤷‍♀️ | 😎   |
| Double free           | 😢    | 🎉    | 😎   |
| Use after free        | 😢    | 🎉    | 😎   |
| Data race             | 😢    | 😢    | 😎   |


Guaranteed by Rust's ownership system at compile time

---

# Memory safety: a strict compiler

- It can take some time until your program compiles
- Lifetimes can be complicated
    - “error: `x` does not live long enough”


However:
- “If it compiles, it usually works”
- Far fewer difficult bugs
- Far less debugging
    - No data races!
- Refactoring is safe and painless

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- Memory safety without GC
  - Concurrency without dataraces
- **Powerful type system**
  - **High-level code, low-level performance**

---

# High-level code

```rust
enum Event {
    Load,
    KeyPress(char),
    Click { x: i64, y: i64 }
}

fn print_event(event: Event) {
    match event {
        Event::Load => println!("Loaded"),
        Event::KeyPress(c) => println!("Key {} pressed", c),
        Event::Click {x, y} => println!("Clicked at x={}, y={}", x, y),
    }
}
```

Algebraic data types (enums), Pattern matching & Hygienic macros

---

# High-level code

```rust
enum Event {
    Load,
    KeyPress(char),
    Click { x: i64, y: i64 }
}

fn print_event(event: Event) {
    match event {
        Event::Load => println!("Loaded"),
        Event::KeyPress(`c`) => println!("Key {} pressed", `c`),
        Event::Click {x, y} => println!("Clicked at x={}, y={}", x, y),
    }
}
```

Algebraic data types (enums), Pattern matching & Hygienic macros

---

# High-level code

```rust
enum Event {
    Load,
    KeyPress(char),
    Click { x: i64, y: i64 }
}

fn print_event(event: Event) {
    match event {
        Event::Load => println!("Loaded"),
        Event::KeyPress(c) => println!("Key {} pressed", c),
        Event::Click {`x`, `y`} => println!("Clicked at x={}, y={}", `x`, `y`),
    }
}
```

Algebraic data types (enums), Pattern matching & Hygienic macros

---

# No null pointers

```rust
enum Option<T> {
  Some(T),
  None,
}
```

Generics

---

# No null pointers

```rust
enum Option<T> {
* Some(T),
  None,
}
```

Generics

---

# No null pointers

```rust
enum Option<T> {
  Some(T),
* None,
}
```

Generics

---

# No null pointers

```rust
fn print_first(v: Vec<String>) {
  match v.first() {
    Some(s) => println!("{}", s.to_uppercase()),
    None => println!("Not found"),
  }
}
```

---

# No null pointers

```rust
fn print_first(v: Vec<String>) {
  match v.first() {
    Some(`s`) => println!("{}", `s`.to_uppercase()),
    None => println!("Not found"),
  }
}
```

---

# High-level code

```rust
fn load_images(paths: &[PathBuf]) -> Vec<Image> {
    paths.iter()
         .map(|path| Image::load(path))
         .collect()
}
```

Iterators, Traits, Generics & Closures

---

# Powerful type system: mutexes

```rust
// mutex owns data
let mutex = Mutex::new(data);

// compilation error: data was moved
data.push(4);

let mut d = mutex.lock().unwrap();
d.push(5);
// released at end of scope
```

⇒ Rust ensures that Mutex is locked before accessing data

???

- Impossible to access data behind a Mutex without locking
- Represent contracts in code instead of documentation

---
<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- Memory safety without GC
  - Concurrency without dataraces
- Powerful type system
  - High-level code, low-level performance
- **Modern conveniences**
  - **Tooling**

---

<img src="content/images/cargo-logo.png" alt="Cargo logo" width="150rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Great tooling

- **rustup**: Use multiple Rust versions for different directories
- **cargo**: Automatically download, build, and link dependencies

.center[
<img src="content/images/cratesio.png" alt="Crates.io screenshot" width="500rem">
]

---

<img src="content/images/cargo-logo.png" alt="Cargo logo" width="150rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Great tooling

- **rustup**: Use multiple Rust versions for different directories
- **cargo**: Automatically download, build, and link dependencies
- **rustfmt**: Format Rust code according to style guidelines
- **clippy**: Additional warnings for dangerous or unidiomatic code

--
- **Rust Playground**: Run and share code snippets in your browser

![Rust Playground screenshot](content/images/playground.png)

---

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto" style="position: absolute; right: 0rem; margin-top: -2rem;">

# Why people love Rust?

- Performance
  - Zero-cost abstractions
- Memory safety without GC
  - Concurrency without dataraces
- Powerful type system
  - High-level code, low-level performance
- Modern conveniences
  - Tooling
- **Community**

---

# Community

.center[
<img src="content/images/community.jpg" alt="Rust community" width="650rem">

.smaller[Open, friendly, welcoming, inspiring, craftmanship, learn]
]

---

# Community

- China
  - Active and growing
  - PingCAP, Baidu X-Lab, Bilibili, Cryptape, QTUM, Nervos, ...
  - RustCon Asia
  - WeChat
  - 中文: books, blogs, articles, meetups

---

# Async programming

- **Zero cost abstractions**
  - minimal runtime
  - no green threads
  - minimal allocation

---

# Async programming

- **Futures**
  - low-level
  - powerful
  - combinator programming style

---

# Async programming

- **Futures**

```rust
stores
    .and_then(move |(key_data, store)| ...)
    .map_ok(move |(request, mut response)| {
        let locks = response.take_locks();
        if !locks.is_empty() {
            return resolve_locks(locks, pd_client.clone())
                .map_ok(move |_| request.response_stream(pd_client))
                .try_flatten_stream();
        }
        stream::once(future::ok(response))
    })
    .try_flatten()
```

---

# Async programming

- **`async`/`await`**
  - ergonomic
  - low-cost
  - safe

---

# Async programming

- **`async`/`await`**

```rust
async fn get(&self, key: Key) -> Result<Option<Value>> {
    let cluster = self.cluster.connect().await?;
    cluster.get(key).await
}
```

---

# Async programming

- **Async io**
  - low-level and high-level libraries
  - platform-native

---

# Async programming

- **Async io**

```rust
async fn accept_loop(addr: impl ToSocketAddrs) -> Result<()> {
    let listener = TcpListener::bind(addr).await?;
    let mut incoming = listener.incoming();
    while let Some(stream) = incoming.next().await {
        ...
    }
    Ok(())
}
```

---

# gRPC

- RPC system developed by Google
- based on http2 and protobufs
- multi-language support
- unary and streaming protocols
- becoming de facto standard

---

# gRPC in Rust

- grpc.rs
  - low cost
  - ergonomic
  - stable
- Tonic
  - native Rust
  - potentially *very* fast
  - new

---

# gRPC in Rust

- rust-protobuf, Prost, h2
- Transparent code generation

---

# gRPC in Rust

|   | QPS Rust | QPS C++ | Latency Rust | Latency C++ |
|---|---:|---:|---:|---:|
|streaming|8151|8653|209|192|
|unary (large)|282|157|5250|26988|
|unary (small)|94024|99139|128909|165768|

Initial benchmarking of Tonic is promising.

---

# Prometheus

* De facto metrics gathering
* Easily integrates with Grafana
* Multi-language support
* Plaintext, human readable output
* Pull based (Not push, **why?**)

---

# Prometheus

* **Counters**: Single number, only increments
* **Guage**: Single number, freely mutable
* **Histogram**: Sum of observations & observation count
* **Vector** versions of each, for when you want to count the same thing, but on different dimensions.

---

# Prometheus Terms

* **Metrics** provide collectors.
* **Registries** contain those.
* **Encoders** can output them.

**Executables** construct a **registry**,
feed **collectors**, and provide an **encoder**.

**Libraries** don’t.

---

# rust-prometheus

* Highly optimized (nanosecond scale!)
* PingCAP maintained
* Used in TiKV
* Published
* Easy to use
* Optional *Static metrics*

---

# Example

```rust
// Build a registry for collectors.
let r = `Registry::new`();
// Build a collector.
let counter = `Counter::with_opts`(Opts::new(
    "cookies_baked",
    "Number of cookies baked."
)).unwrap();
// Register it.
r.`register`(Box::new(counter.clone()))
    .unwrap();
// Increment it
counter.`inc`();
```

---

# Example

```rust
let mut buffer = vec![];
// Gather metrics (Pull!)
let metric_families = r.`gather`();
// Build an encoder, encode it
let encoder = `TextEncoder::new()`;
encoder.`encode`(
    &metric_families,
    &mut buffer
).unwrap();
// Print it
println!("{}", String::from_utf8(buffer)
    .unwrap());
```

---

# Example: Output

```rust
hoverbear@nomad:~/git/prom$ `cargo run`
    Finished dev [unoptimized + debuginfo] target(s) in 0.01s
     Running \`target/debug/prom\`
# HELP cookies_baked Number of cookies baked.
# TYPE cookies_baked counter
cookies_baked 1
```

---

# To sum up

- **Rust is a high performance and safe systems programming language**

---

# To sum up

- Rust is a high performance and safe systems programming language
- **Used by a lot of big names already (Mozilla, Google, Facebook, Amazon, Microsoft, etc)**

---

# To sum up

- Rust is a high performance and safe systems programming language
- Used by a lot of big names already (Mozilla, Google, Facebook, Amazon, Microsoft, etc)
- **People love Rust**
  - **Performance**
  - **Memory safety without GC**
  - **Powerful type system**
  - **Modern conveniences**
  - **Community**

---

class: center
name: title
count: false

<img src="content/images/rust-logo-blk.svg" alt="Rust logo" width="250rem" height="auto">

# Thanks

.grey[Email: nick@pingcap.com]
.grey[GitHub: nrc]<br/>
.grey[Twitter: nick_r_cameron]<br/>
