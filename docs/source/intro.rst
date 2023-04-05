Introduction
============

OCHRE is a python based building energy modeling (BEM) tool specifically for residential buildings. The key strengths of OCHRE are the ability to use it with advanced or custom controllers for flexible loads HVAC and water heating as well as the ability to use OCHRE in co-simulation with a grid model.
OCHRE uses `HPXML <https://hpxml.nrel.gov>`_ as the format for inputs. HPXML is a standardized, interoperable format for sharing residential building characteristics across platforms. Most notably, HPXML integration means OCHRE inputs can be generated from any `OS-HPXML <https://github.com/NREL/OpenStudio-HPXML>`_ based workflow. 

Scope 
-----
OCHRE is closely integrated with other OS-HPXML based tools. This means that OCHRE inherits any limitations of these tools. OCHRE is capable of modeling residential single family, multifamily, and manufactured housing. For multifamily buildings, each unit is modeled individually rather than modeling the entire building all at once. See the `OS-HPXML Documentation <https://openstudio-hpxml.readthedocs.io/en/latest/>`_. for more information.
OCHRE can also be used to model a specific piece of equipment so long as the boundary conditions are appropriately defined. For example, a water heater could be simulated alone so long as draw profile, ambient air temperature, and mains temperature are defined.

License
-------
This project is available under a BSD-3-like license, which is a free, open-source, and permissive license. For more information, check out the `license file <https://github.nrel.gov/Customer-Modeling/ochre/blob/main/LICENSE>`_.
