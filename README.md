# 速查表
- [Git](#git)
  - [远程仓库](#远程仓库)
  - [git add 防止被大文件卡死](#git-add-防止被大文件卡死)
  - [push](#push)
  - [设置 ssh key](#设置ssh-key)
- [Linux](#linux)
  - [目录树生成](#目录树生成)
  - [查看杀死进程](#查看杀死进程)
  - [后台不挂断运行](#后台不挂断运行)
  - [延时运行命令](#延时运行命令)
  - [查看文件大小](#查看文件大小)
  - [移动目录文件](#移动目录文件)
  - [复制文件](#复制文件)
  - [解压缩文件](#解压缩文件)

## Git
### 远程仓库
```bash
git remote add <remote_name> <remote_url> # 添加
git remote set-url <remote_name> <new_remote_url> # 修改
git remote -v # 查看当前
git remote remove <remote_name> # 删除
```

---

### git add 防止被大文件卡死
* 自动只加 50M 以下文件
```bash
find . -type f -size -50M -print0 | xargs -0 git add
```

* add时使用`--verbose`参数，或缩略版`-v`:
```bash
git add -v .
```
会看到飞快滚动的被添加的文件。如果卡在哪里，说明可能太大了
然后可以修改`.gitignore`文件，例如：
```bash
*.[oa] # 忽略所有以 .a 或 .o 为扩展名的文件
!lib.a # 但是 lib.a 文件或者目录不要忽略
/TODO # 只忽略根目录下的 TODO, 子目录的 TODO 不忽略
build/ # 无论是在根目录和子目录，只要叫build/ 目录下的文件就会被忽略
doc/*.txt # 忽略 doc/.txt, 但 doc/server/.txt 不忽略
doc/**/*.pdf # 忽略 doc文件夹下所有的*.pdf
```
摘自https://xueqing.github.io/blog/git/git_ignore/


---

### push

```bash
git push <remote_name> <branch_name>
# 假如想设置upstream，保证以后默认推到这里，那么
git push -u <remote_name> <branch_name>
```


### 设置ssh key
```
# 1. 在集群的登录节点上执行
ssh-keygen -t ed25519 -C "your_email@example.com" # 这个email可以不是真实email，随便设，只是作为标识
# 出现提示后，连续按enter，默认保存到 ~/.ssh/id_ed25519

# 2. 启动ssh代理并添加密钥
eval "$(ssh-agent -s)" # 启动ssh-agent
ssh-add ~/.ssh/id_ed25519 # 添加私钥到ssh-agent

# 3. 查看并复制公钥
cat ~/.ssh/id_ed25519.pub

# 4. 添加到github: GitHub → Settings → SSH and GPG keys, 点击"New SSH key"
#    Key type: 保持默认 Authentication Key
#    Key: 粘贴刚才复制的公钥内容

# 5. 测试连接
ssh -T git@github.com
# 如果成功，会显示Hi <username>! You've successfully authenticated...
```

---

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

---

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

---

### 后台不挂断运行

```bash
nohup ./run.sh > nohup.out &
```

如果没有写权限：Permission denied

```bash
sudo chmod -R 777 dir
```

---

### 延时运行命令

```bash
sleep 2h && your_command

sleep 5m && your_command

sleep 60 && your_command
```

---

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



**使用 `du` 命令**

1. 显示当前目录下各文件夹大小：`du -h --max-depth=1`
2. 显示某个目录总大小：`du -sh /path/to/dir`
3. 只显示目录本身总大小：`du -sh .`
4. 按大小排序显示：`du -h --max-depth=1 | sort -h`

说明：

- -h 以人类可读方式显示（KB/MB/GB）
- -s 只显示总计
- --max-depth 控制目录深度

---

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

---

### 复制文件

```bash
cp <source_file> <target> # target如果是文件夹，就保持原名，不然就写到file级别指明要叫什么名

# 复制文件夹：需要-r递归
cp -r <source_dir> <target>
```

### 解压缩文件

```bash
# 解压 .tar
tar -xf archive.tar

# 解压 .tar.gz / .tgz
tar -xzf archive.tar.gz

# 解压 .zip
unzip archive.zip

# 解压到指定目录
tar -xzf archive.tar.gz -C /path/to/target/
unzip archive.zip -d /path/to/target/

# 压缩目录为 .tar.gz
tar -czf archive.tar.gz directory/

# 压缩目录为 .zip
zip -r archive.zip directory/
```
