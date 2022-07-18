---
layout: default
title: Linux/unix system information
parent: Linux
grand_parent: Study
nav_order: 4
permalink: /docs/linux/linuxinfo
---

# Linux/unix System information
{: .no_toc }

<details markdown="block">
  <summary>
	Table of contents
  </summary>
{: .fs-3 .text-delta }

- TOC
{:toc}
</details>

---

> test OS: archlinux, ubuntu 18.04
>
> test(일부) OS: Solaris 10 (권한 제한됨)

## OS

##### OS 정보

```shell
cat /etc/*release
```

## `uname`

- print system information

### All information

```shell
uname -a
```

```
<kernel name> <host name> <kernel release> <kernel version> <architecture> <processor> <hardware platform> <OS>
```

- 시스템에 따라 출력되는 항목과 출력되지 않는 항목 있음

### Kernel name

```shell
uname
```

```shell
uname -s
```

### Host name

```shell
uname -n
```

### Kernel release

```shell
uname -r
```

### Architecture

```shell
uname -m
```

### OS

```shell
uname -o
```

## IP address

### `curl`을 통해 웹에서 제공하는 정보 이용

> solaris `curl` 지원 안 함

##### ifconfig.me

```shell
curl ifconfig.me
```

- 외부 IP address(공인 IP address)

### `ifconfig`(interface configuration)

> archlinux, solaris `ifconfig` 지원 안 함
>
> archlinux `ifconfig` 설치
>
> ```shell
> sudo pacman -S net-tools
> ```

```shell
ifconfig
```

- inet: network interface에 할당된 IP address

### `ip route`

> solaris `ip` 지원 안 함

```shell
ip route
```

## CPU Information

### /proc/cpuinfo

> solaris에 없음

- CPU information

```shell
cat /proc/cpuinfo
```

##### 장착된 CPU 개수

```shell
cat /proc/cpuinfo | grep "physical id" | sort | uniq | wc -l
```

##### CPU 모델

```shell
cat /proc/cpuinfo | grep "model name" | uniq | cut -c 14-
```

##### CPU core 개수

```shell
cat /proc/cpuinfo | grep "cpu cores" | sort | uniq | cut -c 13-
```

##### CPU thread 개수

```shell
cat /proc/cpuinfo | grep "siblings" | sort | uniq | cut -c 12-
```

### `lscpu`

> solaris `lscpu` 지원 안 함

- Display information about the CPU architecture

```shell
lscpu
```

##### CPU architecture

```shell
lscpu | grep "Arch"
```

## CPU usage

### `mpstat`

- Report processors related statistics

- CPU, core 별 사용율 모니터링

```shell
mpstat
```

##### 실시간

```shell
mpstat <interval> (<count>)
```

### `top`

> solaris 지원 안 함

- Display Linux processes

```shell
top
```

### `htop`

> 설치 필요

- Interactive process viewer

```shell
htop
```

### `prstat`

> archlinux, ubuntu 지원 안 함

- Report active process statistics

```shell
prstat
```

##### 실시간

```shell
prstat <interval> (<count>)
```

## Memory

### /proc/meminfo

> solaris에 없음

- Memory information

```shell
cat /proc/meminfo
```

### `free`

> solaris 지원 안 함

- Display amount of free and used memory in the system

```shell
free -h
```

- `h`: 읽기 편하게 조정된 단위로 출력

### `vmstat`

- Report virtual memory statistics

```shell
vmstat
```

##### 실시간

```shell
vmstat <interval> (<count>)
```

## Disk

### `lsblk` (list block)

> solaris 지원 안 함

- block device 용량

```shell
lsblk
```

### `df` (disk free)

- file system에 마운트된 용량

```shell
df -h
```

- `h`: 읽기 편하게 조정된 단위로 출력

##### 경로 지정

```shell
df -h <path>
```

- <path>가 위치한 file system 용량 출력

## PCI device

> PCI (peripheral compoponent interconnect bus)
>
> 컴퓨터 메인보드에 주변 장치를 장착하는 데 쓰이는 컴퓨터 버스의 일종

### `lspci`

> solaris 지원 안 함

- list all PCI devices

##### Graphic card

- graphic card 모델명

```shell
lspci | grep -i VGA | cut -c 36-
```
