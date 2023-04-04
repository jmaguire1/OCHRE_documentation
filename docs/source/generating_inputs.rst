Generating OCHRE input files
============================

OCHRE is integrated with OS-HPXML, which means that you can use other OS-HPXML based tools to be able to generate most of the OCHRE inputs you need through any OS-HPXML based tool.
There are three inputs needed for any OCHRE model:

- hpxml file: a description of all of the building characteristics affecting energy consumption
- schedule file: schedule of occupant driven loads. A `stochastic occupant model  <https://www.sciencedirect.com/science/article/pii/S0306261922011540>`_ is available in OS-HPXML and can be used to model more realistic occupant behavior.
- weather file: weather data for this home. It is important to use the same weather data to generate the HPXML file and run OCHRE, as some fields in the HPXML file depend on weather. Most notably, OS-HPXML does autosizing calculations for the HVAC capacity based on the weather data. Weather data must be in either epw file format OR come from the `National Solar Radiation Database (NSRDB)  <https://nsrdb.nrel.gov/>`_