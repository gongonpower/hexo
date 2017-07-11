---
title: tmux vi key binding
date: 2017-07-10 10:48:13
tags:
---
## Add vi key binding to .tmux.conf
File: ~/.tmux.conf
```
unbind C-b
set -g prefix C-j
set-window-option -g mode-keys vi
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
bind-key -t vi-copy 'v' begin-selection
bind-key -t vi-copy 'y' copy-selection
set-window-option -g automatic-rename off
set-option -g allow-rename off

```
reload the conf file while in tmux:
```
<c-b>:
source-file ~/.tmux.conf
```
## tmux copy mode usage using vi key style
```
#Start copy mode
<c-b> [
#To exit the copy mode, just press <Esc> or q while in the copy mode
q
#Press j,k,h,l to navigate cursor
jkkkjh
#press v to start high light selection
v
#press y to copy content to buffer and cancel selection
y
#switch to another pane by press Ctrl-b and then h or l to navigate to another key
<c-b> h
#press Ctrl-b and then ] to paste the buffer to the target pane
<c-b> ]
```
## tmux pane zoom key
Press first time to zoom and press again to restore
```
<c-b> z
```
## Rename window key
```
<c-b> ,
```

