---
# Leave the homepage title empty to use the site title
title:
date: 2024-03-25
type: landing

sections:

  - block: markdown
    content:
      title: "<span style='font-size:200%; font-weight:bold;'>About Me</span>"
      text: |
        <div style="display: flex; align-items: center; gap: 40px;">
          <!-- 왼쪽 프로필 이미지 -->
          <div style="flex: 1; text-align: center;">
            <img src="avatar.jpg" alt="프로필 사진" style="border-radius: 50%; width: 180px; height: 180px; object-fit: cover;">
          </div>

          <!-- 오른쪽 프로필 정보 -->
          <div style="flex: 2;">
            <p style="font-size: 120%; line-height: 1.6;">
              <strong>학교:</strong> 전북대학교<br>
              <strong>전공:</strong> IT지능정보공학과<br>
              <strong>연구 분야:</strong> 의료 AI, 계산 과학<br>
              <strong>관심 분야:</strong> AI 기반 응용, 풀스택 개발<br><br>
              <span style="font-size: 110%;">저는 현재 전북대학교 컴퓨터 공학과에 재학 중이며, 의료 인공지능 및 계산 과학에 관심을 두고 연구하고 있습니다. 다양한 AI 기반 응용 프로그램 개발에 열정을 가지고 있으며, 풀스택 개발에도 많은 경험을 쌓고 있습니다.</span><br><br>

              <!-- 이력서 다운로드 버튼 -->
              <a href="3학년_경력활동계획서.pdf" style="background-color: #007bff; color: white; padding: 10px 20px; border-radius: 5px; text-decoration: none; font-size: 110%;">Download Resume (PDF)</a><br><br>

              <!-- Contact Me 버튼 -->
              <a href="./contact/" style="background-color: #28a745; color: white; padding: 10px 20px; border-radius: 5px; text-decoration: none; font-size: 110%;">Contact Me</a>
            </p>
          </div>
        </div>
    design:
      columns: '1'


  - block: features
    content:
      title: <span style="font-size:70%"> This web is my portfolio website </span>
      text: <br><span style="font-size:125%">제 포트폴리오 웹 사이트에 오신 것을 환영합니다!.</span> <br><br>
        {{% cta cta_link="./field/" cta_text="See Research Field →" %}}
      


  - block: slider
    content:
      slides:

        - title: <span style="font-size:70%">Recruit</span>
          content: <span style="font-size:70%">Interested in MacsLAB?</span>
          align: center
          background:
            image:
              filename: Ai.jpg
              filters:
                brightness: 0.4
            position: center
            color: '#000'
          link:
            icon: user
            icon_pack: fas
            text: <span style="font-size:60%">Join Us</span>
            text-color: '#000'
            url: contact

        - title: <span style="font-size:70%">AI</span>
          content: <span style="font-size:70%">의료/항공우주/컨텐츠 등 특성화 분야에 적용 가능한 AI 기술 개발<span style="font-size:70%">
          align: center
          background:
            image:
              filename: Ai.jpg
              filters:
                brightness: 0.4
            position: center
            color: '#000'

        - title: <span style="font-size:70%">Healthcare</span>
          content: <span style="font-size:70%">의료 및 헬스케어 분야에 적용 가능한 AI 기술 개발</span>
          align: center
          background:
            image:
              filename: Ai.jpg
              filters:
                brightness: 0.4
            position: center
            color: '#000'

        - title: <span style="font-size:70%">Mathematics</span>
          content: <span style="font-size:70%">AI와 관련된 수학 및 최적화 이론 연구</span>
          align: center
          background:
            image:
              filename: Ai.jpg
              filters:
                brightness: 0.4
            position: center
            color: '#000'

        - title: <span style="font-size:70%">Development</span>
          content: <span style="font-size:70%">기반 기술을 활용한 Full-Stack 어플리케이션 개발</span>
          align: center
          background:
            image:
              filename: Ai.jpg
              filters:
                brightness: 0.4
            position: center
            color: '#000'

    design:
      # Slide height is automatic unless you force a specific height (e.g. '400px')
      slide_height: '350px'
      slide_width: '100px'
      is_fullscreen: false
      # Automatically transition through slides?
      loop: true
      # Duration of transition between slides (in ms)
      interval: 3000


  - block: features
    id: features
    content:
      title: <span style="font-size:65%">hayoung's Interests</span>
      text: 저는 이런 분야에 관심을 두고 있어요.<br><br><br><br>
      items:
        - name: 정보보안
          icon: key
          icon_pack: fas
          description: <span style="font-size:80%">의료 (Medical), 항공우주 (Aerospace), 컨텐츠 (Contents) 등 다양한 특성화 분야에 적응형 AI 기술 적용.</span><br><br>
        - name: 멀티모달(Multi-modality)
          icon: globe
          icon_pack: fas
          description:  <span style="font-size:80%">Vision & Language 분야의 기반 AI 기술 개발 및 관련 응용 어플리케이션에 기술 적용.</span><br><br>
        - name: 의료수학(Medical Math)
          icon: calculator
          icon_pack: fas
          description:  <span style="font-size:80%">의료 분야에 대한 통계 분석 수행 및 의료 질병에 대한 수학적인 모델링 관련 연구 수행.</span><br><br>
        - name: 컨텐츠 (Contents)
          icon: comment-dots
          icon_pack: fas
          description:  <span style="font-size:80%">웹툰 및 미디어 컨텐츠와 관련된 AI 기반 기술 개발 및 고도화.</span><br><br>
        - name: 개발 (Development)
          icon: laptop
          icon_pack: fas
          description:  <span style="font-size:80%">Full-Stack 기반의 응용 어플리케이션 개발.</span><br><br>
        - name: 솔루션 (Solution)
          icon: app-store-ios
          icon_pack: fab
          description:  <span style="font-size:80%">AI 기반기술 및 관련 어플리케이션에 적용을 통한 통합 솔루션 개발!</span><br><br>


  - block: collection
    content:
      id: section-1
      title: Notifications & News
      subtitle:
      text:
      count: 3
      offset: 0
      order: desc
      filters:
        folders:
          - notification
          - post
          - event
    design:
      view: community/custom_card
      columns: '2'

  - block: collection
    content:
      title: Latest Publications
      subtitle:
      text:
      count: 3
      filters:
        author: ''
        category: ''
        exclude_featured: false
        publication_type: ''
        tag: ''
      offset: 0
      order: desc
      page_type: publication
    design:
      view: community/custom_card
      columns: '2'
    advanced:
      css_style: "text-align: center;"

  - block: markdown
    content:
      title:
      subtitle:
      text: |
        {{% cta cta_link="./contact/" cta_text="Join team →" %}}
    design:
      columns: '1'
---
