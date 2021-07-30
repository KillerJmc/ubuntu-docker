FROM ubuntu

MAINTAINER Jmc

# change home path from /root to /home
ENV HOME /home
 
WORKDIR $HOME

# copy oh-my-zsh config
COPY init/.oh-my-zsh $HOME/.oh-my-zsh
COPY init/.zshrc $HOME

# copy .bashrc 
COPY init/.myzshrc $HOME

RUN \
    # set mirrors
    sed -i s@/archive.ubuntu.com/@/mirrors.ustc.edu.cn/@g /etc/apt/sources.list; \
    \
    # update pkgs
    apt clean && apt update; \
    \
    # download zsh
    apt install zsh -y; \
    \
    # set time zone
    ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && apt install tzdata -y; \
    \
    # download other pkgs(vi, ifconfig, jdk, mysql) 
    apt install vim \
                net-tools \
                openjdk-16-jdk \
		        mysql-server \
    -y;
    
# expose mysql on 3306 port
EXPOSE 3306

# start mysql service and zsh
CMD service mysql start && clear && /bin/zsh

