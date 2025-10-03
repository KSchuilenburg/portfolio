---
layout: default
title: Portfolio
---

<div id="welcomeMessage">
  <h2>Nice to meet you!</h2>
  <p>Hi, I am Kylian!</p>
</div>

<div id="about">
  <h2>About Me [WIP]</h2>
  <p>
    Student at Breda University of Applied Sciences<br>
    Gameplay & AI programmer<br>
    Experience with Unreal, Unity, Godot, custom C++ engine
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
</div>