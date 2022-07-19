<center><h1>三、tmux的使用</h1></center>

<h4>1. 安装tmux</h4>

```shell
sudo apt-get install tmux
```

<h4>2. 配置tmux</h4>

```shell
cd ~
vim .tmux.conf
```

将下列配置写入`.tmux.conf`文件中

```shell
set-option -g status-keys vi
setw -g mode-keys vi

setw -g monitor-activity on

# setw -g c0-change-trigger 10
# setw -g c0-change-interval 100

# setw -g c0-change-interval 50
# setw -g c0-change-trigger  75


set-window-option -g automatic-rename on
set-option -g set-titles on
set -g history-limit 100000

#set-window-option -g utf8 on

# set command prefix
set-option -g prefix C-a
unbind-key C-b
bind-key C-a send-prefix

bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

bind -n M-Left select-pane -L
bind -n M-Right select-pane -R
bind -n M-Up select-pane -U
bind -n M-Down select-pane -D

bind < resize-pane -L 7
bind > resize-pane -R 7
bind - resize-pane -D 7
bind + resize-pane -U 7


bind-key -n M-l next-window
bind-key -n M-h previous-window



set -g status-interval 1
# status bar
set -g status-bg black
set -g status-fg blue


#set -g status-utf8 on
set -g status-justify centre
set -g status-bg default
set -g status-left " #[fg=green]#S@#H #[default]"
set -g status-left-length 20


# mouse support
# for tmux 2.1
# set -g mouse-utf8 on
set -g mouse on
#
# for previous version
#set -g mode-mouse on
#set -g mouse-resize-pane on
#set -g mouse-select-pane on
#set -g mouse-select-window on


#set -g status-right-length 25
set -g status-right "#[fg=green]%H:%M:%S #[fg=magenta]%a %m-%d #[default]"

# fix for tmux 1.9
bind '"' split-window -vc "#{pane_current_path}"
bind '%' split-window -hc "#{pane_current_path}"
bind 'c' new-window -c "#{pane_current_path}"

# run-shell "powerline-daemon -q"

# vim: ft=conf
```

<h4>3. tmux教程</h4>

* 功能：

  * 分屏
  * 允许断开`Terminal`连接后，继续运行进程

* 结构：

  * 一个`tmux`可以包含多个`session`，一个`session`可以包含多个`window`，一个`window`可以包含多个`pane`

  * 实例：

    ![image-20220719180540375](https://raw.githubusercontent.com/zrmin/BlogImages/master/images/202207191805501.png)

* 操作

  （1）`tmux`：新建一个`session`，其中包含一个`window`，`window`中包含一个`pane`，`pane`里打开了一个`shell`对话框

  （2）按下`Ctrl + a`后手指松开，然后按`%`：将当前`pane`左右平分成两个`pane`

  （3）按下`Ctrl + a`后手指松开，然后按`"`（双引号）：将当前`pane`上下平分成两个`pane`

  （4）`Ctrl + d`：关闭当前`pane`；如果当前`window`的所有`pane`均已关闭，则自动关闭`window`；如果当前`session`的所有`window`均已关闭，则自动关闭`session`

  （5）鼠标点击可以选`pane`

  （6）按下`ctrl + a`后手指松开，然后按方向键：选择相邻的`pane`

  （7）鼠标拖动`pane`之间的分割线，可以调整分割线的位置

  （8）按住`ctrl + a`的同时按方向键，可以调整`pane`之间分割线的位置

  （9）按下`ctrl + a`后手指松开，然后按`z`：将当前`pane`全屏/取消全屏

  （10）按下`ctrl + a`后手指松开，然后按`d`：挂起当前`session`

  （11）`tmux a`：打开之前挂起的`session`

  （12）按下`ctrl + a后手指松开，然后按`s`：选择其他`session`

  * 方向键——上：选择上一项`session/window/pane`
  * 方向键——下：选择下一项`session/window/pane`
  * 方向键——右：展开当前项`session/window`
  * 方向键——左：闭合当前项`session/window`

  （13）按下`ctrl + a`后手指松开，然后按`c`：在当前`session`中创建一个新的`window`

  （14）按下`ctrl + a`后手指松开，然后按`w`：选择其他`window`，操作方法与（12）完全相同

  （15）按下`ctrl + a`后手指松开，然后按`PageUp`：翻阅当前`pane`内的内容

  （16）鼠标滚轮：翻阅当前`pane`内的内容

  （17）在`tmux`中选中文本时，需要按住`shift`键。（仅支持`Windows`和`Linux`，不支持`Mac`，不过该操作并不是必须的，因此影响不大）

  （18）`tmux`中复制/粘贴文本的通用方式：

  * 按下`ctrl + a`后松开手指，然后按`[`
  * 用鼠标选中文本，被选中的文本会被自动复制到`tmux`的剪贴板
  * 按下`ctrl + a`后松开手指，然后按`]`，会将剪贴板中的内容粘贴到光标处

  

  

