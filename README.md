# 速查表

## 查看/杀死进程

```linux
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



## 后台不挂断运行

```bash
nohup ./run.sh > nohup.out &
```

如果没有写权限：Permission denied

```bash
sudo chmod -R 777 dir
```



## 延时运行命令

```bash
sleep 2h && your_command

sleep 5m && your_command

sleep 60 && your_command
```



## 查看文件大小

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



## 移动目录/文件

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
