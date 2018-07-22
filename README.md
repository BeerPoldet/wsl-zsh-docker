# Windows Subsystem for Linux (WSL)'s Terminal Setup

## Powerline fonts
1. Download repo https://github.com/powerline/fonts
2. Open Powershell as admin and run `Set-ExecutionPolicy Bypass`
3. Execute `.\install.ps1` inside powerline/fonts repo
4. Run `Set-ExecutionPolicy Default` to turn policy back

## ZSH
1. in terminal `sudo apt-get install zsh`
2. `vim ~/.bashrc` add 
```
if [ -t 1 ]; then
  exec zsh
fi
```

## Oh My ZSH
1. go to https://github.com/robbyrussell/oh-my-zsh
2. find installation command ex.
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
3. change theme or add plugin in `~/.zshrc`
```
# changing theme
ZSH_THEME="robbyrussell" # or "agnoster"
```
```
# adding plugins
plugins=(
  git
  bundler
  dotenv
  osx
  rake
  rbenv
  ruby
)
```

## Docker in WSL

1. Open Windows's Docker Settings Window 
    * General Tab
    * Check **Expose daemon on tcp://localhost:2375 without TSL**
2. install docker for ubuntu *ref: https://docs.docker.com/install/linux/docker-ce/ubuntu/#extra-steps-for-aufs*
2. install docker-compose for ubuntu *ref: https://docs.docker.com/compose/install/#prerequisites*
3. Add `export DOCKER_HOST=tcp://0.0.0.0:2375` to `~/.zshrc`
4. `sudo vim /etc/wsl.conf` add:
```
[automount]
root = /
options = "metadata"
```
5. to mount drive `:C/` do `sudo mkdir /c` and `sudo mount --bind /mnt/c /c`, you can do this with other drive as well
6. auto mount by add `sudo mount --bind /mnt/c /c` to bottom of file `~/.zshrc`
7. auto mount without asking for password `sudo visudo` then add `poldet ALL=(root) NOPASSWD: /bin/mount` at bottom of file, *Replace `poldet` with user username*


## Tips
* Create `~/dev` link for short access path `ln -s /c/Users/Poldet/dev ~/dev` 

reference: 
> https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly