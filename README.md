# 前言
轻量级 Vim 配置框架，全中文注释，这既是一份合理的轻量级配置，更是一份简明教程。话说，网上的 Vim 配置多的数不过来，这里又做一个干嘛？这些配置都有一些问题：

- 注释不够，很多配置就是劈里啪啦一堆 VimScript 看的人一头雾水，新人顶多只能 “用”，没法跟着 “学”。
- 大部分都是针对 Vim 7 以前的版本，太过陈旧，对 8.0/8.1 以后的各种现代编辑器特征支持不足。
- 模块化不够好，全部塞在一个几百行的 `vimrc` 文件里，各部分搅在一起，增改都比较麻烦。
- 插件没有分组，不能根据需要灵活选择功能组，所有插件一上就全上了，要禁止就是进去注释代码。
- 它们有很多错误的地方，比如中文编码都没设对，很多 Windows 下的 PowerShell 脚本都打开不了。
- 错误的习惯，比如把 jk 映射成 ESC 的，顺着从 a 打倒 z 都打不流畅，输入个 `Dijkstra` 都输入不了。
- 对 C/C++ 开发支持不足。

还有不少插件自己给设置门槛的，比如把方向键禁用掉，我见过很多才用 Vim 的新人，大部分都呆在插入模式下，保存文件才会退出一下，至少人家开始用了，等到熟练了，该用 hjkl 的时候自然会去用。你这上来就把方向键和鼠标禁止了，除了阻挡新人外，我不知道有什么作用。

总之，山寨居多，还有某些著名的广为流传的 Vim 配置，我都不想点名了，把 Leader 键映射成逗号了，它不知道逗号/分号在 Vim 里是用来定位 f/t 搜索的下一个/上一个结果的么？就和 n/N 定位斜杠搜索一样。把 Leader 定义成空格我都还觉得挺科学，定义成逗号和分号的这些配置，是在把错误的用法源源不断的交给未来的新用户。

所以网上缺一份合理的轻量级配置，适合新人学习那种，于是有了这个项目。


# 安装

将项目克隆到你喜欢的目录内，比如 `~/.vim` 内：

```bash
cd ~/.vim
git clone https://github.com/skywind3000/vim-init.git
```

然后创建你的 `~/.vimrc` 文件，里面只有一句话：

```VimL
source ~/.vim/vim-init/init.vim
```

请调整你的终端软件，确保对 ALT 键的支持，以及 Backspace 键发送正确扫描码：

[终端软件下正确支持 ALT 键和 Backspace 键](https://github.com/skywind3000/vim-init/wiki/Setup-terminals-to-support-ALT-and-Backspace-correctly)

然后启动 Vim，在命令行运行 `:PlugInstall` 安装依赖插件即可。

# 结构

本配置按顺序，由如下几个主要模块组成：

- `init.vim`: 配置入口，设置 runtimepath 检测脚本路径，加载其他脚本。
- `init-basic.vim`: 所有人都能同意的基础配置，去除任何按键和样式定义，保证能用于 `tiny` 模式（没有 `+eval`）。
- `init-config.vim`: 支持 +eval 的非 tiny 配置，初始化 ALT 键支持，功能键键盘码，备份，终端兼容等
- `init-tabsize.vim`: 制表符宽度，是否展开空格等，因为个人差异太大，单独一个文件好更改。
- `init-plugin.vim`: 插件，使用 vim-plug，按照设定的插件分组进行配置。
- `init-style.vim`: 色彩主题，高亮优化，状态栏，更紧凑的标签栏文字等和显示相关的东西。
- `init-keymaps.vim`: 快捷键定义。

最好 fork 一份到你自己的仓库，然后不断修改，把它修改成你自己的东西，平时要更新时到这里同步下上游仓库，然后自己合并一下即可。

除去 vim-plug 额外安装的插件外，本配置自带一些依赖较大的[插件](https://github.com/skywind3000/vim-init/wiki/Integrated-Plugins)，保证内网连不了网的情况下，把本配置压缩包解压一下就能跑得起来，且基本功能可用，它们都比较简单，往往一两个文件，分布于 `plugin` 和 `autoload` 两个目录中，你可以根据自己需要增改。

# 帮助

既然是全中文注释，帮助主要看 [init-keymaps.vim](https://github.com/skywind3000/vim-init/blob/master/init/init-keymaps.vim) 和 [init-plugins.vim](https://github.com/skywind3000/vim-init/blob/master/init/init-plugins.vim) 两个文件，每个点我都写满了注释了，也是未来你自己可能修改的最多的两个文件。每次你修改或者调试了单个 .vim 配置文件后，命令行输入 `:so %` 即可重新载入，so 是 `source` 的简写，意思是加载脚本，`%` 代表当前正在编辑脚本的名字。

# Credit

TODO


# 我改进后的配置

## 主题配色

更新了 PaperColor 主题，默认使用 PaperColor。主题修改位于文件 ./init/init-style.vim 中

## 修改了默认的 TAB 和空格

使得所有类型文件的 tab 均为 4 个空格，不再使用 '\t'。修改位于文件 ./init/init-tabsize.vim 中

## 增加了部分个人的配置

如：开启相对行号、高亮第 80 列、根据符号进行折行展示。修改位于文件 ./init/init-config.vim 中

## 安装 YCM 的笔记

在 `./init/init-plugins.vim` 插件文件中，增加 YCM 插件。使用 :PlugInstall 安装，失败的话，运行 :PlugClean 并删除 `.vim/bundle/YouCompleteMe/` 文件夹，重新安装。直到成功安装，安装完成后。需要进入文件夹内，进行相应地编译操作。

对 C 系语言使用 libclang：

cd ~/.vim/bundle/YouCompleteMe
./install.py --clang-completer

对 C 系语言使用 clangd：

cd ~/.vim/bundle/YouCompleteMe
./install.py --clangd-completer

libclang 和 clangd 可以同时安装，除非再配置中使用 `let g:ycm_use_clangd = 0` 命令禁止了 clangd，否则将默认使用 clangd 进行补全。

不需要支持 C 系：

cd ~/.vim/bundle/YouCompleteMe
./install.py

YCM 还支持一些其他语言：

- C#：install Mono with Homebrew or by downloading the Mono macOS package and add --cs-completer when calling install.py.
- Java: install JDK8 (version 8 required) and add --java-completer when calling install.py.
- JavaScript and TypeScript: install Node.js and npm and add --ts-completer when calling install.py.
- Go：install Go and add --go-completer when calling install.py.
- Rust：add --rust-completer when calling install.py.
If your Python interpreter is older than 2.7.9, you will also need rustup in your PATH.

如果你需要尽可能多的支持，那么你需要使用 --all 选项。注意，--all 中并不包含 --clangd-completer

cd ~/.vim/bundle/YouCompleteMe
./install.py --all

# 增加时间统计功能，wakatime 插件（默认不开启）

在 `./init/init-plugins.vim` 插件文件中，增加了 wakatime 用来统计时间。

# 与远程库同步更新

步骤：1、配置上游项目地址。即将你 fork 的项目的地址给配置到自己的项目上。比如我 fork 了一个项目，原项目是 wabish/fork-demo.git，我的项目就是 cobish/fork-demo.git。使用以下命令来配置。
```
➜ git remote add upstream https://github.com/wabish/fork-demo.git
```
然后可以查看一下配置状况，很好，上游项目的地址已经被加进来了。
```
➜ git remote -v
origin  git@github.com:cobish/fork-demo.git (fetch)
origin  git@github.com:cobish/fork-demo.git (push)
upstream    https://github.com/wabish/fork-demo.git (fetch)
upstream    https://github.com/wabish/fork-demo.git (push)
```
2、获取上游项目更新。使用 fetch 命令更新，fetch 后会被存储在一个本地分支 upstream/master 上。➜ git fetch upstream

3、合并到本地分支。切换到 master 分支，合并 upstream/master 分支。➜ git merge upstream/master

4、提交推送。根据自己情况提交推送自己项目的代码。➜ git push origin master
由于项目已经配置了上游项目的地址，所以如果 fork 的项目再次更新，重复步骤 2、3、4即可。
