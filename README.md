/*
*  该代码内容修改自IGH 1.6版本，主要修改项:
*  1.master.c 新增绑定master驱动到3号核心，同时在grub中将3号核心隔离出来以获取更好的性能，同时可以配合修改kernel中的hrtimer，指定2好核心直接在硬中断中执行下文可以进一步提高性能（该功能非通用，当前代码已屏蔽，需要的可以去打开）
*  2.适配了6.5.2版本内核的 r8169 , e100e , igb ,igc 实时网卡驱动
*  3.编写了对应的PLCOpen运动运动控制主站代码，可以控制伺服做大部份常规运动控制功能，该代码由于和我自行编写的非开源激光模块深度绑定正在拆分中，需要等到10月左右开源
*  联系方式：
*  bilibili ：邪饿饿之麻薯薯
*  偶尔直播，邮箱等联系方式因为工作比较忙，暂时不公开，有交流需求可以到bilibili资讯
*
*
*  Translated by GPT:
*
*  The content of this code is modified from IGH version 1.6, with the main modifications as follows:
*  1. Added binding of the master driver to core 3 in master.c, while isolating core 3 in grub for better performance. It can also cooperate with modifications in the kernel's hrtimer, designating core 2 to directly execute the following content in the hard interrupt, which can further improve performance (this feature is not general, the current code is disabled, and can be enabled if needed).
*  2. Adapted real-time network card drivers for kernel version 6.5.2, including r8169, e100e, igb, and igc.
*  3. Developed the corresponding PLCOpen motion control master station code, capable of controlling servos to perform most conventional motion control functions. This code is deeply bound to my self-developed non-open-source laser module and is currently being separated. It is expected to be open-sourced around October.
*  Contact information:
*  bilibili: 邪饿饿之麻薯薯
*  Occasional live streams. Email and other contact information are not disclosed due to busy work schedules. For communication needs, you can reach out on bilibili.
*
*/
This is the README file of the IgH EtherCAT Master.

Contents:

[[_TOC_]]

# General Information

This is an open-source EtherCAT master implementation for Linux 2.6 or newer.

See the [features file](FEATURES.md) for a list of features. For more
information, see http://etherlab.org/en/ethercat.

or contact

>>>
Dipl.-Ing. (FH) Florian Pose <fp@igh.de>  
Ingenieurgemeinschaft IgH  
Nordsternstraße 66  
D-45329 Essen  
http://igh.de
>>>

# Documentation

## Handbook

The PDF documentation is generated via LaTeX and can be build with the
following steps:

```bash
cd documentation
make
```

The PDF is automatically held up-to-date and can be [downloaded from
GitLab](https://gitlab.com/etherlab.org/ethercat/-/jobs/artifacts/stable-1.5/raw/pdf/ethercat_doc.pdf?job=pdf).

## Doxygen

To generate the Doxygen documentation, the following commands can be used.
Therefore, the configure script must have run (see the [install
file](INSTALL.md)).

```bash
git submodule update --init
make doc
```

An up-to-date Doxygen output can be found on
[docs.etherlab.org](https://docs.etherlab.org/ethercat/1.5/doxygen/index.html).

# Requirements

## Software requirements

Configured sources for the Linux 2.6 (or newer) kernel are required to build
the EtherCAT master.

## Hardware requirements

A table of supported hardware can be found at
http://etherlab.org/en/ethercat/hardware.php.

# Building and installing

See the [install file](INSTALL.md).

# Realtime and Tuning

Realtime patches for the Linux kernel are supported, but not required. The
realtime processing has to be done by the calling module (see API
documentation). The EtherCAT master code itself is passive (except for the
idle mode and EoE).

To avoid frame timeouts, deactivating DMA access for hard drives is
recommended (`hdparm -d0 <DEV>`).

# License

Copyright (C) 2006-2023  Florian Pose, Ingenieurgemeinschaft IgH

This file is part of the IgH EtherCAT Master.

The IgH EtherCAT Master is free software; you can redistribute it and/or
modify it under the terms of the GNU General Public License version 2, as
published by the Free Software Foundation.

The IgH EtherCAT Master is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or
FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more
details.

You should have received a copy of the GNU General Public License along with
the IgH EtherCAT Master; if not, write to the Free Software Foundation, Inc.,
51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA

---

The license mentioned above concerns the source code only. Using the EtherCAT
technology and brand is only permitted in compliance with the industrial
property and similar rights of Beckhoff Automation GmbH.

# Coding Style

Developers shall use the coding style rules in the [coding style
file](CodingStyle.md).
