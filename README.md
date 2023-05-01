# rp-pico-blinky
Raspberry Pi Pico Blinky

## Description

This project is just a copy of [pico-blinky](https://github.com/rp-rs/rp-hal-boards/blob/main/boards/rp-pico/examples/pico_blinky.rs) intended to learn how to setup and build a project in rust for Raspberry Pi Pico.

## Requirements
Make sure rust is up to date by running the following command
```shell
rustup upgrade
```

Install target
```shell
rustup target add thumbv6m-none-eabi
```

Install elf2uf2-rs, this is required to create the UF2 file that bootloader uses to flash the rp-pico

```shell
cargo install elf2uf2-rs
```

Install probe-run to automatically flash rp-pico
```shell
cargo install probe-run
```

*Notes*: 
- I had to install libudev-dev to install elf2uf2-rs in Ubuntu **WSL**

```shell
sudo apt install libudev-dev
```

- By the time I'm writing this installing elf2uf2-rs fails in **Windows 10**, this will not stop you from building the project.



## Build the project

```
cargo build
```

### Mounting Pico Bootloader on WSL
Create a mounting directory
```bash
sudo mkdir /mnt/e
```
Assuming in Windows Pico drive is **E:**
```bash
sudo mount -t drvfs E: /mnt/e
```

Build and copy the project to rp-pico
```shell
cargo run
```

To do it manually

```shell
elf2uf2-rs -d target/thumbv6m-none-eabi/release/examples/pico_blinky
```

Or

```shell
elf2uf2-rs target/thumbv6m-none-eabi/debug/examples/pico_blinky /mnt/e/pico_blinky.uf2
```

## References
- [rp-hal](https://github.com/rp-rs/rp-hal)
- [rp-hal-boards](https://github.com/rp-rs/rp-hal-boards)