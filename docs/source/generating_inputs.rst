Generating OCHRE input files
============================

OCHRE is integrated with OS-HPXML, which means that you can use other OS-HPXML based tools to be able to generate most of the OCHRE inputs you need through any OS-HPXML based tool.
There are three inputs needed for any OCHRE model:

- hpxml file: a description of all of the building characteristics affecting energy consumption.
- schedule file: schedule of occupant driven loads. A `stochastic occupant model  <https://www.sciencedirect.com/science/article/pii/S0306261922011540>`_ is available in OS-HPXML and can be used to model more realistic occupant behavior.
- weather file: weather data for this home. It is important to use the same weather data to generate the HPXML file and run OCHRE, as some fields in the HPXML file depend on weather. Most notably, OS-HPXML does autosizing calculations for the HVAC capacity based on the weather data. Weather data must be in either epw file format OR come from the `National Solar Radiation Database (NSRDB)  <https://nsrdb.nrel.gov/>`_

There are multiple tools that can be used to generate OCHRE input files, as an OS-HPXML based workflow can be used. However, the most common ways to generate OCHRE input files is to use either BEopt or ResStock. BEopt is best suited to runs of a single, specific building. ResStock is best suited to larger scale runs, such as trying to simulate all the residential buildings in a neighborhood.

Using BEopt to generate OCHRE Inputs
------------------------------------
BEopt 3.0 or later is required.

`BEopt  <https://www.nrel.gov/buildings/beopt.html>`_ is a software package designed to evaluate a wide range of building efficiency options in residential buildings. It also includes the capability to optimize the building design to find the most cost effective path to different levels of energy savings. BEopt has a drawing tool for defining building geometry, a large selection of prebuilt options corresponding to common efficiency features in residential buildings, and the ability to do financial calculations with an utility rate.
Generating OCHRE input files doesn't require any additional work beyond a normal BEopt run. HPXML files are generated as part of the normal workflow, so any run you do in BEopt will have a corresponding HPXML file you can use in OCHRE. When you perform a simulation, 


Using ResStock to generate OCHRE Inputs
---------------------------------------