class: middle, center, title-slide
count: false

# Building a Columnar Analysis Demonstrator<br>for ATLAS PHYSLITE Open Data<br>using the Python Ecosystem
.large.blue[Matthew Feickert]<br>
on behalf of ATLAS Analysis Model Group<br>
.large[(University of Wisconsin-Madison)]
<br>
[matthew.feickert@cern.ch](mailto:matthew.feickert@cern.ch)
<br>

[International Conference on Computing in High Energy and Nuclear Physics (CHEP) 2024](https://indico.cern.ch/event/1338689/contributions/6015915/)

October 21st, 2024

---
# Self Notes (slide will be removed for talk)

* .bold[Time]: 18 minute talk
   - .bold[15 minutes talk]
   - 3 minutes questions
* .bold[Abstract]:
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
# Challenges for Future Analysis

.kol-1-2[
<!-- box-shadow: 5px 5px 15px rgba(0, 0, 0, 0.5); adds a shadow that is 5px to the right and 5px down from the image, with a blur radius of 15px and a semi-transparent black color (rgba(0, 0, 0, 0.5)). -->
<p style="text-align:center;">
   <a href="https://cds.cern.ch/record/2802918">
      <img src="figures/atlas-disk-projection.png" style="width:100%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>
<!-- .caption[Projected evolution of disk under .blue[conservative] and .red[aggressive] R&D] -->
.center.large[Moving forward won’t be able to store everything on disk]
]
.kol-1-2[
<p style="text-align:center;">
   <a href="https://indico.jlab.org/event/459/contributions/11586/">
      <img src="figures/physlite-model.png" style="width:90%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>
.caption[[Jana Schaarschmidt](https://indico.jlab.org/event/459/contributions/11586/), CHEP 2023]

.center.bold[PHYSLITE]
* Common file format for Run 4 Analysis Model
* Contains already-calibrated objects for fast analysis
* Monolithic: Intended to serve ~80% of physics analysis in Run 4
* Directly used without need for ntuples
]

---
# Columnar Analysis

.center.large.bold[
"columnar analysis" == "array programming for data analysis"
]

.kol-1-2[
.large[
* Higher level APIs for new users and improved user experience
   - People using columnar analysis on ntuples already seem to be loving it
   - Enable the same UX but without ntupling (save disk)
* Potential for higher performance
   - Enable on-the-fly combined performance (CP) tool corrections on PHYSLITE
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

.center.large[Different expressions/representations for same analysis result goals]
.caption[(Nick Smith, [2019 Joint HSF/OSG/WLCG Workshop](https://indico.cern.ch/event/759388/contributions/3306852/))]
]

---
# An Analysis Grand Challenge

.large.center[
HL-LHC era data scale requires rethinking interacting with data during analysis
]

.kol-2-5[
.large[
* .bold[Analysis Grand Challenge] (AGC) community exercise organized by [IRIS-HEP](https://iris-hep.org/) includes the stages of a projected typical HL-LHC analysis
* Demonstrator of development of the required cyberinfrastructure
   - [The 200Gbps Challenge: Imagining HL-LHC analysis facilities](https://indico.cern.ch/event/1338689/contributions/6009824/) (Alexander Held, Monday plenary)
* Opportunity for ATLAS to demonstrate columnar analysis views and areas for improvement
]
]
.kol-3-5[
<p style="text-align:center;">
   <a href="https://iris-hep.org/grand-challenges.html#analysis-grand-challenge">
      <img src="https://iris-hep.org/assets/images/cabinetry-vertical-slice.png"; width=100%>
   </a>
</p>

.center.large[[High level view of operations in an HL-LHC analysis](https://iris-hep.org/grand-challenges.html#analysis-grand-challenge)]
]

---
# Pythonic Analysis Ecosystem for HEP

.kol-2-5[
<p style="text-align:center;">
   <a href="https://web.archive.org/web/20200925025947/https://coiled.io/blog/pydata-dask/">
      <img src="figures/pydata-ecosystem-pycon-2017.png" style="width:100%">
   </a>
</p>

.center.huge[Broader "Scientific Python" ecosystem is designed to be interoperable and support [multiple domain levels](https://www.nature.com/articles/s41586-020-2649-2)]
]

.kol-1-5[
<p style="text-align:center;">
   <img src="figures/pyhep-ecosystem-direction.png" style="width:50%">
</p>
]

.kol-2-5[
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1140031/">
      <img src="figures/pyhep-ecosystem.svg" style="width:100%">
   </a>
</p>

.center.huge[Interoperable domain hierarchy design continued in ["PyHEP" ecosystem](https://indico.cern.ch/event/1140031/)]
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
   - .bold[JupyterLab] as a common interface
   - Highly efficient data delivery with .bold[XCache]
   - Conversion to columnar formats with .bold[ServiceX]
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
# Structure of an ATLAS AGC

<p style="text-align:center;">
   <img src="figures/atlas-pipeline.png"; width=80%>
.center.large[Components of an ATLAS AGC demonstrator pipeline]
</p>

---
# ATLAS Open Data

.kol-1-2[
.large[
* .bold[First] release of [ATLAS Run 2 2015 and 2016 open data](https://atlas.cern/Updates/News/Open-Data-Research) in July 2024
* Using ATLAS open data for AGC
   - Open access data allows for use in testing community projects and problems
   - Released as PHYSLITE (HL-LHC data format)
   - Allows for new students to be able to learn analysis and make contributions quickly
* More on ATLAS Open Data at CHEP 2024:
   - [The First Release of ATLAS Open Data for Research](https://indico.cern.ch/event/1338689/contributions/6013332/) (Zach Marshall, Monday plenary)
   - [Open Data at ATLAS: Bringing TeV collisions to the World](https://indico.cern.ch/event/1338689/contributions/6011129/) (Giovanni Guerrieri, Monday Track 8)
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
# Challenges: Reading all PHYSLITE files

.kol-1-2[
.large[
* Raw PHYSLITE is not easily loadable by columnar analysis tools outside of ROOT
* Awkward Array supports [`behaviors`](https://awkward-array.org/doc/2.6/reference/ak.behavior.html), which allow efficiently reinterpreting data on the fly
   - e.g. correctly handling `ElementLinks`
* ATLAS AMG members have contributed to open ecosystem development to support PHYSLITE in both Uproot and [Coffea](https://coffeateam.github.io/coffea/api/coffea.nanoevents.PHYSLITESchema.html#coffea.nanoevents.PHYSLITESchema)
* Continuing to support fixes to both the PyHEP ecosystem tools as well as reporting issues to PHYSLITE
   - Includes work by [ATLAS IRIS-HEP Fellow Sam Kelson](https://indico.cern.ch/event/1449314/contributions/6101290/)
]
]
.kol-1-2[
<br>
<br>
<p style="text-align:center;">
   <a href="https://github.com/CoffeaTeam/coffea/issues/1135">
      <img src="figures/atlas-wishlist-coffea.png" style="width:100%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>
]

---
# Challenges: Systematics

.kol-1-2[
.large[
* As columnar analysis .bold[processes events in batches] also need CP tools and algorithms to process in batches
* Current CP tools operate on xAOD event data model (EDM) for calculation and write systematics to disk for future access (I/O heavy)
* Challenge: Columnar on-the-fly computation be faster than disk
* Refactoring to columnar studies in ATLAS AMG show .bold[improvements in performance and flexibility]
]
]
.kol-1-2[
<br>
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1330797/contributions/5796636/">
      <img src="figures/cp_tools_columnar.png" style="width:100%">
   </a>
</p>

.center[Columnar .cptools[CP tools] operate on .datacolumn[existing columns] in chunks to generate .newcolumn[new columns]<br>(Matthias Vigl, [ACAT 2024](https://indico.cern.ch/event/1330797/contributions/5796636/))]
]

---
# Challenges and Opportunities: Systematics

<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1330797/contributions/5796636/">
      <img src="figures/columnar_cp_tools_diagram.png" style="width:70%">
   </a>
</p>

.kol-1-2[
.large[
* Refactoring to columnar CP tools has allowed for Pythonic array interfaces to be developed
* Using [next generation](https://nanobind.readthedocs.io/) of C++/Python binding libraries allows
   - [Zero-copy operations](https://nanobind.readthedocs.io/en/latest/ndarray.html) to/from n-dimensional array libraries in Python that supports GPUs
   - Full design control of high-level user API (unified UX)
]
]
.kol-1-2[
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1330797/contributions/5796636/">
      <img src="figures/cp_tools_columnar.png" style="width:85%">
   </a>
</p>
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1330797/contributions/5796636/">
      <img src="figures/columnar_cp_python_api.png" style="width:100%">
   </a>
</p>

.center[Columnar .cptools[CP tools] operate on .datacolumn[existing columns] in chunks to generate .newcolumn[new columns]<br>(Matthias Vigl, [ACAT 2024](https://indico.cern.ch/event/1330797/contributions/5796636/))]
]

---
# Columnar CP tools: $Z \to e^{+}e^{-}$ Demo

.kol-1-2[
.large[
Using zero-copy Python bindings to Egamma CP tool prototype
]

```python
from atlascp import EgammaTools
```
<!--  -->
.large[
1. Use [Uproot](https://uproot.readthedocs.io/) to load PHYSLITE Monte Carlo into [Awkward](https://awkward-array.org/) arrays
2. Apply selections
3. Initialize tools
4. Compute systematics on the fly efficiently scaled with [dask-awkward](https://dask-awkward.readthedocs.io/)
]
]
.kol-1-2[
<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1330797/contributions/5796636/">
      <img src="figures/Zee_mc_systematics.png" style="width:100%">
   </a>
</p>

.caption[Selected $m_{ee}$ under on-the-fly computed systematic variations of electron reconstruction efficiency and corrections<br>(Matthias Vigl, [ACAT 2024](https://indico.cern.ch/event/1330797/contributions/5796636/))]
]

---
# ATLAS Open Data AGC Implementations

.kol-1-2[
.large[
* Tooling ecosystem is proving approachable and performant
* Enabling university students to implement versions of the AGC by themselves with mentorship in a Jupyter notebook
* ATLAS IRIS-HEP Fellow Denys Klekots's [AGC project using ATLAS open data](https://indico.cern.ch/event/1455396/contributions/6126406/) ([implementation on GitHub](https://github.com/iris-hep/agc-physlite))
* Simplified version of [IRIS-HEP AGC top reconstruction challenge](https://agc.readthedocs.io/) using 2025+2016 Run 2 Monte Carlo from the 2024 ATLAS open data release
]
]
.kol-1-2[
.bold[Event selection]
* 1 charged lepton
* $\geq 4$ hadronic jets
* Lepton kinematics: $p_{T} \geq 30~\mathrm{GeV}$, $\left|\eta\right| < 2.1$
* Jet kinematics: $p_{T} \geq 25~\mathrm{GeV}$, $\left|\eta\right| < 2.4$

<p style="text-align:center;">
   <a href="https://indico.cern.ch/event/1455396/contributions/6126406/">
      <img src="figures/denys_agc_mbjj.png" style="width:49%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
   <a href="https://indico.cern.ch/event/1455396/contributions/6126456/">
      <img src="figures/denys_agc_ht.png" style="width:49%; box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.5);">
   </a>
</p>
]

---
# Summary of ATLAS Columnar AGC Efforts

.huge[
* Development of a columnar ATLAS AGC implementation with full systematics is still ongoing
* Columnar analysis tool efforts inside of ATLAS have been promising with CP tools showing performance increases
* ATLAS Open Data proving to be useful for research and community communication
* Technical advancements from AMG research are being incorporated into ATLAS wide tooling
* Contributions upstream to PyHEP community tools
* Advancements in tooling are enabling researchers across career stages
]

---
class: end-slide, center

.huge[Backup]

---
# References

* [Using Legacy ATLAS C++ Calibration Tools in Modern Columnar Analysis Environments](https://indico.cern.ch/event/1330797/contributions/5796636/), Matthias Vigl, [ACAT 2024](https://indico.cern.ch/event/1330797/)
* [How the Scientific Python ecosystem helps answering fundamental questions of the Universe](https://cfp.scipy.org/2024/talk/KCXVVR/), Vangelis Kourlitis, Matthew Feickert, and Gordon Watts, [SciPy 2024](https://www.scipy2024.scipy.org/)
* [The Columnar Analysis Grand Challenge Demonstrator](https://indico.cern.ch/event/1268248/contributions/5326293/), Gordon Watts, [ATLAS S&C Plenary Afternoon: Demonstrators](https://indico.cern.ch/event/1268248/), 2023-10-04 [ATLAS Internal]
* [ATLAS AGC Demonstrator](https://indico.cern.ch/event/1328739/contributions/5605607/), Gordon Watts, [ATLAS AMG+ADC Joint Session](https://indico.cern.ch/event/1328739/), 2023-03-30 [ATLAS Internal]
