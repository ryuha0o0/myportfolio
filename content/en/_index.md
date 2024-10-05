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
          <div style="display: flex; flex-direction: column; align-items: center;">
            <img src="avatar.jpg" alt="Profile Picture" style="border-radius: 100%; width: 200px; height: 200px; object-fit: cover; margin-bottom: 10px;">
            <p style="font-size: 120%; font-weight: bold; margin: 5px 0;color: white;">Ryu Ha-young</p>
            <p style="font-size: 95%;color: white;">Jeonbuk National University</p>
          </div>
          <div style="text-align: left; max-width: 500px;">
            <p style="font-size: 95%;color: white;">
              Major: IT Intelligent Information Engineering<br>
              Hello, I am Ryu Ha-young from Jeonbuk National University! Nice to meet you.<br>
              This website contains various introductions about me, including my major and various interests and study areas.<br>
              My areas of interest are information security and full-stack development.<br><br>
              <a href="./contact/" class="btn">Contact Me</a>
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
        overlay:
          color: '#ffffff'
          opacity: 0.5

  - block: features
    content:
      title: <span style="font-size:70%"> This web is my portfolio website </span>
      text: <br><span style="font-size:125%">Welcome to my portfolio website!</span> <br><br>
        <a href="./post/" class="btn">See my posts</a>

  - block: slider
    content:
      slides:
        - title: <span style="font-size:70%">Contact Me!</span>
          content: <span style="font-size:70%">Hayoung's portfolio!</span>
          align: center
          background:
            image:
              filename: luke-jones-tBvF46kmwBw-unsplash.jpg
              filters:
                brightness: 1
            overlay:
              color: '#0000ff'
              opacity: 0.5
            position: center
            color: '#0000ff'
          link:
            icon: user
            icon_pack: fas
            text: <span style="font-size:60%">contact</span>
            text-color: '#000'
            url: contact

        - title: <span style="font-size:70%">Mobile App Dev</span>
          content: <span style="font-size:70%">Creating mobile applications with various designs<span style="font-size:70%">
          align: center
          background:
            image:
              filename: luke-miller-7meutoti8Vw-unsplash.jpg
              filters:
                brightness: 1
            overlay:
              color: '#0000ff'
              opacity: 0.5
            position: center
            color: '#0000ff'

        - title: <span style="font-size:70%">Information Security</span>
          content: <span style="font-size:70%">Vulnerability assessment of websites for information security</span>
          align: center
          background:
            image:
              filename: nastia-petruk-rZX6KxPw5pg-unsplash.jpg
              filters:
                brightness: 1
            position: center
            color: '#0000ff'

        - title: <span style="font-size:70%">Hacking</span>
          content: <span style="font-size:70%">Developing applicable hacking code</span>
          align: center
          background:
            image:
              filename: philip-oroni-VfOGf5RWkeg-unsplash.jpg
              filters:
                brightness: 1.7
            position: center
            color: '#0000ff'

        - title: <span style="font-size:70%">Development</span>
          content: <span style="font-size:70%">Full-Stack web development</span>
          align: center
          background:
            image:
              filename: steve-johnson-KKDMyLTIyVs-unsplash.jpg
              filters:
                brightness: 1.7
            position: center
            color: '#0000ff'

    design:
      slide_height: '450px'
      slide_width: '90px'
      is_fullscreen: false
      loop: true
      interval: 5000

  - block: features
    id: features
    content:
      title: <span style="font-size:65%">Hayoung's Interests</span>
      text: Here are the areas I am interested in.<br><br><br><br>
      items:
        - name: Web Security
          icon: key
          icon_pack: fas
          description: <span style="font-size:80%">Studying web security based on my web knowledge.</span><br><br>
        - name: Mobile Applications
          icon: mobile-screen
          icon_pack: fas
          description: <span style="font-size:80%">Development of mobile apps based on Android.</span><br><br>
        - name: Software Engineering
          icon: chalkboard-user
          icon_pack: fas
          description: <span style="font-size:80%">Leading projects with leadership based on software engineering.</span><br><br>
        - name: Drawing
          icon: object-ungroup
          icon_pack: fas
          description: <span style="font-size:80%">Drawing various pictures to materialize ideas.</span><br><br>
        - name: Development
          icon: laptop
          icon_pack: fas
          description: <span style="font-size:80%">Full-stack web development with Spring Boot.</span><br><br>
        - name: Penetration Testing
          icon: masks-theater
          icon_pack: fas
          description: <span style="font-size:80%">Creating various hacking codes based on Python.</span><br><br>

  - block: collection
    content:
      id: section-1
      title: Latest Post
      count: 3
      offset: 0
      order: desc
      filters:
        folders:
          - notification
          - post
    design:
      view: community/custom_card
      columns: '1'

  - block: collection
    content:
      id: section-1
      title: Project
      count: 3
      offset: 0
      order: desc
      filters:
        folders:
          - event
    design:
      view: community/custom_card2
      columns: '1'

  - block: collection
    content:
      title: Travel Records
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
      view: community/custom_card3
      columns: '1'

  - block: markdown
    content:
      title:
      subtitle:
      text: |
        {{% cta cta_link="./contact/" cta_text="Join team →" %}}
    design:
      columns: '1'
---
