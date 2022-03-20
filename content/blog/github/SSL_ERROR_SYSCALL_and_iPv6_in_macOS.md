---
title: "Github SSL_ERROR_SYSCALL and iPv6 in MacOS"
date: 2022-03-20T09:39:54+06:00
featureImage: images/blog/tutorials/github/ipv6-github-mac/feature-small.png
postImage: images/blog/tutorials/github/ipv6-github-mac/feature-large.png
---

For a few times, I have faced the following error when trying to push my commit to my Github repository:
`fatal: unable to access 'https://github.com/...': LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443`
This is very annoying when you get but this occurs due to the fact that my mac is running on a IPv6 network. This doesn't create any problem doing other things, but when I try to push my commit, I get this error. There is a workaround for this error. Just disable the IPv6 on your mac and then try to push again.

## Disabling IPv6 on your Mac
To disable IPv6 on your Mac, run the following command in your terminal:
### Disable IPv6 for wireless networks:
`networksetup -setv6off Wi-Fi`
### Disable IPv6 for wired networks:
`networksetup -setv6off Ethernet`

Now you can try to push your commit again and the error should disappear. In case you want to enable IPv6 back, run the following command in your terminal:

## Reenable IPv6 on your Mac
To reenable IPv6 on your Mac, run the following command in your terminal:
### Enable IPv6 for wireless networks:
`networksetup -setv6automatic Wi-Fi`
### Enable IPv6 for wired networks:
`networksetup -setv6automatic Ethernet`