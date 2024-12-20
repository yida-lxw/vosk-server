# vosk-server

基于vosk-api实现的语音识别服务器端

## 环境要求
Python 3.8+
~~~shell
conda create --name py311 python=3.11
conda activate py311
# 切换到vosk-server源码根目录下
cd vosk-server
~~~

## 依赖安装
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/

## 运行说明
python asr_server.py {模型的磁盘绝对路径} <br/>
示例:
~~~Shell
python asr_server.py E:/git_workspace/vosk_test/src/main/resources/vosk-model-cn-0.22/ 127.0.0.1 2700 8000 gpu
~~~
> 5个参数依次说明: <br/>
模型的硬盘绝对路径, 必填项 , 模型下载地址:https://alphacephei.com/vosk/models <br/>
vosk-server所在主机ip或域名, 不填默认值为0.0.0.0 <br/>
vosk-server启动端口, 不填默认值为2700 <br/>
音频文件的采样率,不填默认值为8000 <br/>
使用gpu还是cpu,不填默认使用cpu   <br/>
Tips: 若使用gpu, 则需要vosk==0.3.50依赖,而vosk==0.3.50依赖不能直接通过pip进行安装,需要编译vosk-api源码到本地, <br/>
然后再引用本地的vosk==0.3.50. vosk-api 0.3.50的Python版编译安装, 请查阅vosk-api/python目录下的README.md文档

## 查看vosk-server启动进程id
~~~shell
ps -ef | grep asr_server
~~~

## 验证vosk-server是否使用到GPU
~~~shell
nvidia-smi

+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A     15634      C   python                                     9952MiB |
|    0   N/A  N/A     17005      C   python                                     3154MiB |
|    0   N/A  N/A    218312      C   python                                     1936MiB |
+---------------------------------------------------------------------------------------+
若这里出现了vosk-server的进程id(即PID), 则表明vosk-server已经使用了GPU.
~~~