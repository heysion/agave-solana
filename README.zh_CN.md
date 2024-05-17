<p align="center">
  <a href="https://solana.com">
    <img alt="Solana" src="https://i.imgur.com/0vfIMHo.png" width="250" />
  </a>
</p>

[![Solana crate](https://img.shields.io/crates/v/solana-core.svg)](https://crates.io/crates/solana-core)
[![Solana documentation](https://docs.rs/solana-core/badge.svg)](https://docs.rs/solana-core)
[![Build status](https://badge.buildkite.com/8cc350de251d61483db98bdfc895b9ea0ac8ffa4a32ee850ed.svg?branch=master)](https://buildkite.com/solana-labs/solana/builds?branch=master)
[![codecov](https://codecov.io/gh/solana-labs/solana/branch/master/graph/badge.svg)](https://codecov.io/gh/solana-labs/solana)

# 构建

## **1. 安装 rustc, cargo 和 rustfmt.**

```bash
$ curl https://sh.rustup.rs -sSf | sh
$ source $HOME/.cargo/env
$ rustup component add rustfmt
```

在对master分支进行构建时，请您确保使用的是最新的稳定版本的Rust，如下命令更新Rust：

```bash
$ rustup update
```

当构建特定的release分支时，您应该参考`ci/rust-version.sh`中的Rust版本，通过下述命令安装对应的Rust版本：
```bash
$ rustup install VERSION
```
注意，如果这版本不是您机器上的的Rust版本，更新后cargo命令可能存在问题，需要[重装](https://rust-lang.github.io/rustup/overrides.html)一个正确的版本。

在Linux系统上，您可能需要安装libssl-dev, pkg-config, zlib1g-dev, protobuf等库。

在Ubuntu上：
```bash
$ sudo apt-get update
$ sudo apt-get install libssl-dev libudev-dev pkg-config zlib1g-dev llvm clang cmake make libprotobuf-dev protobuf-compiler
```

在Fedora上:
```bash
$ sudo dnf install openssl-devel systemd-devel pkg-config zlib-devel llvm clang cmake make protobuf-devel protobuf-compiler perl-core
```

## **2. 下载源代码.**

```bash
$ git clone https://github.com/anza-xyz/agave.git
$ cd agave
```

## **3. 构建.**

```bash
$ ./cargo build
```

# 测试

**执行单元测试:**

```bash
$ ./cargo test
```

### 启动一个本地测试网

在本地启动您自己的testnet，具体说明在[在线文档]中(https://docs.solanalabs.com/clusters/benchmark).

### 访问远程的公开的开发集群网

* `devnet`  - 通过devnet.solana.com可访问稳定的公共开发集群网。这些测试网络是24小时在线不间断运行。了解更多关于[公共集群网](https://docs.solanalabs.com/clusters)的信息

# 基准测试

首先，需要安装rustc的每日构建版。`cargo bench`需要使用到仅在每日构建版中的一些不稳定特性。

```bash
$ rustup install nightly
```

执行基准测试:

```bash
$ cargo +nightly bench
```

# 发布流程

该项目的发布流程在[这里](RELEASE.md)描述。

# 代码覆盖率

生成代码覆盖率统计信息:

```bash
$ scripts/coverage.sh
$ open target/cov/lcov-local/index.html
```

为什么要关注覆盖率？虽然大多数人将覆盖率视为代码质量的度量指标，但我们主要将其视为开发者生产力的度量指标。当开发者对代码库进行更改时，这应该是对某些问题的*解决方案*。我们的单元测试集是验证这些*问题*的处理方式。执行单元测试集应该表明您的修改没有*侵犯*到其他人的解决方案。增加一个测试可以*保护*您的解决方案免受未来更改的影响。假如您不明白某行代码存在的原因，可以尝试删除它并执行单元测试。最近的测试失败应该会告诉您那行代码解决了什么问题。如果没有测试失败，那么您可以提交一个合并请求，询问，“这段代码解决了什么问题？”另一方面，如果某个测试确实失败了，而您能想到更好的解决方案，那么附带您解决方案的合并请求会受到最大的欢迎！同样，如果重写测试可以更好地覆盖它要所保护的代码，也请您把修改的补丁发送给我们！
