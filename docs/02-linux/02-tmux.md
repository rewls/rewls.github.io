---
layout: default
title: Tmux
parent: Linux
nav_order: 2
---

# Tmux
{: .no_toc }

> [참고](https://tmuxguide.readthedocs.io/en/latest/tmux/tmux.html)

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

### Installation

```
sudo apt-get install tmux
```

### .tmux.conf

> 먼저 `📁home`에 `📝.tmux.conf`를 만든다.

```
# ~/.tmux.conf

# unbind default prefix and set it to ctrl-a
unbind C-b
set -g prefix C-a
bind C-a send-prefix

# make delay shorter
set -sg escape-time 0

#### key bindings ####

# reload config file
bind r source-file ~/.tmux.conf \; display ".tmux.conf reloaded!"

# quickly open a new window
bind N new-window

# synchronize all panes in a window
bind y setw synchronize-panes

# pane movement shortcuts (same as vim)
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# enable mouse support for switching panes/windows
set -g mouse on

#### copy mode: vim ####

# set vi mode for copy mode
setw -g mode-keys vi

# copy mode using 'ESC'
unbind [
bind Escape copy-mode

# start selection with 'space' and copy using 'y'
bind-key -Tcopy-mode-vi 'v' send -X begin-selection
bind-key -Tcopy-mode-vi 'y' send -X copy-pipe-and-canfel "xclip -i -sel c"

# paste using 'p'
unbind p
bind p paste-buffer
```

| command                                            | Description                |
|----------------------------------------------------|----------------------------|
| set -g                                             | set option                 |
| setw -g                                            | set window option          |
| bind [-cnr] [-t key-table] key command [arguments] | bind key                   |
| unbind-key [-acn] [-t key-table] key               | unbind key                 |
| setw sychronize-panes on                           | set all opened pane option |

### Basic

| Command                     | Description                           |
|-----------------------------|---------------------------------------|
| tmux                        | start tmux                            |
| tmux new -s <name>          | start tmux with <name>                |
| tmux ls                     | show the list of sessions             |
| tmux a #                    | attach the deched-session             |
| tmux a -t <name>            | attach the detached-session to <name> |
| tmux kill-session -t <name> | kill the session <name>               |
| tmux kill-server            | kill the tmux server                  |

---

> ctrl-a를 누른 뒤 아래 표의 명령어를 입력한다.

### Help

| command | Description               |
|---------|---------------------------|
| ?       | show the list of commands |

### Reload

| Command | Description            |
|---------|------------------------|
| r       | reload .tmux.conf file |

### Sessions

> tmux 안의 터미널에서 exit 입력하면 나올 수 있다.

| Command | Description    |
|---------|----------------|
| s       | list sessions  |
| $       | rename session |
| d       | detach session |

### Windows

> ctrl-d는 ctrl-a 누르지 않고 사용되며 window나 pane을 닫는다.

| Command | Description                 |
|---------|-----------------------------|
| w       | list windows and select one |
| ,       | rename window               |
| c or N  | create new window           |
| n       | go to next window           |
| p       | go to previous window       |
| f       | find window                 |
| &       | kill window                 |
| 0-9     | go to window 0-9            |
| l       | go to list window           |
| f       | search window name          |

### Panes(split windows)

| Command    | Description                                    |
|------------|------------------------------------------------|
| %          | vertical split                                 |
| "          | horizontal split                               |
| x          | kill pane                                      |
| o          | go to next pane                                |
| h, j, k, l | go to next pane in vim-style                   |
| z          | toggle full-screen mode for current pane       |
| arrow keys | resize the pane(go to left/down/up/right pane) |
| q          | show pane-numbers                              |
| spase      | change pane layout                             |

### Commands

| Command | Description        |
|---------|--------------------|
| :       | go to command mode |

그 다음 아래의 명령어를 입력한다.

| Command             | Description                 |
|---------------------|-----------------------------|
| list-panes          | show the names of all panes |
| resize-pane -D 20   | resize down                 |
| resize-pane -U 20   | resize up                   |
| resize-pane -L 20   | resize left                 |
| resize-pane -R 20   | resize right                |
| swap-pane -s 3 -t 1 | swap pane '1' with pane '3' |
|

### Copy mode

Esc를 누르면 copy mode에 들어가도록`📝.tmux.conf`에 설정했다.

| Command | Description     |
|---------|-----------------|
| Esc     | go to copy mode |

아래의 명령어는 ctrl-a를 누르지 않고 사용한다.

| Command    | Description                           |
|------------|---------------------------------------|
| q          | quit mode                             |
| j, k, l, h | down, up, right, left                 |
| J or K     | scroll down or up                     |
| F or B     | go to next or previous page
| $          | go to end of line                     |
| 0          | go to beginning of line               |
| w or b     | go to next or previous word           |
| / or ?     | search forward or backward            |
| n          | search next(use after above commands) |
| space      | start selection                       |
| Esc        | clear selection                       |
| y          | copysections                          |

아래의 명령어는 ctrl-a와 함께 사용한다.

| Command | Description     |
|---------|-----------------|
| p       | paste selection |


