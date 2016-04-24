# Context
- basic usage
- programming

---
# Summary
对编辑器的功能要求:
- 文件操作: 打开(C-x C-f), 关闭(C-x C-c), 保存(C-x C-s)
- 光标操作: 移动(C-b/f/n/p), 全选(C-x h), 选中(C-space), 翻页(C/M-v)
- 编辑操作: 插入, 删除(C-d, del), 撤销(C-/), 剪切(C-k, C-w), 复制(M-w), 粘贴(C-y)
- 搜索(C-s/r), 替换
- 标签/窗口管理(C-x 1/2/3/o)
- 编码要求:
    - 注释, 取消注释
    - 语法高亮, 自动缩进, 自动补全
    - 目录视图
    - 函数提示, 跳转定义, 跳转声明

---
# Part I - basic usage
- c->ctrl 
- m->alt(offical) cmd(max port)
- C-->>byte,line(none language)
- M-->>word,sentence,paragraph(language)

### Movement
```
// page down
C-v 
// page up
M-v
// move cursor to center/top/bottom
C-l

// back/froward/previous/next
C-b/f/p/n
// move by word
M-b/f

// move to line start/end
C-a/e
// move to sentence start/end
M-a/e

// move page start/end
M-</>
```

### Manipulation Text
```
// repeat input char
M-number + <char>

// delete char before/after
<del> / C-d

// delete word before/after
M-<del> / M-d

// delete from cursor to line/sentence end
C-k / M-k
 
// select and kill
C-space // start choose, then move cursor
C-w // kill the chosen part

// copy
M-w // kill-ring-save

// yanking召回, 重新插入被移除(kill)的字符
C-y
// 若要召回再之前移除的文字, 则在c-y之后使用m-y
M-y

// undo
C-/

// search
C-s // 向前搜索
C-r // 向后搜索
// 搜索中再次按C-s跳转光标, 按C-g回到初始位置, 按enter保留当前位置
```

### Buffer
```
// open file
C-x C-f

// save file
C-x C-s
// 保存多个缓冲区
C-x s

// 列出缓冲区
C-x C-b
// 选择缓冲区
C-x b

// 离开
C-x 1 // 只保留一个窗口

// 跳转窗格(同一窗口下, 多个buffer)
C-x o // o -> other
// 在一个窗口编辑, 翻页另一个窗口
C-M v
C-M-S v

// 多窗口
M-x make-frame
```

### Command
```
// exit
C-x C-c

// repeat commands
C-u + number + <command>
M-number + <command>
// Exception: 
// roll number lines, not pages
C-u number C/M-v

// cancel command
C-g

// leave only one window
C-x 1

// help
C-h c + <command>
C-h k + <key> // 在新窗格显示函数名称和文档
C-h f + <func>
C-h v + <var> // 显示变量
C-h a + <command>
```

## Extend command
```
C-x 字符扩展
M-x 命令名扩展

// 在终端中, 挂起程序但不杀死, 切换任务完成后, 使用"fg"或"%emacs"返回
C-z
```

---
# Part II - programming
