
# 기본 프로세싱에 대한 이해
markdown 을 이용한 GitHub Pages (websites) 가 최종 형태로서 인터넷 상에서 보여지지만, 최종단계 전까지 보여지는 다양한 중간단계 형태에 대해서 정리가 필요하여 글을 남겨봄

- final result 최종단계
  - GitHub Pages websites hosting my repository
  - GitHub repository view: source & rendered view

- interim result 중간단계
  - VScode editor view

- rendering items
  - images
  - math equations
  - Youtube links

주의사항
- 문서 생성은 [GFM (Github Flavored Markdown)](https://help.github.com/articles/github-flavored-markdown/) 을 사용한다. (확장자 `.md`)
- 파일명은 영어로. 공백은 대쉬(-) 혹은 언더바( _ )로 대체한다.


|   |  VScode | GitHub repo (rendered)  | GitHub Pages |
|:-:| - | - | - |
| images <br/> same folder | - `![test img](test.png)`: work | - `![test img](test.png)` work |   |
| images <br/> different folder | - `![test img](/sub folder/test.png)`: NOT work <br/> - `![test img](/sub%20folder/test.png)`: work <br/> (Note! letter space as `%20` condition) |  - `![test img](/sub folder/test.png)`: NOT work <br/> - `![test img](/sub%20folder/test.png)`: NOT work <br/> - 경로 중 공백이 없어야 GitHub repo에서 rendering이 가능| - on testing  |



# 이미지 representation
`GitHub Pages (GP)`에 이미지를 추가하고 싶다.

GP가 based on Jekyll 이기 때문에 `assets` directory을 만들어야 하는가?
- https://github.com/tomcam/least-github-pages/blob/master/docs/adding-assets-directory-github-pages.md
- https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html#:~:text=The%20Jekyll%20publishing%20system%20used,the%20%2Fdocs%2Fassets%20path.
- Posting 설명을 따라 root에 `/docs/assets` 폴더를 만들고 `![test img](/docs/assets/test.jpg)` markdown 문법으로 이미지 표현
![test img](/docs/assets/test.jpg)
  - 하지만 문제점은, posting(`*.md`) 자체 파일과 resource(image etc.)가 별개로 구분되어 보관되어 managing이 쉽지 않다는 것

Do try some variants and keep a record.
- [ ] 꼭 `assets` directory 여야 하는가? 적절한 directory를 만들고 img 경로만 잘 지정하여 주면 어떻게 표현되는가? 이렇게 할 경우 예상되는 문제점은?
- [ ] 그 밖에 다른 방법들?

- show ima side by side


# math equation representation
| math equations |   |   |   |


| YouTube |   |   |   |
| fonts (mono-spaced) |   |   |   |
| etc. |   |   |   |