---
aliases:
- /server/framework/atlassian-sdk/speakeasy-5669113.html
- /server/framework/atlassian-sdk/speakeasy-5669113.md
category: devguide
confluence_id: 5669113
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669113
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669113
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/speakeasy
new_url: /server/framework/atlassian-sdk/speakeasy
platform: server
product: atlassian-sdk
subcategory: learning
title: Speakeasy
---
# Speakeasy

{{% note %}}

We're no longer developing this plugin, and it won't work with recently-released versions of Confluence.

{{% /note %}}

 

Speakeasy is an experimental extension mechanism for Atlassian's products. Speakeasy extensions are designed to be easy and shareable. They are front-end only--no Java code, just web standards (HTML, Javascript, CSS).

{{% note %}}

To reiterate, the Speakeasy framework is currently *experimental*. We do not recommend running Speakeasy on a publicly accessible application. See [What's the catch?](https://developer.atlassian.com/display/DOCS/Speakeasy#Speakeasy-What%27sthecatch?) for more information.

{{% /note %}}

# What is Speakeasy?

Speakeasy is a new extension mechanism with the following basic design goals:

-   extensions are social
-   extensions are augmentative
-   extensions are per user
-   extensions are written using simple web technologies

If you're familiar with our normal plugin system, you can think of an extension as a subset of a plugin that has slightly less capabilities but is much faster to write, much simpler to write and quicker to deploy. While plugins are still very useful for heavy modifications and full applications, we've learned they're just too heavyweight for simple customisations.

Further to these goals, let me throw a few points out there to clarify.

**For admins:**

-   End users can install, enable and disable their *own* extensions. (The set of users who can install, and the set of users who can enable extensions will eventually be customisable, but for now, it's everyone, so be wary)
-   The augmentative part we're still working on, the broad idea is that if you turn them off, the base product is unchanged. This reduces the "upgrade pain" associated with plugin compatibility somewhat (you can wait for an extension to be made compatible with a new release and still upgrade)
-   Plugins are enabled per server, for everyone. This causes various issues with deployability as a rogue or broken plugin can bring down a server, or at least cause it harm. Extensions however are per user. This means a single user can only hurt themselves (they might get a funny looking interface) and not any other users if they're experimenting or trying a new extension. This again increases the safety for your server. (Note: there is a "disable all" URL that always works - if someone gets themselves into trouble, they can always use that to get out of it)
-   Learn more at the [Troubleshooting Speakeasy](/server/framework/atlassian-sdk/troubleshooting-speakeasy)

**For developers:**

-   Simple web technologies? Yup that's right - extensions require no Java, no Maven, no JDK, no JAR. You can create 'em in any text editor. Don't fear - they can still do powerful things! They're written purely in Javascript, CSS, HTML, JSON. They can access REST and XML-RPC resources. They're packaged in a standard ZIP file.  (Note - you *can* use AMPS or the Atlassian SDK to write an extension if you're a power developer, but you don't have to - and we encourage you not to - try our new tools, you'll never go back)
-   Convention over configuration - the traditional atlassian-plugin.xml configuration file doesn't work that well for small plugins, so we have a new convention based system that makes for much simpler extensions. Just put your files in the right directories, a sprinkling of config (often 4 lines) and zip it up.
-   Extensions are designed to be shared, forked, copied, modified - and even edited online. Speakeasy already comes with a mini web-based IDE built in, so your power users can fork an extension that someone else has written, tweak it and see their tweaks live. It's quite amazing.

There are still one or two major technical pillars we're building - but we're ready to get some feedback from our user community on what we have so far.

# How do I get started with Speakeasy?

Right now, you must [install the Speakeasy plugin](/server/framework/atlassian-sdk/installing-speakeasy) into your server (JIRA 4.3+ or Confluence 3.5+). Any user can then go to "\[DEVNET:Their name\] &gt; Speakeasy" and upload an extension.  Other users can then enable that extension, or fork it, etc. Extensions aren't available on the Atlassian Marketplace yet, but you can build your own or get some that others have built. 

Once you have Speakeasy installed, take a look at [Example Extensions](/server/framework/atlassian-sdk/example-extensions) for a list of extensions we have published, or [Developing Speakeasy Extensions](/server/framework/atlassian-sdk/developing-speakeasy-extensions) to get started developing your own extensions. You can even improve the Speakeasy Plugin itself, as described on [Extending the Speakeasy Plugin](/server/framework/atlassian-sdk/extending-the-speakeasy-plugin).

# What's the catch?

For security reasons, we *do not* recommend that you run Speakeasy on a publicly accessible Atlassian application. That said, if you trust your user base, or have a small set of knowledgeable users, it's pretty solid. You can always turn it off by disabling the Speakeasy plugin itself.

As a reference, we're running it at Atlassian on all our internal instances, and have been for a while. We have upwards of 30 extensions on some instances, with hundreds of user enablements.

# Resources

-   <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/labs/speakeasy-plugin" class="external-link">Maven repository</a>
-   <a href="http://github.com/mrdon/speakeasy-plugin" class="external-link">Github project page</a>
-   Talk: <a href="http://www.atlassian.com/company/about/events/atlascamp/2011/day2/remixing-confluence-with-speakeasy" class="external-link">Remixing Confluence with Speakeasy</a> (AtlasCamp 2011)























































































