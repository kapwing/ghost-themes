# Ghost Themes for Kapwing

This repo is a fork of https://github.com/TryGhost/Themes, which is a monorepo that contains a variety of Ghost themes. The themes that we use are Headline (for company blog and resources) and Ease (for company help center).

This fork is preserved so that it is easy to update changes from the original monorepo when themes update. The original readme is copied below which contains the way to test this theme out locally.

To run a theme locally, you need to symlink a theme to your local Ghost site. On my local machine, I've started a ghost deployment in the `test-ghost` directory, so I use the symlink command to copy this theme into there:

Sometimes for reasons unclear to me, the themes built by gulp in this repo don't match what they should be when built for the marketplace. So the easier way to update themes is sometimes to download the version available from your local ghost deployment (from ghost -> settings -> design) and then edit that open and just copy it into this repo. Make sure to check for dropdown menus and title link colors.

```
# run a theme locally
yarn install
yarn symlink --theme headline --site ~/sites/test-ghost

// or
yarn symlink --theme ease --site ~/sites/test-ghost
```

To create a local ghost instance for testing, follow the instructions here: https://ghost.org/docs/install/local/. On my machine, I created a new directory called `test-ghost`, and this is where I created the local ghost instance that I use for testing theme development.

To create an installable theme zip file in packages/headline/dist/:

# create .zip file

yarn zip --theme headline

## Managing Company Blog Ghost

To manage the blog Ghost deployment, you must access the machine where it is hosted on google cloud. You can read the full instructions here: https://docs.google.com/document/d/1oDY3-kvi_DGZ4t2sBy2I93oHFT7e8IKQfkQlq21Skh0/edit#

Key parts copied below:

First ssh into the machine:

`gcloud compute ssh --zone "us-central1-a" "company-blog-ssl" --tunnel-through-iap --project "kapwing-181323"`

Then switch user to the ghost user:

`sudo su - ghostuser` with password `ghostuser`

Now run `ghost ls` to see the running ghost instances.

Follow the guide here to update ghost: https://ghost.org/docs/update/

Sometimes the logs files get out of hand and eat up all the space on the device.

You have to remove them from the directory:

```
cd /var/www/ghost/content/logs
sudo rm https___www_kapwing_com_blog_production.error.log  https___www_kapwing_com_blog_production.log
sudo touch https___www_kapwing_com_blog_production.error.log  https___www_kapwing_com_blog_production.log
```

You may want to update ghost periodically to make sure it works with newer themes.

You can follow the instructions here: https://ghost.org/docs/update/. The basic commands are:

```
sudo npm install -g ghost-cli@latest
ghost update
```

Sometimes this doesn't work if the machine has not enough free space. I usually run this command to try to figure out what might the largest directories are:

`ghostuser@company-blog-ssl:/var/www/ghost$ du -ah . | sort -rh | head -20`

## Managing Help Center Ghost

To manage the help center Ghost deployment, you must access the machine where it is hosted on google cloud. You can read the full instructions here: https://docs.google.com/document/d/1oDY3-kvi_DGZ4t2sBy2I93oHFT7e8IKQfkQlq21Skh0/edit#

Key parts copied below:

First ssh into the machine:

`gcloud compute ssh --zone "us-central1-a" "help-center-image-aug-1" --project "kapwing-181323"`

Then switch user to the ghost user:

`sudo su - ghostuser` with password ghostuser

Now run `ghost ls` to see the running ghost instances.

Follow the guide here to update ghost: https://ghost.org/docs/update/

Sometimes the logs files get out of hand and eat up all the space on the device.

You have to remove them from the directory:

```
cd /var/www/ghost/content/logs
sudo rm https___www_kapwing_com_help_production.error.log  https___www_kapwing_com_help_production.log
sudo touch https___www_kapwing_com_help_production.error.log  https___www_kapwing_com_help_production.log
```

# Ghost Themes

A monorepo for [Ghost](https://github.com/TryGhost/Ghost) official themes.

## Development

You'll need [Node](https://nodejs.org/), [Yarn](https://yarnpkg.com/) and [Gulp](https://gulpjs.com) installed globally. After that, from the project's root directory:

```bash
# install dependencies
yarn

# run development server
yarn dev
```

Now you can edit files in `packages/<theme-name>/assets/css/` or `packages/<theme-name>/assets/js/`, which will be compiled to `packages/<theme-name>/assets/built/` automatically.

To run a theme locally, you need to symlink a theme to your local Ghost site.

```bash
# run a theme locally
yarn symlink --theme <theme-name> --site /dir/to/your/ghost-site
```

Restart your Ghost instance and the theme will be listed in the `Design` settings.

To create an installable theme zip file in `packages/<theme-name>/dist/`:

```bash
# create .zip file
yarn zip --theme <theme-name>
```

## Copyright & License

Copyright (c) 2013-2022 Ghost Foundation - Released under the [MIT license](LICENSE).
