---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
draft: true
isCJKLanguage: true
weight: 0
tags:
cover:
  image: "<image path/url>" # image path/url
  alt: "<alt text>" # alt text
  caption: "<text>" # display caption under cover
  relative: false # when using page bundles set this to true
  hidden: false # only hide on current single page
---