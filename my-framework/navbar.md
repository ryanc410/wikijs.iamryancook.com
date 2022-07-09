---
title: Responsive Navbar Markup for My Custom Framework
description: 
published: true
date: 2022-07-09T05:45:17.143Z
tags: css, html, javascript, navbar, responsive, custom-framework, custom
editor: markdown
dateCreated: 2022-07-09T05:45:17.143Z
---

# HTML
````html
<nav class="topnav" id="navbarTop">
  <a class="nav-title" href="#">713TechSupport.com</a>
  <a href="#news">Home</a>
  <a href="#contact">Gallery</a>
  <a href="#about">Contact</a>
  <div class="icon" id="toggler">
    <i class="fa fa-bars"></i>
  </div>
</nav>
<main>
  <h1 style="color: white;">Main Page</h1>
</main>
````

# CSS
````html
body {
  max-height: 100vh;
  background-color: #000000;
  font-family: 'Montserrat', sans-serif;
  font-size: 16px;
  display: flex;
  flex-direction: column;
}

footer {
  width: 100vw;
  height: 75px;
  margin-top: 75px;
}

.topnav {
  overflow: hidden;
  padding: 15px;
}

.topnav a {
  float: left;
  display: block;
  color: #f2f2f2;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}

.topnav a:hover {
  color: #00ffff;
  cursor: pointer;
}

.topnav a.nav-title {
  margin-top: -5px;
  font-size: 22px;
  font-weight: 600;
  color: #00ffff !important;
  letter-spacing: 8px;
  text-transform: uppercase;
  background-color: transparent !important;
}

.topnav a.nav-title:hover {
  cursor: default; 
}

.topnav div.icon {
  display: none;
}

.nav-spacer {
  margin-top: 
}

@media screen and (min-width: 768px){
  .topnav a:not(:first-child) {
      margin-left: 100px; 
  }
}

@media screen and (max-width: 1066px) {
  .topnav a:not(:first-child) {display: none;}
  .topnav div.icon {
    float: right;
    display: block;
    font-size: 30px;
    color: #ffffff;
  }
  .topnav div.icon:hover {
    cursor: pointer;
    color: #00ffff;
  }
}

@media screen and (max-width: 1066px) {
  .topnav.responsive {position: relative;}
  .topnav.responsive .icon {
    position: absolute;
    right: 0;
    top: 0;
    padding: 15px;
  }
  .topnav.responsive a {
    float: none;
    display: block;
    text-align: left;
  }
}
````

# Javascript
````javascript
var toggle = document.getElementById('toggler');
var nav = document.getElementById('navbarTop');
var page = document.getElementsByTagName('main');

toggle.addEventListener('click', function(){
	nav.classList.toggle('responsive');
  page.classList.toggle('nav-spacer');
})
````
