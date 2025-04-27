# OpenSUSE 安装笔记

### 系统概要
- OS：OpenSUSE Tumbleweed
- DE：KDE
- WM：KWIN
- Shell：zsh

### 系统更新

```shell
sudo zypper dup
```
或者
```shell
sudo zypper refresh
sudo zypper update
```

### 安装 Edge 浏览器

- 使用现有浏览器下载 Edge 浏览器

### 安装 Brave 浏览器
```shell
sudo zypper install curl
curl -fsS https://dl.brave.com/install.sh | sh
```

- 进入 brave://flags 开启 Wayland 模式

### 安装 Dropbox 并启动

[Dropbox官网](https://www.dropbox.com)

### 设置系统语言

- 使用 YaST 设置系统语言

### 安装中日文输入法

```shell
sudo zypper install fcitx5 fcitx5-configtool fcitx5-mozc fcitx5-chinese-addons
```

### 启用 Flatpak

```shell
sudo zypper install flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak config --set languages "ja;zh"
```

### 重启系统以确保配置生效

### 安装 kwin 插件：Kröhnkite

[Kröhnkite 插件说明](https://github.com/anametologin/krohnkite#readme)

### 安装／移除软件 (Packages)

- 移除不需要的软件：

```shell
sudo zypper remove firefox ibus
```

- 安装常用软件：

```shell
sudo zypper install gcc gcc-c++ make libopenssl-3-devel libopenssl-devel git fastfetch ncdu btop tmux remmina keepassxc strawberry audacity filezilla kdenlive universal-ctags starship wezterm yt-dlp docker aria2 bat lsd cowsay
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

### 安装 Rust

```shell
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
sudo zypper install rustup
cargo install cargo-update
rustup update stable
rustup default stable
```

### 安装 Yazi

```shell
sudo zypper install ueberzugpp ffmpeg 7zip jq ripgrep fzf zoxide ImageMagick chafa fd poppler-tools xclip ouch
cargo install --locked yazi-fm yazi-cli
```

### 安装 VSCode

```shell
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" \
| sudo tee /etc/zypp/repos.d/vscode.repo > /dev/null

sudo zypper refresh
sudo zypper install code
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

- 更新 shell 配置

```shell
cd ~
cat .zshrc
echo >> .zshrc
echo "alias ls='lsd'" >> .zshrc
echo "alias ll='lsd -l'" >> .zshrc
echo "alias la='lsd -a'" >> .zshrc
echo "alias lla='lsd -la'" >> .zshrc
echo "alias lt='lsd --tree'" >> .zshrc
cat .zshrc
```

### 配置 NeoVim (LazyVim)

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

- 更新 shell 配置

```shell
cd ~
cat .zshrc
echo >> .zshrc
echo 'alias vi=vim' >> .zshrc
echo 'alias vim=nvim' >> .zshrc
echo 'export EDITOR=/usr/bin/nvim' >> .zshrc
echo 'export SUDO_EDITOR=/usr/bin/nvim' >> .zshrc
cat .zshrc
```

### 配置 WezTerm

```shell
mv ~/Documents/dotfiles/dotconfig/wezterm ~/.config/
```

### 配置 fastfetch

```shell
mv ~/Documents/dotfiles/dotconfig/fastfetch/config.jsonc ~/.config/fastfetch/config.jsonc
```

### 配置 Yazi

```shell
mv ~/Documents/dotfiles/dotconfig/yazi ~/.config/
ya pack -u
```

### 配置 starship

```shell
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

### 安装常用软件（Flatpak）

```shell
flatpak install -y flathub org.onlyoffice.desktopeditors com.obsproject.Studio com.github.unrud.VideoDownloader io.anytype.anytype org.localsend.localsend_app com.calibre_ebook.calibre com.jgraph.drawio.desktop com.xnview.XnViewMP org.kde.krita net.agalwood.Motrix flathub org.kde.skanpage

flatpak install -y flathub md.obsidian.Obsidian
flatpak install -y flathub org.musescore.MuseScore
flatpak install -y flathub net.ankiweb.Anki
flatpak install -y flathub us.zoom.Zoom
```

### 如果 flatpak 安装后出现乱码

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

Nerdfonts 下载地址：[Nerdfonts Downloads](https://www.nerdfonts.com/font-downloads)

---
## 以下为可选或参考内容

### 配置 SDDM

- 添加以下设置到 /etc/sddm.conf.d/kde_settings.conf 的 [General] 下

```shell
GreeterEnvironment=QT_SCREEN_SCALE_FACTORS=1.5,QT_FONT_DPI=192
```

### 配置 Vim

```shell
sudo zypper install vim gvim
mkdir -p ~/.vim/autoload/
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
mv ~/Documents/dotfiles/.vimrc ~/
```

- 更新 shell 配置

```shell
cat .zshrc
echo >> .zshrc
echo 'alias vi=vim' >> .zshrc
echo 'export EDITOR=/usr/bin/vim' >> .zshrc
echo 'export SUDO_EDITOR=/usr/bin/vim' >> .zshrc
cat .zshrc
```

- 启动 Vim 后运行命令安装插件

```vim
:PlugInstall
```

### 配置 eza

```shell
mv ~/Documents/dotfiles/dotconfig/eza ~/.config/
```

- 更新 shell 配置

```shell
cd ~
cat .zshrc
echo >> .zshrc
echo "alias ls='eza --icons'" >> .zshrc
echo "alias ll='eza -l --icons'" >> .zshrc
echo "alias la='eza -a --icons'" >> .zshrc
echo "alias lla='eza -al --icons'" >> .zshrc
echo "alias lt='eza --tree --icons'" >> .zshrc
echo "alias lta='eza -a --tree --icons'" >> .zshrc
echo "alias lt1='eza --tree --level=1 --icons'" >> .zshrc
echo "alias lta1='eza --tree --level=1 --icons'" >> .zshrc
cat .zshrc
```

### 配置 Hyprland (预配置)

```shell
git clone --depth=1 https://github.com/JaKooLit/OpenSuse-Hyprland.git ~/OpenSuse-Hyprland
cd ~/OpenSuse-Hyprland
chmod +x install.sh
./install.sh
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

### 配置 Ghostty

```shell
mv ~/Documents/dotfiles/dotconfig/ghostty ~/.config/
```

### 配置 Alacritty

```shell
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
```

在 `pip.conf` 中写入内容：

```ini
[global]
break-system-packages = true
```

- 安装需要的库：

```shell
pip3 install pandas
pip3 install Jupyter
pip3 install jupyterlab
pip3 install pip-review
~/.local/bin/pip-review --auto --continue-on-fail
```

### 启用 AppImage

```shell
sudo zypper install libfuse2
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
