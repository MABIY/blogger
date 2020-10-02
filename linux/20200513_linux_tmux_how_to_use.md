<!-- ## tmux  -->

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [tmux简介](#tmux%E7%AE%80%E4%BB%8B)
  - [功能特性](#%E5%8A%9F%E8%83%BD%E7%89%B9%E6%80%A7)
- [安装 tmux](#%E5%AE%89%E8%A3%85-tmux)
- [安装 tmux 插件管理 Tmux Plugin Manager](#%E5%AE%89%E8%A3%85-tmux-%E6%8F%92%E4%BB%B6%E7%AE%A1%E7%90%86-Tmux-Plugin-Manager)
- [通过 tmux-yank plugin 从 ssh 远程机器复制文本](#%E9%80%9A%E8%BF%87-tmux-yank-plugin-%E4%BB%8E-ssh-%E8%BF%9C%E7%A8%8B%E6%9C%BA%E5%99%A8%E5%A4%8D%E5%88%B6%E6%96%87%E6%9C%AC)

<!-- /code_chunk_output -->

### [tmux简介](https://github.com/tmux/tmux)
tmux 是一个终端复用器类自由软件，功能类似 GNU Screen，但使用 BSD 许可发布。用户可以通过 tmux 在一个终端内管理多个分离的会话，窗口及面板，对于同时使用多个命令行，或多个任务时非常方便。
#### 功能特性
* 一个虚拟终端可以管理多个会话，窗口和面板
* 支持分屏，同时处理多个操作
* 窗口、面板可以在会话间自由移动，切换
* 丰富灵活的状态行展示
* 支持自定义快捷键，依照个人习惯配置令操作更高效
* 不受断网影响，避免丢失重要工作进度
* 结对编程，方便演示与协作
* 自带复制粘贴缓冲区管理
* 脚本化配置，可配置多种操作环境
### 安装 tmux
* ubuntu
  ```shell
   ➜ sudo apt install -y tmux
  ```

### 安装 tmux 插件管理 [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm)
* ubuntu
  ```shell
  #运行 tmux
  ➜ tmux
  # git clone
  ➜ git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
  ```
  
  把下面的文本放在~/.tmux.conf底部
  ```shell
  # List of plugins
  set -g @plugin 'tmux-plugins/tpm'
  set -g @plugin 'tmux-plugins/tmux-sensible'

  # Other examples:
  # set -g @plugin 'github_username/plugin_name'
  # set -g @plugin 'git@github.com/user/plugin'
  # set -g @plugin 'git@bitbucket.com/user/plugin'
  
  # Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
  run -b '~/.tmux/plugins/tpm/tpm'
  ```
  重新加载tmux环境,以获取tpm支持
  ```shell
  # type this in terminal if tmux is already running
  ➜ tmux source ~/.tmux.conf
  ```
### 通过 tmux-yank plugin 从 ssh 远程机器复制文本
* ubuntu 安装 [tmux-yank](https://github.com/tmux-plugins/tmux-yank)

  把下面的文本放在~/.tmux.conf里
  ```shell
  set -g @plugin 'tmux-plugins/tmux-yank'
  # 启用 vi 快捷键 方式
  set-window-option -g mode-keys vi
  ```
  重新加载tmux环境
  ```shell
  # type this in terminal if tmux is already running
  ➜ tmux source ~/.tmux.conf
  ```
  使用prefix–I(先按ctrl+b松开按键再按I)快捷键来安装 tmux-yank.

  复制操作如下:
  第一步 登录远程服务器：ssh lh@192.168.0.103 登录成功
  第二步 打开文件： vim test.sh（只能复制一屏幕内容，如果想复制全文本cat test.sh,然后进行复制）
  第三步 先按ctrl+b 松开后按 [ 键位 启用复制。
  第四步 通过 hjkl 移动 选择开始位置
  第五步 按空格键后通过 hjkl 来选择待复制文本
  第六步 y键 完成服务，在本地就可以粘贴获取的文本了
  第四部 可以换成 shift +v 来选择行 然后直接 y件获取文本.



   