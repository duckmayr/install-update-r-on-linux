# install-update-r-on-linux

I use R daily for research and run some flavor of Ubuntu Linux or Linux Mint on my machines.
The Ubuntu repositories (which Linux Mint also uses) typically have a fairly recent version of R, but I prefer to have the most recent version.
What follows is a guide to install/upgrade to the most recent version of R on Ubuntu (18.04) or Mint (19).
I then include details regarding system dependencies for some popular R packages.
Parts of this guide were written in response to [this Stack Overflow question](https://stackoverflow.com/questions/46214061/how-to-upgrade-r-in-linux/).

## Installing/Updating to R 3.5.x on Ubuntu 18.04/Linux Mint 19

First, go to [CRAN's list of mirrors](https://cran.r-project.org/mirrors.html) and find the URL of the mirror that is closest to you.
The terminal commands below assume you choose http://cran.wustl.edu/.
Then we can set up our authenication key and the APT repository for the latest version of R with the following terminal commands:

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
sudo echo "deb http://cran.wustl.edu/bin/linux/ubuntu bionic-cran35/" | sudo tee -a /etc/apt/sources.list
sudo apt update
```
What we do next depends on whether you need to install or upgrade R.
If you're installing for the first time, run

```bash
sudo apt install r-base r-base-dev
```
If you're upgrading R, run

```bash
sudo apt upgrade r-base r-base-dev
sudo apt update
sudo apt upgrade
```

Note also that I have put to install/upgrade `r-base` and `r-base-dev`, but I don't know if you have/want `r-base-dev`. I highly recommend it.

If you're upgrading R, to make sure you have all of your R packages available, in a new R session run

```r
update.packages(checkBuilt = TRUE, ask = FALSE)
```

## Installing System Dependencies for `devtools`

I use [`devtools`](https://CRAN.R-project.org/package=devtools) for R package development.
However, before you can install `devtools`, you need some system dependencies first, which you can pick up with the following terminal commands:

```bash
sudo apt update
sudo apt install libcurl4-gnutls-dev libxml2-dev libssl-dev
```

You may also want the following system "dependencies" for `git2r`, but it isn't strictly necessary:

```bash
sudo apt install libgit2-dev libssh2-1-dev
