---
title: Custom Navbar Stylesheet Template
description: Stylesheet for bootstrap navbar
published: true
date: 2022-07-06T22:31:42.113Z
tags: bootstrap, navbar, template, stylesheet
editor: markdown
dateCreated: 2022-07-06T22:31:42.113Z
---

# Stylesheet Template
Fill in the variables on top inside the :root section.

<br>

````css
:root {
  --body-bg-color: ;
  --main-font-color: ;
  --main-font-style: ;
  --main-font-size: ;
  
  --heading-font-color: ;
  --heading-font-weight: ;
  --heading-letter-spacing: ;
  
  --navbar-bg-color: ;
  
  --navbrand-size: ;
  --navbrand-font-color: ;
  --navbrand-letter-spacing: ;
  --navbrand-font-weight: ;
  
  --navlink-font-size: ;
  --navlink-font-color: ;
  --navlink-text-decoration: ;
  --navlink-transition-duration: ;
  --navlink-hover-color: ;
  --navlink-hover-text-decoration: ;
  
  --dropdown-menu-bg-color: ;
  --dropdown-menu-border: ;
  --dropdown-link-color: ;
  --dropdown-link-hover-color: ;
  --dropdown-link-hover-bg-color: ;
  
  --btn-border-color: ;
  --btn-border: 2px solid var(--btn-border-color); 
}

body {
  max-height: 100vh;
  background-color: var(--body-bg-color);
  font-family: var(--main-font-style);
  color: var(--main-font-color);
  font-size: var(--main-font-size);
  display: flex;
  flex-direction: column;
}

nav.navbar {
  background-color: var(--navbar-bg-color) !important;
}

h1.navbar-brand {
  font-size: var(--navbrand-size) !important;
  font-weight: var(--navbrand-font-weight) !important;
  letter-spacing: var(--navbrand-letter-spacing) !important;
  color: var(--navbrand-font-color) !important;
}

a.nav-link {
  font-size: var(--navlink-font-size) !important;
  color: var(--navlink-font-color) !important;
  text-decoration: var(--navlink-text-decoration) !important;
  transition: var(--navlink-transition-duration) !important;
}

a.nav-link:hover {
  color: var(--navlink-hover-color) !important;
  text-decoration: var(--navlink-hover-text-decoration) !important;
}

ul.dropdown-menu {
  background-color: var(--dropdown-menu-bg-color) !important;
  border: var(--dropdown-menu-border) !important;
}

a.dropdown-item {
  color: var(--dropdown-link-color) !important;
  transition: var(--navlink-transition-duration) !important;
}

a.dropdown-item:hover {
  color: var(--dropdown-link-hover-color) !important;
  background-color: var(--dropdown-link-hover-bg-color) !important;
}

button.submit-btn {
  background: transparent;
  border: var(--btn-border);
  padding: 8px 16px;
}

button.submit-btn:hover {
  
}
````

<br>

# HTML Markup

````html
<nav class="navbar navbar-expand-lg">
  <div class="container-fluid">
    <h1 class="navbar-brand">Navbar</h1>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbar" aria-controls="navbar" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbar">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <a class="nav-link" href="#">Home</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Link</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Dropdown
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item" href="#">Action</a></li>
            <li><a class="dropdown-item" href="#">Another action</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
          </ul>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="#">Contact Us</a>
        </li>
      </ul>
      <div class="d-flex" role="search">
        <button class="submit-btn" id="loginBtn">Login</button>
        <button class="submit-btn" id="signupBtn">Sign Up</button>
      </div>
    </div>
  </div>
</nav>
````