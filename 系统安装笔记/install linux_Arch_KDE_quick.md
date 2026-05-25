# 快速部署自用 Arch linux

## 系统概要

- OS：Arch linux
- DE：KDE
- WM：KWIN
- Shell：fish

### 系统更新

```shell
sudo pacman -Syu && sudo pacman -Sc --noconfirm && paru -Syu && paru -Sc --noconfirm && sudo flatpak update && ya pkg upgrade
```

---

### 安装必要软件

```shell
sudo pacman -S 7zip aria2 audacity bat btop chafa cherrytree curl eza fastfetch fcitx5 fcitx5-chinese-addons fcitx5-configtool fcitx5-gtk fcitx5-mozc fcitx5-pinyin-zhwiki fcitx5-qt fd ffmpeg filezilla fish flatpak fuse2 fzf gcc ghostty git imagemagick jq kdenlive keepassxc lazygit linux-headers make man-db meld ncdu neovide neovim noto-fonts noto-fonts-cjk noto-fonts-emoji noto-fonts-extra obs-studio pkgfile poppler remmina resvg ripgrep sane-airscan showmethekey skanpage starship strawberry ueberzugpp unzip wget wl-clipboard xclip xsel yazi zellij zoxide
```

### 安装 AUR Helper

[paru](https://github.com/morganamilo/paru)

```shell
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

### 安装常用软件（AUR Helper）

```shell
paru -S microsoft-edge-stable-bin
paru -S motrix-next-bin
paru dropbox
※Type 1
```

### 设置 Flatpak

```shell
flatpak config --set languages "ja;zh"
```

### 安装字体

```shell
wget -P ~/.local/share/fonts https://github.com/SpaceTimee/Fusion-JetBrainsMapleMono/releases/download/x.xxxx.xx/JetBrainsMapleMono-NF-XX-XX-XX.zip \
&& cd ~/.local/share/fonts \
&& unzip JetBrainsMapleMono-NF-XX-XX-XX.zip \
&& rm JetBrainsMapleMono-NF-XX-XX-XX.zip \
&& fc-cache -fv
```

- JetBrainsMapleMono 下载地址：[JetBrainsMapleMono Downloads](https://github.com/SpaceTimee/Fusion-JetBrainsMapleMono)

### 安装 Fish shell

```shell
command -v fish | sudo tee -a /etc/shells
chsh -s "$(command -v fish)"
```

#### ※重启系统

### 安装常用软件（Flatpak）

```shell
flatpak install -y flathub io.github.aandrew_me.ytdn org.localsend.localsend_app com.jgraph.drawio.desktop org.kde.krita com.xnview.XnViewMP
```

### 安装Rust开发环境

```shell
sudo pacman -S rustup cargo-update
```

### 安装 NeoVim (LazyVim)

```shell
mv ~/.config/nvim{,.bak}
mv ~/.local/share/nvim{,.bak}
mv ~/.local/state/nvim{,.bak}
mv ~/.cache/nvim{,.bak}
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
```

### 导入我的 dotfiles

```shell
cd ~/Documents
git clone https://github.com/fantaro/dotfiles

mv ~/Documents/dotfiles/.aria2 ~/
mv ~/Documents/dotfiles/.config/btop ~/.config/
mv ~/Documents/dotfiles/.config/environment.d ~/.config/
mv ~/Documents/dotfiles/.config/eza ~/.config/
mv ~/Documents/dotfiles/.config/fastfetch ~/.config/
mv ~/Documents/dotfiles/.config/fish ~/.config/
mv ~/Documents/dotfiles/.config/ghostty ~/.config/
mv ~/Documents/dotfiles/.config/lazygit ~/.config/
mv ~/Documents/dotfiles/.config/microsoft-edge-stable-flags.conf ~/.config/
mv ~/Documents/dotfiles/.config/neovide ~/.config/
mv ~/Documents/dotfiles/.config/nvim/lua/config/keymaps.lua ~/.config/nvim/lua/config/keymaps.lua
mv ~/Documents/dotfiles/.config/nvim/lua/config/options.lua ~/.config/nvim/lua/config/options.lua
mv ~/Documents/dotfiles/.config/nvim/lua/plugins/noice.lua ~/.config/nvim/lua/plugins/noice.lua
mv ~/Documents/dotfiles/.config/starship.toml ~/.config/
mv ~/Documents/dotfiles/.config/tmux ~/.config/
mv ~/Documents/dotfiles/.config/yazi ~/.config/
rm -rf ~/.config/yazi/flavors/*
rm -rf ~/.config/yazi/plugins/*
ya pkg upgrade
mv ~/Documents/dotfiles/.config/zed ~/.config/
```
