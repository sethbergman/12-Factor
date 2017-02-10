The Twelve-Factor App
=====================

DEMO:
[12-factor-ruby.stackriot.xyz](http://12-factor-ruby.stackriot.xyz/)

Development
-----------

    bundle install
    foreman start

[Visit localhost:5000](http://localhost:5000)

Production deploy
-----------------

This application uses the 12 Factor methodology for building applications which run as a service.
Learn more about __<a href="http://12-factor-ruby.stackriot.xyz" target="_blank">The Twelve Factors</a>__.

I use [Dokku](http://dokku.viewdocs.io/dokku/), a Docker powered mini-Heroku like PaaS that I run on a Digital Ocean Ubuntu server.

### Build Steps

```
git remote add dokku dokku@dokku-server.com:12-factor-ruby
git add --all
git commit -m "Deploy to dokku"
git push dokku master
```

### Additional Resources
- [Dokku](http://dokku.viewdocs.io/dokku/)
- [Dokku CLI and other clients](http://dokku.viewdocs.io/dokku/community/clients/)
- [Dokku source on GitHub](https://github.com/dokku/dokku/)
- [Buildpacks](http://dokku.viewdocs.io/dokku/deployment/methods/buildpacks/)
- [DigitalOcean Dokku Image](https://m.do.co/c/ef444ad5d43f)
  - *I recommend at least a 2 GB server for large builds, but for smaller projects 1GB will work just fine.*

![img](http://blog.sethbergman.com/content/images/2017/02/DO-dokku.png)

Meta
----

Created by Adam Wiggins

Contributions from: James Lindenbaum, Mark McGranaghan, Chris Stolt, Ryan
Daigle, Mark Imbriaco, Keith Rarick, Will Leinweber, Jesper Jørgensen, James
Ward, Adam Seligman, Phil Hagelberg, Jon Mountjoy, Matthew Turland, Daniel
Jomphe, Mattt Thompson, Anand Narasimhan, Lucas Fais, Pete Hodgson

Translations and edits by: [@mahnunchik](https://github.com/mahnunchik), [@francescomalatesta](https://github.com/francescomalatesta), [@astralhpi](https://github.com/astralhpi), [@liangshan](https://github.com/liangshan), [@orangain](https://github.com/orangain), [@Keirua](https://github.com/Keirua), Clément Camin, Bob Marteen, [@dmathieu](https://github.com/dmathieu), [@fernandes](https://github.com/fernandes), [@gwmoura](https://github.com/gwmoura), [@lfilho](https://github.com/lfilho) and [more](https://github.com/heroku/12factor/graphs/contributors).

Released under the MIT License: http://www.opensource.org/licenses/mit-license.php
