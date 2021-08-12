Copying .tmux.conf into user home folder


NOTE
------------------------------------------------------------------------------------------

1. Default ${PREFIX} is 'CTRL + b'.
   With this configure file, ${PREFIX} is 'CTRL + w' like vim.
   
   Note: Binding with "w" will cause vim 'CTRL + w' not working, rollback to 'CTRL + b'
   

2. Default key binding for create Vertical and horizon pane are '${PREFIX} + "' and '${PREFIX} + %'
   With this configure file, key bindings are '${PREFIX} + |' and '${PREFIX} + -'


Key bindings
------------------------------------------------------------------------------------------
${CTRL} / C-							'CTRL +'
${MEAT} / M-							'ALT +'
${SHIFT} / S- 							'SHIFT +'

${PREFIX} / C-b							'CTRL + b'

Example:
==========================================================================================
${PREFIX} M-x / C-b M-x					'CTRL + b' + 'ALT + x'


Commands
------------------------------------------------------------------------------------------

Sessions
==========================================================================================
Creating a new naming session			tmux new -s ${SESSION NAME}
Opening an existed session				tmux attach -t ${SESSION NAME}
Listing all existed sessions			tmux ls


Naming current session					'${PREFIX} + $'


Attaching session						'${PREFIX} + s'
De-attaching current sessions			'${PREFIX} + d'
Switching attached session				'${PREFIX} + (' (previous) or '${PREFIX} + )'(next)




Windows
==========================================================================================
Creating a new Window					'${PREFIX} + c'

Navigating Windows						'${PREFIX} + p' (previous) / '${PREFIX} + n' (next) / '${PREFIX} + <number>' 
Changing layout							'${PREFIX} + M-[12345]'		1 - 所有的 panes 都垂直均分畫面
																	2 - 所有的 panes 都水平均分畫面
																	3 - 兩個水平的畫面。一個主畫面，另一個讓其他 pane 均分
																	4 - 兩個重質的畫面。一個主畫面，另一個讓其他 pane 均分
																	5 - 所有的 panes 均分畫面

Panes
==========================================================================================
Splitting Panes (Vertical)				'${PREFIX} + "'			'${PREFIX} + |'
Splitting Panes (Horizon)				'${PREFIX} + %'			'${PREFIX} + -'

Navigating Panes						'${PREFIX} + <arrow keys>'
Zoom in / Zoom out a pane				'${PREFIX} + z'

Resize pane								'${PREFIX} + :'		接下來要輸入指令 "resize-pane -[UDLR] ${NUM}"

Closing panes							exit or 'C - d'


Advanced Commands
------------------------------------------------------------------------------------------

