# bash

chsh -s /bin/bash


# zsh

chsh -s /bin/zsh

# backup

cp ~/.bashrc ~/.bashrc.orig

# oh my bash

git clone https://github.com/ohmybash/oh-my-bash.git ~/.oh-my-bash


echo "export BASH_SILENCE_DEPRECATION_WARNING=1" >> ~/.bash_profile

cp ~/.oh-my-bash/templates/bashrc.osh-template ~/.bashrc


export CLICOLOR=1
alias ls='ls -G'
alias ll='ls -lG'