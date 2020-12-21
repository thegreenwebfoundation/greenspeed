# Greenspeed

Greenspeed is two things.

1. A lightweight wrapper around the excellent sitespeed, with some defaults that are designed to make it easy to use sitespeed as part of the toolbox for carbon-aware, sustanable web design.

2. A forkable repo, as an experiment in using github actions make it easy to record over time how well a site performs, in terms of accessibility, performance, and carbon emissions from data transfer.

# The big idea

We have tools like [Website carbon](http://websitecarbon.com/), which is a really nice way into engaging with the issue of carbon emissions from the energy used to shift data from datacenters to your device.

And in the Green Web Foundation we've worked with the lovely people at Sitespeed [to build a sustainable web plugin](https://www.thegreenwebfoundation.org/news/how-to-build-a-more-sustainable-web-with-a-little-help-from-sitespeed-io/), to help understand the CO2 footprint of a website too, and get some useful context specific tips on how to reduce it.

And if you're like the gang at Wikimedia, you you can even use sitespeed to create dashboards for grafana so you can track performance along metrics like accessibility, performance, and carbon emissions, building leaderboards, and using all the capabilities a full blown monitoring tool like Grafana can offer.[See sitespeed v1's release for example dashboard screens]](https://www.sitespeed.io/sitespeed.io-14.0-browsertime-9.0/).

These are all open source - if you know your way around docker, and can run your own infrastructure, you can set it up the same set up, and it's all well documented [on the sitespeed project's dashboard site](https://www.sitespeed.io/documentation/sitespeed.io/performance-dashboard/).

But what if you can't set up your own set of servers running automated checks, and dashboarding tools, or you're not at that scale yet?

### Greenspeed

This gap is where greenspeed is designed to fit in.

You fork the repo, update the site to check, and then switch on github actions:

Every day, a github action:

- will check the site you've named with sitespeed (this also runs lighthouse against a site, collecting the data it exposes too)
- make a report available for you to download and view in a browser, giving loads of tailoered metrics, advice tailored to your site.
- store the report data into git, in a seperate branch, so you can make comparisons in future, using tools [like Sitespeed's Compare ](https://compare.sitespeed.io/)

### Why Greenspeed exists

It's really useful to be able to track performance, accessibility and digital sustainability over time, and you shouldn't need to run all your own infrastructure for this to be possible. And if you don't *need* to track how a site's performance changes with every single site change you make, then you probably don't need to be running loads of servers just to run a 30 second copmuting job once every day.

Intermittent, but regular jobs like this are a really good fit for github actions.


## How to use it

- fork the repo
- change the url that sitespeed is pointed at, and if necessary tweak budget settings for performance, carbon emissions, accessibility
- activate github actions for your new repo

That's it.

A cronjob will check the site for you every day, and every day, you'll have a little microsite generated, available in the Github Actions tab, giving you:

- Google Lighthouse Scores (all the common metrics, like performance, search enegine performance, PWA suitability, and accessibility)
- Sitespeed Coach scores (similar to above, but these reflct thaty your idea of a healthy internet might be different to Google, a trillion dollar advertising company's idea of a healthy internet)
- A list of accessibility isues, and suggested fixes, provided by Axe.
- Estimated figures for the carbon emissions that result from data being sent over the internet to access your site


## Todo

- [ ] make the url easy to change, like an environment variable, instead having it hardcoded (good first issue!)
- [x] add the cronjob workflow, [so a check can be made every day without you needing to remember](https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#scheduled-events)
- [ ] figure out how to make the report commit to the separate 'runs' branch, [see this post by Simon Willison on what git-scraping is, and why it's neat](https://simonwillison.net/2020/Oct/9/git-scraping/).
- [ ] add a way to check using [the TGWF grid-intensity npm module](https://github.com/thegreenwebfoundation/grid-intensity) to run the job when energy is greenest (running computers to check websites uses energy too, so try to do it when the grid is greenest!)
- [ ] oh, jeez, document this better
