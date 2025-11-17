# 速查表
## Git
### 远程仓库
```bash
git remote add <remote_name> <remote_url> # 添加
git remote set-url <remote_name> <new_remote_url> # 修改
git remote -v # 查看当前
git remote remove <remote_name> # 删除
```



### git add自动只加50M以下的文件

```bash
find . -type f -size -50M -print0 | xargs -0 git add
```



### push

```bash
git push <remote_name> <branch_name>
# 假如想设置upstream，保证以后默认推到这里，那么
git push -u <remote_name> <branch_name>
```



## Linux

### 目录树生成

| 功能                                | Windows             | Linux                         | macOS                         |
| ----------------------------------- | ------------------- | ----------------------------- | ----------------------------- |
| **安装方式**                        | 无需安装            | `sudo apt install tree`       | `brew install tree`           |
| **显示目录树（基础）**              | `tree`              | `tree`                        | `tree`                        |
| **显示文件**                        | `tree /F`           | 默认显示                      | 默认显示                      |
| **显示隐藏文件**                    | 不支持              | `tree -a`                     | `tree -a`                     |
| **使用 ASCII 绘图字符（避免乱码）** | `tree /A`           | `tree --charset=ASCII` 或默认 | `tree --charset=ASCII` 或默认 |
| **限制目录深度**                    | 不支持              | `tree -L 2`                   | `tree -L 2`                   |
| **显示完整路径**                    | 不支持              | `tree -f`                     | `tree -f`                     |
| **显示文件大小**                    | 不支持              | `tree -s`                     | `tree -s`                     |
| **显示权限/所有者等信息**           | 不支持              | `tree -pug`                   | `tree -pug`                   |
| **输出到文件**                      | `tree /F > out.txt` | `tree > out.txt`              | `tree > out.txt`              |



### 查看/杀死进程

```bash
ps -ef | grep python
```

杀死进程

```bash
kill 12345
```

默认是 `SIGTERM`（优雅退出），进程可以自行处理关闭。

如果程序没反应：

```bash
kill -9 12345
```

`-9` 是 `SIGKILL`，强制杀死进程，无法被捕获。



### 后台不挂断运行

```bash
nohup ./run.sh > nohup.out &
```

如果没有写权限：Permission denied

```bash
sudo chmod -R 777 dir
```



### 延时运行命令

```bash
sleep 2h && your_command

sleep 5m && your_command

sleep 60 && your_command
```



### 查看文件大小

**使用 `ls` 命令**

```bash
ls -lh
```

- `-l`：以长列表形式显示
- `-h`：人类可读的单位（KB、MB、GB）

比如：

```bash
ls -lh /path/to/folder
```

会显示该目录下每个文件的大小。



### 移动目录/文件

**移动文件**
```bash
mv file.txt /home/user/
```
把 `file.txt` 移动到 `/home/user/` 目录下（保持文件名不变）  

**移动目录**

```bash
mv my_folder /home/user/
```
把整个 `my_folder` 目录移动到 `/home/user/` 里。

**移动并重命名**

```bash
mv file.txt newfile.txt
```
把 `file.txt` 移动到当前目录下，并改名成 `newfile.txt`；或者同时改名并换位置：

```bash
mv file.txt /home/user/newfile.txt
```



### 复制文件

```bash
cp <source_file> <target> # target如果是文件夹，就保持原名，不然就写到file级别指明要叫什么名

# 复制文件夹：需要-r递归
cp -r <source_dir> <target>
```
