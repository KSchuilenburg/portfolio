---
layout: default
title: Portfolio
---

<div id="welcomeMessage">
  <h2>Nice to meet you!</h2>
  <p>Hi, I am Kylian!</p>
</div>

<div id="about">
  <h2>About Me</h2>
  <p>
    I am a Game Developer with a passion for Gameplay and Game AI. <br>
    I have experience working with Unreal Engine, Unity, Godot, and custom C++ engines. <br>
    <br>
    In addition to Entertainment Games, I have a great interest in Serious Games. Using the entertaining side of games as a means of education is something I am believe in and am passionate about. Games can be more than just entertainment and I will do my best to prove that. <br>
    <br>
    While I also like creating small games on my own, I deeply value the interdisciplinary aspect of games. I try my best to be a team player and help where I can. I have experience working in smaller teams (3-5 people) and larger teams (12-16 people). Since I value working in a team, I have also taken a lead role in teams to ensure both the programmers and the rest of the team have a smooth working environment.
  </p>
</div>

<div id="work">
  <h2>My Work</h2>
  <div class="work-container">
    {% for project in site.data.projects %}
      <div class="work-block">
        <a href="{{ site.baseurl }}{{ project.link }}" target="_blank">
          <img src="{{ site.baseurl }}{{ project.image }}" alt="{{ site.baseurl }}{{ project.title }}">
        </a>
        <div class="work-content">
          <div class="work-title">{{ project.title }}</div>
          <div class="work-description">{{ project.description }}</div>
          <div class="work-tags">
            {% for tag in project.tags %}
              <span class="work-tag">{{ tag }}</span>
            {% endfor %}
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
</div>


<div id="contact">
  <h2>Contact Me</h2>
  <a href="mailto:Kylianschuilenburg@live.nl" class="email-button">Email</a>
  <a href="/assets/Kylian_Schuilenburg.pdf" target="blank" class="email-button">Resume</a>
  <a href="https://killyyuun.itch.io/" target="blank" class="email-button">Itch.io</a>
</div>


<div id="links-widget">
  <h2>All my Links</h2>
  <iframe class="links-iframe" src="https://allmylinks.com/widget/profile/kylians-dev.html?dark=1&big=0" width="395" height="216" style="max-width:100%;display: block; margin: 0; border:none;overflow:hidden" scrolling="no" frameborder="0" allowtransparency="true" allow="encrypted-media"></iframe>
</div>