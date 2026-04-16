# Rust & Cargo 安装指南

此文档说明如何安装 Rust 和 Cargo 包管理器。

## Windows 安装

在 Windows 上安装 Rust 环境，核心是使用 `rustup` 这个官方工具来一键安装。

### 🚀 正式安装 Rust

完成前置准备后，就可以安装 Rust 本身了。

1.  **下载安装程序**：访问 Rust 官网 (https://www.rust-lang.org/tools/install)，下载适用于 Windows 的 `rustup-init.exe`。
2.  **运行安装**：双击运行下载的 `rustup-init.exe`，在终端窗口出现时，直接按 **回车键 (Enter)** 选择默认安装即可。

### ✅ 验证安装成功

安装程序完成后，关闭并重新打开一个新的 PowerShell 或命令提示符窗口，依次运行以下命令进行验证：
```bash
rustc --version
cargo --version
```
如果看到版本信息输出（例如 `rustc 1.80.0`），说明安装成功。

### 📝 补充说明：加速下载与常见问题

*   **💨 如何加速下载？**
    如果下载速度很慢，可以在安装**前**在 PowerShell 中设置国内镜像源，然后再运行安装程序：
    ```powershell
    $env:RUSTUP_DIST_SERVER='https://mirrors.tuna.tsinghua.edu.cn/rustup'
    $env:RUSTUP_UPDATE_ROOT='https://mirrors.tuna.tsinghua.edu.cn/rustup/rustup'
    # 然后运行 rustup-init.exe
    ```
*   **❓ 常见问题怎么解决？**
    1.  **找不到 `link.exe` 或编译报错**：通常是没有安装或正确配置 C++ 编译环境，请检查前置步骤是否完成。
    2.  **安装程序提示"Access Denied"**：可以右键点击终端，选择"以管理员身份运行"。
    3.  **命令行找不到 `rustc` 或 `cargo`**：通常是因为环境变量未自动添加。可以手动将 `%USERPROFILE%\.cargo\bin` 这个路径添加到系统的 `PATH` 环境变量中。
