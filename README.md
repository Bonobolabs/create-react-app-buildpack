# Heroku Buildpack for create-react-app

This is a fork of a [fork](https://github.com/4riders/create-react-app-buildpack) of the no longer supported Heroku create-react-app buildpack.

This buildpack just installs and executes multiple child buildpacks:

- heroku-buildpack-apt to install apt deps
- heroku-buildpack-nodejs for npm, compiling the react app
- https://github.com/bonobolabs/create-react-app-inner-buildpack
  - this converts the `static.json` file into a `nginx.conf.erb` file, using a node script. This handles all the routes, headers and proxy redirects defined in the static.json file. It also maintains support for runtime config changes (so we can can change an ENV var and reboot the dyno, rather than having to redeploy + rebuild the whole app)
- https://github.com/heroku/heroku-buildpack-nginx/blob/main/static.md uses nginx to serve the nginx.conf.erb file
