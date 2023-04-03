Introduction
============

OCHRE is a python based building energy modeling (BEM) tool specifically for residential buildings. The key strengths of OCHRE are the ability to use it with advanced or custom controllers for flexible loads HVAC and water heating as well as the ability to use OCHRE in co-simulation with a grid model.
OCHRE uses `HPXML <https://hpxml.nrel.gov>`_ as the format for inputs. HPXML files that work with OCHRE can be generated from any 'OS-HPXML <https://openstudio-hpxml.readthedocs.io/en/latest/>' based workflow. This includes 'ResStock <https://github.com/NREL/resstock>' and 'BEopt <https://www.nrel.gov/buildings/beopt.html>' 3.0 or later.

Scope 
-----
OCHRE is closely integrated with other OS-HPXML based tools. This means that OCHRE inherits any limitations of these tools. OCHRE is capable of modeling residential single family, multifamily, and manufactured housing. For multifamily buildings, each unit is modeled individually rather than modeling the entire building all at once. See the 'OS-HPXML documentation <https://openstudio-hpxml.readthedocs.io/en/latest/intro.html> _' for more information

License
-------
This project is available under a BSD-3-like license, which is a free, open-source, and permissive license. For more information, check out the `license file <https://github.com/NREL/OpenStudio-HPXML/blob/master/LICENSE.md>`_.