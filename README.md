# zsh
Repository containing guidelines for my zsh configuraiton

> Guideline applies only for macos 🍏, because of `gsed`

# Configure OhMyZsh with you ZSH shell:

## Install `brew`:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
```

After the installation you will have the commands below in the output.

```bash
echo >> /Users/${USER}/.zprofile
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> /Users/${USER}/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

## Install `iterm`

```bash
brew install --cask iterm2
```
## Install `gsed`

```bash
brew install gsed
```
## Install Oh My Zsh with my personal perferences:

- If you are using `curl`:
```bash 
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
- If you are using `wget`: 
```bash
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## Install powerlevel10k:

> Note you need to open iterm and follow the on-screen instructions:
1. Clone the repo of powerlevel10k:
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
2. Change the theme in .zshrc:
```bash
gsed -i 's/^ZSH_THEME=.*/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc
```
3. Activate the configuration
```bash
source ~/.zshrc
```
4. Install Plugins:

### Plgins:
1. Clone these for syntax highlighting and auto-suggestions:
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
2. Add this to your `.zshrc` 
```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting web-search)
```
3. Activate the configuration
```bash
source ~/.zshrc
```

# Docker version:

```bash 
docker run -e TERM -e COLORTERM -e LC_ALL=C.UTF-8 -it --rm alpine sh -uec '
  apk add git zsh nano vim
  git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
  echo "source ~/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
  cd ~/powerlevel10k
  exec zsh'
```

# How to update the shell:

```bash
git -C ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k pull
```

# To see how different colors act on your machine: 

```bash
for i in {0..255}; do print -Pn "%K{$i}  %k%F{$i}${(l:3::0:)i}%f " ${${(M)$((i%6)):#3}:+$'\n'}; done
```