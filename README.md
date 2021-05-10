# SSG & SSR 하이브리드 웹 앱을 위한 파일 시스템 구조 아이디어

## Static Site Generator 측면
- 참고: [Next.js의 dynamic-routes](https://nextjs.org/docs/routing/dynamic-routes)
- /page 그 자신과 그의 모든 하위 디렉토리는 아래와 같은 구조를 갖습니다.
    - 루트 디렉토리인 /page만 /404 에러에 대응하는 특별한 dir을 갖습니다.
```
/pathname
    /markup
        /index.html
        /partial
            /...html
    /style
        /style.scss
        /partial
            /...scss
    /js
        /main.js
        /module
            /...js
```
- 이 구조를 수평적 또는 수직적으로 확장 합니다.
```
/pathname
    /pathname
    /pathname
        /pathname
```
- /page 내의 디렉토리 경로가 그대로 웹사이트의 경로가 됩니다.
- /pathname 내의 html, 스타일시트, 자바스크립트들을 배포 전 빌드를 통해 웹브라우저가 해석가능한 형태의 정적인 애셋으로 빌드합니다.
    - 이 애셋들을 웹 서버를 통해 서비스 합니다.

## Server Side Rendering 측면
- 참고: [Next.js의 dynamic-routes](https://nextjs.org/docs/routing/dynamic-routes)
- pathname variable에 따라 뷰가 가변적인 페이지는 경로의 이름을 중괄호\[...\]로 묶습니다.
    - ex) /page/profile/\[id\], /page/reset-pw/\[id\]
- 이 폴더의 소스들은 서버 사이드에서 렌더링 하여 서비스 합니다.

## /api 디렉토리
- 서버에서 제공하는 Rest API 서비스는 없지만 외부의 Rest API 서버와 통신 할때 CORS 이슈를 해결하는 등에 사용.
- /page... 에서는 hostnmae 명시하지 않고 사용가능한 엔드포인트
