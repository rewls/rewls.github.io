---
layout: default
title: Check Specifications in Linux
parent: Linux
nav_order: 4
---

# Check Specifications in Linux
{: .no_toc }

<details open markdown="block">
  <summary>
    Toggle
  </summary>
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
</details>

---

## IP 주소

- IP 주소

	```shell
	curl ifconfig.me
	```

## CPU

- CPU 정보

	```shell
	cat /proc/cpuinfo
	```

	```shell
	lscpu
	```

- 장착된 CPU 개수

	```shell
	cat /proc/cpuinfo | grep "physical id" | sort | uniq | wc -l
	```

- CPU 모델

	```shell
	cat /proc/cpuinfo | grep "model name" | uniq | cut -c 14-
	```
- CPU architecture

	```shell
	arch
	```

	```shell
	lscpu | grep "Arch"
	```

- CPU core 개수

	```shell
	cat /proc/cpuinfo | grep "cpu cores" | sort | uniq | cut -c 13-
	```

- CPU thread 개수

	```shell
	cat /proc/cpuinfo | grep "siblings" | sort | uniq | cut -c 12-
	```

## Memory

- memory 정보

	```shell
	cat /proc/meminfo
	```

	```shell
	free -h
	```

## Disk

- block device 용량

	```shell
	lsblk
	```

	- lsblk(list block)

- file system에 마운트된 용량

	```shell
	df . -h
	```

	- df(disk free)

	- `h` : human readable output

## Graphic card

- graphic card 모델명

	```shell
	lspci | grep -i VGA | cut -c 36-
	```

## Linux 배포판

- linux 배포판 정보

	```shell
	cat /etc/*release
	```
