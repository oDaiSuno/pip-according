# 🛠️安装记录： NerfStudio on Windows11

# 2024-09-09

****

## 版本号

```
python==3.8
pip install torch==2.1.2+cu118
torchvision==0.16.2+cu118
cmake==3.29.1
Visual Studio 2019
```

---

## 安装过程

1. 基础环境安装
   
   ```
   conda create --name nerfstudio -y python=3.8
   conda activate nerfstudio
   python -m pip install --upgrade pip
   ```

2. 安装PyTorch
   
   ```
   pip install torch==2.1.2+cu118 torchvision==0.16.2+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
   ```

3. 安装 `ninja`
   - git clone,下载[ninja](https://github.com/ninja-build/ninja/releases) `https://github.com/ninja-build/ninja/releases`
   
     ```
     git clone https://github.com/ninja-build/ninja.git
     ```
   
   - 打开vs2022命令行工具
   
     ![](E:\Docs\Markdown\pip-according\nerfstudio\images\img.png)

   - cd到`ninja目录`
   - 运行编译命令`python configure.py --bootstrap`
   - 添加环境变量`ninja目录`到Path
   
     ![img.png](images/ninja.png)
   
4. 安装 `tiny-cuda-nn` ：
   
   - git clone 
   
     ```
     git clone --recursive https://github.com/nvlabs/tiny-cuda-nn
     cd tiny-cuda-nn
     ```
   
   - 安装pytorch扩展（使用 **Developer Command Prompt for VS 2019**打开）
     ![img.png](images/develop.png)
   
     ```
     cd tiny-cuda-nn/bindings/torch
     conda activate nerfstudio
     ```
     
   - 执行`python setup.py install`
   - 执行过程中可能出现： `“Error compiling objects for extension”` ，需要修改`tiny-cuda-nn\bindings\torch\setup.py`中的内容：
     
     ```
     # cmdclass={"build_ext": BuildExtension}
     # 修改为
     cmdclass={'build_ext': BuildExtension.with_options(use_ninja=False)}
     ```
   - 如果仍旧报错，运行一下命令转换`msvc`到x64版本
     ```
     "C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Auxiliary\Build\vcvarsall.bat" X64
5. 安装nerfstudio
    ```
    pip install nerfstudio
    ```
