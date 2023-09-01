# 1 源添加nonfree

# 2 安装驱动
``` shell
sudo apt update
sudo apt upgrade
sudo apt install nvidia-driver dia-cuda-toolkit nvidia-cuda-dev 
```

# 3 debian 12 使用了venv环境，所以使用它
```shell 
sudo  apt install python3-venv google-perftools 
# 如果没有开发工具，则
sudo  apt install curl gnupg2 git
```

 初始化Python环境
 ```shell 
 python3 -m venv ~/.venv 
 source ~/.venv/bin/activate
```

从 Git 克隆源并执行一些初始设置工作
```shell
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui 
cd stable-diffusion-webui 
PATH=$PATH:/usr/sbin python3 launch.py
```

# 3 自定义启动脚本
stable-diffusion-webui/webui-user.sh中有配置项
```shell 
# 添加 TCMalloc 的设置
PATH=$PATH:/usr/sbin 
# 指定 venv 环境
venv_dir= "$HOME/.venv" 
# 设置启动参数
# export COMMANDLINE_ARGS= "--listen --lowram --opt- sdp-attention"
```

- listen：绑定现有网络接口（IPv4），以便您可以远程连接。
    - 另一方面，如果您添加监听，您将无法通过网络界面安装扩展等。
- lowram：当您没有 16GB 实际内存（不是 VRAM）时。
- opt-sdp-attention：似乎可以加快生成速度。xformers 的替代品,使用 safetensors 的模型比使用 ckpt 的模型更稳定（加载），可能是因为没有足够的实际内存

# 4 启动方法
```shell
cd stable-diffusion-webui 
./webui.sh
```

#  5 升级stable diffusion

```shell
cd stable-diffusion-webui 
git pull
```