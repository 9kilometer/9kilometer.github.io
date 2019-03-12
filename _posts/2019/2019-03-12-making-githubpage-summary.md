---
title: "나의 githubPage 블로그 제작 과정 요약"
last_modified_at: 2019-03-12T00:00:00
category: record
tag: 
    - jekyll
    - githubPage
---

1. **테마 찾기**  
현재 사용 중인 테마 : [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes)  
깔끔하면서도 원하는 기능은 다 있는 것 같아서 선택함.  
처음에 외형이 가장 맘에 들었던 테마는 [이거](http://bencentra.com/centrarium/)였는데, 카테고리나 태그 전체를 한 눈에 볼 수가 없고 검색 기능도 없어서..ㅠㅠ  
테마를 찾을 때 [githubPage의 의존성](https://pages.github.com/versions/)을 확인하고, 테마의 기능 중에 githubPage에선 못 쓰는게 있는지 확인해봐야 함.(만들어진지 꽤 된 테마라면 아마 별 문제 없겠지만...) 예를 들어 [jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2)를 쓰면 카테고리나 태그의 pagination이 가능한데, githubPage 블로그에선 저 플러그인을 쓸 수 없다.   

1. **원하는대로 외형 수정**  
폰트와 아이콘, 헤더로 쓸 이미지를 추가하고, css도 내 맘대로 수정했다.  
기본 폰트는 KoPub돋움, 코드에는 D2Coding을 쓰고 있다. 나중에 수정할 수도?  
css를 써본 적이 없어서 감으로 막 수정해보다 뻘짓 많이 한 듯...  

1. **검색 엔진 등록**  
sitemap과 feed를 만들어 등록했다.  
이 글이 정리가 잘 되어있어 많은 도움이 되었다.
- 구글  
[https://gmlwjd9405.github.io/2017/10/20/include-blog-in-a-GoogleSearchEngine.html](https://gmlwjd9405.github.io/2017/10/20/include-blog-in-a-GoogleSearchEngine.html)
- 네이버  
[https://gmlwjd9405.github.io/2017/10/21/include-blog-in-a-NaverSearchEngine.html](https://gmlwjd9405.github.io/2017/10/21/include-blog-in-a-NaverSearchEngine.html)