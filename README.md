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

limactl start --name=docker template://docker

docker context create lima-docker --docker "host=unix://${HOME}/.lima/docker/sock/docker.sock"

docker context use lima-docker
```