
# Maintaining your Bioconductor package

## Instructor name and contact information

* Nitesh Turaga ^[Roswell Park Comprehensive Cancer Center, Buffalo, NY] (<nitesh.turaga@roswellpark.org>)

## Workshop Description

Once an R package is accepted into Bioconductor, maintaining it is an
active responsibility undertaken by the package developers and
maintainers. In this short workshop, we will cover how to maintain a
Bioconductor package using existing infrastructure. Bioconductor hosts
a range of tools which maintainers can use such as daily build
reports, landing page badges, RSS feeds, download stats, support site
questions, and the bioc-devel mailing list. Some packages have their
own continuous integration hook setup on their github pages which
would be an additional tool maintainers can use to monitor their
package. We will also highlight one particular git practice which need
to be done while updating and maintaining your package on out git
system.

### Pre-requisites

Accepted Bioconductor package or plans to contribute a Bioconductor
package in the future.

### Participation

Students will be expected to follow along with their laptops if they
choose to, although it is not needed.

### Time outline: 50 mins short workshop

* Introduction: 10 mins
* Why maintain your package
* Infrastructure used for maintenance
* Outline how to use infrastructure: 35 mins
	* Build report
	* Landing page badges
	* RSS feeds
	* Download statistics
	* Support site, Github issues, Bioc-devel mailing list
* Sync package with Github / Bioconductor before every change
	* GitHub + webhooks
* Round up of resources available: 5 mins

### Workshop goals and objectives

* Gain knowledge of how to track Bioconductor packages via download
  statistics, RSS feeds.
* Understand the importance of supporting their user community and how
  to do so using the support site and bioc-devel mailing list.
* Maintain their package and fix bugs using build reports, continuous
  integration tools.
* Update their package consistently on both Github and Bioconductor
  private git server.

## Introduction

**Maintainer** - Who should people contact if they have a problem with
this package? You must have someones name and email address here. You
must make sure this is up to date and accurate.

Maintaining it is an active responsibility undertaken by the package
developers and maintainers. Users contact developers for various
reasons.

**Keep your email up to date in the DESCRIPTION file!**

	Maintainer: Who to complain to <your_fault@fix.it>


Interchangable terminology

*Bioconductor maintainers* <-> *Bioconductor developers* <-> *Package developer* <-> *developer*


## Why maintain your package

1. It's good practice that users appreciate.

1. It'll lead to wide spread usage of your package.

1. It's **required**.

1. Poorly maintained packages get deprecated if they fail build and
   check on Bioconductor during RELEASE cycles. (Bioconductor is
   fairly serious about this)

## Infrastructure used for maintenance

**Build machines** are dedicated towards building your package
*daily*. As a maintianer it's useful to check your package build
report once a week, both in the current RELEASE and DEVEL cycle.

http://bioconductor.org/checkResults/

Build machines cover three platforms (Linux, Windows and OS X) over
RELEASE and DEVEL versions of Bioconductor.

**Version control** - Since last year, GIT has been the primary version
control system.

## Outline how to use infrastructure

Link with most important resources,

http://bioconductor.org/developers/

###	Build report

Bioconductor RELEASE version http://bioconductor.org/checkResults/release/bioc-LATEST/

Bioconductor development version http://bioconductor.org/checkResults/devel/bioc-LATEST/

Six build machines in total at Bioconductor.

DEVEL (3 for devel)

1. Linux (malbec1)
2. Windows (tokay1)
3. OS X (merida1)

![Build machines on DEVEL](Turaga-MaintainBioc/build-machines-devel.png)

RELEASE (3 for release)

1. Linux (malbec2)
2. Windows (tokay2)
3. OS X (merida2)

What is running on these machines?

1. BUILD -- `R CMD build`

1. INSTALL -- `R CMD INSTALL`

1. CHECK -- `R CMD check`


![Build machines on DEVEL](Turaga-MaintainBioc/build-machines-release.png)

The build machines display a status for each package. They indicate different things.

 *TIMEOUT* - INSTALL, BUILD, CHECK or BUILD BIN of package took more than 40 minutes

 *ERROR* - INSTALL, BUILD or BUILD BIN of package failed, or CHECK produced errors

 *WARNINGS* - CHECK of package produced warnings

 *OK* - INSTALL, BUILD, CHECK or BUILD BIN of package was OK

 *NotNeeded* - INSTALL of package was not needed (click on glyph to see why)

 *skipped* - CHECK or BUILD BIN of package was skipped because the BUILD step failed

 *NA*- BUILD, CHECK or BUILD BIN result is not available because of an anomaly in the Build System


###	Landing page badges

What are badges?

![BiocGenerics badges](Turaga-MaintainBioc/Badges.png)

Badges indicate the following:

1. **platforms** availability of the package

1. **downloads** statistics

1. **posts** on support.bioconductor.org which are related to that package based on the `tag`.

1. **in Bioc** how long the package has been in Bioconductor.

1. **build** current build status.

Where can I find these badges?

- Landing page to go to `RELEASE`

	bioconductor.org/packages/release/BiocGenerics

- Landing page to go to `devel`

	bioconductor.org/packages/devel/BiocGenerics

###	RSS feeds

RSS feeds help developers keep track of the development going on in
Bioconductor across all packages. There are multiple ways to use RSS
feeds, and you can use the application of your choice to subscribe to
the feeds.

[Blog which shows the 12 best RSS reader apps](https://zapier.com/blog/best-rss-feed-reader-apps/) across all platforms.

Links for RSS feeds,

http://bioconductor.org/developers/rss-feeds/

Git log published on the website. The git log hosts the last 500
commits to bioconductor across all packages in the development branch
of Bioconductor.

http://bioconductor.org/developers/gitlog/

![Git log on Jul 16th 2018 at 10:30 AM EST](Turaga-MaintainBioc/gitlog.png)

###	Download statistics

The number reported next to each package name is the download score,
that is, the average number of distinct IPs that “hit” the package
each month for the last 12 months (not counting the current month).

http://bioconductor.org/packages/stats/

**Example**

![BiocGenerics Download Statistics](Turaga-MaintainBioc/BiocGenerics-download-stats.png)

###	Support site, Github issues, Bioc-devel mailing list

Support infrastructure set up for Bioconductor **users** to be in
touch with maintainers.

#### Mailing list

Mailing list for `bioc-devel` for all questions related package
development, infrastructure, package support. If a question is
misplaced, the author will be pointed to the correct location to ask
the question.

https://stat.ethz.ch/mailman/listinfo/bioc-devel

#### Support site

Public support site, with easy to use interface to ask questions among
the broader community. Any and all questions are welcome here.

http://support.bioconductor.org/

#### Github issues

Github issues are more developer centric than mailing list and support
site quetsions. This needs to be posted directly on the development
repositories of individual packages. Each package maintainer can
choose to do their development on Github giving an interface for
issues.

The Bioconductor core team manages issues on the repositories
maintained under the [Bioconductor Organization on Github](https://github.com/Bioconductor).

The packages maintained by Bioconductor core follow the structure

	https://github.com/Bioconductor/<PACKAGE_NAME>/issues

Eg: https://github.com/Bioconductor/GenomicRanges/issues

## Sync package with Github / Bioconductor before every change

Do this everytime there is an update on your package from your end, or, before you start developing.

Help with Git.

http://bioconductor.org/developers/how-to/git/

Sync package from Bioconductor repo to Github repo

http://bioconductor.org/developers/how-to/git/sync-existing-repositories/

### GitHub + webhooks


## Round up of resources available