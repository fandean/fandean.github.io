## Git中SSH和HTTPS协议的使用



访问远程仓库时可以选择SSH 或者 HTTPS协议进行访问。

(比如，与gitlab 远程仓库进行进行安全认证可选择使用ssh或者https)，两者的表现形式：

```
SSH  git@gitlab.com:faner/test01.git
HTTPS  https://gitlab.com/faner/test01.git
```


当你选择HTTPS时，会看到它有下面的一段提示"Create a personal access token on your account to pull or push via Https"简单的翻译一下就是"在您的帐户上**创建个人访问令牌**，以通过Https进行pull或push"，并且在你第一次将本地仓库push到远程仓库时会要求你输入gitlab的用户名和密码。

在一次错误中发现了这个问题：由于我的ssh的config文件出现配置错误，当我选择`git@gitlab.com:faner/test01.git`时提示有有误，我就尝试使用了https的`https://gitlab.com/faner/test01.git`路径，之后就让我输入密码并成功连接。



> 从用户操作上来看，HTTPS需要用户输入远程仓库的用户名和密码，比如需要输入gitlab的帐号和密码；SSH无需输入用户和密码。



> 错误内容：
>
> ```
> $ git push -u origin --all
> /c/Users/Fan Dean/.ssh/config line 4: garbage（垃圾） at end of line; "Dean/.ssh/FDGitHub_rsa.pub".
> fatal: Could not read from remote repository.
> 
> Please make sure you have the correct access rights
> and the repository exists.
> ```
> 错误原因是在我的Windows中，ssh配置文件中的路径`/c/Users/Fan Dean/.ssh/config`包含空格，需要使用`""包含路径`，改成如下形式`"/c/Users/Fan Dean/.ssh/config"`



> 之后遇到了第二个问题：Permission denied (publickey)
>
> ```shell
> Fan Dean@Fan-ASUS-DT MINGW64 /d/新建文件夹/Test (master)
> $ git push -u origin master
> Warning: Permanently added the RSA host key for IP address '52.167.219.168' to the list of known hosts.
> Enter passphrase for key 'C:/Users/Fan Dean/.ssh/gmail_dev_2048_id_rsa.pub':
> Permission denied (publickey).
> fatal: Could not read from remote repository.
> 
> Please make sure you have the correct access rights
> and the repository exists.
> 
> Fan Dean@Fan-ASUS-DT MINGW64 /d/新建文件夹/Test (master)
> $ ssh -T git@github.com
> The authenticity of host 'github.com (13.250.177.223)' can't be established.
> RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
> Are you sure you want to continue connecting (yes/no)? yes
> Warning: Permanently added 'github.com,13.250.177.223' (RSA) to the list of known hosts.
> Enter passphrase for key 'C:/Users/Fan Dean/.ssh/FDGitHub_rsa.pub':
> Permission denied (publickey).
> ```
> 解决方法：
>
> ssh准备连接远程服务器却遭提示” Permission denied (publickey) “, 这是由于您没有将公钥( publickey ) 添加到本地 ssh 环境造成的，或者是由于多日未进行ssh 登录操作，本地 publickey 失效造成的。我的mac os x 环境隔几天没有登录ssh 就会报 “Permission denied ” 啦。只要 使用 ssh-add 命令再次添加一下公钥即可。 [Permission denied (publickey). - CSDN博客](https://blog.csdn.net/blog_jihq/article/details/78523513 "Permission denied (publickey). - CSDN博客")
>
> ```shell
>  ssh-add ~/.ssh/id_rsa
> ```
>
> 
>
> 但是当我执行ssh-add命令后又出现下面的问题：Could not open a connection to your authentication agent.
>
> 解决方法：[git:could not open a connection to your authentication agent问题的解决（重新绑定私钥） - CSDN博客 ](https://blog.csdn.net/lizhikang2009/article/details/52188607 "git:could not open a connection to your authentication agent问题的解决(重新绑定私钥) - CSDN博客") 执行如下命令即可：
>
> ```shell
> ssh-agent bash
> ```
>
> 然后在执行上面的 `ssh-add`命令。
>
> 由于我是直接将Linux中的.ssh文件夹复制到Windows下，并且在Git Bash中进行上述操作（ssh应该是安装git时git自带的），然后就出现了上面一系列的问题。




## 添加远程仓库

### Command line instructions

Git global setup

```
git config --global user.name "Fan"
git config --global user.email "ccfan.dev@gmail.com"
```

Create a new repository

```
git clone https://gitlab.com/faner/itheima01.git
cd itheima01
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

Existing folder

```
cd existing_folder
git init
git remote add origin https://gitlab.com/faner/itheima01.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

Existing Git repository

```
cd existing_repo
git remote rename origin old-origin
git remote add origin https://gitlab.com/faner/itheima01.git
git push -u origin --all
git push -u origin --tags
```




问题：

```
.ssh/config line 3: Unsupported option "rsaauthentication"
Load key "C:/Users/Fan Dean/.ssh/GitHub_rsa.pub": invalid format
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository
```



**two different public key formats：** 

[git - key_load_public: invalid format - Stack Overflow](https://stackoverflow.com/questions/42863913/key-load-public-invalid-format "git - key_load_public: invalid format - Stack Overflow")   **two different public key formats** 

这里说，有两种格式的公钥，一种是 putty 生成的，一种是 Openssh生成的，但是之前使用 git bash时是没有问题的，后来使用了 cmder 后就就出现了问题。

public key 格式可以转换。

- OpenSSH Private Key （**我的key一直就是这种格式**）

  ```
  ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAhl/CNy9wI1GVdiHAJQV0CkHnMEqW7+Si9WYFi2fSBrsGcmqeb5EwgnhmTcPgtM5ptGBjUZR84nxjZ8SPmnLDiDyHDPIsmwLBHxcppY0fhRSGtWL5fT8DGm9EfXaO1QN8c31VU/IkD8niWA6NmHNE1qEqpph3DznVzIm3oMrongEjGw7sDP48ZTZp2saYVAKEEuGC1YYcQ1g20yESzo7aP70ZeHmQqI9nTyEAip3mL20+qHNsHfW8hJAchaUN8CwNQABJaOozYijiIUgdbtSTMRDYPi7fjhgB3bA9tBjh7cOyuU/c4M4D6o2mAVYdLAWMBkSoLG8Oel6TCcfpO/nElw== github-example-key
  ```

  

- `.ppk` (PuTTY Private Key) 

  ```
  ---- BEGIN SSH2 PUBLIC KEY ----
  Comment: "github-example-key"
  AAAAB3NzaC1yc2EAAAABJQAAAQEAhl/CNy9wI1GVdiHAJQV0CkHnMEqW7+Si9WYF
  i2fSBrsGcmqeb5EwgnhmTcPgtM5ptGBjUZR84nxjZ8SPmnLDiDyHDPIsmwLBHxcp
  pY0fhRSGtWL5fT8DGm9EfXaO1QN8c31VU/IkD8niWA6NmHNE1qEqpph3DznVzIm3
  oMrongEjGw7sDP48ZTZp2saYVAKEEuGC1YYcQ1g20yESzo7aP70ZeHmQqI9nTyEA
  ip3mL20+qHNsHfW8hJAchaUN8CwNQABJaOozYijiIUgdbtSTMRDYPi7fjhgB3bA9
  tBjh7cOyuU/c4M4D6o2mAVYdLAWMBkSoLG8Oel6TCcfpO/nElw==
  ---- END SSH2 PUBLIC KEY ----
  ```

  

排除上面的可能性。

[key_load_public: invalid format with scp or git clone on Ubuntu 15.10 - Ask Ubuntu](https://askubuntu.com/questions/698997/key-load-public-invalid-format-with-scp-or-git-clone-on-ubuntu-15-10 "key_load_public: invalid format with scp or git clone on Ubuntu 15.10 - Ask Ubuntu")

The public part is probably corrupted, so you can recreate it from private one using this command:

```
ssh-keygen -f ~/.ssh/id_rsa -y > ~/.ssh/id_rsa.pub
```

试用了上面的方法还是不行。