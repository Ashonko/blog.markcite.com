---
title: "How to add custom subdomain in GitHub Pages and Cloudflare"
date: 2021-10-03T20:22:34+06:00
featureImage: images/blog/tutorials/github/git-page-domain-cloudflare/feature-image-small.jpg
postImage: images/blog/tutorials/github/git-page-domain-cloudflare/feature-image.jpg
---
If you are using GitHub pages for hosting your static website like this [MarkCite Blog](https://blog.markcite.com/) and link it to a custom subdomain using Cloudflare, this tutorial is for you.

### Steps in Cloudflare
- [Log in](https://dash.cloudflare.com/login) to your Cloudflare account and select your site.
- Go to the **DNS** settings.
- Click on the **Add record** button.
- Select a **CNAME** type, write the name of your subdomain, (for example: blog), write the GitHub link for your GitHub pages (for example: ashonko.github.io) and click **Save**

Your work at the Cloudflare side is done. Now go to the GitHub Pages.

### Steps in GitHub
- Go to **Settings** > **Pages**.
- Write the name of your subdomain in the **Custom domain** box (for example: blog.markcite.com) and click **Save**

Done. Your work form the GitHub side is also finished. Now you just wait for some time to update the DNS record. It may take form 5 minutes to sometimes a day. After the propagation is done, your site will be up and running in your dedicated custom subdomain.

#### Few points to note
- Make sure that your root link for all the assets of your website is directed to your custom subdomain, not to the link of your github pages, otherwise, the assets will not load.