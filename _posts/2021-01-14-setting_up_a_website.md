# Setting up a website

Establishing web presence is a good learning exercise and a way to keep oneself accountable, by documenting their progress over time. One can build their own web page or website, host it on a server of their choice and buy a domain name for personal branding. Many people opt for using hosting services such as GitLab, GitHub, Bitbucket etc. either standalone, with a domain name of the type of `username.hostingservice.io` (free of charge) or buying their own domain name (cost depends on name choice and availability). 

I decided to do the latter. Below, I am condensing the steps I took to get my webpage up and running ([reference](https://help.github.com/en/articles/using-a-custom-domain-with-github-pages)):
 

1. Buy a domain name for a preferred duration, from a DNS provider of your choice  
2. Setup a repository named `username.hostingservice.io` for instance `inferential.github.io`  
3. Create a file named `CNAME` and enter your domain name without a `www` or `https://` prefix  
3. In the repository's `Settings` tab, look for the field `Custon domain`. Enter the domain name you bought in step 1 and press `Save`  
4. Setup HTTPS was a two-fold step for me.  
  a) in my DNS provider's `DNS Records` tab, I entered the following `A` records: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`  
  b) the next morning, I went back to my repository's `Settings` tab, deleted, saved the change and reentered my domain name in the `Custom domain` field, ensuring `Enforce HTTPS` was selected.  


  Within an hour or two, my website was up and running with HTTPS. 
