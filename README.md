# myos

**myos** 是一个用 C++ 从零编写的简易 x86 操作系统内核，旨在学习操作系统底层原理。

## 功能特性

- 自定义全局描述符表（GDT）
- 中断管理（IDT / PIC）
- 键盘与鼠标驱动
- PCI 设备枚举
- VGA 文字与图形模式输出
- 内存管理（堆分配）
- 多任务调度
- 网络支持：以太网帧、ARP、IPv4、ICMP、UDP、TCP

## 构建方式

```bash
make
```

## 参考资料

https://github.com/intel-innersource/applications.ai.ainas.heliconsearch
