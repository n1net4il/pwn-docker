FROM ubuntu:19.04
WORKDIR /root
ENV LC_CTYPE C.UTF-8
ARG DEBIAN_FRONTEND=noninteractive

RUN dpkg --add-architecture i386

RUN sed -i -re 's/([a-z]{2}.)?archive.ubuntu.com|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
RUN apt update -y
RUN apt install python python-dev python-setuptools python3 python3-pip python3-dev python3-setuptools python-capstone libssl-dev libffi-dev build-essential libc6:i386 libc6-dbg gcc-multilib make gcc netcat git curl wget gdb vim nano zsh ruby-full tmux -y
RUN curl -O https://bootstrap.pypa.io/pip/2.7/get-pip.py && python get-pip.py && rm get-pip.py
RUN python -m pip install --upgrade pip && python3 -m pip install --upgrade pip
RUN python -m pip install --ignore-installed pwntools && python3 -m pip install --ignore-installed pwntools
RUN gem install one_gadget seccomp-tools

RUN git clone https://github.com/pwndbg/pwndbg .pwndbg
RUN sed -i 's/raise\ Exception(\x27Cannot\ override\ non-whitelisted\ built-in\ command\ \x22%s\x22\x27\ %\ command_name)/pass/g' .pwndbg/pwndbg/commands/__init__.py   
RUN python3 -m pip install -r .pwndbg/requirements.txt
RUN git clone https://github.com/hugsy/gef .gef
RUN python3 -m pip install -r .gef/requirements.txt
RUN git clone https://github.com/scwuaptx/Pwngdb .pwngdb
RUN echo "source ~/.pwngdb/pwngdb.py\\nsource ~/.pwngdb/angelheap/gdbinit.py\\n\\npython\\nimport angelheap\\nangelheap.init_angelheap()\\nend\\n\\ndefine init-pwndbg\\nsource ~/.pwndbg/gdbinit.py\\nend\\n\\ndefine init-gef\\nsource ~/.gef/gef.py\\nend" > .gdbinit
RUN echo "#!/bin/sh\\nexec gdb -q -ex init-pwndbg \"\$@\"" > /usr/bin/gdb-pwndbg
RUN echo "#!/bin/sh\\nexec gdb -q -ex init-gef \"\$@\"" > /usr/bin/gdb-gef
RUN chmod +x /usr/bin/gdb-*

RUN mkdir .zsh
RUN git clone https://github.com/sindresorhus/pure .zsh/pure
RUN git clone https://github.com/zdharma/fast-syntax-highlighting .zsh/fast-syntax-highlighting
RUN echo "ZSH_THEME=""\\nsource /root/.zsh/fast-syntax-highlighting/fast-syntax-highlighting.plugin.zsh\\nfpath+=/root/.zsh/pure\\nautoload -U promptinit; promptinit\\nprompt pure" > .zshrc

echo set -g mouse on > ~/.tmux.conf

RUN mkdir /pwn
WORKDIR /pwn
CMD [ "/bin/zsh" ]
