# docker_ros_hrgsv

Clone the project:
```bash
git clone --recurse-submodules git@github.com:HenrikTrom/docker_ros_hrgsv.git
cd docker_env 
git checkout <your-branch-name> 
git submodule init
git submodule update
```


Set commands on host machine (and install zsh):

``` bash
sudo apt install -y zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"

sudo sed -i 's/ZSH_THEME=.*/ZSH_THEME="spaceship"/' ~/.zshrc
sudo sed -i 's/plugins=.*/plugins=(git docker docker-compose)/' ~/.zshrc

sudo echo 'xhost +local:docker &> /dev/null11' >> ~/.zshrc 
```

For terminal session with container:

Set your tp as (i.e. "tp3") set the alias
```
KeikoTP=<your-tp>
sudo echo 'alias dcexec="docker exec -it keiko-ros-env-$KeikoTP bash"' >> ~/.zshrc 

```

Docker commands:

```
dcb     # docker compose build: builds the docker image
dcupd   # docker compose up -d: starts docker container using the image in the background (-d)
dcexec  # docker compose exec -it keiko-ros-env: starts interactive terminal session with container
dcstop  # docker compose stop: shuts down the container

```


Important notes:

* When installing stuff in the docker container, install it using the Dockerfile!!
* *Add your code in a user specific folder in catkin_ws/src!* 