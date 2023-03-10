
## 利用npm 发布包

发布包之前你首先要有一个npm的账号

### 第一次发布包：

在终端输入npm adduser，提示输入账号，密码和邮箱，然后将提示创建成功

### 非第一次发布包：

在终端输入npm login，然后输入你创建的账号和密码，和邮箱，登陆

【注意】npm adduser成功的时候默认你已经登陆了，所以不需要再接着npm login.

**例子：**

（因为我已经创建过账号了，所以直接登录）

1. 进入项目目录下，然后再登陆：

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202446840-1610696376.png)

2. 通过npm publish发包

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202514403-849332036.png)

包的名称和版本就是你项目里package.json里的name和version哦！

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202540872-285752890.png)

3. 然后你到npm的搜索里就可以找到被发布的APP啦！

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202554387-223704071.png)

**【注意点1】不能和已有的包的名字重名！**

例如我尝试把包名改成'react'显然已有的包：

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202622778-691361295.png)

然后发包的时候就会...

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202701200-1982551319.png)

(翻译：你没有发布react包的权限，请问你是以react所有者的身份登陆的吗？)

【提示】在发包前可以通过npm的搜索引擎查找是否已存在相同名称的包

**【注意点2】还有一点要注意的是npm对包名的限制：不能有大写字母/空格/下滑线!**

(其实在上面的例子中我原本打算写成penghuwanAPP的，报错。。。改成penghuwan_app，又报错，最后不得不改成penghuwanapp。。。)

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202724981-936653704.png)

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202749747-1696746026.png)

**【注意点3】你的项目里有部分私密的代码不想发布到npm上？**

将它写入.gitignore 或.npmignore中，上传就会被忽略了

## 利用npm撤销发布包

这里要说一点，取消发布包可能并不像你想象得那么容易，这种操作是受到诸多限制的，撤销发布的包被认为是一种不好的行为

**（试想一下你撤销了发布的包[假设它已经在社区内有了一定程度的影响]，这对那些已经深度使用并依赖你发布的包的团队是件多么崩溃的事情！）**

示例：

我现在将之前发布的包penghuwanapp撤销掉：输入npm unpublish 包名

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202809872-2061110882.png)

 【吐槽】注意看红框框住的字，你就知道npm官方撤销已发布的包对这种行为的态度了....

 【注意】如果报权限方面的错，加上--force

再去npm搜索已经搜不到了

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202853184-1883393075.png)

1. 根据规范，只有在发包的**24小时内才允许**撤销发布的包（ unpublish is only allowed with versions published in the last 24 hours）

2. **即使**你撤销了发布的包，**发包的时候也不能再和被撤销的包的名称和版本重复了**（即不能名称相同，版本相同，因为这两者构成的唯一标识已经被“占用”了）

例如我在撤销包后尝试再发布同一名称+同一版本的包：

![](https://images2015.cnblogs.com/blog/1060770/201706/1060770-20170609202937153-1561244414.png)

报错，并建议我修改包的版本

**npm unpublish的推荐替代命令：npm deprecate <pkg>[@<version>] <message>**

使用这个命令，**并不会在社区里撤销你已有的包，但会在任何人尝试安装这个包的时候得到警告**

例如：npm deprecate penghuwanapp '这个包我已经不再维护了哟～'