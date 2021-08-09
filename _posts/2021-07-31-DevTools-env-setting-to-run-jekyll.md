---
layout: post
date: 2021-08-07
title: "[GitHub Blog] 블로그를 위한 ruby + jekyll 로컬 개발 환경 설정"
subtitle: "Environment Setting to Run Jekyll"
abstract: "로컬에서 블로그 호스팅을 위한 ruby + jekyll 동작 환경 설정"
categories: DevTools
tags: DevTools Tools blog post jekyll ruby
comments: true
---

## 요약
> rbenv 를 활용한 ruby 가상환경 세팅 및 jekyll & bundler 를 설치하고 <br/>
> 로컬 환경에서 테스트를 위한 jekyll 블로그를 호스팅하는 방법에 대한 설명입니다.

# Development Env Settings

GitHub 블로그는 ruby 와 Jekyll 기반으로 동작합니다.

ruby 와 Jekyll 이 동작할 수 있는 로컬 개발 환경을 세팅해봅시다. <br/>
( 아래 환경 설정 가이드는 MacOS 를 기준으로 작성되어있습니다. Windows 환경은 추후 작성 예정입니다 )

## For MacOS

### Xcode 설치

Native 확장기능을 컴파일할 수 있도록 Xcode 설치 (이미 설치되어 있다면 생략해도 무방합니다)

```bash
xcode-select --install
```

### ruby + jekyll 환경 세팅

맥 시스템에는 기본적으로 ruby 가 설치되어 있지만, 해당 ruby 는 시스템 구성을 위한 패키지 이므로 가능한 손 대지 않는 편이 좋습니다. <br/>
따라서 rbenv 와 ruby-build 패키지를 활용해 ruby 가상환경을 만들고, 해당 환경을 통해 ruby + jekyll 이 동작하도록 구성합니다.

1. rbenv ruby-build 설치 (HomeBrew 를 통해 설치합니다)
   
   ```bash
   brew update
   brew install rbenv ruby-build
   ```

2. rbenv 실행을 위한 환경변수 설정
   
   - bash 환경에 적용
     
   ```bash
   rbenv init
   # 만일 적용이 되지 않는다면 아래 ~/.zshrc 를 수정해준것과 같이 ~/.bashrc 를 수정해줘야 합니다.
   ```
   
   - zsh 환경에 적용 
     
   zsh 환경에 적용 하려면, `vim ~/.zshrc` 를 통해 zsh 설정에 진입한 후,
     
   ```bash
   # >>> rbenv PATH setting >>>
   [[ -d ~/.rbenv  ]] && \
   export PATH=${HOME}/.rbenv/bin:${PATH} && \
   eval "$(rbenv init -)"
   # <<< rbenv PATH setting <<<
   ```
     
   를 입력해줍니다. <br/>
   이후, `source ~/.zshrc` 를 통해 zsh 를 재시작 해주면 rbenv 환경이 터미널에 반영됩니다.


3. 설치 완료 후 테스트 (현재 설치된 ruby 가상환경 리스트를 확인할 수 있습니다)
   
   ```bash
   rbenv versions
   ```

3. ruby 가상환경 세팅
   
   ```bash
   # 설치 가능한 루비 버전 목록 출력
   rbenv install -l
   
   # 원하는 버전의 ruby 설치 (예시는 2.6.8 버전입니다)
   rbenv install 2.6.8
   
   # 해당 버전의 가상환경이 설치 되었는지 확인
   rbenv versions
   
   # 설치한 버전의 ruby 환경으로 진입
   rbenv global 2.6.8
   
   # 해당 버전의 ruby 환경이 맞는지 확인
   ruby -v
   # >>> ruby 2.6.8p205 (2021-07-07 revision 67951) [x86_64-darwin20]
   # 가상환경 세팅이 원활히 되지 않았다면 2.6.3p62 같이 기존 시스템 버전이 출력된다
   ```
   
4. jekyll & bundler 설치

   RubyGems 를 통해 Jekyll 과 bundler 를 설치

   ```
   gem install jekyll bundler
   ```

5. jekyll 을 통해 개발용 블로그 페이지 호스팅

   ```
   # 테스트용 블로그가 작성된 곳에서 실행
   bundle exec jekyll serve
   ```

   만약 아래와 같은 문구가 뜨면서 서버 실행이 안 된다면, 

   ```   
   Running `bundle update` will rebuild your snapshot from scratch, 
   using only the gems in your Gemfile, which may resolve the conflict.
   ```

   `bundle update` 명령어를 통해 bundle 을 update 하여 해결 할 수 있습니다.

원본이 되는 한글 가이드는 [여기](http://jekyllrb-ko.github.io/docs/) 에서 보실 수 있습니다. <br/>
( 다만 작성 시점 이후 시간이 조금 지나 몇몇 트러블 슈팅이 필요한 부분이 있을 수 있습니다 )

* 현재 작성된 개발환경 세팅 방법에 대한 마지막 확인 일자 : __2021.08.07__
