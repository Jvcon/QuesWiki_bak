# WSL
## Install Ubuntu WSL

- Step1 进入控制面板->程序->启用或关闭Windows功能->适用于Linux的Windows子系统（如果自制系统镜像的话就已经启用该功能）

- Step2 通过Windows Store安装[Ubuntu](https://www.microsoft.com/store/productId/9NBLGGH4MSV6)到WSL

## Install Arch WSL

## WSL DrvFS Solution

```shell
sudo vim /etc/wsl.conf
```

```conf
[automount]
enabled = true
root = /mnt/
options = "metadata,umask=22,fmask=11"
mountFsTab = true
```
## XForwarding

```shell
sudo apt install libgtk2.0-0 libxss1 libasound2
echo 'export DISPLAY=:0.0' >> .profile
```

## VS Code with WSL

> Ref:https://spencerwoo.com/dowww/#%E5%89%8D%E8%A8%80

### 调用WSL作为终端

```json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe"
}
```

### 调用WSL的Git

- 配置VS Code

    Github：[wslgit - `Releas`](https://github.com/andy-5/wslgit/releases)

    ```json
    {
        "git.path": "C:\\$更换为 wslgit.exe 的路径$\\wslgit.exe"
    }
    ```
- 优化性能

    添加新的环境变量`WSLGIT_USE_INTERACTIVE_SHELL`设值为`0`

### 调用WSL编译调试

####　Code Runner
- 安装VS Code插件 [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)
- 配置Code Runner
    ```json
    {
        "code-runner.runInTerminal": true,
        "code-runner.terminalRoot": "/mnt/",
        "code-runner.fileDirectoryAsCwd": true,
        "code-runner.ignoreSelection": true,
        "code-runner.saveAllFilesBeforeRun": true,
        "code-runner.saveFileBeforeRun": true,
        "code-runner.executorMap": {
        "javascript": "node",
        "java": "cd $dir && javac $fileName && java $fileNameWithoutExt",
        "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
        "cpp": "cd $dir && g++ $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
        "objective-c": "cd $dir && gcc -framework Cocoa $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt",
        "php": "php",
        "python": "python3 -u",
        "perl": "perl",
        "perl6": "perl6",
        "ruby": "ruby",
        "go": "go run",
        "lua": "lua",
        "groovy": "groovy",
        "powershell": "powershell -ExecutionPolicy ByPass -File",
        "bat": "cmd /c",
        "shellscript": "bash",
        "fsharp": "fsi",
        "csharp": "scriptcs",
        "vbscript": "cscript //Nologo",
        "typescript": "ts-node",
        "coffeescript": "coffee",
        "scala": "scala",
        "swift": "swift",
        "julia": "julia",
        "crystal": "crystal",
        "ocaml": "ocaml",
        "r": "Rscript",
        "applescript": "osascript",
        "clojure": "lein exec",
        "haxe": "haxe --cwd $dirWithoutTrailingSlash --run $fileNameWithoutExt",
        "rust": "cd $dir && rustc $fileName && $dir$fileNameWithoutExt",
        "racket": "racket",
        "ahk": "autohotkey",
        "autoit": "autoit3",
        "dart": "dart",
        "pascal": "cd $dir && fpc $fileName && $dir$fileNameWithoutExt",
        "d": "cd $dir && dmd $fileName && $dir$fileNameWithoutExt",
        "haskell": "runhaskell",
        "nim": "nim compile --verbosity:0 --hints:off --run"
        },
    }
    ```
#### Python
- 安装VS Code插件 [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)


```json
{
    "python.pythonPath": "d:\\Applications\\Scoop\\apps\\wsltools\\current\\python3.exe",
    "python.linting.pylintPath": "d:\\Applications\\Scoop\\apps\\wsltools\\current\\pylint.exe",
    "python.workspaceSymbols.ctagsPath": "d:\\Applications\\Scoop\\apps\\wsltools\\current\\ctags.exe",
    "python.formatting.autopep8Path": "d:\\Applications\\Scoop\\apps\\wsltools\\current\\autopep8.exe"
}

```
#### C/C++

#### LaTex

#### Node.js

