---
title: 🛣️ File Vulnerability
summary: about File Upload Vulnerability & File Download Vunerability!
date: 2024-09-30
authors:
  - admin
tags:
  - Hugo
  - Hugo Blox
  - Markdown
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com)'
---

## File Upload Vulnerability(파일 업로드 취약성)

⇒ 공격자의 파일을 업로드하는 과정에서 발생. 파일 시스템 상 임의 경로에 원하는 파일을 업로드, 악성 확장자를 갖는 파일을 업로드할 수 있을 때 발생.

원하는 cmd를 실행하는 원격 코드 실행 취약점을 유발할 수 있다

### Path Traversal**🛣️**

⇒ 파일 업로드를 허용하는 대게의 서비스는 보안을 위해 특정 디렉터리에만 업로드를 허용한다. 만약 이러한 제약이 없다면 악의적인 이용자가 웹 서버의 소스 코드나 서버에 있는 중요 시스템 파일을 덮어 쓸 위험이 있다. Path Traversal 취약점은 업로드에 존재하는 이러한 제약을 우회하여, 임의 디렉터리에 파일을 업로드할 수 있는 취약점을 의미한다.

```python
from flask import Flask, request
app = Flask(__name__)
@app.route('/fileUpload', methods = ['GET', 'POST'])
def upload_file():
	if request.method == 'POST': # 사용자가 파일 업로드할 때 POST 요청
		f = request.files['file'] # 파일 객체 가져옴
		f.save("./uploads/" + f.filename) # 파일 저장
		return 'Upload Success'
	else: # GET 요청이 들어오면 파일을 업로드할 수 있는 HTML 폼을 반
		return """
		<form action="/fileUpload" method="POST" enctype="multipart/form-data">
			<input type="file" name="file" />
			<input type="submit"/>
		</form>
		"""
if __name__ == '__main__':
	app.run()
```

→ Path Traversal  취약점이 있는 코드이다.

이용자가 입력한 파일 이름을 그대로 사용하기 때문에 공격자가 `../` 와 같은 메타문자를 사용한다면 uploads를 벗어나 상위 디렉토리에도 파일을 업로드할 수 있다.

```python
POST /fileUpload HTTP/1.1
Host: storage.dreamhack.io
Origin: https://storage.dreamhack.io
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary20y3eoLVSNf9Ns5i
------WebKitFormBoundary20y3eoLVSNf9Ns5i
Content-Disposition: form-data; name="file"; filename="test.txt"
Content-Type: text/plain
upload test !
------WebKitFormBoundary20y3eoLVSNf9Ns5i--
```

```python
POST /fileUpload HTTP/1.1
Host: storage.dreamhack.io
Origin: https://storage.dreamhack.io
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary20y3eoLVSNf9Ns5i
------WebKitFormBoundary20y3eoLVSNf9Ns5i
Content-Disposition: form-data; name="file"; filename="../hack.py"
Content-Type: text/plain
[malicious file content]
------WebKitFormBoundary20y3eoLVSNf9Ns5i--
```

```python
$ ls -lR
-rw-r--r--  1 dreamhack  staff  461  1 30 21:52 app.py
drwxr-xr-x  3 dreamhack  staff   96  1 30 21:31 uploads
./uploads:
total 8
-rw-r--r--  1 dreamhack  staff   13  1 30 21:31 test.txt
```

```python
$ ls -lR
-rw-r--r--  1 dreamhack  staff  461  1 30 21:52 app.py
-rw-r--r--  1 dreamhack  staff  431  1 30 22:12 hack.py
drwxr-xr-x  3 dreamhack  staff   96  1 30 21:31 uploads
./uploads:
total 8
-rw-r--r--  1 dreamhack  staff   13  1 30 21:31 test.txt
```

### 악성 파일 업로드

⇒ 악성 파일 업로드 취약점은 이용자가 파일을 업로드할 때, 이를 제대로 검사하지 않아서 발생하는 취약점,

**웹 셸:**

웹 서버는 `.php` , `.jsp` , `.asp` 와 같은 확장자 파일을 Common Gateway Interface(CGI) 로 실행하고, 그 결과를 이용자에게 반환한다. Remote Code Execution, Cross Site Scripting (XSS) 가능, 간접적으로 Cookie Hijacking, Cross Site Request Forgery (CSRF) 가능

```html
<FilesMatch ".+\.ph(p[3457]?|t|tml)$">
    SetHandler application/x-httpd-php
</FilesMatch>
```

→ 이용자가 요청한 파일의 확장자가 정규표현식을 만족하면 `x-httpd-php`로 핸들링 하게 하는 Apache 설정 파일이다. `x-httpd-php`는 PHP 엔진이며 요청한 파일을 실행하고, 그 결과를 반환한다. `.php` , `.php3` , `.phtml` 이 이 위의 정규표현식을 만족.

많은 웹 서버들이 php 파일에 대해 위와 같은 핸들링을 지원, 따라서 공격자가 임의의 php 파일을 `.php` 확장자로 업로드하고, GET 요청을 보낼 수 있다면 CGI에 의해 해당 코드가 실행되도록 할 수 있음.

<aside>
💡

**Common Gateway Interface(CGI)란?**

---

*요즘 시대에는 정적인 웹 페이지만 제공하는 웹 애플리케이션은 거의 찾아보기 힘들다. 동적인 컨텐츠를 처리하기 위해서 웹 서버와 php 같은 외부의 프로그램에 사이에서 인터페이스를 제공하는 프로토콜이 CGI이다.*

---

</aside>

### 악의적인 웹 리소스

## File Download Vulnerability(파일 다운로드 취약성)

⇒ 웹 서비스의 파일 시스템에 존재하는 파일을 다운로드 하는 과정에서 발생. 이용자가 다운로드할 파일의 이름을 임의로 정할 수 있을 때 발생한다. 공격자는 웹 서비스의 파일 시스템에 존재하는 임의 파일을 다운로드 받을 수 있다. Path Traversal을 이용한 파일 다운로드 취약점은 설정 파일, 패스워드, DB 백업 본 파일 등을 다운로드 할 수 있다.

**파일 다운로드 취약점이 자주 발생하는 URL 패턴**

---

https://vulnerable-web.dreamhack.io/download/?filename=notes.txt

---

https://vulnerable-web.dreamhack.io/download/?filename=../../../../../../etc/passwd

---

https://vulnerable-web.dreamhack.io/images.php?fn=6ed0dd02806fa89e233b84f4.png

---

## 실습

**Q4. 파일 다운로드 취약점이 발생하는 코드이다, "filename" 인자에 어떠한 값을 넣어야 현재 실행중인 프로세스의 메모리 정보를 볼 수 있는가? 해당하는 답안을 모두 고르시오.**

`@app.route("/download")
def download():
filename = request.args.get("filename")
content = open("/data/uploads/" + filename, "rb").read()
return content`

**정답으로 생각되는 답안을 모두 선택해 주세요.**

**/../../etc/passwd**

**../../proc/self/maps**✅

**../root/memory_information**

**../../../etc/memory**

**../../etc/memory**

**../proc/self/maps**

**../../../proc/self/maps**✅

[image-storage](https://dreamhack.io/wargame/challenges/38/)를 풀어보면서 파일 취약점을 이용한 공격을 실습해보겠습니다.

# **문제의 목표**

image-storage 문제의 목표는 파일 업로드 취약점을 통해 플래그를 획득하는 것입니다. 문제의 설명은 다음과 같습니다.

> php로 작성된 파일 저장 서비스입니다.
>
>
> *파일 업로드 취약점을 이용해 플래그를 획득하세요. 플래그는* `/flag.txt`에 있습니다.
>

### **웹 서비스 분석**

### **인덱스 페이지**

**index.php**는 list.php와 upload.php로 이동하는 메뉴를 출력합니다.

```php
<li><a href="/">Home</a></li>
<li><a href="/list.php">List</a></li>
<li><a href="/upload.php">Upload</a></li>
```

[data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjkiIGhlaWdodD0iMzQiIHZpZXdCb3g9IjAgMCAyOSAzNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTIxIDAuNUgzQzEuMzUgMC41IDAgMS44NSAwIDMuNVYyNC41SDNWMy41SDIxVjAuNVpNMjUuNSA2LjVIOUM3LjM1IDYuNSA2IDcuODUgNiA5LjVWMzAuNUM2IDMyLjE1IDcuMzUgMzMuNSA5IDMzLjVIMjUuNUMyNy4xNSAzMy41IDI4LjUgMzIuMTUgMjguNSAzMC41VjkuNUMyOC41IDcuODUgMjcuMTUgNi41IDI1LjUgNi41Wk0yNS41IDMwLjVIOVY5LjVIMjUuNVYzMC41WiIgZmlsbD0iIzFBMUExQiIvPgo8L3N2Zz4K](data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjkiIGhlaWdodD0iMzQiIHZpZXdCb3g9IjAgMCAyOSAzNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTIxIDAuNUgzQzEuMzUgMC41IDAgMS44NSAwIDMuNVYyNC41SDNWMy41SDIxVjAuNVpNMjUuNSA2LjVIOUM3LjM1IDYuNSA2IDcuODUgNiA5LjVWMzAuNUM2IDMyLjE1IDcuMzUgMzMuNSA5IDMzLjVIMjUuNUMyNy4xNSAzMy41IDI4LjUgMzIuMTUgMjguNSAzMC41VjkuNUMyOC41IDcuODUgMjcuMTUgNi41IDI1LjUgNi41Wk0yNS41IDMwLjVIOVY5LjVIMjUuNVYzMC41WiIgZmlsbD0iIzFBMUExQiIvPgo8L3N2Zz4K)

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/ef1b48c2-b8f0-434c-9322-bccc2a248af8/de0e09ac-00a3-4629-a9cc-24520df0a32b/image.png)

### **파일 목록 리스팅**

**list.php**는 `$directory`의 파일들 중 `.`, `..`, `index.html`을 제외하고 나열합니다.

```php
<?php
    // 파일이 저장된 디렉토리 경로를 정의 (uploads 폴더)
    $directory = './uploads/';

    // 해당 디렉토리에서 파일 및 폴더 목록을 가져오고, '..'상위, '.'현재, 'index.html'을 제외
    $scanned_directory = array_diff(scandir($directory), array('..', '.', 'index.html'));

    // 디렉토리의 파일 목록을 순환
    foreach ($scanned_directory as $key => $value) {
    //key = 배열의 키 , value = 파일명
        // 파일 링크를 리스트 형식으로 출력
        // 파일명과 경로를 a 태그로 링크 생성 후, <li> 태그로 감싸서 보여줌
        echo "<li><a href='{$directory}{$value}'>".$value."</a></li><br/>";
    }
?>  
```

### **파일 업로드**

**upload.php**는 이용자가 업로드한 파일을 `uploads`폴더에 복사하며, 이용자는 `http://host1.dreamhack.games:[PORT]/uploads/[FILENAME]` URL을 통해 접근할 수 있습니다.

만약 같은 이름의 파일이 있다면 "already exists"라는 메시지를 반환합니다. 업로드할 파일에 대해 어떠한 검사도 하지 않으므로, 웹 셸 업로드 공격에 취약합니다.

```php
<?php
  // HTTP 요청이 POST 방식으로 왔는지 확인
  if ($_SERVER['REQUEST_METHOD'] === 'POST') {

    // 업로드된 파일이 있는지 확인
    if (isset($_FILES)) {

      // 업로드된 파일이 저장될 디렉토리 경로 설정
      $directory = './uploads/';

      // 업로드된 파일의 정보 추출
      $file = $_FILES["file"];         // 업로드된 파일 객체
      $error = $file["error"];         // 파일 업로드 과정에서 발생한 에러 코드
      $name = $file["name"];           // 파일 이름
      $tmp_name = $file["tmp_name"];   // 서버에 임시로 저장된 파일 경로

      // 파일 업로드 중 에러가 발생했는지 확인
      if ( $error > 0 ) {
        // 에러가 발생하면 에러 코드를 출력
        echo "Error: " . $error . "<br>";
      } else {
        // 동일한 이름의 파일이 이미 존재하는지 확인
        if (file_exists($directory . $name)) {
          // 파일이 이미 존재하면 해당 메시지를 출력
          echo $name . " already exists. ";
        } else {
          // 파일을 임시 저장 경로에서 지정된 디렉토리로 이동
          if(move_uploaded_file($tmp_name, $directory . $name)){
            // 파일이 성공적으로 저장되었으면 저장 경로 출력
            echo "Stored in: " . $directory . $name;
          }
        }
      }
    } else {
      // 파일이 업로드되지 않았을 경우 에러 메시지 출력
      echo "Error !";
    }

    // 스크립트 종료
    die();
  }
?>

```

** you can see my past posts in my velog https://velog.io/@iq1564/posts