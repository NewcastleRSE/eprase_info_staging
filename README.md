# ePRaSE Basic Info site

Sveltekit version of the basic ePRaSE info site, superseding previous version in the Eprase-Info-Site repo, which can be (and may have been by now) deleted. The site is hosted as a static GitHub Pages site with the custom domain https://eprase.info.

## About

This is a public-facing site that explains what ePRaSE is and includes user guides and reports.

### Project Team

* Becky Osselton, Newcastle University  ([rebecca.osselton@newcastle.ac.uk](mailto:rebecca.osselton@newcastle.ac.uk))
* John Schoneboom, Newcastle University  ([John.Schoneboom@newcastle.ac.uk](mailto:John.Schoneboom@newcastle.ac.uk))
* Stephanie Klein, The Newcastle Hospitals NHS Foundation Trust  ([stephanie.klein@nhs.net](mailto:stephanie.klein@nhs.net))
* Ellie Merrison, The Newcastle Hospitals NHS Foundation Trust  ([eleanor.merrison1@nhs.net](mailto:eleanor.merrison1@nhs.net))

### RSE Contact
* Becky Osselton, RSE Team, Newcastle University
* John Schoneboom, RSE Team, Newcastle University

### Built With

* Sveltekit - https://svelte.dev/

## Local Development

This may be the simplest Sveltekit site ever built. Basically there's a link to a Font Awesome stylesheet in src/app.html and everything else that's us and not Svelte's internal business is in the src/routes directory. 

The main layout with header, footer, global and home page styles, and main Svelte imports is in routes/+layout.svelte. Individual page content is in the various +page.svelte files: the home page at the top level of routes, and the others in their own directories (about, faq, lab, news, results, and using). Those each contain only basic HTML and (in a couple of cases) page-specific styles. None of them have their own scripts or import their own Svelte tricks.

Easy peasy.

To view/test the site locally in a browser you can run 

`npm run dev`

## Deployment

When you push master, a GitHub action will build the static site into a directory called 'build' and place its contents into a branch that it creates called gh-pages. That's the branch that feeds the custom domain eprase.info (and is set as such in Settings => Pages).

The build and deployment instructions are in .github/workflows/deploy.yml. Note that it specifies the "publish_dir", the directory where the built site resides, which (by Svelte default) is called 'build'. It also includes 'cname: eprase.info', specifying the custom domain.

That's about all there is to it.