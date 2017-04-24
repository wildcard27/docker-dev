# Amazing Docker Dev Environment!

This will create a docker container that almost replicates the PVTL dev server. The build currently includes all the  dependencies for SiteHQ & Magento 1:

* Ubuntu 14.04 LTS
* PHP 5.6
* MySQL 5.6


## Why must I use this?

1. **Speed**. Tests have shown that running sites out of this container are significantly faster than Vagrant. A Magento 1 site loads, on average, half a second faster from this container than it does from the office dev server. How? Voodoo.

1. **Portability**. So long as the machine you want to use has all of the prerequisites above covered, you can easily move this around anywhere you need. Even to a production environment!

1. **Enjoyment**. OK, this may just be me! But seriously, when you know you can basically carry your own dev server around on a USB stick, it feels pretty good! Bring back the "fun" in functional development environments!


## Prerequisites

Unfortunately, Docker won't run everywhere. To use this environment, you will need to be running a machine with MacOS, Windows 10 Pro or Linux.

Virtualisation must be available and enabled on your CPU.


## How do I use this magic?

Firstly, you're gonna need Docker and Docker Compose. Instructions on installing these for your OS can be found [here](https://docs.docker.com/compose/install/).

Once you have Docker successfully running, do the following:

1. Create a folder on your computer and clone this repo
1. Modify docker-compose.yml at the line: `- ~/web/:/files/web/`. Change `~/web/` to be your folder containing all of your local projects. For example, inside my `~/web/` folder I have a folder called `vast`. After following these steps, I will be able to visit `vast.pvtl.io` and it will run the files contained in the `vast` folder.
1. Open a command prompt/terminal and run `docker-compose up -d`. This will download dependencies for the container and set it up from scratch. The first time running this will take a few minutes, after that, a few seconds.
1. Modify your hosts file to point the site url to 127.0.0.1. For example, I have a line in mine that is `127.0.0.1    vast.pvtl.io`. This will point all calls to `vast.pvtl.io` to my Docker container.
1. Dev away! Use the files on your local machine as you normally would! (eg. `http://vast.pvtl.io`)


## Things you may need to change

* **DB connect configs**. The container includes MySQL server (more info below) but you probably want to use the one on the dev server. Make sure the database connection file (`/includes/dbconnect.php` in SiteHQ and `/app/etc/local.xml` in Magento 1) is pointing to `192.168.0.5` for the office dev server.

* **The name of your project web folder**. The container is set up to route the folder name to `[folder_name].pvtl.io`. If you want to connect to `vast.pvtl.io`, the folder containing all of your Vast project files needs to be named `vast`. It is set up this way so that you can just comment out the line in your hosts file and load the copy of the site stored on the office dev server.
If you feel as though you would like to change this behaviour, feel free to modify the `dev.conf` to suit yourself.


## MySQL
You can connect to the MySQL server running in the container using [MySQL Workbench](https://www.mysql.com/products/workbench/), [Navicat](https://www.navicat.com/) or [Sequel Pro](https://www.sequelpro.com/).

| Parameter | Value |
|-------------|---|
| Connection | Standard TCP/IP |
| Server / IP | `db` (from a container) OR `localhost` (from your computer) |
| Port | `3306` |
| Username | `root` |
| Password | `dbroot` |