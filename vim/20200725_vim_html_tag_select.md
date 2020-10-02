## vim 如何快速操作 html tag

 你可以使用vim visual model 来完成 html tag的快熟操作.

### 例子 
1. 移动光标到 html tag 内.
2. 按 v 键 进入 visual model .
3. 你可以通过 按 a+t 来选择 整个 html tag 元素，也可以通过 i+t 来选择 元素所包含的内容.

现在你可以通过 o 键或O键来跳转 到 选中内容的开头或结尾，或 键入 c 键来改变，或键入 y键来复制.

```
键入at  <tag></tag> block(选中整个元素)
it inner <tag></tag> block(元素内容不包含 开始和结束标记)
```

参考文档：
https://superuser.com/questions/189815/how-to-navigate-between-begin-and-end-html-tag-in-vim/878981#878981?newreg=e47f8bdc58884f1293f38502e9fa2ef5