FROM registry.fedoraproject.org/fedora

RUN dnf -y install golang neovim tmux make powerline

RUN groupadd dbuckley -g 82894 && \
    useradd dbuckley -d /home/dbuckley -u 82894 -g 82894 && \
    pip3 install neovim && \
    go get -u github.com/mdempsky/gocode && \
    curl -fLo home/dbuckley/.local/share/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

ADD init.vim /home/dbuckley/.config/nvim/init.vim
ADD bashrc /home/dbuckley/.bashrc
#ADD /home/dbuckley/.ssh /home/dbuckley/.ssh

RUN chown dbuckley:dbuckley -R /home/dbuckley && \
    su dbuckley 'git config --global user.email dgbuckley@protonmail.com && \
    git config user.name "Derek Buckley"'

ENV GOPATH /srv/go
ENV GOBIN /srv/go/bin
ENV PATH /srv/go/bin:$PATH

WORKDIR "/srv/go"

USER dbuckley
ENTRYPOINT ["bash", "/usr/local/bin/run"]
LABEL RUN "/usr/bin/docker run --init -it --privileged -v /srv:/srv:Z --net=host --name NAME IMAGE tmux -l"

