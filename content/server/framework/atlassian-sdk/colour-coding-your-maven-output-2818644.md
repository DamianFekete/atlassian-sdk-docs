---
title: Colour Coding Your Maven Output 2818644
aliases:
    - /server/framework/atlassian-sdk/colour-coding-your-maven-output-2818644.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818644
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818644
confluence_id: 2818644
platform:
product:
category:
subcategory:
---
# Documentation : Colour-Coding your Maven Output

If you are using the Atlassian Plugin SDK in  a UNIX, Linux, or OSX environment you can ensure that your Maven output comes in true colour. Just add an environment variable with the name `MAVEN_COLOR` and value `true`.

``` bash
export MAVEN_COLOR=true
```

Your Maven output will look something like this:  
![](/server/framework/atlassian-sdk/images/mavencolourisedoutput.png)
