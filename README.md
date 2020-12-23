# Greenspeed

Greenspeed is two things:

1. A lightweight wrapper around the excellent [Sitespeed](https://www.sitespeed.io/), with some defaults that are designed to make it easy to use sitespeed as part of the toolbox for carbon-aware, sustainable web design.

2. A forkable repo, as an experiment if using GitHub Actions makes it easy to record over time how well a site performs, in terms of accessibility, performance, and carbon emissions from data transfer.

# The Big Idea

We have tools like [Website carbon](http://websitecarbon.com/), which is a really nice way to engage with the issue of carbon emissions from the energy used to shift data from datacenters to your device.

And in the Green Web Foundation we've worked with the lovely people at Sitespeed [to build a sustainable web plugin](https://www.thegreenwebfoundation.org/news/how-to-build-a-more-sustainable-web-with-a-little-help-from-sitespeed-io/), to help understand the CO2 footprint of a website too, and get some useful context specific tips on how to reduce it.

And if you're like the gang at Wikimedia, you you can even use Sitespeed to create dashboards for Grafana, a monitoring/observability tool, so you can track performance along metrics like accessibility, performance, and carbon emissions.

In fact, if you are able to run Grafana, you can even use a bunch of pre-built dashboards and ranking tables, to expose ths information to your team, and if you want all of your users. [See sitespeed v1's release for example dashboard screens](https://www.sitespeed.io/sitespeed.io-14.0-browsertime-9.0/).

These are all open source - if you know your way around Docker, and can run your own infrastructure, you can run a whole monitoring service your own applications and websites to track all this. It's all well documented [on the sitespeed project's dashboard site](https://www.sitespeed.io/documentation/sitespeed.io/performance-dashboard/).

### But what if you're not at that scale yet?

Sure, it makes sense for the people running Wikipedia to have an entire team dedicated to running a fleet of servers that running automated checks, and maintaining cool dashboards.

But if you're not running at the scale that Wikipedia has acheived, you might still want to track these metrics, even if you can't justify running a full observability platform to do so.

If you don't have a whole performance/accessibility/carbon monitoring setup in place, you probably don't *need* to track how a site's performance changes with every single site change you make, and check it every few minutes. Just running one 30 second computing job once every day will likely be an improvement on where you are right now.

### Greenspeed

This gap is that Greenspeed is designed to fit into. If you have a site you want to track the performance of over time, you can do so, using existing infrastructure made availabe by code hosting services like Github.

You fork the repo, update the site to check, and then switch on GitHub Actions:

Every day, a GitHub action will:

- check the site you've named with sitespeed (and also lighthouse), collecting the metrics
- make a report available for you to download and view in a browser, giving loads of tailored metrics, and advice specific to your site.
- store the report data into git, in a seperate branch, so you can make comparisons in future, using tools [like Sitespeed's Compare](https://compare.sitespeed.io/).



## How to Use It

- Fork the repo
- Change the URL that sitespeed is pointed at, and if necessary tweak budget settings for performance, carbon emissions, accessibility
- Activate GitHub Actions for your new repo

That's it.

A cronjob will check the site for you every day, and every day, you'll have a little microsite generated, available in the GitHub Actions tab, giving you:

- **Google Lighthouse Scores** (all the common metrics, like performance, search enegine performance, PWA suitability, and accessibility)
- **Sitespeed Coach Scores** (similar to above, but these reflect that your idea of a healthy internet might be different to Google, a trillion dollar advertising company's idea of a healthy internet)
- **A list of accessibility issues if they exist, and suggested fixes**, provided by Axe.
- **Estimated figures for the carbon emissions** that result from data being sent over the internet to access your site


## Todo

- [ ] make the url easy to change, like an environment variable, instead having it hardcoded (good first issue!)
- [x] add the cronjob workflow, [so a check can be made every day without you needing to remember](https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#scheduled-events)
- [ ] figure out how to make the report commit to the separate 'runs' branch, [see this post by Simon Willison on what git-scraping is, and why it's neat](https://simonwillison.net/2020/Oct/9/git-scraping/).
- [ ] add a way to check using [the TGWF grid-intensity npm module](https://github.com/thegreenwebfoundation/grid-intensity) to run the job when energy is greenest (running computers to check websites uses energy too, so try to do it when the grid is greenest!)
- [ ] oh, jeez, document this better
