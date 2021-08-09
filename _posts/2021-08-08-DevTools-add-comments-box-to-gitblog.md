---
layout: post
date: 2021-08-08
title: "[GitHub Blog] 깃허브 블로그에 덧글 상자 만들기"
subtitle: "Add Comments Box to GitBlog"
abstract: "깃허브 저장소의 issue 와 매핑되는 블로그 덧글 상자 만들기 (with utterances)"
categories: DevTools
tags: DevTools Tools blog comments jekyll ruby utterances
comments: true
---

## 요약
> utterances 를 활용하여 깃허브 블로그 Repository 의 Issue 와 연동되는 덧글 상자를 만들어보자
> ( DISQUS 보다 가볍고 광고도 없답니다! )

# 사용 방법

[utterances](https://github.com/apps/utterances) 링크로 접속하여, 
우선 내 GitHub 에 utterances 앱을 설치합니다. <br/>
Install 을 완료하면 뜨는 페이지에서 아래 정보들을 입력해주면, 덧글 상자를 적용할 수 있는 스크립트가 만들어집니다.

- Repository <br/>
  사용하는 저장소 <br/>
  ( 보통 `<username>/github.io` 를 권장합니다 )
  
- Blog Post ↔️ Issue Mapping <br/>
  블로그 포스트의 덧글과 저장소의 Issue 를 매핑하는 방법 <br/>
  `Issue title contains page pathname` 를 선택하길 권장합니다 <br/>
  ( 블로그 포스팅 경로에 따라서 이슈를 생성하고, 해당 이슈의 덧글을 자동으로 매핑 )  

- Theme <br/>
  덧글 상자의 테마 <br/>
  본인이 좋아하는 테마를 선택하시면 됩니다.

위의 값들은 처음 덧글 박스를 생성할 때 필수적으로 고려해야 할 값들입니다. <br/>
해당 값들을 바탕으로 아래와 같은 포맷의 스크립트가 생성되게 됩니다.

```html
<script src="https://utteranc.es/client.js"
        repo="YuParan/yuparan.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>
```

이제 덧글 상자가 만들어지길 원하는 위치에 해당 스크립트를 삽입하면 됩니다. <br/>
현재 사용중인 이 블로그 탬플릿의 경우, 
`_includes/comments.html` 파일에 스크립트를 입력하면 자동으로 페이지에 맞춰 덧글 상자를 생성해줍니다. <br/>
다른 블로그 탬플릿도 comments 를 담당하는 html 파일을 찾아 스크립트를 삽입하는 방식으로 덧글 상자를 생성 할 수 있습니다. <br/>
(없다면... 페이지를 담당하는 html 파일에 직접 삽입 하시면 됩니다 TㅁT)

보다 많은 커스터마이징을 하고 싶으시다면, 
[가이드 페이지](https://utteranc.es/?installation_id=18743944&setup_action=install)를 참조해 
본인의 입맛에 맞게 커스터마이징 하면 됩니다! <br/>
( 정확히... 어느정도까지 커스터마이징을 할 수 있는지는 잘 모르겠네요... 저도 이제 막 공부중인 단계라서 ㅠ_ㅠ )

블로그에 스크립트를 적용하고, utterances 가 GitHub Issue 를 잘 관리 할 수 있는지 테스트 해보면 끝입니다! <br/>
