---
title: ⚔️ CSRF & XSS
summary: Let's talk about Cross Site Request Forgery (CSRF) & Cross-Site-Scripting (XSS)!
date: 2024-09-30
authors:
  - admin
tags:
  - Hugo Blox
  - Markdown
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com)'
---

# **Cross Site Scripting (XSS)**

XSS는 클라이언트 사이드 취약점 중 하나로, 공격자가 웹 리소스에 악성 스크립트를 삽입해 이용자의 웹 브라우저에서 해당 스크립트를 실행할 수 있습니다. 공격자는 해당 취약점을 통해 특정 계정의 세션 정보를 탈취하고 해당 계정으로 임의의 기능을 수행할 수 있습니다. 예를 들어, 드림핵 웹 페이지에서 XSS 취약점이 존재하면 https://dreamhack.io 내에서 오리진 권한으로 악성 스크립트를 삽입합니다. 이후에 이용자가 악성 스크립트가 포함된 페이지를 방문하면 공격자가 임의로 삽입한 스크립트가 실행되어 쿠키 및 세션이 탈취될 수 있습니다.

# **XSS 발생 예시와 종류**

XSS 공격은 이용자가 삽입한 내용을 출력하는 기능에서 발생합니다. 이러한 기능의 예로는 로그인 시 출력되는 “안녕하세요, OO회원님”과 같은 문구 또는 게시물과 댓글이 있습니다.

클라이언트는 HTTP 형식으로 웹 서버에 리소스를 요청하고 서버로부터 받은 응답, 즉 HTML, CSS, JS 등의 웹 리소스를 시각화하여 이용자에게 보여줍니다. 이때, HTML, CSS, JS와 같은 코드가 포함된 게시물을 조회할 경우 이용자는 변조된 페이지를 보거나 스크립트가 실행될 수 있습니다

| **종류** | **설명** |
| --- | --- |
| Stored XSS | XSS에 사용되는 악성 스크립트가 서버에 저장되고 서버의 응답에 담겨오는 XSS |
| Reflected XSS | XSS에 사용되는 악성 스크립트가 URL에 삽입되고 서버의 응답에 담겨오는 XSS |
| DOM-based XSS | XSS에 사용되는 악성 스크립트가 URL Fragment에 삽입되는 XSS
• Fragment는 서버 요청/응답 에 포함되지 않습니다. |
| Universal XSS | 클라이언트의 브라우저 혹은 브라우저의 플러그인에서 발생하는 취약점으로 SOP 정책을 우회하는 XSS |

### **Cross Site Request Forgery (CSRF)**

→ 쿠키 또는 세션을 사용해 이용자를 식별한다. 임의 이용자의 쿠키를 사용할 수 있다면, 이는 곧 임의 이용자의 권한으로 웹 서비스의 기능을 사용할 수 있음을 뜻한다.

CSRF는 임의 이용자의 권한으로 임의 주소에 HTTP 요청을 보낼 수 있는 취약점이다. 공격자는 임의 이용자의 권한으로 이득을 취한다.

```jsx
# 이용자가 /sendmoney에 접속했을때 아래와 같은 송금 기능을 웹 서비스가 실행함.
@app.route('/sendmoney')
def sendmoney(name):
    # 송금을 받는 사람과 금액을 입력받음.
    to_user = request.args.get('to')
	amount = int(request.args.get('amount'))
	
	# 송금 기능 실행 후, 결과 반환	
	success_status = send_money(to_user, amount)
	
	# 송금이 성공했을 때,
	if success_status:
	    # 성공 메시지 출력
		return "Send success."
	# 송금이 실패했을 때,
	else:
	    # 실패 메시지 출력
		return "Send fail."
```

### Cross Site Request Forgery 동작

CSRF 공격에 성공하기 위해서는 공격자가 작성한 악성 스크립트를 이용자가 실행해야 함. → 메일 보내거나 글 작성으로 이용자가 이를 조회하도록 유도

, CSRF 공격 스크립트는 HTML 또는 JS를 통해 작성할 수 있다. 이미지를 불러오는 img 태그를 사용하거나 웹 페이지에 입력된 양식을 전송하는 form 태그를 사용하는 방법이 있다. 이 두 개의 태그를 사용해 HTTP 요청을 보내면 HTTP 헤더인 Cookie에 이용자의 인증 정보가 포함된다.

```jsx
/* 새 창 띄우기 */
window.open('http://bank.dreamhack.io/sendmoney?to=Dreamhack&amount=1337');
/* 현재 창 주소 옮기기 */
location.href = 'http://bank.dreamhack.io/sendmoney?to=Dreamhack&amount=1337';
location.replace('http://bank.dreamhack.io/sendmoney?to=Dreamhack&amount=1337');
```

# **XSS와 CSRF의 차이**

XSS와 CSRF는 스크립트를 웹 페이지에 작성해 공격한다는 점에서 매우 유사합니다. 그렇다면 두 취약점의 공통점과 차이점을 알아보겠습니다.

## **공통점**

두 개의 취약점은 모두 클라이언트를 대상으로 하는 공격이며, 이용자가 악성 스크립트가 포함된 페이지에 접속하도록 유도해야 합니다.

## **차이점**

두 개의 취약점은 공격에 있어 서로 다른 목적을 가집니다. XSS는 인증 정보인 세션 및 쿠키 탈취를 목적으로 하는 공격이며, 공격할 사이트의 오리진에서 스크립트를 실행시킵니다.

CSRF는 이용자가 임의 페이지에 HTTP 요청을 보내는 것을 목적으로 하는 공격입니다. 또한, 공격자는 악성 스크립트가 포함된 페이지에 접근한 이용자의 권한으로 웹 서비스의 임의 기능을 실행할 수 있습니다.

** you can see my past posts in my velog https://velog.io/@iq1564/posts