# Arch 安装笔记

### 系统概要

- OS：Arch linux
- WM：Hyprland
- Shell：zsh

### 系统截图
![MyArchLinux.png](https://github.com/fantaro/Knowledge-Wiki/blob/master/%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85%E7%AC%94%E8%AE%B0/MyArchLinux.png)

### 系统更新

```shell
sudo pacman -Syu
sudo pacman -Sc
paru -Syu
paru -Sc
```

### Pacman 命令说明
[软件包管理器命令对应关系](https://wiki.archlinux.org/title/Pacman/Rosetta)

---
### 安装必要软件

```shell
sudo pacman -S gcc make git bat lsd curl wget wl-clipboard xclip xsel kwalletmanager kwallet-pam fuse2
```

### 配置 Hyprland (预配置)

- KooL's
```shell
sh <(curl -L https://raw.githubusercontent.com/JaKooLit/Hyprland-Dots/main/Distro-Hyprland.sh)
```

- HyDE（备用）
```shell
pacman -S --needed base-devel
git clone --depth 1 https://github.com/HyDE-Project/HyDE ~/HyDE
cd ~/HyDE/Scripts
./install.sh
```

- ML4W（备用）
```shell
bash <(curl -s https://raw.githubusercontent.com/mylinuxforwork/dotfiles/main/setup-arch.sh)
```

### 安装 Edge 浏览器

[Edge官网](https://www.microsoft.com/ja-jp/edge)

```shell
paru -S microsoft-edge-stable-bin
```

- 进入 edge://flags 开启 Wayland 模式

```shell
echo '--ozone-platform-hint=wayland' > ~/.config/microsoft-edge-stable-flags.conf
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
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
paru dropbox ※Type 1

echo 'exec-once = dropbox' >> ~/.config/hypr/UserConfigs/Startup_Apps.conf
```
### 安装 Joplin

[Joplin官网](https://joplinapp.org)

```shell
wget -O - https://raw.githubusercontent.com/laurent22/joplin/dev/Joplin_install_and_update.sh | bash
```

### 安装中日文输入法

```shell
sudo pacman -S fcitx5 fcitx5-mozc fcitx5-configtool fcitx5-gtk fcitx5-qt fcitx5-chinese-addons noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
```

- 设置 fcitx5 自启动

```shell
echo 'exec-once = fcitx5-remote -r' >> ~/.config/hypr/UserConfigs/Startup_Apps.conf
echo 'exec-once = fcitx5 -d --replace' >> ~/.config/hypr/UserConfigs/Startup_Apps.conf
```

### 启用 Flatpak

```shell
sudo pacman -S flatpak
flatpak config --set languages "ja;zh"
```

#### ※重启系统

### 安装／移除软件 (Packages)

- 安装常用软件：

```shell
sudo pacman -S fastfetch ncdu btop tmux remmina keepassxc strawberry audacity filezilla kdenlive universal-ctags ghostty yt-dlp docker aria2
paru showmethekey
```

### 下载我的 dotfiles

```shell
cd ~/Documents
git clone https://github.com/fantaro/dotfiles
```

### 安装 Yazi

```shell
sudo pacman -S yazi ffmpeg 7zip jq poppler fd ripgrep fzf zoxide imagemagick chafa ueberzugpp
paru -S resvg
```

- 更新插件
```shell
mv ~/Documents/dotfiles/.config/yazi ~/.config/
ya pkg upgrade
```

### 安装 VSCode

```shell
paru -S visual-studio-code-bin
```

### 安装 NeoVim (LazyVim)

```shell
sudo pacman -S neovim lazygit neovide

mv ~/.config/nvim{,.bak}
mv ~/.local/share/nvim{,.bak}
mv ~/.local/state/nvim{,.bak}
mv ~/.cache/nvim{,.bak}
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git

mv ~/Documents/dotfiles/.config/nvim/lua/config/keymaps.lua ~/.config/nvim/lua/config/keymaps.lua
mv ~/Documents/dotfiles/.config/nvim/lua/config/options.lua ~/.config/nvim/lua/config/options.lua

mv ~/Documents/dotfiles/.config/neovide ~/.config/

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
mv ~/Documents/dotfiles/.config/btop ~/.config/
```

### 配置 lsd

```shell
mv ~/Documents/dotfiles/.config/lsd ~/.config/
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
mv ~/Documents/dotfiles/.config/ghostty ~/.config/
```

### 配置 fastfetch

```shell
mv ~/Documents/dotfiles/.config/fastfetch/config.jsonc ~/.config/fastfetch/config.jsonc
```

### 安装常用软件（Flatpak）

```shell
flatpak install -y flathub org.onlyoffice.desktopeditors com.obsproject.Studio com.github.unrud.VideoDownloader org.localsend.localsend_app com.jgraph.drawio.desktop org.kde.krita
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

### 安装打印机

```shell
sudo pacman -S cups cups-pdf sane-airscan simple-scan
sudo systemctl start cups.service
sudo systemctl enable cups.service
```

- 访问 http://localhost:631 添加打印机

---
## 以下为可选或参考内容

### 配置 SDDM

- 添加以下设置到 /etc/sddm.conf.d/kde_settings.conf

```shell
# echo '[General]' >> /etc/sddm.conf.d/kde_settings.conf
# echo 'GreeterEnvironment=QT_SCREEN_SCALE_FACTORS=1.5,QT_FONT_DPI=192' >> /etc/sddm.conf.d/kde_settings.conf
```

### 安装 Vim

```shell
sudo pacman -S vim gvim
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
sudo pacman -S starship
mv ~/Documents/dotfiles/.config/starship.toml ~/.config/
```

### 安装 eza

```shell
sudo pacman -S eza
mv ~/Documents/dotfiles/.config/eza ~/.config/
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
sudo pacman -S wezterm
mv ~/Documents/dotfiles/.config/wezterm ~/.config/
```

### 安装 Alacritty

```shell
sudo pacman -S alacritty
mv ~/Documents/dotfiles/.config/alacritty ~/.config/
```

### 安装 python3

```shell
sudo pacman -S python3 python3-pip
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
sudo pacman -S linux-headers
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
