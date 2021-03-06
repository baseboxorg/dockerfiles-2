FROM debian:jessie
MAINTAINER Sébastien M-B <essembeh@gmail.com>

RUN apt-get -q update
RUN apt-get install -y -q locales bash-completion curl wget && apt-get clean
RUN apt-get install -y -q zsh tmux git vim tig lftp tree moreutils realpath p7zip-full && apt-get clean
## Devel
#RUN apt-get install -y -q build-essential manpages && apt-get clean

## Checkout projects
WORKDIR /root/System
RUN git clone https://github.com/essembeh/oh-my-zsh && cd oh-my-zsh && git checkout -b custom origin/custom
RUN git clone https://github.com/essembeh/script-utils 
RUN git clone https://github.com/essembeh/dotfiles

## Locale
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen
RUN locale-gen 
RUN update-locale LANG=fr_FR.UTF-8
ENV LANGUAGE fr_FR.UTF-8
ENV LANG fr_FR.UTF-8
ENV LC_ALL fr_FR.UTF-8

## Custom env
WORKDIR /root
RUN mv .bashrc .bashrc.0 && \
	ln -s System/oh-my-zsh .oh-my-zsh && \
	ln -s System/dotfiles/bash/alias .alias  && \
	ln -s System/dotfiles/bash/bashrc .bashrc && \
	ln -s System/dotfiles/bash/custompath .custompath && \
	ln -s System/dotfiles/zsh/zshenv .zshenv && \
	ln -s System/dotfiles/zsh/zshrc .zshrc && \
	ln -s System/dotfiles/tmux/tmux.conf .tmux.conf && \
	ln -s System/dotfiles/vim .vim && \
	ln -s System/dotfiles/vim/vimrc .vimrc && \
	ln -s System/dotfiles/git/gitconfig .gitconfig

## Default shell
RUN chsh root -s /bin/zsh
CMD ["/bin/zsh"]
