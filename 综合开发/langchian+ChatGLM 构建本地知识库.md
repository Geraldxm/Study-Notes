## 进展和步骤

- clone包，chatglm2-2b模型和text2vec的包

- 为了解决路径问题，不预先下载chatglm的模型，而从网站上调用时才下载

- 修改 `langchain-ChatGLM/configs/model_config.py`中的`"text2vec": "text2vec"` 

- 修改 `LLM_MODEL = "chatglm2-6b"` 

- 如果出现网络问题错误提示，多次重试即可
- 使用了知识库的检索![[chatpdf_webui_testcss.jpg]]
- 未使用知识库的检索![[chatpdf_webui_testcss 1.jpg]]

## 问题和解决

- 需要在服务器上安装git lfs才可以管理大文件，暂无权限

- 将 `configs/model_config.py` 中chagtlm2-6b模型的本地路径设置为 `none` 即可，此时默认从huggingface上下载

- 下载模型的时候报网络错误，多次重试即可

## 参考文章

1. [LangChain + ChatGLM2-6B 搭建个人专属知识库 (baidu.com)](https://baijiahao.baidu.com/s?id=1771368707788465976&wfr=spider&for=pc)

2. [chatchat-space/langchain-ChatGLM: langchain-ChatGLM, local knowledge based ChatGLM with langchain ｜ 基于本地知识库的 ChatGLM 问答 (github.com)](https://github.com/chatchat-space/langchain-ChatGLM)