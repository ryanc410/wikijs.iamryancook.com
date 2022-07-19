---
title: Bootstrap Registration Form Template
description: Bootstrap v5
published: true
date: 2022-07-19T16:06:54.996Z
tags: bootstrap, forms, template, bootstrap v5, registration
editor: markdown
dateCreated: 2022-07-19T16:06:54.996Z
---

# Registration Form Template

<br>

## **Bootstrap v5 CDN Links**

<br>

**CSS**
````html
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor" crossorigin="anonymous">
````
**Javascript**
````html
	    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-pprn3073KE6tl6bjs2QrFaJGz5/SUsLqktiwsUTF55Jfv3qYSDhgCecCxMW52nD2" crossorigin="anonymous"></script>
````

<br>

## HTML Markup

````html
<div class="container-fluid mt-4">
    <div class="row d-flex justify-content-center">
        <div class="col-6 d-block mx-auto">
            <h1>Jquery Custom Form Validation Example</h1>
            <form action="" method="post" id="customForm">
                <div class="mt-3">
                    <label for="formUser" class="mb-1">Username</label>
                    <input type="text" class="form-control" name="formUser" id="formUser" />
                </div>
                <div class="username-msg mb-2"></div>
                <div>
                    <label for="formEmail" class="mb-1">Email Address</label>
                    <input type="text" class="form-control" name="formEmail" id="formEmail" />
                </div>
                <div class="email-msg mb-2"></div>
                <div>
                    <label for="formPass" class="mb-1">Password</label>
                    <input type="password" class="form-control" name="formPass" id="formPass" />
                </div>
                <div class="password-msg mb-2"></div>
                <div>
                    <label for="formConfirmPass" class="mb-1">Confirm Password</label>
                    <input type="password" class="form-control" name="formConfirmPass" id="formConfirmPass" />
                </div>
                <div class="confirmPass-msg mb-2"></div>
                <div>
                    <input type="submit" class="btn btn-outline-dark allowed-submit" id="submit-btn" value="Submit" />
                </div>
            </form>
        </div>
    </div>
</div>
````