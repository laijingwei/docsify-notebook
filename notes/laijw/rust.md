# Rust

## Visual Studio 2017 C++ Build Tools

```bash
# visualcppbuildtools_full.exe
# vs_community.exe

# 使用命令行创建本地缓存

vs_community.exe --layout d:\vs2017layout --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang zh-CN


# 从本地缓存安装 Visual Studio

d:\vs2017layout\vs_community.exe --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeOptional
```

## rust 安装

[rustup-init.exe 安装](https://kaisery.gitbooks.io/rust-book-chinese/content/content/Getting%20Started%20%E5%87%86%E5%A4%87.html)


## 中国镜像

### 环境变量

| 变量名             | 变量值                                         |
| ------------------ | ---------------------------------------------- |
| CARGO_HOME         | %USERPROFILE%\.cargo                            |
| RUSTUP_DIST_SERVER | https://mirrors.ustc.edu.cn/rust-static        |
| RUSTUP_UPDATE_ROOT | https://mirrors.ustc.edu.cn/rust-static/rustup |


### 配置文件

``"%USERPROFILE%\.cargo\config"``

```bash
[registry]
index = "https://mirrors.ustc.edu.cn/crates.io-index/"
[source.crates-io]
replace-with = 'ustc'
[source.ustc]
registry = "https://mirrors.ustc.edu.cn/crates.io-index/"
```


## rustup

以下列出rustup的部分命令：

```bash
rsutup show : 列出现在使用的和已安装的rust版本。
rustup update : 更新所有已安装版本，由于nightly偶尔会爆肝日更，所以谨慎更新。
rustup default: 设置将要使用的版本。
rustup component <sub> : 检查(list)、安装(add)、移除(remove)组建。
```

## Cargo

cargo既是一个类似于npm、pip的包管理软件，又是一个像marven一样的项目框架。

```bash
build       Compile the current package
check       Analyze the current package and report errors, but don't build object files
clean       Remove the target directory
doc         Build this package's and its dependencies' documentation
new         Create a new cargo package
init        Create a new cargo package in an existing directory
run         Build and execute src/main.rs
test        Run the tests
bench       Run the benchmarks
update      Update dependencies listed in Cargo.lock
search      Search registry for crates
publish     Package and upload this package to the registry
install     Install a Rust binary. Default location is $HOME/.cargo/bin
uninstall   Uninstall a Rust binary
```