# Introduction

The purpose of this book is to document a bespoke installation of Arch Linux on a desktop computer. Specific goals included:

1. Enhancing security without compromising normal usage too much
2. Protecting data from hardware failure, accidents, and bitrot
3. Dual booting with Windows

It is divided into 0x (system setup), and 1y (user setup).

## Hardware

The most significant choices here are:

* x86 Platform
* Intel or AMD GPU because [Nvidia does not support the standard GBM interface][nvidia-support]
* External drives or cloud storage for backups

[nvidia-support]: https://github.com/swaywm/sway/issues/490
