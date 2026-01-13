# ePRaSE Basic Info site

Sveltekit version of the basic ePRaSE info site, superseding previous version in the Eprase-Info-Site repo.

## About

This is a public-facing site that explains what ePRaSE is and includes user guides and reports.

### Project Team

* Becky Osselton, Newcastle University  ([rebecca.osselton@newcastle.ac.uk](mailto:rebecca.osselton@newcastle.ac.uk))
* John Schoneboom, Newcastle University  ([John.Schoneboom@newcastle.ac.uk](mailto:John.Schoneboom@newcastle.ac.uk))
* Stephanie Klein, The Newcastle Hospitals NHS Foundation Trust  ([stephanie.klein@nhs.net](mailto:stephanie.klein@nhs.net))
* Ellie Merrison, The Newcastle Hospitals NHS Foundation Trust  ([eleanor.merrison1@nhs.net](mailto:eleanor.merrison1@nhs.net))

### RSE Contact
Becky Osselton, RSE Team, Newcastle University
John Schoneboom, RSE Team, Newcastle University

### Built With

* Sveltekit - https://svelte.dev/

## Local Development

See the Svelte documentation for full details of site structure, but basically I added a link to a Font Awesome stylesheet in app.html and everything else is in the routes directory. The main layout with header, footer, global and home page styles, and main Svelte imports is in +layout.svelte. Individual page content is in the various +page.svelte files: the home page at the top level of routes, and the others in their own directories (about, faq, lab, news, results, and using). Those contain basic HTML and any page-specific styles.

Easy peasy.

To view/test the site locally you can run 

`npm run dev`

You don't need to build the site locally because that's handled by a GitHub action when you push master.

## Deployment

When you push to origin master, a GitHub action will build the site and place the output in a branch that it creates called gh-pages. That's the branch from which the web-ready code is deployed to the custom domain eprase.info.


