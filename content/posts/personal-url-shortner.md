---
title: "go.pasindujr.me - Personal Url Shortner 🔗"
date: 2021-05-04T20:42:34+05:30
draft: false
tags: [blog, projects]
---

This is to roll my own short URLs (Sometimes those URLs are actually not short 😉, I just created this and connected a domain I own for the fun and that's all.) 
This is how I created and deployed this.

 1. Create a new repository inside your favorite git hosting service (In my case its GitHub.)
 2. Inside the repo, create ``_redirects`` file without any extension.
 3. Inside the file, type your "short-paths" and "long-URLs" like this.
 
```
/a-short-path   http://some-place-on-the-web
...
```
4. You can put as much as fields as you want and make sure you put a space/s between short path and long path.
5. Go to [Netlify](https://www.netlify.com/), create an account and deploy the above created repo connecting your Git hosting service. Need help? Check [documentation](https://www.netlify.com/blog/2016/09/29/a-step-by-step-guide-deploying-on-netlify/).
6. You will be provided a Netlify-created sub domain and you can change it for whatever you want.
7. That's it. With the power of ✨Netlify's optimized edge redirects via it's redirects API✨, Now you have a "Personal URL Shortner". You can connect your own domain if You have one.

Check my GitHub repo [here](https://github.com/pasindujr/personal-url-shortner).

If You have any questions or want to step up this project with automating stuff, check [this video](https://youtu.be/HL6paXyx6hM).

