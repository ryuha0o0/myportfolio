---
# Leave the homepage title empty to use the site title
title:
date: 2024-03-25
type: landing

sections:
  - block: markdown
    content:
      title:
      text: |
        <span style='font-size:300%; font-weight:bold; color: white; justify-content: center; align-items: center;'>About Me</span>
        <div style="display: flex; justify-content: center; align-items: center; gap: 50px;">
          <!-- 왼쪽: 프로필 사진과 이름, 학교 정보 -->
          <div style="display: flex; flex-direction: column; align-items: center;">
            <img src="avatar.jpg" alt="프로필 사진" style="border-radius: 100%; width: 200px; height: 200px; object-fit: cover; margin-bottom: 10px;">
            <p style="font-size: 120%; font-weight: bold; margin: 5px 0;color: white;">류하영</p>
            <p style="font-size: 95%;color: white;">전북대학교</p>
          </div>
          <!-- 오른쪽: 소개 정보 -->
          <div style="text-align: left; max-width: 500px;">
            <p style="font-size: 95%;color: white;">
              전공: IT지능정보공학<br>
              안녕하세요, 전북대학교 IT지능정보공학과의 류하영입니다! 잘 부탁 드립니다<br>
              본 웹 사이트는 제 다양한 소개를 담은 사이트입니다. 제 전공 소개부터 다양한 제 관심사와 공부 분야에 대해서 이야기해 드립니다<br>
              관심 분야는 정보보안, 풀스택 개발입니다<br><br>
              <a href="./contact/" style="background-color: #007bff; color: white; padding: 10px 20px; border-radius: 5px; text-decoration: none; font-size: 100%;">Contact Me</a>
            </p>
          </div>
        </div>
    design:
      columns: '1'
      background:
        image:
          filename: faraaz-zuberi-YoIq2GyYcAU-unsplash.jpg
          filters:
            brightness: 0.8
        overlay:  # 오버레이 추가
          color: '#ffffff'  # 흰색
          opacity: 0.5  # 투명도 조절




  - block: features
    content:
      title: <span style="font-size:70%"> This web is my portfolio website </span>
      text: <br><span style="font-size:125%">제 포트폴리오 웹 사이트에 오신 것을 환영합니다!.</span> <br><br>
        {{% cta cta_link="./field/" cta_text="See Research Field →" %}}
      


  - block: slider
    content:
      slides:

        - title: <span style="font-size:70%">Contact Me!</span>
          content: <span style="font-size:70%">hayoung's portfolio!</span>
          align: center
          background:
            image:
              filename: luke-jones-tBvF46kmwBw-unsplash.jpg
              filters:
                brightness: 1
            overlay:  # 오버레이 추가
              color: '#0000ff'  # 흰색
              opacity: 0.5  # 투명도 조절
            position: center
            color: '#0000ff'
          link:
            icon: user
            icon_pack: fas
            text: <span style="font-size:60%">Join Us</span>
            text-color: '#000'
            url: contact

        - title: <span style="font-size:70%">Mobile App Dev</span>
          content: <span style="font-size:70%">다양한 디자인의 모바일 어플리케이션 제작<span style="font-size:70%">
          align: center
          background:
            image:
              filename: luke-miller-7meutoti8Vw-unsplash.jpg
              filters:
                brightness: 1
            overlay:  # 오버레이 추가
              color: '#0000ff'  # 흰색
              opacity: 0.5  # 투명도 조절
            position: center
            color: '#0000ff'

        - title: <span style="font-size:70%">Information Security</span>
          content: <span style="font-size:70%">정보보호를 위한 웹사이트의 취약점 진단</span>
          align: center
          background:
            image:
              filename: nastia-petruk-rZX6KxPw5pg-unsplash.jpg
              filters:
                brightness: 1
            position: center
            color: '#0000ff'

        - title: <span style="font-size:70%">Hacking</span>
          content: <span style="font-size:70%">적용 가능한 해킹 코드 개발</span>
          align: center
          background:
            image:
              filename: philip-oroni-VfOGf5RWkeg-unsplash.jpg
              filters:
                brightness: 1.7
            position: center
            color: '#0000ff'

        - title: <span style="font-size:70%">Development</span>
          content: <span style="font-size:70%">Full-Stack 웹 개발</span>
          align: center
          background:
            image:
              filename: steve-johnson-KKDMyLTIyVs-unsplash.jpg
              filters:
                brightness: 1.7
            position: center
            color: '#0000ff'

    design:
      # Slide height is automatic unless you force a specific height (e.g. '400px')
      slide_height: '450px'
      slide_width: '90px'
      is_fullscreen: false
      # Automatically transition through slides?
      loop: true
      # Duration of transition between slides (in ms)
      interval: 5000


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
      view: /layouts/patials/custom_card
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
      view: patials/custom_card
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
