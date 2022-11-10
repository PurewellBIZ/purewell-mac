# Purewell MAC 설정

## 개요

나와 같이 MAC에 적응 못하는 자들을 위한 간단한 설정.

## Karabiner

프로그램 설치: `https://karabiner-elements.pqrs.org/`

설정파일 위치: `~/.config/karabiner/karabiner.json`

## 글꼴

D2coding: `https://github.com/naver/d2codingfont/releases/download/VER1.3.2/D2Coding-Ver1.3.2-20180524.zip`

## Apple Terminal

iTerm2 설치 및 설정이 번잡스럽고 귀찮아, 기본 쉘을 사용

## SSH key

```shell
mkdir ~/.ssh
chmod 0700 ~/.ssh

# id_rsa 파일 복사
mv ~/Downloads/id_rsa ~/.ssh/
chmod 0600 ~/.ssh/id_rsa

# id_rsa.pub 생성
ssh-keygen -f id_rsa -y > ~/id_rsa.pub
```

## Bash

zsh가 기본 쉘이라고 하는데, bash에서만 동작하는 명령 등이 있음.

```shell
cp bash/bash_profile ~/.bash_profile
```

## Brew

설치: `https://brew.sh`

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## GNU utils

```shell
brew install coreutils binutils diffutils ed findutils gawk gnu-indent gnu-sed \
  gnu-tar gnu-which gnutls grep gzip screen watch wdiff wget bash bash-completion \
  gdb gpatch m4 make nano file-formula git less openssh python rsync svn unzip vim \
  jq
```

```shell
# root 권한
echo '/usr/local/bin/bash' >> /etc/shells

# GNU Bash를 기본 쉘로 변경
chsh -s /usr/local/bin/bash
```

## JDK

설치: `https://formulae.brew.sh/cask/temurin`

```shell
brew install --cask temurin
```

## Docker

설치: `https://itnext.io/replace-docker-desktop-with-lima-88ec6f9d6a19`

```shell
brew install lima docker

# LIMA SETUP BEGIN

limactl start docker --name=docker template://docker

limactl stop docker -f

# 홈디렉토리(Host)에 대해 쓰기 권한 줌
# mounts:
# - location: "~"
#   writable: true
# 메모리 기본 사용량이 4GBi인데, 이것 가지고는 컴파일이 되지 않는 것이 많으므로, 8G로 설정이 필요함
# memory: 8G
# 디스크 기본 사용량이 100GBi인데, 이것 가지고는 컴파일이 되지 않는 것이 많으므로, 200G로 설정이 필요함
# disk: 200G
vi ~/.lima/docker/lima.yaml

limactl start docker

# LIMA SETUP END

docker context create lima-docker --docker "host=unix://${HOME}/.lima/docker/sock/docker.sock"

docker context use lima-docker
```

SSH Key를 바꾸면, LIMA가 QEMU를 통해 띄우는 Ubuntu Linux 컨테이너와 통신이 되지 않는다.

만약 `~/.ssh/id_XXX` 를 새로 생성하거나 수정했다면, `~/.lima/docker` 디렉토리를 삭제하고, `LIMA SETUP BEGIN` 부터 `LIMA SETUP END` 까지 다시 실행한다.
