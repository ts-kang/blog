---
layout: post
title:  "Jekyll을 이용해 Github Pages에서 블로그 만들기"
categories: etc
---
GitHub에서는 [GitHub Pages](https://pages.github.com/)라는 서비스를 통해 사용자가 자유롭게 정적 페이지를 만들 수 있는 환경을 제공한다.
이것만으로도 블로그를 만드는 것은 가능하지만, 불편한 점이 많다.

GitHub Pages에서는 [Jekyll](https://jekyllrb.com/)이라는 Ruby 기반의 정적 페이지 생성 프로그램을 사용할 수 있다.
Jekyll의 여러가지 편리한 기능을 사용하면 손쉽게 블로그를 만들 수 있다.

Jekyll 설치
---

Jekyll을 설치하기 위해 먼저 Ruby와 Bundler를 설치한다.
[Bundler](https://bundler.io/)는 가장 널리 쓰이는 Ruby Gem(패키지) 관리 프로그램이다.

현재 macOS Big Sur를 사용하고 있으므로, Homebrew를 통해 Ruby를 설치하였다.
```sh
$ brew install ruby
```

Ruby가 설치된 상태에서 다음 명령어를 실행하면 Bundler와 Jekyll을 설치한다.
```sh
$ gem install bundler jekyll
```

### webrick 설치
Ruby 3.0.0 이상의 버전을 사용한다면 webrick이 기본으로 설치되어있지 않아 직접 설치해줘야한다.
[참고](https://github.com/jekyll/jekyll/issues/8523)

```sh
$ bundle add webrick
```

Jekyll 사이트 만들기
---

아래 명령어를 실행하면 `blog` 디렉토리에 Jekyll 사이트의 뼈대가 생성된다.
```sh
$ jekyll new blog
$ bundle install
```

뼈대를 생성하고 난 후에는 `_config.yml`파일에서 기본적인 설정을 해야한다.

```yaml
title: Your awesome title
email: your-email@example.com
description: >- # this means to ignore newlines until "baseurl:"
  Write an awesome description for your new site here. You can edit this
  line in _config.yml. It will appear in your document head meta (for
  Google search results) and in your feed.xml site description.
baseurl: "" # the subpath of your site, e.g. /blog
url: "" # the base hostname & protocol for your site, e.g. http://example.com
twitter_username: jekyllrb
github_username:  jekyll
```

이 부분은 자신에게 맞게 변경하면 된다.

GitHub에 업로드하기 전에, 로컬에서 서버를 열어볼 수 있다.
```sh
$ bundle exec jekyll serve
```

사이트를 생성하고 아무 것도 안하면 이런 모습이다.

![Jekyll 기본 뼈대]({{'/assets/img/jekyll_scaffold.png' | relative_url}})

여기서 원하는 테마를 적용시킬 수도 있고, 그 밖에도 커스터마이징이 가능한 부분이 많다.

개인적으로는 글 링크 형식이 마음에 안들어서 바꿔보았다.

`_config.yml`에서 `permalink`라는 속성을 설정하면 된다. [참고](https://jekyllrb.com/docs/permalinks/)
```yaml
permalink: /:year/:month/:day/:title/
```

GitHub 업로드
---
GitHub에서는 `사용자이름.github.io`라는 이름으로 리포지토리를 생성하면 해당 도메인을 무료로 사용할 수 있다.
원한다면 설정페이지 또는 `CNAME`파일로 원하는 도메인을 사용하는 것도 가능하다. [참고](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

GitHub에서 리포지토리를 생성한 뒤,
다음과 같이 아까 생성한 Jekyll 사이트 디렉토리에서 git 저장소를 만들어서 push해주면 된다.

```sh
$ git init
$ git remote add origin <저장소URL>
$ git add .
$ git commit -m'Initial commit'
$ git push origin main
```

`github.io`로 리포지토리를 생성했으면 바로 해당 도메인으로 접속해볼 수 있다.
그렇지 않은 경우는 리포지토리 설정의 Pages에서 어떤 브랜치에서 GitHub Pages를 사용할지 설정할 수 있다. [참고](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
