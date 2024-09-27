class: middle, center, title-slide
count: false

# Building a Columnar Analysis Demonstrator<br>for ATLAS PHYSLITE Open Data<br>using the Python Ecosystem
.large.blue[Matthew Feickert]<br>
.large[(University of Wisconsin-Madison)]
<br>
[matthew.feickert@cern.ch](mailto:matthew.feickert@cern.ch)
<br>

[International Conference on Computing in High Energy and Nuclear Physics (CHEP) 2024](https://indico.cern.ch/event/1338689/contributions/6015915/)

October 21st, 2024

---
# Self Notes

* Time: 18 minute talk
   - 15 minutes talk
   - 3 minutes questions

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

---
# An Analysis Grand Challenge

.large[
HL-LHC era data scale requires rethinking how we engage with the data when we preform analysis
]

.kol-1-3[
* .bold[Analysis Grand Challenge] (AGC) community exercise organized by [IRIS-HEP](https://iris-hep.org/) includes the stages of a projected typical HL-LHC analysis
* Binned columnar analysis, reinterpretation [fix]
* Development of the required cyberinfrastructure [fix]
* Opportunity for ATLAS to demonstrate how a columnar analysis view and areas for improvement
   - Accessing PHYSLITE, systematics
]
.kol-2-3[
<p style="text-align:center;">
   <a href="https://iris-hep.org/grand-challenges.html#analysis-grand-challenge">
      <img src="https://iris-hep.org/assets/images/cabinetry-vertical-slice.png"; width=100%>
   </a>
</p>

.caption[[High level view of operations in an HL-LHC analysis](https://iris-hep.org/grand-challenges.html#analysis-grand-challenge)]
]

---
# Columnar Analysis

.center[
"columnar analysis" == "array programming for data analysis"
]

.kol-1-2[
.large[
* Higher level APIs for new users and improved user experience
   - People using columnar analysis on ntuples already seem to be loving it
   - Enable the same UX but without ntupling (save disk)
* Potential for higher performance
   - Enable on-the-fly CP tool corrections on PHYSLITE
* Broader scientific data analysis ecosystem integration
   - Extend and scale ATLAS tools with large and performant ecosystem
]
]
.kol-1-2[
<!-- box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.5); adds a shadow that is 5px to the right and 5px down from the image, with a blur radius of 15px and a semi-transparent black color (rgba(0, 0, 0, 0.5)). -->
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1340782/contributions/5711534/">
      <img src="figures/columnar_analysis_hep_view.png" style="width:100%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>

.caption[(Image credit to [Nick Smith](https://indico.cern.ch/event/759388/contributions/3306852/), [Matthias Vigl](https://indico.cern.ch/event/1340782/contributions/5711534/))]
]

---
# ATLAS Open Data

.kol-1-2[
.large[
* Release of [ATLAS Run 2 2015 and 2016 open data](https://atlas.cern/Updates/News/Open-Data-Research) in July 2024
* Benefits of using ATLAS open data
   - Sharing the data freely with open access allows for use in testing community projects and problems
   - Allows for students to be able to participate in analysis and make an impact while still inexperienced.
]
]
.kol-1-2[
<!-- box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.5); adds a shadow that is 5px to the right and 5px down from the image, with a blur radius of 15px and a semi-transparent black color (rgba(0, 0, 0, 0.5)). -->
<p style="text-align:center;">
   <a href="https://atlas.cern/Updates/News/Open-Data-Research">
      <img src="figures/atlas-open-data-announcement.png" style="width:100%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>

<!-- .caption[13 TeV open data release from ATLAS] -->

<p style="text-align:center;">
   <a href="https://atlas.cern/Updates/News/Open-Data-Research">
      <img src="figures/open-access-principles.png" style="width:100%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>
]

---
# Pythonic Analysis Ecosystem

.kol-1-2[
<p style="text-align:center;">
   <a href="https://coiled.io/blog/pydata-dask/">
      <img src="figures/pydata-ecosystem-pycon-2017.png" style="width:100%">
   </a>
</p>

.caption[Broader "Scientific Python" ecosystem]
]

Complexity bit goes between two

.kol-1-2[
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1140031/">
      <img src="figures/pyhep-ecosystem.svg" style="width:100%">
   </a>
</p>

.caption[In [2022](https://indico.cern.ch/event/1140031/) we created a view for the PyHEP ecosystem]
]

---
# Pythonic Ecosystem for ATLAS Analysis

.kol-1-3[
.large[
Providing the elements of an analysis pipeline
<br>
* Data query and access
* Reading data files (ROOT and others) and columnar access
* Data transformation and histogramming
* Distributed analysis frameworks
* Statistical inference
* Analysis reinterpretation
]
]
.kol-2-3[
<br>
<p style="text-align:center;">
   <a href="https://scikit-hep.org/">
      <img src="figures/pyhep-tool-view.png" style="width:100%">
   </a>
</p>
]

---
# Prototyping on US ATLAS Analysis Facilities

.kol-1-3[
.large[
* [University of Chicago Analysis Facility](https://af.uchicago.edu/) .bold[provides testing bed] with Coffea-casa
* Provides support for:
   - JupyterLab as a common interface
   - Highly efficient data delivery with XCache
   - Conversion to columnar formats with ServiceX
* Excellent integration exercise between analysis and operations
]
]
.kol-2-3[
<p style="text-align:center;">
   <a href="https://iris-hep.org/projects/coffea-casa.html">
      <img src="figures/coffea-casa.png"; width=100%>
   </a>
</p>

.caption[Platform for interactive analysis]
]

---
# Envisioning an ATLAS AGC

<p style="text-align:center;">
   <img src="figures/atlas-pipeline.png"; width=80%>
.center.large[Components of an ATLAS AGC demonstrator pipeline]
</p>

---
# Summary

.huge[
* Whirlwind tour
* Not a hopeless bog
]

---
# References

* [Using Legacy ATLAS C++ Calibration Tools in Modern Columnar Analysis Environments](https://indico.cern.ch/event/1330797/contributions/5796636/), Matthias Vigl, [ACAT 2024](https://indico.cern.ch/event/1330797/)
* [How the Scientific Python ecosystem helps answering fundamental questions of the Universe](https://cfp.scipy.org/2024/talk/KCXVVR/), Vangelis Kourlitis, Matthew Feickert, and Gordon Watts, [SciPy 2024](https://www.scipy2024.scipy.org/)
* [The Columnar Analysis Grand Challenge Demonstrator](https://indico.cern.ch/event/1268248/contributions/5326293/), Gordon Watts, [ATLAS S&C Plenary Afternoon: Demonstrators](https://indico.cern.ch/event/1268248/), 2023-10-04 [ATLAS Internal]
* [ATLAS AGC Demonstrator](https://indico.cern.ch/event/1328739/contributions/5605607/), Gordon Watts, [ATLAS AMG+ADC Joint Session](https://indico.cern.ch/event/1328739/), 2023-03-30 [ATLAS Internal]

---
class: end-slide, center

Backup

---
# Opportunities and Challenges of the HL-LHC
<!--  -->
<p style="text-align:center;">
   <a href="https://hilumilhc.web.cern.ch/content/hl-lhc-project">
      <img src="figures/HL-LHC_schedule.png"; width=69%>
   </a>
   <img src="figures/lhc_lumi.png"; width=30%>
</p>
<!--  -->
.large[
* Increase in "luminosity" of roughly order of magnitude [FIX THIS SLIDE UP]
   - Factor of .bold[20-25] times the amount of collisions delivered from Run-2 of the LHC
* Boon for measurements constrained by statistical uncertainties, searches for rare processes
]

---
# Thing

.huge[
X
]

---

class: end-slide, center
count: false

The end.
