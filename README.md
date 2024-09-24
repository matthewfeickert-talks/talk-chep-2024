# [Building a Columnar Analysis Demonstrator for ATLAS PHYSLITE Open Data using the Python Ecosystem](https://indico.cern.ch/event/1338689/contributions/6015915/)

Talk given in the [Simulation and Analysis Tools track](https://indico.cern.ch/event/1338689/sessions/553988/#20241021) of [CHEP 2024](https://indico.cern.ch/event/1338689/contributions/6015915/).

Viewable online [here](https://matthewfeickert-talks.github.io/talk-chep-2024/).

## Abstract

The ATLAS experiment is in the process of developing a columnar analysis demonstrator, which takes advantage of the Python ecosystem of data science tools.
This project is inspired by the analysis demonstrator from IRIS-HEP.
The demonstrator employs PHYSLITE OpenData from the ATLAS collaboration, the new Run 3 compact ATLAS analysis data format.
The tight integration of ROOT features within PHYSLITE presents unique challenges when integrating with the Python analysis ecosystem.
The demonstrator is constructed from ATLAS PHYSLITE OpenData, ensuring the accessibility and reproducibility of the analysis.
The analysis pipeline of the demonstrator incorporates a comprehensive suite of tools and libraries.
These include uproot for data reading, awkward-array for data manipulation, Dask for parallel computing, and hist for histogram processing.
For the purpose of statistical analysis, the pipeline integrates cabinetry and pyhf, providing a robust toolkit for analysis.
A significant component of this project is the custom application of corrections, scale factors, and systematic errors using ATLAS software.
The infrastructure and methodology for these applications will be discussed in detail during the presentation, underscoring the adaptability of the Python ecosystem for high-energy physics analysis.

## Acknowledgments

- [Matthew Feickert](http://www.matthewfeickert.com/) is supported in part by IRIS-HEP
[![NSF-2323298](https://img.shields.io/badge/NSF-2323298-blue.svg)](https://nsf.gov/awardsearch/showAward?AWD_ID=2323298)
