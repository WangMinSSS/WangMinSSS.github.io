#### 常用快捷键
    
    Ctrl d      # 键盘输入结束或推出终端
    Ctrl s      # 暂停当前程序，按下任意键恢复运行
    Ctrl z      # 将当前程序放到后台运行，恢复到前台的命令为 fg
    Ctrl a      # 将光标移至输入行头，相当于Home键
    Ctrl e      # 将光标移至输入行末，相当于End键
    Ctrl k      # 删除从光标所在位置到行末
    Alt Backspace   # 向前删除一个单词
    Shift PgUp  # 将终端显示向上滚动
    Shift PgDn  # 将终端显示向下滚动

#### Shell常用通配符

    *       # 匹配0或多个字符
    ?       # 匹配任意一个字符
    [list]  # 匹配list中任意单一字符
    [!list] # 匹配list中任意单一字符以外的字符
    [c1-c2] # 匹配c1-c2中任意单一字符，如：[0-9] [a-z]
    {string1,string2,...}   # 匹配其中任意一个字符串
    {c1..c2}    # 匹配c1-c2中全部字符，如{1..10}
   
#### 帮助命令
    
    man ls          # 查看命令手册
    man 1 ls        # 分区查看
    info ls         # 查看详细信息
    ls --help       # 简单查看参数

#### 常用命令1

    cd          # 前往路径 . .. ~
    pwd         # 显示当前路径
    tree        # 树形表示目录结构
    touch       # 新建文件
    mkdir       # 创建新目录
    cp          # 复制文件或者目录  -r
    rm          # 删除文件或者目录  -r
    mv          # 移动文件或者重命名文件
    rename      # 批量重命名文件
    
    cat tac     # 查看文件，正序、倒序
    more less   # 阅读文件
    head tail   # 查看文件头几行或者尾几行
    file        # 查看文件类型
    
    df          # 查看磁盘的容量
    du          # 查看目录的容量
    
    bg          # 将一个在后台暂停的命令，变成继续执行
    fg          # 将后台中的命令调至前台继续运行
    jobs        # 查看当前有多少在后台运行的命令
    ctrl + z    # 可以将一个正在前台执行的命令放到后台，并且暂停

#### 常用命令2

who
    
    -a      # 打印全部
    -d      # 打印死掉的进程
    -q      # 打印当前登陆用户数用户名
    -u      # 打印当前登陆用户信息
    
ls

    -A      # 显示包括隐藏的所有文件
    -l      # 显示完整属性
    -s      # 显示大小
    -h      # 将大小转换为比较方便的形式

#### 操作

创建一个变量，读取变量

    declare tmp         # 声明变量
#### 小工具

    w3m         # 命令行简易浏览器

#### screen后台运行程序

常用命令

    screen -S yourname -> 新建一个叫yourname的session
    screen -ls -> 列出当前所有的session
    screen -r yourname -> 回到yourname这个session
    screen -d yourname -> 远程detach某个session
    screen -d -r yourname -> 结束当前session并回到yourname这个session
    #################################
    
举例

    1.  screen -r Firework      创建分支
    2.  运行程序
    3.  ctrl+z  暂停程序放到后台
    4.  bg  将后台程序变成继续运行
    5.  screen -d   会话分离与恢复 Screen会给出detached提示
    6.  screen -ls  半个小时之后回来了，找到该screen会话
    7.  screen -r 12865 重新连接会话