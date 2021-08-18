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

Tmux also provide some commands, you need to use **C-:** to enter tmux command prompt first.


## Session management

There will be a tmux session in your machine, live forever until machine shutdown or you leave your tmux. You can deattch from tmux, and re-use deattched tmux session later. It is a very powerful feature for running stress test.

Description | Commands | Explanation
----------- | -------- | ------------
Creating a new naming session | tmux new -s ${SESSION NAME} | 
Opening an existed session | tmux attach -t ${SESSION NAME} | 
Listing all existed sessions | tmux ls | 
Killing session | tmux kill-session -t ${SESSION NAME} | 
-- | tmux kill-session -a | Kill all tmu sessions

## Key bindings

You also can do similar jobs in tmux, and here are commands in tmux:
Description | Key bindings | Explanation
----------- | ------------ | ------------
Naming current session | **${CTRL}-b $** / **C-b $** | 
Attaching session | **${CTRL}-b s** / **C-b s** | 
De-attaching current sessions | **${CTRL}-b d** / **C-b d** | 
Switching attached session | **${CTRL}-b (** / **C-b (** | previous session
-- | **${CTRL}-b )** / **C-b )** | next session 
-- | **${CTRL}-b s** / **C-b s** | Showing a menu to display all sessions

## Window management

### Key bindings

Description | Key bindings | Explanations
----------- | ------------ | -------------
Creating a new Window | **${CTRL}-b c** / **C-b c** | 
Closing current Window | **${CTRL}-b &** / **C-b &** | With double confirm
Renaming current window | **${CTRL}-b ,** / **C-b ,** |   
Navigating Windows | **${CTRL}-b p** / **C-b p** | previous window
-- | **${CTRL}-b n** / **C-b n** | next window
-- | **${CTRL}-b w** / **C-b w** | 
-- | **${CTRL}-b <number>** / **C-b <number>** | Showing a menu to display all panes
Changing layout | **${CTRL}-b ${META}-1** / **C-b M-1** | 所有的 panes 都垂直均分畫面
-- | **${CTRL}-b ${META}-2** / **C-b M-2** | 所有的 panes 都水平均分畫面
-- | **${CTRL}-b ${META}-3** / **C-b M-3** | 兩個水平的畫面。一個主畫面，另一個讓其他 pane 均分
-- | **${CTRL}-b ${META}-4** / **C-b M-4** | 兩個重質的畫面。一個主畫面，另一個讓其他 pane 均分
-- | **${CTRL}-b ${META}-5** / **C-b M-5** | 所有的 panes 均分畫面
-- | **${CTRL}-b ${SPACE} / **C-b ${SPACE}** | 

## Pane management

### Key bindings

Description | Key bindings | Explanations
----------- | ------------ | -------------
Splitting Panes | **${CTRL}-b "** / **C-b "** | Vertical 
-- | **${CTRL}-b %** / **C-b %** | Horizan 
Navigating Panes | **${CTRL}-b <arrow keys>** / **C-b <arrow keys> | 
-- | **{CTRL}-b o** / **C-b o | Rotate panes in current window
Zoom in / Zoom out | **${CTRL}-b z** / **C-b z** | 
Independent | **${CTRL}-b !** / **C-b !** | Making current pane into new window 
Closing panes | **${CTRL}-d** / **C-d** | Only work in shell prompt.
Closing panes | **${CTRL}-b x** / **C-b x** | With double confirm
-- | exit | Input "exit" in shell 

## Commands

These commands should be input in tmux command prompt, you need to use key binding **C-:** to open it.

Description | Commands | Explanations
----------- | -------- | -------------
Resize pane | "resize-pane -[UDLR] ${NUM}" | [UDLR] is the direction


