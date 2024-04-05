# （2）Demo实战



## Lagent智能体

## 部署internLM2-chat-7B

### 创建开发机

- SSH
- 直接进入开发机

### 终端配置环境

- bash命令行获取demo

  - ```bash
    bash /root/share/install_conda_env_internlm_base.sh internlm-demo  # 执行该脚本文件来安装项目实验环境
    ```

- 激活环境

  - ```
    conda activate internlm-demo
    ```

- 安装依赖

  - ```
    python -m pip install --upgrade pip
    
    pip install modelscope==1.9.5
    pip install transformers==4.35.2
    pip install streamlit==1.24.0
    pip install sentencepiece==0.1.99
    pip install accelerate==0.24.1
    ```

### 模型下载

```
mkdir -p /root/model/Shanghai_AI_Laboratory
cp -r /root/share/temp/model_repos/internlm-chat-7b /root/model/Shanghai_AI_Laboratory
```

python /root/model/download.py

```
import torch
from modelscope import snapshot_download, AutoModel, AutoTokenizer
import os
model_dir = snapshot_download('Shanghai_AI_Laboratory/internlm-chat-7b', cache_dir='/root/model', revision='v1.0.3')
```

### 代码准备

- `clone` 代码

```
cd /root/code
git clone https://gitee.com/internlm/InternLM.git
```

- 切换 commit 版本

```
cd InternLM
git checkout 3028f07cb79e5b1d7342f4ad8d11efad3fd13d17
```

- 将 `/root/code/InternLM/web_demo.py` 中 29 行和 33 行的模型更换为本地的 `/root/model/Shanghai_AI_Laboratory/internlm-chat-7b`。

### 终端运行

- 新建一个 `cli_demo.py` 文件
- python /root/code/InternLM/cli_demo.py

### web demo 运行

- 运行 `/root/code/InternLM` 目录的 `web_demo.py` 文件
- 本地浏览器输入 `http://127.0.0.1:6006`
- 问题：/root/.conda/envs/internlm-demo/lib/python3.10/site-packages/torch/_utils.py:776: UserWarning: TypedStorage is deprecated. It will be removed in the future and UntypedStorage will be the only storage class. This should only matter to you if you are using storages directly.  To access UntypedStorage directly, use tensor.untyped_storage() instead of tensor.storage()
    return self.fget.__get__(instance, owner)()
-  参考方案：
  - [zomehwh/sovits-models · TypedStorage is deprecated. It will be removed in the future and UntypedStorage will be the only storage class. (huggingface.co)](https://huggingface.co/spaces/zomehwh/sovits-models/discussions/10)
  - [repeated warning `UserWarning: TypedStorage is deprecated` · Issue #97207 · pytorch/pytorch · GitHub](https://github.com/pytorch/pytorch/issues/97207)


## Demo测试

- internlm2-chat-1_8b
- 创作一个 300 字的小故事
- ![](C:/Users/LTstatu/Desktop/Capture d’écran 2024-04-05 181609.png)

## web demo

### 连结SSH

- 先查询端口，再根据端口键入命令 
- 复制密码

### 安装openSSH

1. 打开 PowerShell 作为管理员。在开始菜单中搜索 PowerShell，并右键单击它，然后选择“以管理员身份运行”。
2. 在 PowerShell 中运行以下命令来安装 OpenSSH 客户端：

```
bashCopy code
Add-WindowsCapability -Online -Name OpenSSH.Client
```

### 路径问题

1. **使用完整路径运行 SSH 客户端**：如果您知道 SSH 客户端的安装路径，可以在 PowerShell 中使用完整路径来运行它。例如，如果您使用的是 OpenSSH 客户端并且安装在默认位置，您可以尝试以下命令：

```
bashCopy code
C:\Windows\System32\OpenSSH\ssh -CNg -L 6006:127.0.0.1:6006 root@ssh.intern-ai.org.cn -p 41361
```

2. 将 SSH 客户端的路径添加到系统环境变量中

3. streamlit问题

   ```
   streamlit run /root/Tutorial/helloworld/bajie_chat.py --server.address 127.0.0.1 --server.port 6006 bash: streamlit: command not found
   ```

   ```
   pip install streamlit
   ```

   **确保 `bajie_chat.py` 存在**：确认您要运行的 Python 脚本 `bajie_chat.py` 是否存在于指定的路径 `/root/Tutorial/helloworld/` 中，并且文件名拼写正确。

   **使用绝对路径**：作为一种临时解决方案，您可以尝试使用 `streamlit` 的绝对路径来运行它，而不是依赖系统路径。例如：

   ```
   bashCopy code
   /root/your/path/to/streamlit run /root/Tutorial/helloworld/bajie_chat.py --server.addre
   ```

### 连结时长

- 在本地powershell中输入ssh -CNg -L 6006:127.0.0.1:6006 root@ssh.intern-ai.org.cn -p 41361，很长时间才有相应
- 且没有密码验证
- 但是效果ok

![](C:/Users/LTstatu/Desktop/Capture d’écran 2024-04-05 211559.png)

![](C:/Users/LTstatu/Desktop/Capture d’écran 2024-04-05 212046.png)
