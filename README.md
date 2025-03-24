# php-cursor-docker-quickstart

A project template that works with Cursor and Docker for PHP for 
development.

## Quick start

This project is a template for a PHP projects using Docker. 
It is meant to be a starting point for a PHP project using Docker.
You should replace this readme and code with your own.
You should fork or copy from this project and make it your own.

Make sure you have Docker Desktop installed and running.

### Debugging with xDebug Helper browser Extension

To debug PHP from a web browser, you need to install the xDebug Helper
Extension.

Chrome:
[https://chromewebstore.google.com/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=en](https://chromewebstore.google.com/detail/xdebug-helper/eadndfjplgieldjbigjakmdgkmoaaaoc?hl=en)

Edge:
[https://microsoftedge.microsoft.com/addons/detail/xdebug-helper/ggnngifabofaddiejjeagbaebkejomen?hl=en-US](https://microsoftedge.microsoft.com/addons/detail/xdebug-helper/ggnngifabofaddiejjeagbaebkejomen?hl=en-US)

Firefox:
[https://addons.mozilla.org/en-US/firefox/addon/xdebug-helper-for-firefox/](https://addons.mozilla.org/en-US/firefox/addon/xdebug-helper-for-firefox/)

Then set up the helper under Extension->Xdebug Helper `details` then `extension options`.

IDE key: `DEBUG`

Trace Trigger Value: `XDEBUG_TRACE`

Profile Trigger Value: `XDEBUG_PROFILE`

In the browser press `[ctrl][shift][x]` or click the bug icon on the toolbar, the select `debug` to trigger debugging.


Open the web page http://localhost:8088 in your browser.

To Debug PHP code:

TBD

## To (re)build a production image

TBD

## To access the production image locally

Open your browser to [http://localhost:9088](http://localhost:9088/).

## To publish the production image

Edit the lines in `docker-compose.yml` that specify the `image:` name to
match your Docker Hub account and repository.

To push the production image to Docker Hub, run 
`docker compose push php-prod` from the project root directory.

## Production hosting

https://www.hostingadvice.com/how-to/best-docker-container-hosting/


## To access the development Database

If you have not done so already, start the Docker containers Run->Run `Build Interactive`.

By default, PhpMyAdmin is available at
[http://localhost:7088](http://localhost:7088/).

To access the database from outside the Docker container, you can use
a database client like MySQL Workbench or DBeaver.  
Use the following connection information:

- Host: `localhost`
- Port: `5000`
- Username: `root`
- Password: `password`
- Database: `app`

# Extended Documentation

## Howto get `ssh` and `git` working inside the container

At the top of the `docker-compose.yml` file you will see `secrets:`.
This is a list of secrets passed into the container.

The `secrets` are used to create a `~/.ssh` directory inside the container.
This ssh key is used to connect to the GitHub server to download composer packages
under development. You will need to uncomment the `secrets` sections in the 
`docker-compose.yml` file there are two of them.

You need to have your ssh keys in the `~/.ssh` directory on your local machine.

To test that the ssh key is working:

* `docker-compose exec php-dev bash` to get into the container.
* `ssh git@github.com` to test the connection.
* You should see something like `Hi jstormes! You've successfully authenticated ...`
* `exit` to leave the container.

## AWS secrets inside the container

The `secrets` are used to create a `~/.aws` directory inside the container.

You need to have your AWS keys in the `~/.aws` directory on your local machine.
You will need to uncomment the `secrets` sections in the `docker-compose.yml` file.
Also uncomment the `Install AWS-CLI` in the `php?.dev.dockerfile` file.

To test that the aws connection is working:

* `docker-compose exec php-dev bash` to get into the container.
* `aws sts get-caller-identity` to test the connection.
* You should see something like ` "UserId": "AROAUH3TAFGAASDFIZ675T:..." `
* `exit` to leave the container.

