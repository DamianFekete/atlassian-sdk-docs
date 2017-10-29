# Atlassian Plugin SDK developer documentation

This repository contains the content for Atlassian Plugin SDK. Documentation is written in Markdown and
published to the Atlassian NPM repository.

## What's inside

Inside this directory you will find the content and navigation structure for your docs. These will
be published at:

https://developer.atlassian.com/atlassian-sdk

```
README.md
node_modules/
package.json
.gitignore
.spelling
content/
atlassian-sdk/
    apis/
        index.md
        sample.md
    products/
        index.md
        sample.md
    images/
        screenshot.jpg
    getting-started.md
    index.md
data/
    atlassian-sdk.json
```

As you can see, the configuration and folder structures are simple, and you
only generate the files that you need to document your app/service.

Once the installation is done, you can run some commands inside this folder:

## Preview your documentation set locally
You can instantly preview changes to your documentation set as you make them using the `npm run preview` command.
See the [viewing docs locally guide](https://developer.atlassian.com/dac/viewing-docs-locally/) for full details.

## Spell check with npm test
Once the installation is done, you can run the `npm test` command inside the project folder:

* `npm test`: Runs a spell checker on Markdown files
* `npm run-script spellcheck`: Interactively fix or ignore spelling errors

Edit the `.spelling` file to add words to your dictionary.

## Release your documentation set
The initial release of your documentation set will require help from the DAC team.
After that, further changes can be released by publishing your documentation set to npm.

See the [releasing your documentation guide](http://developer.atlassian.com/dac/publish/) for full details.

## Markdown front matter

We require markdown files to have a few front matter fields, so that DevHub can
populate correctly the top navigation and left navigation around the document.

For information on the front matter required in your pages, please visit:

    http://developer.atlassian.com/dac/markdown-metadata/

