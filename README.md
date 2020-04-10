# stremio-beamup
🛠️ A platform as a service (PaaS) hosting for Stremio addons: as easy a Heroku/Now.sh, but DYI and without the restrictions.

It is based on [Dokku](https://github.com/dokku/dokku), but with two significant differences:
* It's designed with public use in mind - you can authenticate yourself using your GitHub account and push apps
* It only supports Stremio addons and it's optimized for them (by using specific caching policies)


To deploy this yourself, you'll need:

* A Cherryservers account and API key
* Terraform

## Deployment

**WARNING:** this only refers to deploying stremio-beamup itself, not deploying apps to it

1. Run `ssh-keygen -t ed25519 -f id_deploy`
2. Register on [Cherryservers](cherryservers.com) and fund your account
3. Create an API key and paste it into a new file: `creds/cherryservers`; paste your numeric project ID into `creds/cherryservers-project-id`
4. Run `terraform apply`

By default, this will bootstrap a single server called `deployer` that can be used to deploy addons too.


## Deploying an addon

To deploy an addon, you first need to have your SSH key added to your GitHub account; then, `cd` into the directory of your app, and do `./cli/beamup <beamup deployer hostname> <github username> <app name>`; then, `git push beamup master`

Prerequisites and good to know:
* Works on UNIX-like operating systems (Linux, macOS) but it should also work on Windows in Git Bash or the Linux subsystem
* You can use `git push beamup master` to update your addons as well
* Also, when you run `git push beamup master`, you'll see the deployment log and the URL at which you can access your addon
* Your addon repo must suppport one of the Heroku buildpacks or must have a `Dockerfile`; with Nodejs, simply having a `package.json` in the repo should be sufficient
* It's based on Dokku, so whatever you can deploy there you can also deploy on Beamup (it's using the same build system); however, some features are not supported such as custom NGINX config


## FAQ

### Why Cherryservers?

### Can I use this as a general purpose PaaS?

### Does it only support nodejs?
No, it supports every stack that there's a heroku buildpack for, as well as any Docker container.
