---
title: minimal-mistakes 테마를 이용한 GitHub 블로그 생성
categories:
  - Blogs
tags:
  - Blog
  - minimal-mistakes
---

> ## 서론
Github Pages상에 Jekyll 기반의 블로그 사이트 구축

> ## 준비작업
- Github Pages 상에서 블로그 호스팅을 위해서는 특별한 이름의 repository가 필요
- `#{GITHUB_ID}.github.io` 라는 이름으로 리파지토리를 생성

> ## 테마 가져오기

- 아래 내용은 [minimal-misatakes의 퀵가이드](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) 를 참조 및 요약한 글.

- [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes) 에서 Fork 또는 downlaod 및 업로드를 통하여 소스를 카피. 
- 소스 카피 시 필요 없는 파일은 삭제(삭제 리스트는 아래와 같다).
 - .editorconfig
 - .gitattributes
 - .github
 - /docs
 - /test
 - CHANGELOG.md
 - minimal-mistakes-jekyll.gemspec
 - README.md
 - screenshot-layouts.png
 - screenshot.png

> ## 포스트 쓰기
- 포스트는 특정 제목으로 작성(YYYY-MM-DD-{TITLE}.md)로 작성
- 내용은 크게 두 부분으로 구분 
  - 메타데이터를 위한 yaml 부분
  - 본문을 위한 마크다운 부분
- yaml은 md 파일의 머릿말에 적으면 된다. 아래가 그 예제

```yaml
---
title: Jekyll과 minimal-mistakes 테마를 이용한 블로그 생성
categories:
  - Blog
tags:
  - Blog
---
```

> ## 카테고리 및 태그 적용
- minimal-mistakes 테마는 카테고리와 태그를 지원은 하지만 기본 설정되어 있지는 않다. 
- minimal-mistakes의 [깃헙 페이지의 docs 폴더](https://github.com/mmistakes/minimal-mistakes/tree/master/docs) 를 참고하면 다양한 예제들을 가져올 수 있다. 
- 해당 예제들은 [데모](https://mmistakes.github.io/minimal-mistakes/)로 제공되는 페이지의 코드들이다. 
- 이 폴더의 `_pages` 하위 폴더의 `category-archive.html`와 `tag-archive.html`을 그대로 가져와서 `_pages`를 만들고 옮겨놓으면 된다.

