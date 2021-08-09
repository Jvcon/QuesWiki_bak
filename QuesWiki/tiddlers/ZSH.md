> zsh oh-my-zsh zsh-autosuggestions zsh-syntax-highlighting

- zsh & Oh-my-zsh
先在root用户下安装，再在普通用户安装
    ```shell
    sudo apt install zsh
    sudo chsh -s $(which zsh)
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    ```
- zsh-autosuggestions
    ```shell
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    vim ~/.zshrc
    ```
    ```conf
    plugins=(
        zsh-autosuggestions
        )
    ```
- zsh-syntax-highlighting
    ```shell
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    vim ~/.zshrc
    ```
    ```conf
    plugins=(
        zsh-autosuggestions
        zsh-syntax-highlighting
        )
    ```