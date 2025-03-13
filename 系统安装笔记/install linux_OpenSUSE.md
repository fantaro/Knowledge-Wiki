# OpenSUSE 安装笔记

### 系统更新

```bash
sudo zypper dup　※推荐
# 或者
sudo zypper refresh
sudo zypper update
```

### 下载我的 dotfiles

```bash
cd ~/Documents
git clone https://github.com/fantaro/dotfiles
```

### 安装 Edge 浏览器

*请使用现有浏览器下载 Edge 浏览器*

### 安装 brave-browser

```bash
sudo zypper install curl
sudo rpm --import https://brave-browser-rpm-release.s3.brave.com/brave-core.asc
sudo zypper addrepo https://brave-browser-rpm-release.s3.brave.com/brave-browser.repo
sudo zypper install brave-browser
```

### 安装 Dropbox 并启动

[Dropbox官网](https://www.dropbox.com)

### 设置系统语言（YaST）

*请使用 YaST 设置系统语言*

### 安装中日文输入法

```bash
sudo zypper install fcitx5 fcitx5-configtool fcitx5-mozc fcitx5-chinese-addons
```

### 启用 Flatpak

```bash
sudo zypper install flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak config --set languages "ja;zh"
```

### 重启系统

*重启系统以确保配置生效*

### 安装 kwin 插件：Kröhnkite

请参阅：[Kröhnkite 插件说明](https://github.com/anametologin/krohnkite#readme)

### 安装和配置程序 (Packages)

首先移除 Firefox：

```bash
sudo zypper remove firefox
```

然后安装常用软件：

```bash
sudo zypper install gcc gcc-c++ make libopenssl-3-devel libopenssl-devel git fastfetch ncdu btop tmux remmina keepassxc strawberry audacity filezilla kdenlive universal-ctags starship wezterm yt-dlp docker aria2 bat diff-so-fancy lsd
```

### Rust

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo install cargo-update
rustup update stable
rustup default stable
```

### Yazi

```bash
sudo zypper install ueberzugpp ffmpeg p7zip jq ripgrep fzf zoxide imagemagick chafa fd poppler
cargo install --locked yazi-fm yazi-cli
```

### VSCode

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" \
| sudo tee /etc/zypp/repos.d/vscode.repo > /dev/null

sudo zypper refresh
sudo zypper install code
```

### 安装常用软件（Flatpak）

```bash
flatpak install -y flathub org.onlyoffice.desktopeditors com.obsproject.Studio com.github.unrud.VideoDownloader io.anytype.anytype org.localsend.localsend_app com.calibre_ebook.calibre com.jgraph.drawio.desktop com.xnview.XnViewMP org.kde.krita net.agalwood.Motrix flathub org.kde.skanpage

flatpak install -y flathub md.obsidian.Obsidian
flatpak install -y flathub org.musescore.MuseScore
flatpak install -y flathub net.ankiweb.Anki
flatpak install -y flathub us.zoom.Zoom
```

### 如果 flatpak 安装后出现乱码

```bash
flatpak run --command=fc-cache {AppName} -f -v
```

### 配置 tmux

```bash
mv ~/Documents/dotfiles/.tmux.conf ~/
```

### 配置 aria2

```bash
mv ~/Documents/dotfiles/.aria2 ~/
```

### 配置 btop

```bash
mv ~/Documents/dotfiles/dotconfig/btop ~/.config/
```

### 配置 lsd

```bash
mv ~/Documents/dotfiles/dotconfig/lsd ~/.config/
```

在 home 目录下更新 bash 配置：

```bash
cd ~
cat .bashrc
echo >> .bashrc
echo "# alias" >> .bashrc
echo "alias ls='lsd'" >> .bashrc
echo "alias ll='lsd -l'" >> .bashrc
echo "alias la='lsd -a'" >> .bashrc
echo "alias lla='lsd -la'" >> .bashrc
echo "alias lt='lsd --tree'" >> .bashrc
cat .bashrc
```

### 配置 NeoVim (LazyVim)

```bash
sudo zypper in neovim lazygit neovide

cd ~
cat .bashrc
echo >> .bashrc
echo 'alias vim=nvim' >> .bashrc
echo 'export EDITOR=/usr/bin/nvim' >> .bashrc
echo 'export SUDO_EDITOR=/usr/bin/nvim' >> .bashrc
cat .bashrc

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

### 配置 WezTerm

```bash
mv ~/Documents/dotfiles/dotconfig/wezterm ~/.config/
```

### 配置 fastfetch

```bash
mv ~/Documents/dotfiles/dotconfig/fastfetch/config.jsonc ~/.config/fastfetch/config.jsonc
```

### 配置 Yazi

```bash
mv ~/Documents/dotfiles/dotconfig/yazi ~/.config/
ya pack -u
```

### 配置 starship

```bash
cd ~
cat .bashrc
echo >> .bashrc
echo 'if command -v starship &> /dev/null; then' >> .bashrc
echo '  eval "$(starship completions bash)"' >> .bashrc
echo '  eval "$(starship init bash)"' >> .bashrc
echo 'fi' >> .bashrc
cat .bashrc

mv ~/Documents/dotfiles/dotconfig/starship.toml ~/.config/
```

### 安装字体

```bash
wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/Hack.zip \
&& wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/SourceCodePro.zip \
&& wget -P ~/.local/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/FantasqueSansMono.zip \
&& wget -P ~/.local/share/fonts https://github.com/yuru7/udev-gothic/releases/download/v2.1.0/UDEVGothic_NF_v2.1.0.zip \
&& cd ~/.local/share/fonts \
&& unzip Hack.zip \
&& unzip SourceCodePro.zip \
&& unzip FantasqueSansMono.zip \
&& unzip UDEVGothic_NF_v2.1.0.zip \
&& rm Hack.zip \
&& rm SourceCodePro.zip \
&& rm FantasqueSansMono.zip \
&& rm UDEVGothic_NF_v2.1.0.zip \
&& fc-cache -fv
```

Nerdfonts 下载地址：[Nerdfonts Downloads](https://www.nerdfonts.com/font-downloads)

---
## 以下为可选或参考内容

### 配置 Vim

```bash
sudo zypper install vim gvim
mkdir -p ~/.vim/autoload/
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
mv ~/Documents/dotfiles/.vimrc ~/
```

更新 bash 配置：

```bash
cat .bashrc
echo >> .bashrc
echo 'export EDITOR=/usr/bin/vim' >> .bashrc
echo 'export SUDO_EDITOR=/usr/bin/vim' >> .bashrc
cat .bashrc
```

启动 Vim 后运行命令安装插件：

```vim
:PlugInstall
```

### 配置 eza

```bash
mv ~/Documents/dotfiles/dotconfig/eza ~/.config/
```

更新 bash 配置：

```bash
cd ~
cat .bashrc
echo >> .bashrc
echo "# alias" >> .bashrc
echo "alias ls='eza --icons'" >> .bashrc
echo "alias ll='eza -l --icons'" >> .bashrc
echo "alias la='eza -a --icons'" >> .bashrc
echo "alias lla='eza -al --icons'" >> .bashrc
echo "alias lt='eza --tree --icons'" >> .bashrc
echo "alias lta='eza -a --tree --icons'" >> .bashrc
echo "alias lt1='eza --tree --level=1 --icons'" >> .bashrc
echo "alias lta1='eza --tree --level=1 --icons'" >> .bashrc
cat .bashrc
```

### 配置 Hyprland (预配置)

```bash
git clone --depth=1 https://github.com/JaKooLit/OpenSuse-Hyprland.git ~/OpenSuse-Hyprland
cd ~/OpenSuse-Hyprland
chmod +x install.sh
./install.sh
```

### 配置 Docker

```bash
sudo systemctl start docker
mkdir ~/Docker
cd ~/Docker
unzip ~/Dropbox/Software/Utility/WindowsInDocker.zip
sudo docker compose up

sudo systemctl stop docker
```

### 配置 Ghostty

```bash
mv ~/Documents/dotfiles/dotconfig/ghostty ~/.config/
```

### 配置 Alacritty

```bash
mv ~/Documents/dotfiles/dotconfig/alacritty ~/.config/
```

### 安装 python3

```bash
sudo zypper install python3 python3-pip
```

### 升级 Python 库

```bash
pip3 install --upgrade pip
```

如果出现 `error: externally-managed-environment` 错误，可执行以下步骤：

```bash
mkdir ~/.config/pip
vi ~/.config/pip/pip.conf
```

在 `pip.conf` 中写入内容：

```ini
[global]
break-system-packages = true
```

然后继续安装需要的库：

```bash
pip3 install pandas
pip3 install Jupyter
pip3 install jupyterlab
pip3 install pip-review
~/.local/bin/pip-review --auto --continue-on-fail
```

### 启用 AppImage

```bash
sudo zypper install libfuse2
```

### 安装 Anaconda

```bash
bash Anaconda3-yyyy.mm-Linux-x86_64.sh
conda upgrade --all
conda clean --packages
```

### 安装 VMware Workstation Pro

```bash
sudo bash ./VMware-Workstation-Full-xxxx.x86_64.bundle
# System service scripts directory: /etc/systemd/system
sudo zypper install kernel-default-devel
```

### 使用终端卸载 Workstation

对于 Red Hat/CentOS/openSUSE：

1. 列出已安装的 vmware 包：
   ```bash
   rpm -qa | grep vmware
   ```
2. 其他检查：
   ```bash
   ls /usr/bin | grep vmware
   ls /usr/sbin | grep vmware
   vmware --version
   ```
3. 停止 VMware 服务：
   ```bash
   sudo systemctl stop vmware.service
   sudo systemctl stop vmware-USBArbitrator.service
   sudo systemctl status vmware
   ```
4. 卸载 VMware：
   - 列出产品：
     ```bash
     vmware-installer --list-products
     ```
   - 卸载 Workstation：
     ```bash
     sudo vmware-installer -u vmware-workstation
     ```
   - 卸载 Player：
     ```bash
     sudo vmware-installer -u vmware-player
     ```
   - 扩展命令：
     ```bash
     sudo /usr/bin/vmware-installer --uninstall-product=vmware-workstation
     ```
5. 删除配置文件：
   ```bash
   sudo rm -rf /etc/vmware*
   sudo rm -rf /usr/lib/vmware*
   sudo rm -rf /usr/share/doc/*vmware
   sudo rm -rf /usr/bin/vmware-usbarbitrator
   sudo rm -rf /usr/bin/vmnet*
   sudo rm -rf /usr/bin/vmware*
   sudo rm -rf /usr/share/applications/vmware*
   ```

#### (vmware-host-modules)

```bash
git clone https://github.com/mkubecek/vmware-host-modules
cd vmware-host-modules
git checkout workstation-17.0.0
sudo make; sudo make install
```
