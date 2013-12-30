---
layout: post
title: "Annoying Small Fact about JSP Syntax"
description: ""
category: ""
tags: ["jsp"]
---
{% include JB/setup %}

When creating a new variable, I do the following:

```<c:set var="isFromCC-Entry" value=true />```

JSP templating system doesn’t recognize the punctuation “-“. When I get the output of
`${isFromCCEntry}`, I expect the output to be `true`, but however, I get the following printed error on the page:  0.

The solution is to remove the dash “-“, like so:

```<c:set var="isFromCCEntry" value=true />```

This is a syntax problem in JSP templates.