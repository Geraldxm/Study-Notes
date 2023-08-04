------
## 周 23/07/29 至 23/08/04

### &ensp;项目1：Win10下部署ChatGLM2-6B

- 我的obsidian链接：[[ChatGLM2-6B Win10本地部署]]
- 我的github链接：[MdText/部署/ChatGLM2-6B Win10本地部署.md](https://github.com/GeraldIAD/MdText/blob/main/%E9%83%A8%E7%BD%B2/ChatGLM2-6B%20Win10%E6%9C%AC%E5%9C%B0%E9%83%A8%E7%BD%B2.md)

### &ensp;项目2：Win10下实现ChatPDF

- 我的obsidian链接：[[langchian+ChatGLM 构建本地知识库]]
- 我的github链接：[MdText/综合开发/langchian+ChatGLM 构建本地知识库.md](https://github.com/GeraldIAD/MdText/blob/fcaf27ddd458625c65361ff974b4be338ea9f1df/%E7%BB%BC%E5%90%88%E5%BC%80%E5%8F%91/langchian%2BChatGLM%20%E6%9E%84%E5%BB%BA%E6%9C%AC%E5%9C%B0%E7%9F%A5%E8%AF%86%E5%BA%93.md)

### &ensp;项目3：通过两个昇腾微认证考试

- 我的obsidian链接：[[初识开发者套件 Atlas 200I DK A2]]
- 我的github链接：[Mdtext/学习/华为/初识开发者套件 Atlas 200I DK A2.md](https://github.com/GeraldIAD/MdText/blob/06ff37406d6736a9333e8ebab3a9c6260caa6e65/%E5%AD%A6%E4%B9%A0/%E5%8D%8E%E4%B8%BA/%E5%88%9D%E8%AF%86%E5%BC%80%E5%8F%91%E8%80%85%E5%A5%97%E4%BB%B6%20Atlas%20200I%20DK%20A2.md)

------
## 周 23/07/22 至 23/07/28

###   项目 1：收集Linux选择判断题

- 在网上收集了200道Linux选择判断题。然后使用正则表达式和手工的方式将格式改为统一格式。
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=YjZkMGQ3NDZmOTA1NDYyYTYzZWE2MzI5NmI3MmE3YmJfdldmcTlhWkpJRVZyQXY2dmo1OWRKWVcwcDU5U1pXMGdfVG9rZW46QTZkU2JLbTJ0b25vYVR4MUlvTmNhTGhrblFjXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

- 然后用将问题分割，使用GPT4的接口回答所有问题，把所有的问题和答案放到一个csv文件中。
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=N2FmMjQxM2Q1NzVkNmQ2YzE5NDBkZDM1NjNjODBiZmVfa21LdFlJUkgxYW9lbko3aG9RbnViZW8ySXJkU0RNeURfVG9rZW46R2wzYWJ4OHVab0RYejZ4aTZsdmN4eG5ubmFnXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

- 将所有问题中涉及到的知识点整理到一起，但是有些部分重复较多，还需要手工处理
    
- 将整理后的知识点用text-embedding-ada-002的接口，和原来的知识点一起生成到一个csv文件中，待后续处理
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzg2MzQ2M2Y0NmE2NDhhYTQ4NWZmYzkyZTc4YTQ2YzFfZ25TcjlkdFdtc01yeDk2ZW82alhUNDVlOW16MGtySk9fVG9rZW46WGZ3RmIzbHV3b2tYNFF4RmNtcmMwMG1nbmVmXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

###   项目 2：学习ChatGPT的API使用方法

- ChatGPT的API使用
    
    - **官方****API****说明：**https://platform.openai.com/docs/api-reference/chat/create
        
    - **Python样例代码：**https://github.com/openai/openai-cookbook/blob/main/examples/How_to_format_inputs_to_ChatGPT_models.ipynb
        
    - 请求正文中的几个较重要参数
        
        - temperature：范围0~2，数值越大越容易产生随机的结果
            
        - top_p：范围0~1，表示包含前top_p可能性的会被考虑
            
        - max_tokens：生成的chat completion所能包含的最大tokens数量
            
    
    ![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=MmU3NTliODI5ZjdmYTE0YTIyMTJmMTViNzYxNDhjMGNfQm8wYlVmMzIxQWNMSmx3OFNiYjBJeGJxdGdWN0Fjek9fVG9rZW46RnFXNmJGanFQbzhQN0l4bE55R2M1YnY3bkhiXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)
    
    - 由于网络限制等问题，不太稳定，经常无法使用，后面继续尝试别的方法
        

###   项目 3：学习Anaconda基础知识

- Anaconda本质上是一个用于环境配置的软件工具。不同环境类似于不同的空间，里面可以配置不同的python版本和不同的包
    
- 常用命令：
    
    - conda create -n [环境名] # 创建新的环境
        
        - conda create -n [环境名] python=x.x # 创建指定python版本的环境
            
    - conda info --envs # 查看系统已有的所有环境
        
    
    ![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=OWRlODY2M2JiNDcyOTQ1MDBiMWRjOGRiYWJiNjQzMDdfd0VWdXdXOWdjQURLbFVlcG1vUmR3VFBlcFY2eVhDaHFfVG9rZW46QWhyamI1TndYb0ZTS0p4MFhrWGNsRDZ2bndkXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)
    
    - Conda activate [环境名] # 激活环境
        
        - Conda list # 查看环境中的包
            
        
        ![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=MDY4NGE2YjFhOTE0MTQxNTdlN2I4ZWY3MDhhMjkyOThfbVhpclJHaDkyMjBzZ2l0eEdUT3dBWkRrN01XS2MzRG1fVG9rZW46VG1wVWI0U01hb2MzZVR4OTY0OWM2WVp4bnpoXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)
        
        - Conda install [包名] # 在该环境下安装包
            
        - Deactivate [环境名] # 退出当前环境
            
    - Conda remove -n [环境名] --all # 删除环境
        

###   项目 4：学习实现ChatPDF

###     原理：

1. 任何文本，如doc，txt，pdf等先转换成text
    
2. 将text拆分成segment，可以按照句子拆分，也可以按照固定单词数量拆分
    
3. 将拆分完毕的segment进行向量处理，得到对应embedding
    
4. 输入问题后，转为embedding向量，进行语义搜索
    
5. 将搜索得到的上下文和问题一起发送给LLM，然后显示返回结果即可
    

###     实现：

1. 先定义一个loader，解析文件内容成为一个大文本
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=YmM5N2YyZWNjOGI3N2Y5Y2IxMTZhMWJjOTRhMGMxYjhfWkhnV3V3SUNNWmJCeVVPOUdxOWw1azREbmZmMzh2OHFfVG9rZW46SVNKZWJQeVdob21UZEF4TjM1OWNHaXBHbnVjXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

2. 定义文本分块规则
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=MDk0ZmNlNjYxOTU0NTM4ZDdiZjNkZTEzYWQxYTQ4ZThfV1FsZ3dURlNEdUVuQ2h1SkJBOG0zM2VTNWxqclBSVUNfVG9rZW46TnR4VWJFTmlxb1dRRmR4VDN5TmNzb05abkRRXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

3. 使用sentence-transformers模型把文本转换为向量
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=MTJjNjAxZjJmYmFjZjRiYmY2OTFkYzRjMDg4ZjczN2FfZHV2YU9TRWhqSkRPallnMmdwOVFkazJudHU0b2F1aDNfVG9rZW46RmJ6a2JTbElkb2Uxc1l4TVBaUmNaR0F5bmNZXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

4. 用Chroma存储切分后的文本和embeddings
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=OGNmNWY5ODdhNGFiMjE3NTA1NWI3YmM4NzA4MjVjYTdfTERKZXNzWnl2cG5leExmQ3V2dW9WSkhoekphUTVQNzVfVG9rZW46UVhFOWI0d2J5bzV1b3Z4dmVRQWNUTUhlbldjXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

5. llm选择ChatOpenAI，但是在这里使用会有网络连接错误，后面转为ChatGLM2-6B
    

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2MxYzBiODg0MmUyMzVjZTJmZGExZGFjZjBjMjZjZThfTTN4blRpaVZzTHJhRDhrZFdpV0RqeXRKZXlxSzFOMURfVG9rZW46RjkyQ2JaaEMzb0pCN0Z4TnQ1ZGNEbENLbk9iXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

      报错内容：

![](https://rxoz4m0is2t.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjdkNmY2ZTUzN2I2MDBlODFlYWYxZGVhNTQ2MmE0ZjVfaWEwNmNBQXMxU3dEV2c5MGpuZ0poOXJva09KRWxIajlfVG9rZW46UVJBQmJ2eTZBbzRqamp4NXp3eGNEZXV1bk1nXzE2OTExMzA3MDQ6MTY5MTEzNDMwNF9WNA)

6. 用langchain里的chain定义流程，然后只需提问，等待回答即可