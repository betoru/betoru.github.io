---
layout: post
date: 2020-03-16 16:59:00 +0900
title: 'JavaScript: jQuery lazyload()'
category:
  - javascript
tags:
  - javascript
  - image
  - lazy
  - lazyload
img: js-1.png # Add image post (optional)  
---

* Kramdown table of contents
{:toc .toc}

## lazyload

> 웹페이지를 호출 할 때, 모든 이미지를 로드하지 않고 사용자가 보는 화면의 이미지부터 순차적으로 로드하여 화면을 빠르게 호출한다.

#### 참고한 글
- [https://appelsiini.net/projects/lazyload/](https://appelsiini.net/projects/lazyload/)


```html
<html>
<head>
    <script type="text/javascript" src="http://code.jquery.com/jquery.min.js"></script>
    <script type="text/javascript" src="jquery.lazyload.js"></script> // 플로그인 참조
    <script type="text/javascript">
        $(function(){
            $('img.gocoder').lazyload({        // 이미지를 동적으로 호출 하도록
                placeholder : 'loading.gif',    // 로딩 이미지
                threshold: 0,                 // 접근 ~px 이전에 로딩을 시도한다.
                load : function(){              // 로딩시에 이벤트
                    $(this).attr('alt',$(this).attr("data-original"));
                }
            });
        });
    </script>
</head>
<body>
    <Table>
        <tr>
            <td><img data-original="img (1).jpg"  class="gocoder" width="300"></td>
            <td><img data-original="img (2).jpg"  class="gocoder" width="300"></td>
        </tr>
        <tr>
            <td><img data-original="img (3).jpg"  class="gocoder" width="300"></td>
            <td><img data-original="img (4).jpg"  class="gocoder" width="300"></td>
        </tr>
    </Table>
</body>
</html>
```
```html

1. lazyload() -> 7번째 줄
$('img.gocoder').lazyload()
- 해당 기능을 호출합니다. 이렇게만 쓰셔도 옵션 없이 정상 작동합니다.

2. placeholder -> 8번째 줄
placeholder : 'loading.gif'
- 호출 전 이미지를 지정합니다. 보통 로딩 gif가 올거 같네요. img 태그의 src의 주소를 매칭하여 사용할 수 있습니다.

3. threshold -> 9번째 줄
threshold: 0,
- 호출 할 시점을 입력합니다. 숫자가 높을 수록 먼저 로딩을 하고 있습니다.

4. load -> 10~12번째 줄
load : function()
- 호출 시점에 이벤트를 실행 할 수 있습니다. 파일명을 이미지 속성 alt에 입력 되게 해보았습니다.
