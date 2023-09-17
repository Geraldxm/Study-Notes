## 在pycharm中

- ### 配置解释器

配置项目的解释器时，如果该项目使用了conda环境，选择`先前配置的解释器`，在里面选择`conda-[以前创建的环境]`即可。

- 终端

如果终端中未成功打开conda环境，先进入`Anaconda Prompt`命令行，执行
```conda
conda init powershell
```
按提示操作即可。

## 基本使用方式

- Anaconda本质上是一个用于环境配置的软件工具。不同环境类似于不同的空间，里面可以配置不同的python版本和不同的包

### 常用命令：

- conda create -n [环境名] # 创建新的环境

- conda create -n [环境名] python=x.x # 创建指定python版本的环境

- conda info --envs # 查看系统已有的所有环境

- conda list # 查看环境中的包

- conda install [包名] # 在该环境下安装包

- conda deactivate [环境名] # 退出当前环境

- conda remove -n [环境名] --all # 删除环境