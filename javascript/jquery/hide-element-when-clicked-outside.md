---
title: Detect a Click event Outside of an Element and Close it
description: 
published: true
date: 2022-09-09T03:46:49.996Z
tags: jquery, how-to, hide, show, click, event, closest, target
editor: markdown
dateCreated: 2022-09-09T03:46:49.996Z
---

# Hide an Element when a Click is Detected outside of it
````javascript
$(document).mouseup(function (e) {
  if ($(e.target).closest("ELEMENT").length === 0) {
    $("ELEMENT").hide("slow");
  }
});
````