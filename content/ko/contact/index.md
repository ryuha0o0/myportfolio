---
title: Contact
date: 2022-10-24

type: landing

sections:
  - block: contact
    content:
      title: Contact
      text: |-
        연락을 원하시는 분은 이 페이지를 참고해주세요
      email: iq1564@jbnu.ac.kr
      phone: 010-7148-3023
      address:
        street: 전북대 7호관
        city: 전북특별자치도 전주
        postcode: '94305'
        country: 대한민국
        country_code: KO
      coordinates:
        latitude: '35.84601324617979'
        longitude: '127.13444961966684'
      contact_links:
        - icon: comments
          icon_pack: fas
          name: 디스코드로 연락
          link: 'https://discord.com/channels/1143851795567869952/1143851796155076630'
    
      # Automatically link email and phone or display as text?
      autolink: true
    
      # Email form provider
      form:
        provider: netlify
        formspree:
          id:
        netlify:
          # Enable CAPTCHA challenge to reduce spam?
          captcha: false
    design:
      columns: '1'
      spacing:
        padding: ['40px', '0px', '40px', '0px']  # 위아래 패딩만 설정
      margin:
        top: '0px'
        right: '20px'  # 오른쪽 여백 설정
        bottom: '0px'
        left: '20px'  # 왼쪽 여백 설정

  - block: markdown
    content:
      title:
      subtitle: ''
      text:
    design:
      columns: '1'
      background:
        image: 
          filename: contact.jpg
          filters:
            brightness: 1
          parallax: false
          position: center
          size: cover
          text_color_light: true
      spacing:
        padding: ['40px', '20px', '40px', '20px']
      css_class: fullscreen
---
