# myos

一个用 C++ 从零编写的简易 x86 操作系统内核，适合学习操作系统底层原理。

---

## 简介

myos 是一个运行在 x86（32 位）架构上的玩具操作系统内核。项目涵盖了操作系统的核心组成部分，包括启动引导、内存管理、硬件驱动、中断处理、图形界面和网络协议栈，适合作为学习操作系统原理的参考实现。

---

## 主要特性

- **引导加载**：通过 GRUB Multiboot 协议启动，汇编编写的引导程序（`loader.s`）
- **全局描述符表（GDT）**：段式内存保护机制
- **内存管理**：简单的堆内存分配器
- **中断处理**：可编程中断控制器（PIC）及中断描述符表（IDT）支持
- **PCI 总线枚举**：自动检测并初始化 PCI 设备
- **硬件驱动**：
  - 键盘驱动（PS/2）
  - 鼠标驱动（PS/2）
  - VGA 图形驱动（320×200，8 位色）
  - AMD AM79C973 网卡驱动
- **图形界面（GUI）**：基础 Widget / Window / Desktop 框架（通过宏 `GRAPHICMODE` 开启）
- **多任务**：简单的协作式任务调度
- **网络协议栈**：
  - 以太网帧收发
  - ARP（地址解析协议）
  - IPv4
  - ICMP
  - UDP
  - TCP

---

## 项目结构

```
myos/
├── include/                 # 头文件
│   ├── common/              # 基础类型定义
│   ├── drivers/             # 驱动头文件（键盘、鼠标、VGA、网卡）
│   ├── gui/                 # GUI 组件头文件
│   ├── hardwarecommunication/  # 硬件通信（端口、中断、PCI）
│   ├── net/                 # 网络协议头文件
│   ├── gdt.h                # 全局描述符表
│   ├── memorymanagement.h   # 内存管理
│   └── multitasking.h       # 多任务
├── src/                     # 源文件（与 include 结构对应）
│   ├── kernel.cpp           # 内核入口
│   └── loader.s             # 汇编引导程序
├── linker.ld                # 链接脚本
└── Makefile                 # 构建脚本
```

---

## 构建与运行

### 依赖

- `g++`（支持 32 位交叉编译，`-m32`）
- `as`（GNU 汇编器）
- `ld`（GNU 链接器）
- `grub-mkrescue` + `xorriso`（用于生成 ISO 镜像）
- VirtualBox（用于运行）

### 构建

```bash
# 编译生成内核二进制
make

# 生成可启动的 ISO 镜像
make mykernel.iso

# 在 VirtualBox 中运行（需提前创建名为 "my os" 的虚拟机）
make run
```

### 清理

```bash
make clean
```

---

## 开发说明

- 图形模式默认关闭，可在编译时加入 `-DGRAPHICMODE` 宏开启 VGA 图形界面与 GUI 窗口。
- 网络功能依赖 AMD AM79C973 网卡（VirtualBox 的 PCnet 虚拟网卡与之兼容）。
