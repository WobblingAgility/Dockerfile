FROM registry.fedoraproject.org/fedora

RUN dnf -y install golang neovim tmux make

ADD init.vim root/.config/nvim/init.vim
ADD neovim /root/.neovim
ADD bashrc root/.bashrc

ENV GOPATH /srv/go
ENV GOBIN /srv/go/bin
ENV PATH /srv/go/bin:$PATH

RUN pip3 install neovim && \
    go get -u github.com/mdempsky/gocode && \
    curl -fLo ~/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim && \
    nvim silent! +PlugInstall +qall && \
    sed -i 's/""colorscheme/  colorscheme/' /root/.config/nvim/init.vim

WORKDIR "/srv/go"

ENTRYPOINT ["tmux", "-l"]

LABEL RUN "/usr/bin/podman -it -v $HOME/srv:/srv --name NAME -e NAME=NAME -e IMAGE=IMAGE IMAGE"
