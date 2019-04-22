# 7 brat 安装

 原网页：<http://brat.nlplab.org/installation.html>

本页面描述如何安装brat服务器及其第三方依赖。

（如果您已经有一个正在运行的服务器，您可能希望在下一步阅读有关标注配置的内容。）

**请注意**：您不需要安装 brat 来尝试使用它；brat 在您的浏览器中运行，并且可以使用brat主页链接的实时演示系统。

如果您希望为标注项目设置自己的本地brat安装，请遵循以下说明。

## 目录

- [快速开始](http://brat.nlplab.org/installation.html#quick_start)
- [详细说明](http://brat.nlplab.org/installation.html#detailed_instructions)
- [第三方组件](http://brat.nlplab.org/installation.html#thirdparty_components)
- [备份](http://brat.nlplab.org/installation.html#backups)

## 快速开始

以下简短的技术说明提供了一种快速、最少的方法来设置 brat 服务器。如果您不确定您的设置是否满足技术要求，请跳过本节并阅读下面的详细说明。

brat 服务器是一个 python（版本2.5+）程序，默认情况下作为CGI应用程序运行，安装脚本采用类似Unix的环境。如果要在与支持CGI的现有Web服务器兼容的环境中设置 brat 服务器，则使用CGI的快速使用说明应该有效。如果您没有安装Web服务器，并且希望在本地试用 brat，则可能需要试用独立服务器的快速使用说明。出于安全原因，我们强烈建议在生产环境中通过完整的Web服务器（如Apache）为 brat 提供服务。

首先，从首页下载 brat 安装包。

然后，解压安装包，例如在在主目录的'public_html'子目录中解压。

```
tar xzf brat-v1.3_Crunchy_Frog.tar.gz
```

接下来，进入 brat 安装文件夹。

```
cd brat-v1.3_Crunchy_Frog
```

下一步取决于您打算在CGI环境中运行 brat 还是作为独立服务器运行。

### 快速安装1：使用CGI运行

运行安装脚本并遵循指示。

```
./install.sh
```

系统将提示您输入以下信息：

- brat 用户名(例如 “editor”) 
- brat 密码 (例如 “annotate”) 
- 管理员联系邮箱 (例如 “admin@example.com”) 

最后，如果您没有以超级用户身份运行安装，脚本将提示您输入sudo密码。（这是向Web服务器分配“工作”和“数据”目录的写入权限所必需的。）

如果这样做的话，brat 的安装就完成了。既然安装了brat，如果您的系统上还没有CGI功能的Web服务器，您就必须安装和配置它。然后，您只需要确保Web服务器允许brat目录的CGI（有关说明，请参阅下面的Apache2.x部分）。

### 快速安装2：作为独立服务器运行

首先，请注意以下事项：

- brat独立服务器仅在brat v1.3及更高版本中可用。
- 独立服务器是试验性的，不应用于从Internet访问的敏感数据或系统。

以“非特权”模式运行安装脚本

```
./install.sh -u
```

并遵循说明（如上所述）。然后，启动独立服务器

```
python standalone.py
```

然后，您应该能够从standalone.py输出的地址访问brat服务器。有关详细信息，请参阅下面的独立服务器说明。

### 快速安装：接下来的步骤

在初始安装之后，您可能需要在brat安装中设置自己的一些数据。为此，请查看下面的"放入数据"部分。

如果要添加其他用户，可以编辑“config.py”文件。

如果您觉得安装需要更精细的配置，请参阅下面的“手动安装”一节。

如果在这些快速入门说明中遇到任何问题，请继续阅读以获取详细说明。您也可以查看故障排除页面。(http://brat.nlplab.org/troubleshooting.html#server-trouble) 

## 详细说明

### 预备知识

brat 服务器是用Python实现的，需要运行2.5版（或2.x系列中更高版本）的Python。如果您当前没有安装python，我们建议您在python.org的2.x系列中安装最新版本的python。

在其标准设置中，brat是通过Web服务器提供服务的。如果要在当前未运行Web服务器的计算机上安装brat服务器，则应考虑从安装一个服务器开始。brat目前是针对Apache2.x开发的，我们建议使用Apache。

为了通过 Web 服务器为 brat 提供服务，这些说明主要采用 Apache，但是如果您愿意，我们在代码仓库中也有lighttpd 配置文件，并且任何支持 CGI 的 Web 服务器都可以配置为运行 brat 服务器。

或者，您可能希望考虑使用1.3及以上版本中包含的独立实验服务器运行brat。在这种情况下，不需要Web服务器。

最后，brat服务器的这些安装说明和部分假定为类似于UNIX的环境。在大多数Linux发行版上，这些指令应该可以不做任何更改而工作。如果您运行的是OS X（Mac），请在下面的说明中注意几个特定于OS X的点。如果您运行的是Windows，运行brat服务器的最简单方法是在运行类似于Unix的操作系统（如Ubuntu）的虚拟机中。

### 手动安装

首先，下载 brat 安装包。

然后，解压安装包。

```
tar xzf brat-VERSION.tar.gz
```

(其中 `VERSION` 是版本字符串，例如 “v1.1_Albatross”)。

接下来，进入 brat 目录。

```
cd brat-VERSION
```

#### 设置工作目录

brat 服务器需要读写数据到几个目录。让我们创建它们：

```
mkdir -p data work
```

我们现在需要设置目录的权限，以便 Web 服务器能够读写它们。我们建议通过将目录分配给Apache组并设置组权限来实现这一点。要做到这一点，您需要了解Apache组。为方便确定这一点，提供了以下脚本

```
./apache-group.sh
```

（如果这不起作用，请参见本文档的“查找 Apache 2 Group”部分）。
然后，只需更改目录组（用上面得到的输出替换`${YOUR_APACHE_GROUP}`），并设置正确的权限：

```
sudo chgrp -R ${YOUR_APACHE_GROUP} data work
chmod -R g+rwx data work
```

如果您不能成功完成上述操作，或者您不关心安全性（比如说它是一个单用户系统），那么您可以运行下面的命令。这将使系统上的每个用户都可以写和读目录。（如果上述命令成功，则无需执行此操作。）

```
chmod 777 data work
```

#### 设置依赖

brat 使用 JSON 进行 client-server 通信。由于所有受支持的 Python 版本中都不包含 JSON 支持，因此您可能需要设置一个 JSON 库。

首先，您可以运行以下命令来确定python的版本：

```
python --version
```

如果您的 Python 版本是2.5或更低，则需要安装一个外部 JSON 库。从v1.2开始，brat 支持两个 JSON 库：UltraJSON 和 SimpleJSON。您只需要设置其中一个，建议使用 UltraJSON，因为它的速度要快得多。

要安装 UltraJSON，请在 brat 根目录中运行以下命令：

```
( cd server/lib/ && unzip ujson-1.18.zip && cd ujson-1.18 &&
  python setup.py build && mv build/lib.*/ ../ujson )
```

如果失败，或者您更喜欢 simplejson，请将 simplejson 安装为：

```
( cd server/lib && tar xfz simplejson-2.1.5.tar.gz )
```

标准 brat 操作不需要设置其他库。

（如果您需要日文标记化技术支持，请设置 MeCab，包含在“external/”目录中。）

#### brat 服务器配置

brat 服务器的总体配置由 brat 根目录中的“config.py”控制。此配置文件在运行“install.sh”时自动创建，但可以按以下方式手动设置：

由配置模板生成配置文件：

```
cp config_template.py config.py
```

使用您最喜欢的文本编辑器编辑配置文件，例如：

```
emacs config.py
```

安装的详细说明包含在配置文件本身中。

#### brat 独立服务器

从1.3版开始，brat 包括一个独立的实验服务器。这是运行 brat 服务器的另一种选择，brat 服务器不需要单独的Web服务器（如 Apache），而且速度可以大大加快，在某些情况下，服务器响应时间减少了90%。

但是，独立服务器目前没有像 brat 的其他服务器那样经过安全性强化或全面测试。因此，我们强烈建议通过完整的 Web 服务器（如生产环境中的Apache）、涉及敏感数据的项目以及从 Internet 访问的系统为 brat 提供服务。

在标准安装中，brat 独立服务器通常可以如下方法运行：

```
APACHE_USER=`./apache-user.sh`
sudo -u $APACHE_USER python standalone.py
```

（此命令将提示输入密码。）

更详细地说：要运行独立服务器，需要在brat目录中执行脚本“standalone.py”。此脚本应具有对工作目录的写入权限（通常为`work/`和`data/`）。如果您已经使用'install.sh'或根据工作目录部分中的说明设置了这些目录，那么Apache用户应该可以写它们（如果存在）。上面尝试确定apache的用户名（`./apache user.sh`），然后作为这个用户运行`standalone.py`（`sudo-u`）。

如果没有安装Apache，则可以使用如下命令运行：

```
sudo -u USER python standalone.py
```

其中'user'是对brat work 和 data 目录具有写权限的任何用户。

### 放入数据

您的安装现在应该已经准备好了，只需将您的数据放在`data`目录中，并像上面所做的那样使用`chmod`确保它具有正确的权限。

您可以将数据文件直接放在`data`目录中，也可以在`data`下创建目录结构。我们建议为您正在处理的每个（版本A）语料库在`data`中创建一个子目录。

brat 以独立格式存储其数据，每个文档使用两个文件：一个包含文档文本的`.txt`文件（UTF-8编码）和一个包含标注的`.ann`文件。要启动一个新的标注项目，只需将`.txt`文件放在所需的位置，并创建一个与每个`.txt`对应的空`.ann`文件。在`data`目录中复制`.txt`文件后，可以按如下方式创建`.ann`文件：

```
find data -name '*.txt' | sed -e 's|\.txt|.ann|g' | xargs touch
```

（还请记住为这些文件设置写权限。）

现在，您可以通过使用受支持的Web浏览器从Web服务器检索 brat 目录或`index.xhtml`文件来访问 brat。

## 第三方组件

这部分主要聚焦在Ubuntu系统上，但是这些说明应该很容易地适用于其他基于`*nix`的系统。

### Apache 2.x

brat 支持 FastCGI，它可以将安装速度提高大约x10，因为您不必为每个请求调用Python解释器。
如果您想使用 FastCGI 而不是 cgi，请注意与之相关的配置标注。

注意：brat中的 FastCGI 支持仍然是一些实验性的，并且存在一些已知的问题，特别是与在更改配置文件时重新加载系统方面的失败有关。我们建议只对固定的标注配置使用 FastCGI。

为了使用 FastCGI，你需要安装[flup](http://trac.saddi.com/flup) Python 库：

```
( cd server/lib/ && tar xfz flup-1.0.2.tar.gz )
```

如果您还没有安装，请安装 Apache 2.x：

```
sudo apt-get install apache2
```

从这里开始，OS X和其他类似Unix的系统（如Linux）的设置过程就不同了。请检查下面与您的系统相关的部分。

#### 在类UNIX系统上设置 Apache（非苹果mac系统）

接下来编辑配置文件：

```
sudo vim /etc/apache2/httpd.conf
```

如果你在home的`public_html`子目录中安装brat，添加如下内容：

```
<Directory /home/*/public_html>
    AllowOverride Options Indexes FileInfo Limit
    AddType application/xhtml+xml .xhtml
    AddType font/ttf .ttf
    # For CGI support
    AddHandler cgi-script .cgi
    # Comment out the line above and uncomment the line below for FastCGI
    #AddHandler fastcgi-script fcgi
</Directory>

# For FastCGI, Single user installs should be fine with anything over 8
#FastCgiConfig -maxProcesses 16
```

如果你没有在home的`public_html`子目录中安装brat，只要对应调整上面的目录 ( `<Directory /home/*/public_html>`)。

如果你在home的`public_html`子目录中安装brat，要确保userdir模块已经启用。

```
sudo a2enmod userdir
```

对于 FastCGI，您还需要安装其模块，然后添加它和我们用于将cgi请求重定向到 FastCGI 的“重写”模块：

```
sudo apt-get install libapache2-mod-fastcgi
sudo a2enmod fastcgi
sudo a2enmod rewrite
```

最后一个 FastCGI 步骤在brat安装目录的`.htaccess`中详细介绍，它涉及取消标注和配置`rewrite`模块。

最后告诉Apache2.x加载新的配置。

```
sudo /etc/init.d/apache2 reload
```

#### 在苹果 Mac OS X 系统上配置 Apache

接下来编辑配置文件：

```
sudo vim /etc/apache2/users/USER.conf
```

 `USER` 是你的用户名。

I如果要将brat安装到主目录中的“sites”目录中，请确保包含以下内容：

```
<Directory "/Users/USER/Sites/">
   Options Indexes MultiViews FollowSymLinks
   Order allow,deny
   Allow from all

   AllowOverride Options Indexes FileInfo Limit
   AddHandler cgi-script .cgi
   AddType application/xhtml+xml .xhtml
   AddType font/ttf .ttf
</Directory>
```

 `USER` 还是你的用户名。

最后重启apache。

```
sudo apachectl restart
```

（对于 FastCGI，我们目前正在尝试确定一个在OS X上工作的配置，一旦完成，我们就会提供说明。）

### 寻找 Apache 2 Group

理想情况下，您应该根据需要为Apache2组设置所有权限，但发现这可能会很痛苦。

了解 Apache 组名是什么，通常是“apache”或“www data”；可以在“apache2.conf”或“httpd.conf”中找到，位于`/etc/apache2/`或`/etc/httpd/`。假设它是“www-data”。然后：

```
sudo chgrp -R www-data data work
chmod -R g+rwx data work
```

实际上，由于Linux分段的乐趣，您也可以在其他地方找到这个组。下面是一个小的启发式方法，它至少在两个Linux发行版上工作：

```
locate --regex '(apache2|httpd)\.conf$' | xargs cat | grep 'Group'
```

如果你从中得到的看起来很奇怪（像一个变量），比如说前面有一个$，试试这个：

```
locate envvars | grep -E '(apache2|httpd)' | grep '/etc/' \
    | xargs cat | grep -i 'group'
```

如果这不起作用，请进入`/etc/group`并希望您能找到至少看起来像'apache'或'www data`的内容：

```
cat /etc/group | cut -d : -f 1 | sort
```

## Back-ups 备份

有一个脚本可以与“cron”一起使用。如下所示。

为您的Apache用户在crontab中添加一行：

```
0 5 * * * ${PATH_TO_brat_INSTALLATION}/tools/backup.py
```

现在，您将在每天早上五点在工作目录中创建备份。