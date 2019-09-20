# install-update-r-on-linux

I use R daily for research and run some flavor of Ubuntu Linux or Linux Mint on my machines.
The Ubuntu repositories (which Linux Mint also uses) typically have a fairly recent version of R, but I prefer to have the most recent version.<sup>1</sup>
What follows is a guide to install/upgrade to the most recent version of R on Ubuntu (18.04) or Mint (19).
I then include details regarding system dependencies for some popular R packages.
Parts of this guide were written in response to [this Stack Overflow question](https://stackoverflow.com/questions/46214061/how-to-upgrade-r-in-linux/).

## Installing/Updating to R 3.6.x on Ubuntu 18.04/Linux Mint 19

First, go to [CRAN's list of mirrors](https://cran.r-project.org/mirrors.html) and find the URL of the mirror that is closest to you.
The terminal commands below assume you choose http://cran.wustl.edu/.
Then we can set up our authenication key<sup>2</sup> and the APT repository for the latest version of R with the following terminal commands:

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo echo "deb http://cran.wustl.edu/bin/linux/ubuntu bionic-cran35/" | sudo tee -a /etc/apt/sources.list
sudo apt update
```

What we do next depends on whether you need to install or upgrade R.
If you're installing for the first time, run

```bash
sudo apt install r-base r-base-dev
```

Note also that I have put to install `r-base` **and** `r-base-dev`, but I don't know if you want `r-base-dev`.
I highly recommend it.

If you're upgrading R, run

```bash
sudo apt upgrade
```

If you're upgrading R, to make sure you have all of your R packages available, in a new R session run

```r
update.packages(checkBuilt = TRUE, ask = FALSE)
```

## Installing System Dependencies for `devtools` and/or `tidyverse`

I use [`devtools`](https://CRAN.R-project.org/package=devtools) for R package development and sometimes use packages from the [`tidyverse`](https://CRAN.R-project.org/package=tidyverse) for data manipulation.
However, before you can install `devtools` or `tidyverse`, you need some system dependencies first, which you can pick up with the following terminal commands:

```bash
sudo apt update
sudo apt install libcurl4-openssl-dev libxml2-dev libssl-dev
```

You may also want the following system "dependencies" for `git2r`, but it isn't strictly necessary:

```bash
sudo apt install libgit2-dev libssh2-1-dev
```

-----

<sup>1</sup> This statement is no longer quite true.
I still use R daily for research, but have moved to [Manjaro Linux](https://manjaro.org/) as my primary OS on my work and personal machine.
However, I still intend to keep this guide up to date (and of course, may end up with a machine running Ubuntu as the primary OS again in the future).

<sup>2</sup> I put here the full key, though many other guides you may see will use only the "short key."
I have updated this guide to use the full key out of security concerns (see [here](https://forums.sonarr.tv/t/ubuntu-apt-repo-key-collision-security-concern/20285), for example).
