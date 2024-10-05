---
title: Contact
date: 2022-10-24

type: landing

sections:
  - block: contact
    content:
      title: Contact
      text: |-
        Please refer to this page if you wish to get in touch.
      email: iq1564@jbnu.ac.kr
      phone: 010-7148-3023
      address:
        street: Jeonbuk National University, Building 7
        city: Jeonju, Jeonbuk
        postcode: '94305'
        country: South Korea
        country_code: KO
      coordinates:
        latitude: '35.84601324617979'
        longitude: '127.13444961966684'
      contact_links:
        - icon: comments
          icon_pack: fas
          name: Contact via Discord
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
        padding: ['40px', '0px', '40px', '0px']  # Set top and bottom padding only
      margin:
        top: '0px'
        right: '20px'  # Set right margin
        bottom: '0px'
        left: '20px'  # Set left margin

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
