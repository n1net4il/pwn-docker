# pwn-docker
  

### docker build image command

```sh
cd pwn-docker/16.04
docker build --tag pwn-docker:16.04 .

cd pwn-docker/18.04
docker build --tag pwn-docker:18.04 .

cd pwn-docker/19.04
docker build --tag pwn-docker:19.04 .

cd pwn-docker/20.04
docker build --tag pwn-docker:20.04 .

cd pwn-docker/21.04
docker build --tag pwn-docker:21.04 .
```

### docker run contianer command

```sh

docker run --rm -it -v $(pwd):/root/pwn --name ubuntu_16 pwn-docker:16.04 /bin/zsh

```



### docker alias

```sh
alias pwn16="docker run --rm -it -v $(pwd):/pwn --name ubuntu_16 pwn-docker:16.04 /bin/zsh"
alias pwn18="docker run --rm -it -v $(pwd):/pwn --name ubuntu_18 pwn-docker:18.04 /bin/zsh"
alias pwn19="docker run --rm -it -v $(pwd):/pwn --name ubuntu_19 pwn-docker:19.04 /bin/zsh"
alias pwn20="docker run --rm -it -v $(pwd):/pwn --name ubuntu_20 pwn-docker:20.04 /bin/zsh"
alias pwn21="docker run --rm -it -v $(pwd):/pwn --name ubuntu_21 pwn-docker:21.04 /bin/zsh"
```