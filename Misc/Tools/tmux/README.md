# Introduction

Tmux is a terminial multiplexer like GNU screen. It's easy to create multiple "pane" in one window, and multiple windows in one session.

# Common usages

There are two kinds of command for using tmux; one is running on shell, and the other is running inside tmux. To issue commands in tmux, there are some key bindings you need to know:

## Key combination

Prefix | key bindings
------ | ------------
${CTRL}- / C- | **CTRL +**
${META}- / M- | **ALT +**
${SHIFT}- / S- | **SHIFT +**

Here is some key binding examples:

Key bindings | example
------------ | -------
${CTRL}-b / C-b | **CTRL + b**
${CTRL}-b ${META}-x / C-b M-x | **CTRL + b** + **ALT + x**

You can see all key bindings with **${CTRL}-b ?**

## Tmux command

Tmux also provide some commands, you need to use **C-:** to enter tmux command prompt first. Pressing **q** to leave command mode.

# Session management

There will be a tmux session in your machine, live forever until machine shutdown or you leave your tmux. You can deattch from tmux, and re-use deattched tmux session later. It is a very powerful feature for running stress test.

## Commands

Description | Commands | Explanation
----------- | -------- | ------------
Creating a new naming session | tmux new -s ${SESSION NAME} | 
Opening an existed session | tmux attach -t ${SESSION NAME} | 
Listing all existed sessions | tmux ls | 
Killing sessions | tmux kill-session -t ${SESSION NAME} </br> tmux kill-session -a | Kill all tmux sessions

## Key bindings

You also can do similar jobs in tmux, and here are commands.

Description | Key bindings | Explanation
----------- | ------------ | ------------
Naming current session | **${CTRL}-b $** / **C-b $** | 
Attaching session | **${CTRL}-b s** / **C-b s** | 
De-attaching current sessions | **${CTRL}-b d** / **C-b d** | 
Switching attached session | **${CTRL}-b (** / **C-b (** </br> **${CTRL}-b )** / **C-b )** </br> **${CTRL}-b s** / **C-b s** | previous session </br> next session </br> Showing a menu to display all sessions
Searching | **${CTRL}-b f** / **C-b f** | Seraching key words in current session

# Window management

## Key bindings

Description | Key bindings | Explanations
----------- | ------------ | -------------
Creating a new Window | **${CTRL}-b c** / **C-b c** | 
Closing current Window | **${CTRL}-b &** / **C-b &** | With double confirm
Renaming current window | **${CTRL}-b ,** / **C-b ,** |   
Navigating Windows | **${CTRL}-b p** / **C-b p** </br> **${CTRL}-b n** / **C-b n** </br> **${CTRL}-b w** / **C-b w** </br> **${CTRL}-b ${number}** / **C-b ${number}** | previous window </br> next window </br>  </br> Showing a menu to display all panes </br> 切換到對應的 panel
Changing layout | **${CTRL}-b ${META}-1** / **C-b M-1** </br> **${CTRL}-b ${META}-2** / **C-b M-2** </br> **${CTRL}-b ${META}-3** / **C-b M-3** </br> **${CTRL}-b ${META}-4** / **C-b M-4** </br> **${CTRL}-b ${META}-5** / **C-b M-5** </br> **${CTRL}-b ${SPACE}** / **C-b ${SPACE}** | 所有的 panes 都垂直均分畫面 </br> 所有的 panes 都水平均分畫面 </br> 兩個水平的畫面。一個主畫面，另一個讓其他 pane 均分 </br> 兩個重質的畫面。一個主畫面，另一個讓其他 pane 均分 </br> 所有的 panes 均分畫面 </br> 依序改變 layout

# Pane management

## Key bindings

Description | Key bindings | Explanations
----------- | ------------ | -------------
Splitting Panes | **${CTRL}-b "** / **C-b "** </br> **${CTRL}-b %** / **C-b %** | Vertical </br> Horizan 
Navigating Panes | **${CTRL}-b ${ARROW}** / **C-b ${ARROW}** </br> **{CTRL}-b o** / **C-b o** | Moving to pane where ${ARROW} point  </br> Rotate panes in current window
Zoom in / Zoom out | **${CTRL}-b z** / **C-b z** | 
Independent | **${CTRL}-b !** / **C-b !** | Making current pane into new window 
Closing panes | **${CTRL}-b x** / **C-b x** | With double confirm

## Commands

These commands should be input in tmux command prompt, you need to use key binding **C-:** to open it.

Description | Commands | Explanations
----------- | -------- | -------------
Resize pane | "resize-pane -[UDLR] ${NUM}" | [UDLR] is the direction </br> U for up, D for Down, L for Left, and R for Right


# Copy Mode

## Key bindings

Description | Key bindings | Explanations
----------- | ------------ | -------------
Entering copy mode | **${CTRL}-b [** / **C-b [** | 
Leaving copy mode | **q** |
Starting selection | **${CTRL} SPACE** / **C SPACE** | Mark the start of data you want to copy
Selection | ${ARROW} | Using ${ARROW} to select data you want to copy
Copying selection | **${CTRL} w** / **C w** | Copying data from your mark to current cursor into buffer
Clearing selection | ESC |
Pastle lines | **${CTRL}-b ]** / **C-b ]** | Paste from buffer

All the data in buffer can only paste in tmux. Here is a way to copy it into system buffer (clipboard)

1. You need to install xclip utility
2. Adding 'bind -t vi-copy y copypipe "xclip -sel clip -i"' into you .tmux.conf file

## Commands

There are some commands to check buffers

Commands | Description
-------- | -----------
:show-buffer | Display recently copied buffer
:list-buffers | Display all copied buffer
:delete-buffer -b n | Delete n copied buffer
:capture-pane | Copying entire contents of pane into a buffer
:save-buffer ${FILE} | Copying recently copied buffer into file ${FILE}
