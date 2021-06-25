## Getting Started

### 메타 태그 삽입

- [설치 가이드](https://support.dable.io/wordpress-setting-guide/)

  (1) 데이블 플러그인 설치하기 > (2) 플러그인 설정하기 > Default Setting & Open Graph

- 메타 태그 직접 삽입은 매우 까다로우므로 반드시 데이블 플러그인을 통해 삽입해주세요
  - 플러그인 설치시 생성되는 meta tag
    - dable:item_id
    - dable:published_time
    - dable:author
    - dable:image
      - 본문 내 첫 번째 이미지가 자동 설정됩니다
      - 본문 내 이미지가 없을 경우 생성되지 않습니다
    - article:section
  - Create Open Graph 옵션 활성화시 생성되는 meta tag
    - og:url
    - og:title
    - og:description
      - 본문의 [excerpt](https://wordpress.org/support/article/excerpt/)가 자동 적용됩니다
      - excerpt가 작성되지 않은 경우, 본문의 첫 55개 단어가 자동 저장됩니다
    - og:image
      - 본문 내 첫 번째 이미지가 자동 설정됩니다
      - 본문 내 이미지가 없을 경우 생성되지 않습니다
    - article:published_time

### 위젯 코드 삽입

1. Dable Plugin (Recommended)

   - [설치 가이드](https://support.dable.io/wordpress-setting-guide/)

     (2) 플러그인 설정하기 > Widget Setting

2. 직접 삽입 (Not Recommended)

   - **직접 삽입 방식은 추천하지 않습니다.**
   - 작업에 필요한 **php 코드 수정**은 잘못될 경우 **사이트 전체에 영향을 미치거나, 다른 플러그인과 충돌할 수 있습니다.** 코드 작업에 익숙하지 않은 매체는 플러그인을 활용해주세요
   - 2021 기본 테마(Twenty Twenty-One) 기준의 가이드를 제공하며, 테마별 커스텀 가이드는 제공하지 않습니다
   - 🤔 How to

     1. Appearance > Theme Editor

        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be08c4ff-18ef-44d3-9588-506544057bee/_2021-01-13__1.20.13.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be08c4ff-18ef-44d3-9588-506544057bee/_2021-01-13__1.20.13.png)

     2. Theme Files > template-parts

        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4aa82137-9b0c-4440-b404-08f40e06c045/_2021-01-13__1.20.55.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4aa82137-9b0c-4440-b404-08f40e06c045/_2021-01-13__1.20.55.png)

        - content > content-page.php
          - Pages 타입에 위젯을 삽입할 경우, 이 파일을 선택합니다
        - content > content-single.php
          - Posts 타입에 위젯을 삽입할 경우, 이 파일을 선택합니다
        - 테마에 따라 template-parts의 하위 구조는 다를 수 있습니다

     3. 코드 에디터에서 본문 영역을 찾은 뒤, 적절한 위치에 위젯 스크립트를 삽입하고 저장(Update file)합니다

        ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77e6182e-4546-4cec-a6b5-2f85caccd8cd/_2021-01-13__1.23.54.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77e6182e-4546-4cec-a6b5-2f85caccd8cd/_2021-01-13__1.23.54.png)

        - 본문 영역 네이밍은 테마에 따라 상이하지만, className에 `content`가 포함된 경우가 많으니 참고해주세요
        - 기존 코드를 수정하지 않도록 주의해주세요
        - php 코드 사이에 삽입되지 않도록 주의해주세요

          ```php
          <?php
          	/* original php code */
          	/* do not insert dable code */
          ?>
          ```

## FAQ

### 위젯이 원하지 않는 페이지에도 노출됩니다.

- 🤔 위젯이 노출되는 페이지의 기준은 무엇인가요?

  - 위젯이 노출될 페이지는, Dable Plugin > Default Settings > Target Post Types 에서 설정할 수 있습니다

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f33282a7-81cf-4185-a84b-0e4abf193b83/_2021-01-11__4.50.34.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f33282a7-81cf-4185-a84b-0e4abf193b83/_2021-01-11__4.50.34.png)

  - Target Post Types은 매체에서 해당 페이지를 어떤 타입으로 생성했냐에 따라 달라지며, og:type 속성과는 별개입니다

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f252811-b5ba-4c39-bdd5-34f0e9593a3a/_2021-01-11__4.52.00.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f252811-b5ba-4c39-bdd5-34f0e9593a3a/_2021-01-11__4.52.00.png)

  - 대부분의 게시물은 `Posts` 타입으로 생성됩니다.
    `Pages` 타입은 Contact나 Privacy Policy와 같은 단일 페이지 생성시 쓰입니다.
    `Pages` 타입은 `Posts`와 달리 시간 역순으로 노출되지 않는다는 차이가 있습니다.

- 🤔 어떻게 막을 수 있나요?

  1. 해당 페이지들의 생성 타입을 확인합니다

     - 데이블에서 확인할 수 있는 방법

       - Chrome DevTools > 템플릿 class명에 page 혹은 post가 포함되어 있을 수 있습니다

         ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5597867e-a086-4c70-80fd-3344a2b5c9c7/_2021-03-09__10.40.53.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5597867e-a086-4c70-80fd-3344a2b5c9c7/_2021-03-09__10.40.53.png)

         Pages type인 경우

         ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e38058a-c161-461e-9646-fd00c0daf736/_2021-03-09__10.40.28.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e38058a-c161-461e-9646-fd00c0daf736/_2021-03-09__10.40.28.png)

         Posts type인 경우

       - 테마에 따라 class명에 명시되어 있지 않을 수 있습니다

     - 매체에서 확인할 수 있는 방법
       - Posts 타입이라면, Posts > All Posts 에서 확인할 수 있습니다
       - Pages 타입이라면, Pages > All Pages 에서 확인할 수 있습니다

  2. Target Post Types 옵션으로 걸러낼 수 있다면, 옵션을 변경합니다

     예) 원치 않는 페이지가 모두 Pages 타입인 경우, Target Post Types에서 Pages 옵션을 Off

  3. 걸러낼 수 없다면, 위젯 스크립트를 커스텀하여 다시 적용합니다

     - Script Custom Sample

       ```jsx
       <!-- Begin Dable bottom / For inquiries, visit http://dable.io -->
       <div id="dablewidget_1oV9EjXP" data-widget_id="1oV9EjXP">
       <script>
       (function(d,a,b,l,e,_) {
       if(d[b]&&d[b].q)return;d[b]=function(){(d[b].q=d[b].q||[]).push(arguments)};e=a.createElement(l);
       e.async=1;e.charset='utf-8';e.src='//static.dable.io/dist/plugin.min.js';
       _=a.getElementsByTagName(l)[0];_.parentNode.insertBefore(e,_);
       })(window,document,'dable','script');
       dable('setService', 'kabargames.id');
       dable('sendLogOnce');

       **var urls = [
       'https://www.kabargames.id/about-us/',
       'https://www.kabargames.id/contact-us/',
       'https://www.kabargames.id/kebijakan-privasi/'
       ];**

       if (urls.indexOf(document.URL) === -1) {
       	dable('renderWidget', 'dablewidget_1oV9EjXP');
       }
       </script>
       </div>
       <!-- End bottom / For inquiries, visit http://dable.io -->
       ```

       - 원치 않는 페이지 URL을 `' '`single quote로 감싼 뒤 urls 배열 안에 삽입합니다. 페이지가 여러 개일 경우 `,`로 구분합니다
       - 스크립트 커스텀이 필요한 경우, 개발팀에 제작 혹은 검토를 요청해주세요

### 위젯의 위치를 임의로 조정할 수 있나요?

1. Dable Plugin (Recommended)

   - 위젯의 위치는 Widget Setting 옵션에 따라 자동으로 삽입되며, 위치를 변경할 수 없습니다

     - `Bottom of article` article 영역 직후
     - `Left side of article` / `Right side of article` article 영역의 직전

       - 현재로서 Left와 Right의 차이는 없습니다

         ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eff5d9c4-ae9c-4d0c-a084-209bc44ebde3/_2021-01-12__11.23.34.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eff5d9c4-ae9c-4d0c-a084-209bc44ebde3/_2021-01-12__11.23.34.png)

         Left side of article

         ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ec7fdff-3ae6-4e9d-aed1-3c6e43bd48d6/_2021-01-12__11.22.29.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ec7fdff-3ae6-4e9d-aed1-3c6e43bd48d6/_2021-01-12__11.22.29.png)

         Right side of article

2. 직접 삽입 (Not Recommended)
   - php 코드 수정에 익숙한 매체의 경우, [원하는 위치에 스크립트를 삽입](https://www.notion.so/WordPress-726443fcf7134dd09b0b7ed755a72c63)하면 위치를 조정할 수 있습니다
   - 혹은, [인아티클 효과](https://www.notion.so/WordPress-726443fcf7134dd09b0b7ed755a72c63)를 활용할 수 있습니다
3. 타 플러그인 활용

   - 일부 Ad management 플러그인을 통해 삽입할 수 있습니다
   - 단, 노출 위치는 [해당 플러그인에서 제공하는 특정 조건](https://www.notion.so/WordPress-726443fcf7134dd09b0b7ed755a72c63)에 한해서만 설정 가능합니다
   - Ad management 플러그인 중 가장 사용자가 많은 Ad Inserter 기준의 기본 가이드만 제공하며, 추가 문의는 대응하지 않습니다

     - 🤔 How to

       1. [Ad Inserter 플러그인](https://wordpress.org/plugins/ad-inserter/) Install > Activate
       2. Settings > Ad Inserter 에디터 창에 위젯 스크립트를 삽입합니다

          ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63e37d51-ee85-48e8-a756-4e38d417b48b/_2021-01-14__6.02.02.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63e37d51-ee85-48e8-a756-4e38d417b48b/_2021-01-14__6.02.02.png)

       3. 코드를 적용할 페이지 속성을 선택할 수 있습니다

          ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1efc9bf-887f-435d-9aff-c02ab400fd91/_2021-01-14__6.11.17.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1efc9bf-887f-435d-9aff-c02ab400fd91/_2021-01-14__6.11.17.png)

       4. 코드를 적용할 페이지 내 위치를 선택할 수 있습니다

          ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5dd9a32-1cbe-40ad-a28a-4e65c99d79d0/_2021-01-14__6.13.31.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5dd9a32-1cbe-40ad-a28a-4e65c99d79d0/_2021-01-14__6.13.31.png)

       5. 이외의 설정 방법은 [Ad Inserter 공식 가이드](https://adinserter.pro/documentation/common-settings)를 참고해주세요

### 인아티클/시크릿 위젯 효과를 적용할 수 있나요?

1. Dable Plugin (Recommended)
   - 두 가지 효과 모두 적용할 수 없습니다
2. 직접 삽입 (Not Recommended)
   - 인아티클 효과
     - 적용 가능합니다
     - 단, `itemprop="articleBody"` 가 적용되어 있어야 합니다
     - 적용되어 있지 않은 경우, Default Setting > Content Wrapper Setting 옵션을 활성화해주세요
   - 시크릿 효과
     - 적용 가능합니다
     - `본문 최상단 스크롤` 옵션
       - [코드 삽입시](https://www.notion.so/WordPress-726443fcf7134dd09b0b7ed755a72c63) articleBody 태그 안에 위젯 스크립트를 삽입해야 합니다
       - 테마에 따라 articleBody 위치를 임의로 변경하는 등의 부가 작업이 필요할 수 있습니다
         - 이 작업은 사이트 전체에 영향을 미칠 수 있어 추천하지 않습니다
     - `페이지 최상단 스크롤` 옵션
       - [코드 삽입시](https://www.notion.so/WordPress-726443fcf7134dd09b0b7ed755a72c63) 페이지의 최상단 위치에 위젯 스크립트를 삽입해야 합니다

### Sidebar 영역에 위젯을 적용할 수 있나요?

- 네, 매체에서 사용하는 테마가 아래 조건을 모두 만족하는 경우 가능합니다

  - 🤔 Requirement

    1. Widgets 기능 지원
       - Apprearance 하위 메뉴에 Widgets가 있는지 확인해주세요
    2. Sidebar 영역 구분

       - Appearance > Widgets 우측 영역에 Sidebar가 있는지 확인해주세요

         - Sidebar의 정확한 네이밍은 테마에 따라 다를 수 있습니다

         ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c5d71f5-5fef-4ed9-8152-a93024b92789/_2021-01-12__1.20.21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c5d71f5-5fef-4ed9-8152-a93024b92789/_2021-01-12__1.20.21.png)

- 조건을 만족한다면, 가이드를 따라해주세요.

  - 🤔 How to

    1. Avaliable Widgets > Dable 을 drag&drop해서 Sidebar 영역에 삽입합니다

       ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d17bcaed-cf5e-41b3-8a47-c3f3c7d7cb7c/_2021-01-12__1.18.24.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d17bcaed-cf5e-41b3-8a47-c3f3c7d7cb7c/_2021-01-12__1.18.24.png)

       - Available Widgets 목록에 Dable이 없다면, 플러그인 설치 여부를 확인해주세요
       - 플러그인 install/activate를 하면 Available Widgets 목록에 나타납니다

    2. Title과 Widget ID를 작성합니다

       ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0528bc6a-bc69-48b4-ae1a-fa05522c135e/_2021-01-12__1.32.20.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0528bc6a-bc69-48b4-ae1a-fa05522c135e/_2021-01-12__1.32.20.png)

       - Title은 사이드바 영역의 제목으로, 위젯의 title 영역과는 별개입니다

         📝 Title이 비어있는 경우, 위젯이 생성되지 않습니다. 타이틀을 작성하거나, 작성한 뒤 Do not show title 옵션을 선택해주세요

       - Widget ID를 기준으로 스크립트가 자동 생성되기 때문에 위젯 코드는 삽입하지 않아도 됩니다

    3. 아래와 같이 Sidebar 영역에 노출됩니다

       ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f7526bd-cf6e-4d69-91b6-3b1470d142e8/_2021-01-12__1.34.31.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4f7526bd-cf6e-4d69-91b6-3b1470d142e8/_2021-01-12__1.34.31.png)

- 🤔 반응형 위젯도 적용할 수 있나요?
  - 하나의 위젯에 반응형 설정이 된 경우, 적용할 수 있습니다
    - 단, 매체에서 사용하는 테마에 따라 사이드바 영역의 너비, 모바일에서의 처리방법이 다르기 때문에, 반응형 설정이 까다로운 경우 적용이 불가능할 수 있습니다
  - Responsive Pair 위젯은 적용할 수 없습니다

### 반응형 사이트지만 PC/MO에서 각각 다른 테마를 사용하고 있습니다

- 테마가 다르다면 비 반응형 사이트로 취급해야 합니다
- `Script for Responsive Web` 옵션이 아닌, `Script for PC/Mobile Web` 옵션으로 스크립트를 삽입해주세요

### 대시보드에 섬네일이 노출되지 않거나, 🚫 섬네일로 바뀌어 보입니다

- 아래 두 가지 상황을 확인해주세요. ([Media FAQ](https://www.notion.so/f87a73a4165047229c4119253c31b522) 참고)

1. 이미지 접근 권한이 허용되지 않은 경우

   - 3rd party access 허용을 요청해주세요
   - WP-CORS 플러그인을 통한 가이드를 제공합니다
   - 🤔 How to

     1. WP-CORS 플러그인 Install > Activate
     2. Settings > CORS > 아래 코드 삽입

        `http://dable.io, https://dable.io, http://api.dable.io, https://api.dable.io`

2. 이미지 hotlinking을 막아둔 경우
   - hotlink 제한 해제를 요청해주세요
   - 매체에서 직접 설정하지 않았더라도 테마에 따라 자동 설정되어 있을 수 있습니다
   - [참고 가이드](https://www.hostinger.com/tutorials/hotlinking#3-Using-WordPress-Plugins) (설정 방법이지만 역으로 추적할 수 있습니다)

### 매체 서버에 있는 폰트를 적용할 수 있나요?

- 네, 다만 매체에서 [3rd party access를 허용](https://www.notion.so/WordPress-726443fcf7134dd09b0b7ed755a72c63)해줘야 합니다
  - 단, 폰트 파일 서빙에 대한 서버비는 매체에서 부담하게 됩니다
- 만약 매체에서 허용을 원치 않거나 허용을 하지 못할 경우,
  1. 데이블 서버에 폰트 파일을 업로드해 사용할 수 있습니다 (Not Recommended)
     - 단, 데이블에서 서버비용을 지불하게 되므로 CDN 비용을 미리 계산해 매체별 지원여부를 결정하는 것이 좋습니다
     - [CDN 비용 계산 가이드](https://www.notion.so/b034b9bc1b9e46cf903dad92549f45b0)
  2. 유사한 대체 폰트를 적용할 수 있습니다

### Wordpress + AMP에서도 Dable Plugin이 정상 동작하나요?

- 네, 다만 아래 조건을 모두 만족하는 경우에만 가능합니다
  - 🤔 Requirement
    1. **매체의 테마 + amp 플러그인 + dable 플러그인 조합에서 충돌이 없어야 합니다**
       - 충돌 여부는 데이블에서는 미리 확인할 수 없으며, 플러그인 실행 단계에서 매체에서 파악할 수 있습니다
       - 충돌로 인해 위젯이 정상 작동하지 않는다면 amp에 적용이 불가능합니다
    2. **모바일 페이지가 모두 AMP로만 제공되는 것이 동의되어야 합니다**
       - 가이드대로 적용할 경우, 모바일로 접근시 모두 AMP로 redirect됩니다
       - 모바일과 AMP가 분리되어야 하는 경우라면 아직 지원하지 않습니다
       - 단, 모바일은 WordPress를 사용하지 않고, AMP 전용으로 WordPress를 사용하는 경우, redirect 없이 모바일과 AMP를 분리하여 사용할 수 있습니다.
       - 동의된 경우, PC와 AMP 위젯 2종만 있으면 됩니다
    3. **PC 에서 수집된 로그가 있어야 합니다 (AMP에서는 로그 수집이 불가능)**
       - AMP 위젯이 PC(+Mobile) SID에 속해 있다면 별도 세팅하지 않아도 됩니다
       - AMP SID가 분리되어 있다면 db alias로 받아옵니다
    4. **AMP 위젯이 추천 위젯인 경우, 관련기사 알고리즘은 사용할 수 없습니다**
       - `data-item-id` 세팅이 불가능하기 때문에 지원하지 않습니다
- 조건을 만족한다면, 가이드를 따라해주세요.
  단, 가이드는 AMP 공식 플러그인 기준이며, 타 플러그인에 대해서는 가이드를 제공하지 않습니다 - 🤔 How to 1. [AMP 공식 플러그인](https://wordpress.org/plugins/amp/) Install > Activate 2. 데이블 WP 플러그인을 통해 코드를 삽입합니다 - Script for PC/Mobile Web 옵션 선택 - PC 위젯 코드는 PC 영역에, AMP 위젯 코드는 Mobile 영역에 삽입합니다 - AMP 코드에서 `data-item-id="ITEM_ID_TO_BE_REPLACED"` 는 삭제해주세요

                  (광고 전용 위젯은 해당되지 않습니다)

              ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd17aa9b-fff4-4441-8a14-118c4a5bf7d5/_2020-12-30__2.58.21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd17aa9b-fff4-4441-8a14-118c4a5bf7d5/_2020-12-30__2.58.21.png)

          3. AMP 플러그인 세팅에서 redirect 옵션을 활성화해주세요
              - Settings > Advanced Settings > Redirect mobile visitors to AMP

              ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef2eff77-4fc9-45f2-b4b1-3ca061fcb363/_2020-12-30__2.40.06.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef2eff77-4fc9-45f2-b4b1-3ca061fcb363/_2020-12-30__2.40.06.png)

### Wordpress + infinite scroll 구조에서 Dable Plugin을 적용할 수 있나요?

- 적용할 수는 있으나, 최초 로드된 기사에만 위젯이 노출됩니다
- 모든 기사에 위젯을 노출하기 위해서는 아래 조건과 가이드를 따라주세요

  1. 매체에서 inifnite scroll을 어떻게 구현했는지 확인합니다
     - 워드프레스에서 infinite scroll을 구현하는 방법
       1. [php 코드를 수정](https://wpengine.com/resources/infinite-scroll-wordpress/#Adding_Infinite_Scroll_With_Code)
       2. [infinite scroll 플러그인을 활용](https://wpengine.com/resources/infinite-scroll-wordpress/#Adding_Infinite_Scroll_With_a_Plugin)
  2. 구현 방식에 따라 지원 여부가 달라집니다

     - 코드를 수정한 경우, 테마에 따른 코드 수정 방식이 천차만별이므로 가이드를 제공하지 않습니다
     - 플러그인을 사용한 경우, 기본 가이드를 제공합니다

       가이드는 infinite scroll 플러그인 중 가장 사용자가 많은 [Ajax Load More](https://wordpress.org/plugins/ajax-load-more/) 기준이며, 추가 문의는 대응하지 않습니다

       - 🤔 How to

         - Ajax Load More > Repeater Templates 이동
         - Template Code창에 위젯 스크립트를 삽입합니다

           - 추천 위젯이라면, `reco-Infinite Scroll / SPA-specific` 버전을

             광고 위젯이라면, `ads-Infinite Scroll / SPA-specific` 버전을 삽입해주세요

             ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77cb3dc9-b387-4332-b5e0-bbdffebe3fb3/_2021-01-08__12.58.43.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77cb3dc9-b387-4332-b5e0-bbdffebe3fb3/_2021-01-08__12.58.43.png)

           - `reco+SendLog` 버전을 삽입할 경우, Dable Plugin과 동일하게 최초 로드된 기사에만 위젯이 노출됩니다

         - 이외의 설정 방법은 [Ajax Load More 공식 가이드](https://connekthq.com/plugins/ajax-load-more/docs/implementation-guide/)를 참고해주세요

### 위젯이 Mobile(or PC)에서만 사라집니다

- 플러그인의 Widget Setting > Widget 옵션을 확인해주세요

  ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9292e5b4-2ab3-40f2-bb35-dad5225f1c0a/_2021-02-08__11.11.22.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9292e5b4-2ab3-40f2-bb35-dad5225f1c0a/_2021-02-08__11.11.22.png)

- 반응형 위젯 코드를 `Script for PC/Mobile Web` 옵션 선택 후,
  - PC textarea에만 삽입한 경우, Mobile에서는 위젯이 노출되지 않습니다
  - Mobile textarea에만 삽입한 경우, PC에서는 위젯이 노출되지 않습니다
- 반응형 위젯이라면 반드시 `Script for Responsive Web` 옵션을 선택해야 합니다
- 🤔 PC의 mobile view에서 refresh를 하기 전에는 잘 보이는데, refresh를 하면 사라집니다
  - 페이지 로딩 시점에 기기를 감지하고, 감지된 기기를 기준으로 위젯을 보여줍니다
  - PC로 보다가 mobile view로 변경했더라도 refresh를 하지 않았다면 여전히 기기는 PC로 감지된 상태입니다
  - 때문에, resize 혹은 mobile view 변경 시점에는 잘 보이던 위젯이, refresh를 통해 mobile이 감지되면서 사라질 수 있습니다

### 워드프레스 환경을 테스트해볼 수 있나요?

- 워드프레스 로컬 테스트 툴을 설치해 테스트해볼 수 있습니다
- 🤔 How to

  1. [LocalWordPress](https://localwp.com/) > Download > 환경 선택 > 정보 입력 후 다운로드 > 파일 실행
  2. 설치된 Local 실행 > 테스트 사이트 생성

     ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2f3155f-7444-4d00-b8d2-33459bf8f662/_2021-03-09__4.08.08.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2f3155f-7444-4d00-b8d2-33459bf8f662/_2021-03-09__4.08.08.png)

     - Setup Site > site name 입력
     - Setup Environment > Preferred 선택
     - Setup WordPress > Admin 접속시 사용할 계정 정보 입력 (실제 WordPress 계정과는 무관)

  3. 생성된 사이트 선택 > Admin 접속

     ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2ae5077-b387-4ac4-b86b-8c353f4d005b/_2021-03-10__10.25.13.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2ae5077-b387-4ac4-b86b-8c353f4d005b/_2021-03-10__10.25.13.png)

  4. 데이블 플러그인 설치

     ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c374938-fe6c-43a9-af7c-d46a16ed010f/_2021-03-10__11.06.06.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c374938-fe6c-43a9-af7c-d46a16ed010f/_2021-03-10__11.06.06.png)

     - Plugins > Add New > `Dable` 검색 > Install Now > Activate

---

- 👩‍💻 관련자료 (for dev team)

  [기획문서](https://anxmi8.axshare.com/#g=1&p=pc)

  [Github](https://github.com/teamdable/wordpress)

  [플러그인 동작 확인 및 배포 방법](https://www.notion.so/77ad6938a13541489827a087da5af108)
