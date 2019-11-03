# wrf-sandbox

A sandbox to experiment with the [WRF](https://github.com/wrf-model/WRF) Open Source weather model.

>The Weather Research and Forecasting (WRF) model[1] /ˈwɔːrf/ is a numerical weather prediction (NWP) system designed to serve both atmospheric research and operational forecasting needs. NWP refers to the simulation and prediction of the atmosphere with a computer model, and WRF is a set of software for this. WRF features two dynamical (computational) cores (or solvers), a data assimilation system, and a software architecture allowing for parallel computation and system extensibility. The model serves a wide range of meteorological applications across scales ranging from meters to thousands of kilometers. [1]

My goal is to a) run the WRF model with data provided by a university, or a research centre like NOAA or Nasa, b) understand the moving parts of the model, and c) investigate how workflow and scheduler systems are used with WRF.

## Why worry about workflow and scheduler systems?

Most tutorials and pages that I found about WRF did not mention workflows or scheduler, with exception to batch systems like PBS, SGE, etc. Which could mean that most sites are free to implement their own solutions. While this gives the sites more freedom, it also means they could be working on similar solutions, without sharing any knowledge.

Furthermore, the batch systems are good to manage only the workflow part when a single job is actually executed in the batch system. It is much harder when you have multiple jobs, specially if these jobs have dependencies to external files or systems that are not part of the batch system.

A good workflow and/or scheduler system may also help to fill the "white space" [2] of computational resources. [Cylc](https://cylc.github.io) is exceptionally good at it.

### Why Cylc for workflows and job scheduling?

I am biased, as that is the system I work with.

Cylc is Open Source, actively maintained, and used to power the operational NWP workflows at UK Met Office, NZ NIWA, and other sites in Europe, Asia, and North America.

Cylc also supports cycling workflows, going beyond the DAG (directed acyclic graphs). It looks like some groups were able to use WRF and Cylc, for example, see [wrfpy](https://github.com/ERA-URBAN/wrfpy), "a python application that provides an easy way to set up, run, and monitor (long) Weather Research and Forecasting (WRF) simulations (...) and integrates with Cylc to access distributed computing and storage resources as well as monitoring" [3].

## Tutorials

Abbreviations and acronyms:

WRF: Weather Research And Forecasting model
WPS: WRF Pre-processing System
WRF ARW: WRF Advanced Research WRF
WRFDA: WRF Data Assimilation
WRF-Chem: WRF Amospheric Chemistry model
WRF-Hydro: WRF Hydrological modeling system

### WRF compilation tutorial

From http://www2.mmm.ucar.edu/wrf/OnLineTutorial/compilation_tutorial.php. The tutorial includes a lot of useful information. But alas not easy to follow and reproduce with no issues.

This is probably a much better guide for developers using Ubuntu: https://www.enviroware.com/installing-and-running-wrf-3-8-on-linux-ubuntu-lts-16-04-with-intel-i7-8-core-cpu/


### WRF ARW tutorial

The only [HackerNews thread](https://news.ycombinator.com/item?id=19296015) about WRF has a comment from a user about running WRF:

>If you want to set up and use the WRF model linked in the submission to generate your own forecasts, you can follow this tutorial: http://www2.mmm.ucar.edu/wrf/OnLineTutorial/index.php
>
>For all but the most extreme configurations, WRF will run on a modern 2-4 core Linux desktop. It will be fairly slow, but it will run.
>
>You can use the raw data from the official model runs published by NOAA as initial and boundary conditions for your model runs: https://nomads.ncep.noaa.gov . One of the coolest and most under appreciated things about NOAA is that they publish everything online for free for everyone.
>
>Or you can just get the raw data from the official runs from the link above and do your own extraction, and maybe post processing if you like.

#### Installation

There is a [Docker container]() for WRF, but the last commit is from years ago, so I will install the files manually. First, downloaded from http://www2.mmm.ucar.edu/wrf/users/download/get_sources.html:

- WRFV4.0.TAR.gz
- WPSV4.0.TAR.gz

The page for downloads also includes a link to NOAA's [WRF Portal](https://esrl.noaa.gov/gsd/wrfportal/WRFPortal.html), which appears to support workflow managers.

**(!) It supports batch systems, or Ruby workflow. Maybe we could have Cylc added to the list?**

#### Test Data

- http://www2.mmm.ucar.edu/wrf/users/download/test_data.html
- http://www2.mmm.ucar.edu/wrf/users/download/get_sources_wps_geog.html

## References

[1] Wikipedia article on WRF https://en.wikipedia.org/wiki/Weather_Research_and_Forecasting_Model
Hacker News article about WRF https://news.ycombinator.com/item?id=19296015
[2] U.S. Operational Numerical Weather Prediction: What's Wrong and How it Can Be Fixed https://cliffmass.blogspot.com/2016/10/us-operational-numerical-weather.html
[3] wrfpy https://github.com/ERA-URBAN/wrfpy