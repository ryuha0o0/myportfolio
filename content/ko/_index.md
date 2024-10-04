---
# Leave the homepage title empty to use the site title
title:
date: 2024-03-25
type: landing

sections:
# Display name

# Name pronunciation (optional)
name_pronunciation: ryu ha young


# Full name (for SEO)
first_name: ha young
last_name: ryu

# Status emoji
status:
  icon: ☕️

# Is this the primary user of the site?
superuser: true

# Highlight the author in author lists? (true/false)
highlight_name: true

# Role/position/tagline
role: Student of JBNU

# Organizations/Affiliations to display in Biography blox
organizations:
  - name: Jeonbuk national university
    url: https://www.jbnu.ac.kr/kor/

# Social network links
# Need to use another icon? Simply download the SVG icon to your `assets/media/icons/` folder.
profiles:
  - icon: at-symbol
    color: '#eeac02'
    color_border: '#f0bf23'
    url: 'mailto:iq1564@jbnu.ac.kr'
    label: E-mail Me
  - icon: brands/instagram
    color: '#eeac02'
    color_border: '#f0bf23'
    url: https://www.instagram.com/ha.0_1114/
  - icon: brands/github
    color: '#eeac02'
    color_border: '#f0bf23'
    url: https://github.com/ryuha0o0

interests:
  - Information security
  - Web Service
  - Computer network

education:
  - area: IT Intelligence Information Engineering
    institution: Jeonbuk national university
    date_start: 2022-03-01
    summary: |
      In order to systematically and efficiently educate students who will work in the future intelligent information society and hyperconnected society while actively responding to AI and new technology needs, our department aims to cultivate 5C-GIANT global digital talents based on demand for industries with problem-solving capabilities in the future technology-oriented manner.
    button:
      text: 'Introduction to the department'
      url: 'https://csai.jbnu.ac.kr/csai/index.do'

  - block: features
    content:
      title: <span style="font-size:70%">Medical AI & Computational Science (Macs) Lab </span>
      text: <br><span style="font-size:125%">전북대학교 의료 AI 및 계산 과학 연구실 홈페이지에 오신 것을 환영합니다.</span> <br><br>
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
      title: <span style="font-size:75%">Lab's Interests</span>
      text: 저희 연구실에서는 다음과 같은 연구/개발 분야에 관심을 쏟고 있습니다.<br><br><br><br>
      items:
        - name: 인공지능(AI)
          icon: code-branch
          icon_pack: fas
          description: <span style="font-size:90%">의료 (Medical), 항공우주 (Aerospace), 컨텐츠 (Contents) 등 다양한 특성화 분야에 적응형 AI 기술 적용.</span><br><br>
        - name: 멀티모달(Multi-modality)
          icon: globe
          icon_pack: fas
          description:  <span style="font-size:90%">Vision & Language 분야의 기반 AI 기술 개발 및 관련 응용 어플리케이션에 기술 적용.</span><br><br>
        - name: 의료수학(Medical Math)
          icon: calculator
          icon_pack: fas
          description:  <span style="font-size:90%">의료 분야에 대한 통계 분석 수행 및 의료 질병에 대한 수학적인 모델링 관련 연구 수행.</span><br><br>
        - name: 컨텐츠 (Contents)
          icon: comment-dots
          icon_pack: fas
          description:  <span style="font-size:90%">웹툰 및 미디어 컨텐츠와 관련된 AI 기반 기술 개발 및 고도화.</span><br><br>
        - name: 개발 (Development)
          icon: laptop
          icon_pack: fas
          description:  <span style="font-size:90%">Full-Stack 기반의 응용 어플리케이션 개발.</span><br><br>
        - name: 솔루션 (Solution)
          icon: app-store-ios
          icon_pack: fab
          description:  <span style="font-size:90%">AI 기반기술 및 관련 어플리케이션에 적용을 통한 통합 솔루션 개발!</span><br><br>


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
