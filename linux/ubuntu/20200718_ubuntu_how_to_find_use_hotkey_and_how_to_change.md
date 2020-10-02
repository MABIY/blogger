- [查找与替换](#查找与替换)
<!-- ## ubuntu 如何查询某个快捷键被使用及如何禁用或修改  -->
> 适用采用 Debian configuration system 的linxu 发行版如 debain,ubuntu ...
### 查找与替换
查找快捷键以s结尾的设置
```shell
gsettings list-recursively | grep -i \>s\'

result:

org.gnome.shell.extensions.screenshot-window-sizer cycle-screenshot-sizes-backward ['<Shift><Alt><Control>s']
org.gnome.shell.extensions.screenshot-window-sizer cycle-screenshot-sizes ['<Alt><Control>s']
org.gnome.settings-daemon.plugins.media-keys screenreader '<Alt><Super>s'
org.gnome.shell.keybindings toggle-overview ['<Super>s']
```
替换 org.gnome.shell.keybindings toggle-overview ['<Super>s'] 快捷键

```shell
# 禁用 <Super>s 快捷键对应功能使用
gsettings set org.gnome.shell.keybindings toggle-overview  "[]" 
# 还原<Super>s 快捷键功能的使用
gsettings set org.gnome.shell.keybindings toggle-overview  "['<Super>s']" 
```
