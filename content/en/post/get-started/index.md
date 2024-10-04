---
title: 🍪 Cookie & Session
summary: Let's talk about our Data, Cookie & Session!
date: 2024-09-30

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com)'

authors:
  - admin
  - Ted

tags:
  - Academic
  - Hugo Blox
  - Markdown
---

### 쿠키 (Cookie)

→ 클라이언트의 IP 주소와 User-Agent는 매번 변경될 수 있다. HTTP 프로토콜의  Connectionless & Stateless 특징 때문에 웹 서버는 클라이언트를 기억할 수 없다.

- Connectionless: 하나의 요청에 하나의 응답을 한 후 연결을 종료 새 요청에 항상 새로운 연결
- Stateless: 통신이 끝난 후 상태 정보를 저장하지 않는다. 이전 연결 데이터를 새 연결에서 요구 불가능

쿠키는 Key롸 Value로 이뤄진 일종의 단위. 서버→클라이언트 (쿠키 발급), 클라이언트→서버(쿠키 전송), 서버는 클라이언트의 요청에 포함된 쿠키를 확인해 클라이언트 구분


### 쿠키 변조

쿠키는 클라이언트의 브라우저에 저장되고 요청에 포함되는 정보다. 따라서, 악의적인 클라이언트 쿠키 정보를 변조해서 서버에 요청을 보낼 수 있다. 만약 서버사 별다른 검증 없니 쿠키를 통해 이용자의 인증 정보를 식별한다면 공격자가 타 이용자를 사칭해서 정보를 탈취할 수 있다.


### 세션 (Session)

→ 세션은 인증 정보를 서버에 저장하고 해당 데이터에 접근할 수 있는 키(유추할 수 없는 랜덤한 문자열)를 만들어 클라이언트에 전달하는 방식으로 작동한다. 해당 키를 일반적으로 Session ID라고 한다.

브라우저는 해당 키를 쿠키에 저장하고 이후에 HTTP 요청을 보낼 때 사용한다. 서버는 요청에 포함된 키에 해당하는 데이터를 가져와 인증 상태를 확인한다.

### 세션 하이재킹

→ F12 의 네트워크에서 `Preserve log`를 체크하고 로그인을 하면 로그인 성공 시 응답을 볼 수 있습니다. 응답을 살펴보면, 서버에서 `set-cookie` 헤더를 통해 브라우저의 쿠키에 세션 정보를 저장하는 것을 볼 수 있다, 이후 Application에서 쿠키 목록의 Sessionid 를 Delete, 이후 새로운 sessionid를 덧대면 로그인할 수 있다.이게 바로 세션 하이재킹

**키워드**

---

- **Connectionless**: 하나의 요청에 하나의 응답을 한 후 연결을 종료하는 것을 의미합니다.
- **Stateless**: 통신이 끝난 후 상태 정보를 저장하지 않는 것을 의미합니다.
- **쿠키 (Cookie)**: HTTP에서 상태를 유지하기 위해 사용하는 Key-Value 형태의 값
- **세션 (Session)**: 쿠키에 포함된 Session ID를 사용해 서버에 저장된 세션 데이터에 접근하는 방식
- **세션 하이재킹 (Session Hijacking)**: 타 이용자의 쿠키를 훔쳐 인증 정보를 획득하는 공격

이용자가 악의적인 페이지를 접속했을 때, 페이지가 자바스크립트를 이용해 이용자의 SNS 웹 서비스로 요청을 보낸다면 어떻게 될까? 브라우저는 요청을 보낼 때 헤더에 해당 웹 서비스 쿠키를 포함시킬 것이다.

따라서 자바스크립트로 요청을 보낸 페이지는 로그인 된 이용자의 SNS 응답을 받는다. 이에 더해 마음대로 페이지 접속자의 SNS에 글을 올리거나, 삭제하고 SNS 메신저를 읽는 것도 가능할 것이다.

⇒ 이와 같은 문제를 방지하기 위해 동일 출처 정책, Same Origin Policy (SOP) 보안 매커니즘이 탄생했다.

### Same Origin Policy의 오리진(Origin) 구분 방법

→ 이제 브라우저가 가져온 정보의 출처인 Origin은 프로토콜(Protocol, Scheme, 포트(Port), 호스트(Host)로 구성된다. 구성 요소가 모두 일치해야 동일한 오리진이라고 한다.

`https://same-origin.com/`라는 오리진과 아래 URL을 비교했을 때 결과는 다음과 같다

| **URL** | **결과** | **이유** |
| --- | --- | --- |
| https://same-origin.com**/frame.**html | Same Origin | Path만 다름 |
| **http://**same-origin.com/frame.html | Cross Origin | Scheme이 다름 |
| https://**cross.**same-origin.com/frame.html | Cross Origin | Host가 다름 |
| https://same-origin.com**:1234**/ | Cross Origin | Port가 다름 |

### Cross-Origin Resource Sharing(CORS)

→ Same Origin Policy 제한 완화

- 브라우저가 SOP에 구애받지 않고 외부 출처에 대한 접근을 허용해주는 경우가 존재한다. 예를 들어, 자바스크립트, CSS 등의 리소스를 불러오는 < img >, < style >, < script > 등의 태그는 SOP의 영향을 받지 않는다.

- 위 경우 외에도 웹 서비스에서 SOP를 완화하여 다른 출처의 데이터를 처리 해야 하는 경우도 있다. 예를 들어 특정 포철 사이트가 카페, 블로그, 메일 서비스를 운영하고 있다고 하자. 각 서비스의 호스트는 다르며 브라우저는 각 사이트의 오리진이 다르다고 생각.

- 이런 환경에서 이용자가 수신한 메일의 개수를 메인 페이지에 출력하려면 개발자는 메인 페이지에서 메일 서비스에 관련된 리소스를 요청하도록 해야한다. 이 때, 두 사이트는 오리진이 다르므로 SOP를 적용받지 않고 리소스를 공유할 방법이 필요하다.

**⇒ 위와 같은 상황에서 자원을 공유하기 위해 사용할 수 있는 공유 방법을 교차 출처 리소스 공유 (Cross Origin Resource Sharing, COPS)라고 한다.**

: CORS는 HTTP 헤더에 기반하여 Cross Origin 간에 리소스를 공유하는 방법이다. 발신측에서 CORS 헤더를 설정해 요청하면, 수신 측에서 헤더를 구분해 정해진 규칙에 맞게 데이터를 가져갈 수 있도록 설정한다.

### JSON with Padding (JSONP)

JSONP는 SOP에 구애 받지 않고 외부 출처에 대한 접근을 허용하는 < script > 태그로 Cross Origin의 데이터를 불러온다 하지만 < script > 태그 내에서는 데이터를 자바 스크립트의 코드로 인식하기 때문에 Callback 함수를 사용해야 한다. Cross Origin에 요청할 때 callback 파라미터에 어떤 함수로 받아오는 데이터를 핸들링할지 넘겨주면, 대상 서버는 전달된 callback으로 데이터를 감싸 응답한다.

** you can see my past posts in my velog https://velog.io/@iq1564/posts