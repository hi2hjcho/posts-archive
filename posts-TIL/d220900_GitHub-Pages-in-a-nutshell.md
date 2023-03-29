---
layout: single
title:  "Github pages 시작: 기본 설정을 위한 참고자료 및 more reference"
tag:
use_math: true
toc: true
toc_sticky: true
toc_label: "TOC"
---


# Github pages 이용을 위한 길잡이

**기본 설정을 위한 참고자료 in short**
GitHub repository을 비공개로 설정하면, 링크를 통하여 렌더링된 결과물(호스팅 결과물)을 확인 할 수 없다. 다만 비공개 설정이라도 깃 리모트 레포지토리에 대한 `push` 기능은 정상적으로 작동한다.

길잡이가 되는 동영상 - 일단 실체부터 만들고 시작하자.
깃헙(GitHub) 블로그 10분안에 완성하기, 테디노트

<iframe width="560" height="315" src="https://www.youtube.com/embed/ACzFIAOsfpM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

minimal-mistakes(m.m.) Fork 이후 환경설정에 대한 정리
- [x] repo name 변경(as hihjcho.github.io)
- [x] `_config.yml` 수정 : should edit url address
- [x] posting 하기 위해서는 `_posts` 폴더 생성 후 `*.md` 파일 생성

m.m.에 대한 사실 몇 가지
- gem-based theme
- Jekyll
- ruby



# 구체적인 환경설정
참고: 정리가 재밌는 개발자의 [블로그](https://eona1301.github.io/) 및 [Github pages](https://github.com/eona1301/eona1301.github.io)  - minimal-mistakes 거의 모든 세팅에 대한 정리 <br>

다음은 참고한 블로그 포스팅의 주요 내용을 포스팅별로 정리한 것인데, 추후에 포스팅과 무관하게 재정리할 필요있음 <br>

[[Github Blog] Jekyll - minimal mistakes 시작하기](https://eona1301.github.io/github_blog/GithubBlog-Start/)
- [x] Ruby 설치
- [x] Jekyll 설치
- [x] minimal-mistakes Fork
- [ ] 변경된 사항 로컬에서 확인하는 방법
  - [ ] 또 다른 [참고 블로그](https://ryureka.github.io/blog/GitHub-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(2)-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0/): cmd창에서 `bundle exec jekyll serve` 실행, 브라우저에서 `http://localhost:4000`입력

[[Github Blog] minimal mistakes - config.yml 수정하기](https://eona1301.github.io/github_blog/GithubBlog-config/)
- [x] 기본 정보 입력 - 블로그 전반에 적용되는 사항
- [x] 메인 프로필 영역 입력 - 블로그 좌측 프로필 영역
- [x] 하단 프로필 영역 - 블로그 하단 프로필 영역
- [x] 첫 화면 게시물 개수
- [ ] dafaults 설정(?)

[[Github Blog] minimal mistakes - Category 세팅하기](https://eona1301.github.io/github_blog/GithubBlog-Category/)
- [ ] 'navigation.yml' 수정 - 상단 카테고리 설정
- [ ] 지정된 카테고리 중 원하는 페이지 수정
- [ ] TOC 다루기

본문 영역 및 글자 크기

댓글 기능 추가하기

방문자 통계하기

검색창 노출시키기



## math equation represeantation, 수식 사용을 위한 환경설정:
- 참고 방법 #1: md processor - kramdown 설정, `mathjax_support.html` 생성 등의 과정으로
  - 1: https://chaelin0722.github.io/blog/mathjex/
  - 2: https://mkkim85.github.io/blog-apply-mathjax-to-jekyll-and-github-pages/
  - 3: http://benlansdell.github.io/computing/mathjax/
  - 결과: 인라인 수식은 보이나, 수식 블록은 보이지 않음.

<p>

- 참고 방법 #2: 
  - http://www.ktug.org/xe/index.php?mid=KTUG_open_board&document_srl=248288 

  > 20.8월에 kramdown이 버전이 바뀌면서 올해 초에 발표했던 MathJax 적용이 망가졌습니다
  
  - github와 LateX https://eeeuns.github.io/2020/12/10/githubblog/
  - 결과: 인라인 수식은 안보이고, 수식 블록은 보임 -.-

<p>

- 참고 방법 #3: 시도는 해보지 않았음
  - https://ansohxxn.github.io/blog/math-equation/

- 참고 방법 #4: 역시 본진을 털어야 한다: https://www.mathjax.org/
  - https://baeseongsu.github.io/posts/apply-mathjax-to-jekyll-blog/ math delimiter 을 조정하여야 한다.

- 결론
  - 참고방법 #2에 따라 `/includes/Mathjax.html` 생성, `_layouts/default.html` 수정
  - 참고방법 #4에 따라 math delimiter 추가 


- inline equation: `$...$` syntax
- equation block: `$$...$$` syntax
- specific TeX 문법



## youtube link 예쁘게 보이기 테스트
[Spring - Blender Open Movie](https://www.youtube.com/watch?v=WhWc3b3KhnY){:.glightbox}
https://www.youtube.com/watch?v=WhWc3b3KhnY


블로그 카테고리 클릭 시 해당되는 포스트만 보이기 - 카테고리안에서도 세부적으로 sub-category 좌측 메뉴판에 전시

전체 포스팅을 분류하는 기능도 존재하기 - by year, by topis


# more Github pages REFERENCE
- 정리가 재밌는 개발자 [블로그](https://eona1301.github.io/), [Github pages](https://github.com/eona1301/eona1301.github.io)
- 이수환님 블로그, https://suhwan.dev/2017/06/23/jekyll-project-structure/
- Animadversio WashU 중국 유학생, https://animadversio.github.io/
- 김태곤 교수님, https://github.com/taegon
- [류정관 개발자](https://ryureka.github.io/)
  - 로컬에서 개발 환경 구축하기
- https://ansohxxn.github.io/blog/math-equation/ 카테고리 보이기, 페이지 설정 등 세부 설정 조정방법
- https://github.com/milooy/remote-or-flexible-work-company-in-korea
  - 협업하여 포스팅 할 수 있다는 예시
  - github <-> 홈페이지 보기의 toggle 기능


# Blog with Gibhub

1. 고려할 수 있는 resource
    - Local repository
    - Github repository
    - Visual Studio
    - GitKraken
    - Markdown Language - with math equation
2. 요구사항
    - Github pages 에서도 equation 잘 나타날 수 있도록
    - Github pages dark page로 나타날 수 있도록
    - Github pages 에서 보이는 방법은 git에서 보이는 것과 홈페이지에서 보이는 방법 2가지가 있음
    - post에 연결된 img 및 각종 resource들이 잘 정리될 수 있도록 하기
3. **기본적인 동작원리**
   1. 기본적으로 github pages에 대한 설명은 이곳을 참조 https://pages.github.com/
      1. 조금 더 상세하게 설명된 github pages에 대한 설명은 이곳을 참조
      Types of Github pages site: project, user and orgrnization
      https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites
   2. github 개인 레포지토리(user pages)에 저장된 *.md 파일은 인터넷에서 볼 수 있다.
      1. 메인페이지의 경로는... https://hi2hjcho.github.io/ - it shows us `README.md`
      2. 그 밖에 다른 *.md 파일의 경로(i.e., `2021-10-23-github_pages.md`)는... https://hi2hjcho.github.io/2021-10-23-github_pages.html 에서 확인 할 수 있다.

4. 조금 더 꾸며보기
   1. 이미지 파일
   2. Youtube 동영상이 첨부된 경우
   3. 수식이 첨부된 경우, i.e., $F=ma$
