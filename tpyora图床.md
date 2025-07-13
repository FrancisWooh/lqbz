# PicGo搭建图床

介绍使用PicGo工具，构建github免费稳定图床，实现在Typora内撰写markdown文档时，粘贴图片就能自动上传到图传的方法

# 配置GitHub

![image-20250713163726841](D:\Note\Wiki\resource\image-20250713163726841.png)

进入自己的github账号，点击setting（全局的），选择Developer Setting，找到Token菜单，点击Generate new token按钮，选择Generate new token(classic)来生成一个常规口令。ghp_Y4hI2sz74DvDrWFDpshD3FLL4I7LyI0BahN0923

# 配置PicGo

使用PicGo有两个途径：1、在本地安装PicGo插件，完成windows配置后，在Typora中选择PicGo App方式作为image uploader。2、不安装PicGo插件，直接在Typora中选择PicGo-Core(command-line)方式来作为image upload方式，同时对data.json文件要完成配置。

本文会对两种配置方法都进行说明，但是因为英文版本的Typora只支持命令行方式，实际环境只能选用第二种方式。

![image-20250713174736038](https://raw.githubusercontent.com/FrancisWooh/lqbz/master/resource/image-20250713174736038.png)



方法一：先下载PicGo软件[PicGo is Here | PicGo](https://picgo.github.io/PicGo-Doc/zh/guide/#picgo-is-here)

完成安装后，启动软件，会anchor在windows右下任务栏。按照如下示例完成配置，然后在Typora中选择Picgo App方式就可以了

配置名随便写。仓库名就是你的github账号+仓库。Token就是前一步在github生成的。然后存储路径是需要在仓库中预先创建，如果不填，就直接放置在仓库根目录下。

![image-20250713174841881](https://raw.githubusercontent.com/FrancisWooh/lqbz/master/resource/image-20250713174841881.png)

方法二：在image页面，选中PicGo Core commandline方式后，点download，Typora会自动完成下载并将该应用集成到Typora中作为插件。

![image-20250713174128217](https://raw.githubusercontent.com/FrancisWooh/lqbz/master/resource/image-20250713174128217.png)

进入C:\Users\fancy\\.picgo  目录，对config.json进行如下修改。

```
{
  "picBed": {
	"uploader": "github", // 代表当前的默认上传图床为 jithub,
    "github": {
      "repo": "FrancisWooh/lqbz", // 仓库名，格式是 username/reponame
	  "token": "*************************", // github token
	  "path": "resource/", // 自定义存储路径，比如 img/
	  "customUrl": "", // 自定义域名，注意要加 http://或者 https://
	  "branch": "master" // 分支名，默认是 main
    }
  },
  "picgoPlugins": {}
}
```

