## How to Setup RStudio for Data Visualization

RStudio is the best integrated development environment (IDE) for data science teams that use the R programming language. It includes a syntax-highlighting editor and console alongside plotting, debugging, and workspace management tools. In addition, R Studio makes working with R easier by providing a much more friendly and robust GUI environment for working with R. In this article; I'll show you how to install the R programming language and R Studio on your most preferred operating system.

![RStudio products catalog](https://cdn.hashnode.com/res/hashnode/image/upload/v1631685662544/UX-jnGlg2.png)

## Prerequisites

- Background knowledge of R programming language.
- A computer machine running Windows, Linux, or macOS operating system.
- Ability to use the web browser and command-line interface.
- A little smile? :)

## R Installation Guide

To use RStudio, you need to install the R programming language first. R is a free software environment for statistical computing and graphics. Next, you have to choose your preferred CRAN (Comprehensive R Archive Network) mirror from the available options to download R. The Comprehensive R Archive Network (CRAN) is a network of FTP and web servers around the world that store identical, up-to-date versions of R and acts as the primary web service distributing R sources, binaries, extension packages, and documentation.

To save yourself some stress, you can choose the `0-Cloud` option, as that will automatically redirect you to the best and closest server.

![A screenshot of the CRAN mirrors page](https://cdn.hashnode.com/res/hashnode/image/upload/v1631599646261/xE--02zOq.png)

### Installing on Windows

Download the latest version of the base distribution of R [here](https://cloud.r-project.org/bin/windows/base). This should download a file with the name `R-4.1.1-win.exe` (version name would change in the future) that will work on 32 and 64 bits. You can then run the installer file and install as you normally [install .exe files](https://www.wikihow.com/Open-EXE-Files). If you want, you can read the Windows [installation guide](https://cloud.r-project.org/bin/windows/base/README.R-4.1.1) for more instructions.

### Installing on Linux

Download the latest version of R for Debian, Fedora, Redhat, Suse, and Ubuntu [here](https://cloud.r-project.org/bin/linux). Alternatively, you can use the commands below to install from your terminal.

#### For Debian

```bash
apt-get update
apt-get install r-base r-base-dev
```

If you want, you can read the Debian [installation guide](https://cloud.r-project.org/bin/linux/debian/) for more instructions.

#### For Fedora

```bash
sudo dnf install R
```

If you want, you can read the Fedora [installation guide](https://cloud.r-project.org/bin/linux/fedora/) for more instructions.

#### For Redhat

```bash
sudo dnf install R
```

If you want, you can read the Redhat [installation guide](https://cloud.r-project.org/bin/linux/redhat/) for more instructions.

#### For Suse

```bash
VERSION=$(grep "^PRETTY_NAME" /etc/os-release | tr " " "_" | sed -e 's/PRETTY_NAME=//' | sed -e 's/"//g')
zypper addrepo -f http://download.opensuse.org/repositories/devel\:/languages\:/R\:/patched/$VERSION/ R-base
```

```bash
zypper install R-base R-base-devel
```

If you want, you can read the Suse [installation guide](https://cloud.r-project.org/bin/linux/suse/README.html) for more instructions.

#### For Ubuntu

```bash
# update indices
apt update -qq

# install required helper packages
apt install --no-install-recommends software-properties-common dirmngr

# add the signing key
wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc

# add the R 4.0 repo from CRAN
add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
```

```bash
apt install --no-install-recommends r-base
```

If you want, you can read the Ubuntu [installation guide](https://cloud.r-project.org/bin/linux/ubuntu/) for more instructions.

### Installing on macOS

Download the latest version of the base distribution of R [here](https://cloud.r-project.org/bin/macosx/). This should download a file with the name `R-4.1.1.pkg` (version name would change in the future). You can then run the installer file and install as you normally [install .pkg files](https://www.laptopmag.com/articles/install-unininstall-mac-software).

If you want, you can read the macOS [installation guide](https://cloud.r-project.org/bin/macosx/) for more instructions.

## R Studio Installation Guide

There are two versions of RStudio; the RStudio Desktop (the desktop app) and RStudio Server (the server running on a web browser). Both have free and paid editions with several additional features, as seen in the screenshots taken from the R Studio official website below:

![RStudio Desktop features](https://cdn.hashnode.com/res/hashnode/image/upload/v1631686827205/GfW9Ow7Jw.png)

![RStudio Server features](https://cdn.hashnode.com/res/hashnode/image/upload/v1631686844085/mr017Mq7B.png)

To download either of the versions, head to the [download page](https://www.rstudio.com/products/rstudio/download/) and click on the "download" button for RStudio Desktop or RStudio Server. Alternatively, you can click on the "buy" button if you want to purchase the other editions. Once you click on "download," you will be redirected to the download page, which will automatically detect your operating system and recommend the file to download (this works only for RStudio Desktop. You can find the RStudio Server [installation guide](https://www.rstudio.com/products/rstudio/download-server/) here). Below that, you will also find a list of other installers for different operating systems. So, pick what you want and download the file.

![RStudio Desktop download page](https://cdn.hashnode.com/res/hashnode/image/upload/v1631687450808/nz6dN-bxg.png)

## Conclusion

Upon successful installation, you can now use RStudio Desktop to write your R programs whilst enjoying all the benefits of R Studio. As seen in the screenshot below from my setup, you'll get the editor at the left-corner, console, terminal, and jobs at the bottom-left-corner, environment at the right-corner, and plots/packages, at the bottom-right corner of the application window. Of course, you can customize the arrangement, change your theme, download R packages, and other settings as you deem fit.

![RStudio Desktop demo](https://cdn.hashnode.com/res/hashnode/image/upload/v1631688076708/BlLt7aW7wp.png)

That's all for this tutorial, and I hope it was helpful. I'll be publishing an introductory guide to the R programming language for beginners soon, so ensure to [subscribe to my newsletter](https://bawd.bolajiayodeji.com/) to get updated. For RStudio product guides and helpful tutorials, you can check out the [RStudio documentation page](https://docs.rstudio.com/). Cheers! 💙

## Attributions

- [R Project](https://www.r-project.org)
- [RStudio product website](https://www.rstudio.com)
- [R Programming Tutorial - Learn the Basics of Statistical Computing](https://www.youtube.com/watch?v=_V8eKsto3Ug)