# OpenSUSE 安装笔记

### 系统概要
- OS：OpenSUSE Tumbleweed
- DE：KDE
- WM：KWIN
- Shell：zsh

### 系统截图
![MyOpenSUSE.png](https://github.com/fantaro/Knowledge-Wiki/blob/master/%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85%E7%AC%94%E8%AE%B0/MyOpenSUSE.png)

### 系统更新

```shell
sudo zypper dup
sudo zypper clean
```
或者
```shell
sudo zypper refresh
sudo zypper update
sudo zypper clean
```

### Zypper 命令说明
[软件包管理器命令对应关系](https://wiki.archlinux.org/title/Pacman/Rosetta)

---
### 安装必要软件
```shell
sudo zypper install gcc gcc-c++ make libopenssl-3-devel libopenssl-devel libappindicator3-1 git bat lsd curl wget wl-clipboard xclip xsel libfuse2 fetchmsttfonts
```

### 安装 Edge 浏览器

[Edge官网](https://www.microsoft.com/ja-jp/edge)

```shell
sudo zypper addrepo -f --gpgcheck-allow-unsigned https://packages.microsoft.com/yumrepos/edge/ edge-yum
sudo zypper refresh
sudo zypper install microsoft-edge-stable
```

### 安装 Brave 浏览器

[Brave官网](https://brave.com/ja)

```shell
curl -fsS https://dl.brave.com/install.sh | sh
```

- 进入 brave://flags 开启 Wayland 模式

### 安装 Dropbox

[Dropbox官网](https://www.dropbox.com)

```shell
sudo zypper install dropbox dolphin-plugins
```
### 安装 Joplin

[Joplin官网](https://joplinapp.org)

```shell
wget -O - https://raw.githubusercontent.com/laurent22/joplin/dev/Joplin_install_and_update.sh | bash
```

### 设置系统语言

- 使用 YaST 设置系统语言

### 安装中日文输入法

```shell
sudo zypper install fcitx5 fcitx5-chinese-addons fcitx5-configtool fcitx5-configtool-kcm6 fcitx5-gtk3 fcitx5-gtk4 fcitx5-mozc fcitx5-qt5 fcitx5-qt6 fcitx5-table-extra fcitx5-table-other
```

### 启用 Flatpak

```shell
sudo zypper install flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak config --set languages "ja;zh"
```

#### ※重启系统

### 安装／移除软件 (Packages)

- 移除不需要的软件：

```shell
sudo zypper remove -u firefox ibus
```

- 安装常用软件：

```shell
sudo zypper install fastfetch ncdu btop tmux remmina keepassxc strawberry audacity filezilla kdenlive universal-ctags ghostty yt-dlp docker aria2
```

### 下载我的 dotfiles

```shell
cd ~/Documents
git clone https://github.com/fantaro/dotfiles
```

### 安装 zsh
```shell
sudo zypper install zsh
zsh --version
chsh -s $(which zsh)
```

- 登出再登入
- 进入终端并对zsh做初期设置
- 确认zsh版本

```shell
echo $SHELL
$SHELL --version
```

### 安装 Oh My Zsh
```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
mv ~/Documents/dotfiles/.zshrc ~/
```

- 更新 Oh My Zsh
```shell
omz update
```

### 安装 Rust

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
sudo zypper install rustup
cargo install cargo-update
rustup update stable
rustup default stable
```

- 更新 Rust 本身和已安装软件
```shell
rustup update
cargo install-update -a
```

### 安装 Yazi

```shell
sudo zypper install ueberzugpp ffmpeg 7zip jq ripgrep fzf zoxide ImageMagick chafa fd poppler-tools ouch
cargo install --locked yazi-fm yazi-cli
```

- 更新插件
```shell
mv ~/Documents/dotfiles/dotconfig/yazi ~/.config/
ya pkg upgrade
```

### 安装 pokemon-colorscripts

```shell
cd ~/Documents
git clone https://gitlab.com/phoneybadger/pokemon-colorscripts.git
cd pokemon-colorscripts
sudo ./install.sh
pokemon-colorscripts
cd ..
rm -rf pokemon-colorscripts
```

### 安装 VSCode

```shell
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper addrepo -f https://packages.microsoft.com/yumrepos/vscode vscode
sudo zypper refresh
sudo zypper install code
```

### 安装 NeoVim (LazyVim)

```shell
sudo zypper in neovim lazygit neovide

mv ~/.config/nvim{,.bak}
mv ~/.local/share/nvim{,.bak}
mv ~/.local/state/nvim{,.bak}
mv ~/.cache/nvim{,.bak}
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git

mv ~/Documents/dotfiles/dotconfig/nvim/lua/config/keymaps.lua ~/.config/nvim/lua/config/keymaps.lua
mv ~/Documents/dotfiles/dotconfig/nvim/lua/config/options.lua ~/.config/nvim/lua/config/options.lua

mv ~/Documents/dotfiles/dotconfig/neovide ~/.config/

nvim
```

- 别名

```alias
alias vi=vim
alias vim=nvim
```

- 设置为主编辑器
```shell
export EDITOR=/usr/bin/nvim
export SUDO_EDITOR=/usr/bin/nvim
```

### 安装 Virtualbox

```shell
sudo zypper install virtualbox virtualbox-guest-tools
```

### 配置 tmux

```shell
mv ~/Documents/dotfiles/.tmux.conf ~/
```

### 配置 aria2

```shell
mv ~/Documents/dotfiles/.aria2 ~/
```

### 配置 btop

```shell
mv ~/Documents/dotfiles/dotconfig/btop ~/.config/
```

### 配置 lsd

```shell
mv ~/Documents/dotfiles/dotconfig/lsd ~/.config/
```

- 别名

```alias
alias ls=lsd
alias ll='ls -l'
alias la='ls -a'
alias lla='ls -la'
alias lt='ls --tree'
alias lta='ls -a --tree'
```

### 配置 Ghostty

```shell
mv ~/Documents/dotfiles/dotconfig/ghostty ~/.config/
```

### 配置 fastfetch

```shell
mv ~/Documents/dotfiles/dotconfig/fastfetch/config.jsonc ~/.config/fastfetch/config.jsonc
```

### 安装常用软件（Flatpak）

```shell
flatpak install -y flathub org.onlyoffice.desktopeditors com.obsproject.Studio com.github.unrud.VideoDownloader org.localsend.localsend_app com.jgraph.drawio.desktop
```

- 更新 Flatpak 软件
```shell
sudo flatpak update
```

- 如果 Flatpak 软件安装后出现乱码
```shell
flatpak run --command=fc-cache {AppName} -f -v
```

### 安装字体

```shell
wget -P ~/.local/share/fonts https://github.com/subframe7536/maple-font/releases/download/vx.0/MapleMono-NF-CN-unhinted.zip \
&& wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/vx.x.0/FantasqueSansMono.zip \
&& wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/vx.x.0/FiraMono.zip \
&& cd ~/.local/share/fonts \
&& unzip MapleMono-NF-CN-unhinted.zip \
&& unzip FantasqueSansMono.zip \
&& unzip FiraMono.zip \
&& rm MapleMono-NF-CN-unhinted.zip \
&& rm FantasqueSansMono.zip \
&& rm FiraMono.zip \
&& fc-cache -fv
```

- MapleMono 下载地址：[MapleMono Downloads](https://github.com/subframe7536/maple-font)
- Nerdfonts 下载地址：[Nerdfonts Downloads](https://www.nerdfonts.com/font-downloads)

---
## 以下为可选或参考内容

### 配置 SDDM

- 添加以下设置到 /etc/sddm.conf.d/kde_settings.conf

```shell
# echo '[General]' >> /etc/sddm.conf.d/kde_settings.conf
# echo 'GreeterEnvironment=QT_SCREEN_SCALE_FACTORS=1.5,QT_FONT_DPI=192' >> /etc/sddm.conf.d/kde_settings.conf
```

### 安装 kwin 插件：Kröhnkite

[Kröhnkite 插件说明](https://github.com/anametologin/krohnkite#readme)

- 导入自定义快捷键
  
  - KDEシステム設定　➡　キーボード　➡　ショートカット　➡　Import...
  - ~/Documents/dotfiles/dotconfig/KDE_Keymaps.kksrc


### 安装 Vim

```shell
sudo zypper install vim gvim
mkdir -p ~/.vim/autoload/
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
mv ~/Documents/dotfiles/.vimrc ~/
vim
:PlugInstall
```

- 别名

```alias
alias vi=vim
```

- 设置为主编辑器
```shell
export EDITOR=/usr/bin/vim
export SUDO_EDITOR=/usr/bin/vim
```

### 安装 starship

```shell
sudo zypper install starship
mv ~/Documents/dotfiles/dotconfig/starship.toml ~/.config/
```

- 更新 shell 配置

```shell
cd ~
cat .bashrc
echo >> .bashrc
echo 'if command -v starship &> /dev/null; then' >> .bashrc
echo '  eval "$(starship init bash)"' >> .bashrc
echo 'fi' >> .bashrc
cat .bashrc
```

### 安装 eza

```shell
sudo zypper install eza
mv ~/Documents/dotfiles/dotconfig/eza ~/.config/
```

- 别名

```alias
alias ls='eza --icons'
alias ll='eza -l --icons'
alias la='eza -a --icons'
alias lla='eza -al --icons'
alias lt='eza --tree --icons'
alias lta='eza -a --tree --icons'
alias lt1='eza --tree --level=1 --icons'
alias lta1='eza --tree --level=1 --icons'
```

### 配置 Docker

```shell
sudo systemctl start docker
mkdir ~/Docker
cd ~/Docker
unzip ~/Dropbox/Software/Utility/WindowsInDocker.zip
sudo docker compose up

sudo systemctl stop docker
```

### 安装 WezTerm

```shell
sudo zypper install wezterm
mv ~/Documents/dotfiles/dotconfig/wezterm ~/.config/
```

### 安装 Alacritty

```shell
sudo zypper install alacritty
mv ~/Documents/dotfiles/dotconfig/alacritty ~/.config/
```

### 安装 python3

```shell
sudo zypper install python3 python3-pip
```

### 升级 Python 库

```shell
pip3 install --upgrade pip
```

- 如果出现 `error: externally-managed-environment` 错误，执行以下步骤

```shell
mkdir ~/.config/pip
vi ~/.config/pip/pip.conf
echo '[global]' >> ~/.config/pip/pip.conf
echo 'break-system-packages = true' >> ~/.config/pip/pip.conf
```

- 安装需要的库：

```shell
pip3 install pandas
pip3 install Jupyter
pip3 install jupyterlab
pip3 install pip-review
~/.local/bin/pip-review --auto --continue-on-fail
```

### 安装 微信

下载 WeChat-AppImage 版的 X86 AppImage

[Linux版微信官网](https://linux.weixin.qq.com/)

```shell
chmod u+x WeChatLinux_x86_64.AppImage
./WeChatLinux_x86_64.AppImage --appimage-extract
cd squashfs-root/opt/wechat/
sudo execstack -c ./*.so
./AppRun
```

### 安装 Anaconda

```shell
bash Anaconda3-yyyy.mm-Linux-x86_64.sh
conda upgrade --all
conda clean --packages
```

### 安装 VMware Workstation

```shell
sudo bash ./VMware-Workstation-Full-xxxx.x86_64.bundle
# System service scripts directory: /etc/systemd/system
sudo zypper install kernel-default-devel
```

### 手动卸载 VMware Workstation

1. 列出已安装的 vmware 包：
   ```shell
   rpm -qa | grep vmware
   ```
2. 其他检查：
   ```shell
   ls /usr/bin | grep vmware
   ls /usr/sbin | grep vmware
   vmware --version
   ```
3. 停止 VMware 服务：
   ```shell
   sudo systemctl stop vmware.service
   sudo systemctl stop vmware-USBArbitrator.service
   sudo systemctl status vmware
   ```
4. 卸载 VMware：
   - 列出产品：
     ```shell
     vmware-installer --list-products
     ```
   - 卸载 Workstation：
     ```shell
     sudo vmware-installer -u vmware-workstation
     ```
   - 卸载 Player：
     ```shell
     sudo vmware-installer -u vmware-player
     ```
   - 扩展命令：
     ```shell
     sudo /usr/bin/vmware-installer --uninstall-product=vmware-workstation
     ```
5. 删除配置文件：
   ```shell
   sudo rm -rf /etc/vmware*
   sudo rm -rf /usr/lib/vmware*
   sudo rm -rf /usr/share/doc/*vmware
   sudo rm -rf /usr/bin/vmware-usbarbitrator
   sudo rm -rf /usr/bin/vmnet*
   sudo rm -rf /usr/bin/vmware*
   sudo rm -rf /usr/share/applications/vmware*
   ```

#### 编译 vmware-host-modules

```shell
git clone https://github.com/mkubecek/vmware-host-modules
cd vmware-host-modules
git checkout workstation-17.0.0
sudo make; sudo make install
```
