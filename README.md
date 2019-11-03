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

### WRF ARW tutorial

The only [HackerNews thread](https://news.ycombinator.com/item?id=19296015) about WRF has a comment from a user about running WRF:

>

## References

[1] Wikipedia article on WRF https://en.wikipedia.org/wiki/Weather_Research_and_Forecasting_Model
Hacker News article about WRF https://news.ycombinator.com/item?id=19296015
[2] U.S. Operational Numerical Weather Prediction: What's Wrong and How it Can Be Fixed https://cliffmass.blogspot.com/2016/10/us-operational-numerical-weather.html
[3] wrfpy https://github.com/ERA-URBAN/wrfpy