---
tags: 
  - "personal"
  - "web"
title: "Project Fresco"
subtitle: "JS-based Add-ons Site for XUL Applications"
dateStart: "2022-03"
technologies: 
  - "html-css"
  - "javascript"
points: []
preview: "11"
previewset: true
links: 
  - type: "site"
    url: "https://projectfresco.github.io/"
hasBody: true
---

**Project Fresco** was initially developed as a temporary measure back when the Pale Moon add-ons site went down. It has the following set of features, as of writing:
 * **Full add-on name/description/keywords/author search.** Just type [Lootyhoof](https://projectfresco.github.io/addons/?q=lootyhoof) and all of his extensions will show-up in the results. Partial matches also work!
 * **User pages.** There is now a dedicated page that show every add-on associated with a specific user. Here's an [example](https://projectfresco.github.io/addons/?user=franklindm).
 * **Random add-ons listing in the home page.** Since writing a recommendation algorithm introduces some bias and privacy implications that I'd rather not deal with, the Fresco project [home page](https://projectfresco.github.io/addons/) now shows random applications, extensions, themes, and dictionaries that might be of interest. It does change with every refresh.
 * **Pagination.** Add-on tags don't show everything at once and the listing is now separated by numbered pages.
 * **Release notes.**
 * **Site themes.** Right now, there are 3 site themes to choose from: Default (modern AMO style), Cavendish (classic Mozilla style), and Blue (APMO style).
 * **Dedicated discussion section.** Shown on each add-on page. Hosted via GitHub discussions and supports "reactions".

**Some technical details:** Fresco uses the GitHub API for nearly every add-on entry, which is why it does not require manual changes if a specific add-on releases a new update. Since it sits on top of GitHub Pages, it cannot use PHP or any other tech that would produce static pages with data from the GitHub API, unless we'd (a) go with the manual route, that is, to manually update each and every page with every add-on update; or (b) host it in a separate, independently-hosted site. This isn't practical and is something that I'm not willing to do for a site that acts as a mirror, which is why I've went with a JS approach in accessing the GitHub API and in building the add-on pages and lists.
