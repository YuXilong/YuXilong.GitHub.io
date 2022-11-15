---

layout: post

title: Rust Delopment Tips

date: 2022-11-15 18:28:20 +0800

tags: [Rust]

categories: Rust Development

---



#### `Rust`应用交叉编译

- 安装架构

  ```shell
  rustup target install x86_64-apple-darwin
  ```

- 编译

  ```shell
  cargo build --target x86_64-apple-darwin
  ```

- 使用配置文件`.cargo/config.toml`

  ```toml
  [build]
  target = ["aarch64-apple-darwin", "x86_64-apple-darwin"]
  ```

  
