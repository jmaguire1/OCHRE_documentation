Main index
==========

Getting Started
===============

OCHRE Overview
--------------

OCHRE is a Python-based building energy modeling tool designed
specifically for modeling flexible loads in residential buildings. OCHRE
includes detailed models and controls for flexible devices including
HVAC equipment, water heaters, electric vehicles, solar PV, and
batteries. It is designed to run in co-simulation with custom
controllers, aggregators, and grid models.

More information about OCHRE is available on `NREL’s
website <https://www.nrel.gov/grid/ochre.html>`__ and on
`Github <https://github.com/NREL/OCHRE>`__.

Scope
-----

OCHRE is closely integrated with other OS-HPXML based tools. This means
that OCHRE inherits any limitations of these tools. OCHRE is capable of
modeling residential single family, multifamily, and manufactured
housing. For multifamily buildings, each unit is modeled individually
rather than modeling the entire building all at once. See the \`OS-HPXML
Documentation <https://openstudio-hpxml.readthedocs.io/en/latest/>`\_.
for more information.

Installation
------------

For a stand-alone installation, OCHRE can be installed using \`pip\`
from the command line:

\``\`

pip install git+https://github.nrel.gov/Customer-Modeling/ochre.git

\``\`

Alternatively, you can download the repo and run the \`setup.py\` file:

\``\`

python setup.py install

\``\`

To embed OCHRE in a co-simulation using a conda environment, create an
\`environment.yml\` file in the co-simulation project and include the
following lines:

\``\`

dependencies:

- pip:

- git+https://github.nrel.gov/Customer-Modeling/ochre

\``\`

Usage
-----

OCHRE can be used to simulate a residential dwelling or an individual
piece of equipment. In either case, a python object is instantiated and
then simulated. A set of input parameters must be defined.

Below is a simple example to simulate a dwelling:

\``\`

import os

import datetime as dt

from ochre import Dwelling

from ochre.utils import default_input_path # for using sample files

house = Dwelling(

start_time=dt.datetime(2018, 5, 1, 0, 0),

time_res=dt.timedelta(minutes=10),

duration=dt.timedelta(days=3),

hpxml_file =os.path.join(default_input_path, 'Input Files',
'sample_resstock_properties.xml'),

schedule_input_file=os.path.join(default_input_path, 'Input Files',
'sample_resstock_schedule.csv'),

weather_file=os.path.join(default_input_path, 'Weather',
'USA_CO_Denver.Intl.AP.725650_TMY3.epw'),

verbosity=3,

)

df, metrics, hourly = dwelling.simulate()

\``\`

This will return 3 variables:

\* \`df\`: a Pandas DataFrame with 10 minute resolution

\* \`metrics\`: a dictionary of energy metrics

\* \`hourly\`: a Pandas DataFrame with 1 hour resolution (verbosity >= 3
only)

OCHRE can also be used to model a specific piece of equipment so long as
the boundary conditions are appropriately defined. For example, a water
heater could be simulated alone so long as draw profile, ambient air
temperature, and mains temperature are defined.

For more examples, see the following python scripts in the \`bin\`
folder:

\* Run a single dwelling: \`bin/run_dwelling.py\`

\* Run a single piece of equipment: \`bin/run_equipment.py\`

\* Run a dwelling with an external controller:
\`bin/run_external_control.py\`

\* Run multiple dwellings: \`bin/run_multiple.py\`

\* Run a fleet of equipment: \`bin/run_fleet.py\`

License
-------

This project is available under a BSD-3-like license, which is a free,
open-source, and permissive license. For more information, check out the
\`license file
<https://github.nrel.gov/Customer-Modeling/ochre/blob/main/LICENSE>`\_.

Citation and Publications
-------------------------

When using OCHRE in your publications, please cite:

1. Blonsky, M., Maguire, J., McKenna, K., Cutler, D., Balamurugan, S.
   P., & Jin, X. (2021). **OCHRE: The Object-oriented, Controllable,
   High-resolution Residential Energy Model for Dynamic Integration
   Studies.** *Applied Energy*, *290*, 116732.
   https://doi.org/10.1016/j.apenergy.2021.116732

Below is a list of publications that have used OCHRE:

2.  Munankarmi, P., Maguire, J., Balamurugan, S. P., Blonsky, M.,
    Roberts, D., & Jin, X. (2021). Community-scale interaction of energy
    efficiency and demand flexibility in residential buildings. *Applied
    Energy*, *298*, 117149.
    https://doi.org/10.1016/j.apenergy.2021.117149

3.  Pattawi, K., Munankarmi, P., Blonsky, M., Maguire, J., Balamurugan,
    S. P., Jin, X., & Lee, H. (2021). Sensitivity Analysis of Occupant
    Preferences on Energy Usage in Residential Buildings. *Proceedings
    of the ASME 2021 15th International Conference on Energy
    Sustainability, ES 2021*. https://doi.org/10.1115/ES2021-64053

4.  Blonsky, M., Munankarmi, P., & Balamurugan, S. P. (2021).
    Incorporating residential smart electric vehicle charging in home
    energy management systems. *IEEE Green Technologies Conference*,
    *2021-April*, 187–194.
    https://doi.org/10.1109/GREENTECH48523.2021.00039

5.  Cutler, D., Kwasnik, T., Balamurugan, S., Elgindy, T., Swaminathan,
    S., Maguire, J., & Christensen, D. (2021). Co-simulation of
    transactive energy markets: A framework for market testing and
    evaluation. *International Journal of Electrical Power & Energy
    Systems*, *128*, 106664.
    https://doi.org/10.1016/J.IJEPES.2020.106664

6.  Utkarsh, K., Ding, F., Jin, X., Blonsky, M., Padullaparti, H., &
    Balamurugan, S. P. (2021). A Network-Aware Distributed Energy
    Resource Aggregation Framework for Flexible, Cost-Optimal, and
    Resilient Operation. *IEEE Transactions on Smart Grid*.
    https://doi.org/10.1109/TSG.2021.3124198

7.  Blonsky, M., McKenna, K., Maguire, J., & Vincent, T. (2022). Home
    energy management under realistic and uncertain conditions: A
    comparison of heuristic, deterministic, and stochastic control
    methods. *Applied Energy*, *325*, 119770.
    https://doi.org/10.1016/J.APENERGY.2022.119770

8.  Munankarmi, P., Maguire, J., & Jin, X. (2022). *Occupancy-Based
    Controls for an All-Electric Residential Community in a Cold
    Climate*. 1–5. https://doi.org/10.1109/PESGM48719.2022.9917067

9.  Wang, J., Munankarmi, P., Maguire, J., Shi, C., Zuo, W., Roberts,
    D., & Jin, X. (2022). Carbon emission responsive building control: A
    case study with an all-electric residential community in a cold
    climate. *Applied Energy*, *314*, 118910.
    https://doi.org/10.1016/J.APENERGY.2022.118910

10. O’Shaughnessy, E., Cutler, D., Farthing, A., Elgqvist, E., Maguire,
    J., Blonsky, M., Li, X., Ericson, S., Jena, S., & Cook, J. J.
    (2022). *Savings in Action: Lessons from Observed and Modeled
    Residential Solar Plus Storage Systems*.
    https://doi.org/10.2172/1884300

11. Earle, L., Maguire, J., Munankarmi, P., & Roberts, D. (2023). The
    impact of energy-efficiency upgrades and other distributed energy
    resources on a residential neighborhood-scale electrification
    retrofit. *Applied Energy*, *329*, 120256.
    https://doi.org/10.1016/J.APENERGY.2022.120256

Contact
-------

For any questions, concerns, or suggestions for new features in OCHRE,
contact the developers directly at Jeff.Maguire@nrel.gov and
Michael.Blonsky@nrel.gov

Modeling Approach
=================

Envelope
--------

The envelope model is a simplified resistor-capacitor (RC) model that
tracks temperatures throughout the dwelling. The model is flexible and
can handle multiple zones and boundaries, including:

-  Temperature Zones

   -  Living space

   -  Garage

   -  Attic

   -  Foundation (conditioned basement, unconditioned basement, or
      crawlspace)

-  Boundaries

   -  Exterior walls

   -  Interior walls and furniture

   -  Windows

   -  Roof (flat and tilted)

   -  Floor (slab or raised floor)

   -  Ceiling and gable walls (if attic exists)

   -  Garage walls, roof, and floor (if garage exists)

   -  Foundation walls, slab, ceiling, and rim joists (if foundation
      exists)

   -  Walls between adjacent units in multifamily buildings

Thermal resistance and capacitance coefficients are determined from the
HPXML file and are based on values from EnergyPlus input/output (.eio)
files.

Each boundary is modeled using a resistance/capacitance (RC) network.
OCHRE treats each individual material within the boundary separately,
with a capacitor representing the thermal mass of the material and
resistors with half of the overall material resistance on each side of
the capacitor. Convection, solar radiation, and thermal (long-wave)
radiation are accounted for at both surfaces of each boundary.
Convection is incorporated using constant film coefficients that are
based on the orientation of the surface and its location (interior or
exterior). Radiation is treated as heat added to the surface and is
calculated using the surface temperature, the temperature of other
surfaces in the connected zone, and view factors for each surface.
External surface radiation incorporates the ambient temperature and the
sky temperature. An example of how surfaces are split into a
corresponding RC network is shown below.

|A picture containing diagram Description automatically generated|

The full RC network for the building is generated dynamically depending
on what features are included in the building. The most basic example is
a single conditioned zone on a slab on grade with a flat roof, where
only a single zone is modeled. OCHRE will generate more complicated RC
networks if multiple zones are included in the building. Additional
zones are used to model attics, basements/crawlspaces, and garages. The
figure below shows the most complicated RC network in OCHRE, where an
attic, crawlspace/basement, and garage are all included in the building,
as well as a high-level overview of the heat transfer pathways assumed
in this case.

|Diagram, schematic Description automatically generated| |image1|

OCHRE includes the capability to model multifamily buildings using the
same unit by unit approach as other HPXML based workflows. Each unit is
modeled as a separate dwelling unit with adiabatic surfaces separating
different units. OCHRE does not currently support modeling a whole
multifamily building with multiple units simultaneously or the modeling
of central space and water heating systems.

Thermal mass due to furniture and interior partition walls is also
accounted for in the living space. Partition walls and furniture are
modeled explicitly with surface areas and material properties like any
other surface and exchange heat through both convection and radiation.
The heat capacity of the air is also modeled to determine the living
zone temperature. However, a multiplier is generally applied to this
capacitance. Numerous studies (cite
https://docs.google.com/spreadsheets/d/1ebSmvDFdXEXVRdvkzqMF1C9MwHrHCQKFF75QMkPgd7A/edit?pli=1#gid=0)
have shown that applying a multiplier to the air capacitance provides a
much better match to experimental data when trying to model explicit
cycling of the HVAC equipment conditioning the living space. This
multiplier helps account for the volume of ducts and the time required
for warm and cold air to diffuse through the living space. Values for
this multiplier in the literature range from 3-15 depending on the
study. OCHRE uses a default multiplier of 7.

The envelope includes a humidity model for the living space zone. The
model determines the indoor humidity and wet bulb temperature based on a
mass balance. Moisture can be added or removed from the space based on
airflow from outside through infiltration and ventilation, internal
latent gains from appliances such as dishwashers or cooking ranges, and
latent cooling provided by HVAC equipment. OCHRE does not currently
include a dehumidifier model to control indoor humidity.

Sensible and latent heat gains within the dwelling are taken from
multiple sources:

-  Conduction between zones and material layers

-  Convection and long-wave radiation from zone surfaces

-  Infiltration, mechanical ventilation, and natural ventilation

-  Solar irradiance, including absorbed and transmitted irradiance
   through windows

-  Occupancy and equipment heat gains

-  HVAC delivered heat, including duct losses and heat delivered to the
   basement zone

HVAC
----

OCHRE models several different types of heating, ventilation, and air
conditioning (HVAC) technologies commonly found in residential buildings
in the United States. This includes furnaces, boilers, electric
resistance baseboards, central air conditioners (ACs), room air
conditioners, air source heat pumps (ASHPs), minisplit heat pumps
(MSHPs). OCHRE also includes “ideal” heating and cooling equipment
models that perfectly maintain the indoor setpoint temperature with a
constant efficiency.

HVAC equipment use three types of algorithms for determining equipment
capacity and efficiency:

-  Static capacity: System capacity and efficiency is set at
   initialization and does not change (e.g., Gas Furnace, Electric
   Baseboard)

-  Dynamic capacity: System capacity and efficiency varies based on
   indoor and outdoor temperatures and air flow rate (e.g., Air
   Conditioner, Air Source Heat Pump)

-  Ideal capacity: System capacity is calculated at each time step to
   maintain constant indoor temperature (e.g., Ideal Heater, Ideal
   Cooler)

Some HVAC models include multi-speed options, including single-speed,
two-speed, and variable speed options. The one- and two-speed options
typically use the dynamic capacity algorithm for high resolution
simulations, while the variable speed option typically uses the ideal
capacity algorithm.

The Air Source Heat Pump and Mini Split Heat Pump models include heating
and cooling functionality. The heat pump heating model includes a
defrost algorithm that reduces efficiency and capacity at low
temperatures, as well as an electric resistance element that is enabled
when the outdoor air temperature is below a threshold.

By default, HVAC equipment are controlled using a thermostat control.
Heating and cooling setpoints are defined in the input files and can
vary over time.

All HVAC equipment can be externally controlled by updating the
thermostat setpoints and deadband or by direct load control (i.e.,
shut-off). Static and dynamic HVAC equipment can also be controlled
using duty cycle control or by disabling specific speeds. The equipment
will follow the duty cycle control exactly while minimizing temperature
deviation from setpoint and minimizing cycling.

Ducts
~~~~~

Water Heating
-------------

OCHRE currently supports modeling tank, tankless and heat pump water
heaters. The water tank model is an RC model that tracks temperature
throughout the tank. It is a flexible model that can handle multiple
nodes in the water tank. Currently, a 12-node, 2-node, and 1-node model
are implemented. RC coefficients are derived from the properties file.
The fully mixed tank models the entire tank as a single node with a
uniform temperature. This model is best suited to large timesteps. In
residential waters, stratification occurs as cold water is brought into
the bottom of the tank and buoyancy drives the hottest water to the top
of the tank. The stratified tank model captures this buoyancy and the
effect it has on outlet temperature as well as the “dead volume” below
the lower element in an electric water heater that doesn’t get heated
during normal operation. Note that to model a heat pump water heater a
stratified tank model must be used (2 or 12 nodes, with 12 nodes
generally being more accurate but also more computationally intensive.
In HPWHs, the heat pump performance is a function of the ambient air wet
bulb temperature (calculated using the humidity module in OCHRE) and the
temperature of water adjacent to the condenser (typically the bottom
half of the tank in most products on the market today).

The tank model accounts for internal and external conduction, heat flows
from water draws, and includes an algorithm to simulate temperature
inversion mixing (ie stratification) if more than 1 node is used. The
model can handle regular and tempered water draws. A separate water draw
file is currently required to set the water draw profile. In standard
usage, this draw profile is part of the schedule file generated as part
of creating inputs (see section Inputs:Schedule)

Mechanically, water heaters with a tank follow a similar structure to
HVAC equipment. For example, the Electric Resistance Water Heater has a
static capacity, while the Heat Pump Water Heater has a dynamic capacity
(and a backup electric resistance element similar to the Air Source Heat
Pump). Tankless water heaters operate similarly to Ideal HVAC equipment,
although an 8% derate is applied to the nominal efficiency of the unit
to account for cycling losses in accordance with ANSI/RESNET

Similar to HVAC equipment, water heater equipment has a thermostat
control, and can be externally controlled by updating the thermostat
setpoints and deadband, specifying a duty cycle, or direct shut-off.
Tankless equipment can only be controlled through thermostat control and
direct-shut-off.

Electric Vehicles
-----------------

Electric vehicles are modeled using an event-based model and a charging
event dataset from
`EVI-Pro <https://www.nrel.gov/transportation/evi-pro.html>`__. EV
parking events are randomly generated using the EVI-Pro dataset for each
day of the simulation. One or more events may occur per day. Each event
has a prescribed start time, end time, and starting state-of-charge
(SOC). When the event starts, the EV will charge using a linear model
similar to the battery model described below.

Electric vehicles can be externally controlled through a delay signal or
a direct power signal. A delay signal will delay the start time of the
charging event. The direct power signal will set the charging power
directly at each time step, and it is only suggested for Level 2
charging.

Batteries
---------

The battery model incorporates standard battery parameters including
battery energy capacity, power capacity, and efficiency. The model
tracks battery SOC and maintains upper and lower SOC limits. It tracks
AC and DC power, and it reports losses as sensible heat to the building
envelope. It can also model self-discharge.

The battery model can optionally track internal battery temperature and
battery degradation. Battery temperature is modeling using a 1R-1C
thermal model and can use any envelope zone as the ambient temperature.
The battery degradation model tracks energy capacity degradation using
temperature and SOC data and a rainflow algorithm.

The battery model includes a schedule-based controller and a
self-consumption controller. The schedule-based controller runs a daily
charge and discharge schedule, where the user can define the charging
and discharging start times and power setpoints. The self-consumption
controller sets the battery power setpoint to the opposite of the house
net load (including PV) to achieve zero grid import and export. There is
also an option to only allow battery charging from PV. The battery will
follow these controls until the SOC limits are reached.

The battery can also be externally controlled through a direct setpoint
for real power. There is currently no reactive power control for the
battery model.

Solar PV
--------

Solar photovoltaics (PV) is modeled using PySAM, a python wrapper for
the System Advisory Model (SAM). Standard values are used for the PV
model, although the user can select the PV system capacity, the tilt
angle, and the orientation.

PV can be externally controlled through a direct setpoint for real and
reactive power. The user can define an inverter size and a minimum power
factor threshold to curtail real or reactive power. Watt- and
Var-priority modes are available.

Generators
----------

Gas generators and fuel cells can be modeled for resilience analysis.
These models include power capacity and efficiency parameters similar to
the battery model. Control options are also similar to the battery
model.

Other Loads
-----------

OCHRE includes many other common end-use loads that are modeled using a
load profile schedule. Load profiles, as well as sensible and latent
heat gain coefficients, are included in the input files. These loads can
be electric or natural gas loads. Schedule-based loads include:

-  Appliances (clothes washer, clothes dryer, dishwasher, refrigerator,
   cooking range)

-  Lighting (indoor, exterior, garage, basement)

-  Ceiling fan and ventilation fan

-  Pool Equipment (pool pump and heater, hot tub pump and heater)

-  Miscellaneous electric loads (television, other)

-  Miscellaneous gas loads (grill, fireplace, lighting)

These loads are not typically controlled, but they can be externally
controlled using a load fraction. For example, a user can set the load
fraction to zero to simulate an outage or a resilience use case.

Co-simulation
-------------

OCHRE is designed to be run in co-simulation with controllers, grid
models, aggregators, and other agents. The inputs and outputs of key
functions are designed to connect with these agents for streamlined
integration. These inputs and outputs are defined in [controller
integration] and [outputs and analysis], respectively.

See [citation and publication] for a list of use cases where OCHRE was
run in co-simulation. And feel free to contact the developers [contact]
if you are interested in developing your own use case.

Unsupported OS-HPXML Features
=============================

While OCHRE is intended to work with OS-HPXML and files created through
either BEopt or ResStock, not every feature in those tools is currently
supported in OCHRE. Features not currently supported are generally lower
priority features that are considered future work. Depending on the
impact of the feature, OCHRE should either return a warning or error
when an HPXML file including these options is supplied. Warnings are
used if the option is likely to have a minimal impact on energy results
(such as eaves) and errors are used for a feature with a substantial
impact (such as a ground source heat pump). The current list of
technologies not supported in OCHRE is:

-  Eaves (warning)

-  Overhangs (warning)

-  Structural Insulated Panel (SIP) walls (warning)

-  Ground source heat pumps (error)

-  Fuels other than electricity, natural gas, propane, or oil (error)

   -  Propane and oil equipment are converted to natural gas (warning)

-  Dehumidifiers (error)

-  Solar water heaters (error)

-  Desuperheaters (error)

-  

Input Files and Arguments
=========================

HPXML File
----------

OCHRE uses the Home Performance eXtensible Markup Language, or
`HPXML <https://www.hpxmlonline.com/>`__, file format for defining
building properties. HPXML provides a standardized format for all the
relevant inputs for a building energy model of a residential building.
The full HPXML schema and a validator tool is available
`here <https://hpxml.nrel.gov/>`__. HPXML is continuously updated to
account for additional relevant properties, and in some cases extension
elements can be used to store additional information not currently
included in the schema.

-  Standardized data format designed for interoperability between
   stakeholders

-  Generated during audits with REM/Rate, but also by other NREL tools
   like `ResStock <https://resstock.nrel.gov/>`__ (or any other
   `OS-HPXML <https://github.com/NREL/OpenStudio-HPXML>`__ based
   workflow)

-  HPXML integration allows us to quickly generate corresponding models
   suitable for co-simulation based on other workflows

Schedule Input File
-------------------

A schedule input file is optional but highly recommended. OS-HPXML has
two different types of occupancy models it supports: “asset” and
“operational” (see
`here <https://openstudio-hpxml.readthedocs.io/en/latest/workflow_inputs.html?highlight=occupant#buildingoccupancy>`__
for more information). The “asset” occupant model uses the schedules
defined in `ANSI/RESNET
301 <http://www.resnet.us/wp-content/uploads/archive/resblog/2019/01/ANSIRESNETICC301-2019_vf1.23.19.pdf>`__
for all occupant driven loads, but note that these schedules represent a
smooth average usage for all of the occupant driven loads (hot water
usage, dishwasher, clothes washer, clothes dryer, and cooking range) as
well as occupancy itself. The “operational” calculation uses a
stochastic event generator (described
`here <https://www.sciencedirect.com/science/article/pii/S0306261922011540>`__)
to model more realistic events associated with the occupant driven
loads. The operational (or stochastic) model is most often used in OCHRE
as it more realistically models the on/off usage of these devices and
therefore gets a better estimate of the power spikes associated with
their usage.

The schedule file is generated when using ResStock (named
“schedules.csv”) or when using BEopt and selecting stochastic schedules
for each end use (also named “schedules.csv”). The file contains all
necessary times series schedule information for load profiles as well as
hourly temperature setpoints for both thermostats and water heaters (if
. See the `OS-HPXML
documentation <https://openstudio-hpxml.readthedocs.io/en/latest/workflow_inputs.html#detailed-schedule-inputs>`__
for more information.

Tip: The load profile values in the schedule input file are normalized.
OCHRE can save a schedule file after initialization that contains load
profiles for each scheduled equipment in units of kW.

Weather File
------------

A weather input file is required for simulating a dwelling. OCHRE
accepts
`EnergyPlus <https://bigladdersoftware.com/epx/docs/8-3/auxiliary-programs/energyplus-weather-file-epw-data-dictionary.html>`__
and `National Solar Radiation Database <https://nsrdb.nrel.gov/>`__
(NSRDB) weather file formats.

Generating Input Files
----------------------

A large advantage to using HPXML is the interoperability it provides,
particularly with other NREL building energy modeling tools. HPXML files
can be generated using the
`OS-HPXML <https://github.com/NREL/OpenStudio-HPXML>`__ workflow, which
is documented
`here <https://openstudio-hpxml.readthedocs.io/en/latest/intro.html>`__.
This workflow is used in both
`BEopt <https://www.nrel.gov/buildings/beopt.html>`__ (version 3.0 or
later) and `ResStock <https://github.com/NREL/resstock>`__ (version 3.0
or later). As a result, a user familiar with these other tools generates
OCHRE input files as part of their normal workflow. This allows these
other tools to be used as a front end and enables quick comparisons
between OCHRE and EnergyPlus. OCHRE has been tested with HPXML files
from both workflows, but note it does not currently support all of the
features of these tools.

HPXML and occupancy schedule input files can be generated from:

-  `BEopt <https://www.nrel.gov/buildings/beopt.html>`__ 3.0 or later:
   best for designing a single building model. Includes a user interface
   to select building features. Note that the occupancy schedule file is
   optional.

-  `End-Use Load
   Profiles <https://www.nrel.gov/buildings/end-use-load-profiles.html>`__
   Database: best for using pre-existing building models

-  `ResStock <https://resstock.nrel.gov/>`__: best for existing ResStock
   users and for users in need of a large sample of building models

Weather input files can be generated from:

-  `BEopt <https://www.nrel.gov/buildings/beopt.html>`__ or
   `EnergyPlus <https://energyplus.net/weather>`__: for TMY weather
   files in EPW format

-  `NSRDB <https://nsrdb.nrel.gov/data-viewer>`__: for TMY and AMY
   weather files in NSRDB format

Dwelling Arguments
------------------

A Dwelling model can be initialized using:

\``\`

from OCHRE import Dwelling

house = Dwelling(\**dwelling_args)

\``\`

where \`dwelling_args\` is a Python dictionary of Dwelling arguments.

The table below lists the required arguments for creating a Dwelling
model.

+--------------+---------+---------------------------------------------+
| **Argument   | **A     | **Description**                             |
| Name**       | rgument |                                             |
|              | Type**  |                                             |
+==============+=========+=============================================+
| start_time   | dat     | Simulation start time                       |
|              | etime.d |                                             |
|              | atetime |                                             |
+--------------+---------+---------------------------------------------+
| time_res     | date    | Simulation time resolution                  |
|              | time.ti |                                             |
|              | medelta |                                             |
+--------------+---------+---------------------------------------------+
| duration     | date    | Simulation duration                         |
|              | time.ti |                                             |
|              | medelta |                                             |
+--------------+---------+---------------------------------------------+
| hpxml_file   | string  | Path to HPXML file                          |
+--------------+---------+---------------------------------------------+
| weather_file | string  | weather_file: Path to weather file          |
| or           |         |                                             |
| weather_path |         |                                             |
+--------------+---------+---------------------------------------------+
|              |         | weather_path: Path to directory of weather  |
|              |         | files. The file name can be read from       |
|              |         | “Weather Station” in the HPXML file.        |
+--------------+---------+---------------------------------------------+

The table below lists the optional arguments for creating a Dwelling
model.

+------+-----+---------+----------------------------------------------+
| **   | *   | **      | **Description**                              |
| Argu | *Ar | Default |                                              |
| ment | gum | Value** |                                              |
| Na   | ent |         |                                              |
| me** | Typ |         |                                              |
|      | e** |         |                                              |
+======+=====+=========+==============================================+
| name | str | OCHRE   | Name of the simulation                       |
|      | ing |         |                                              |
+------+-----+---------+----------------------------------------------+
| sch  | str | None    | Path to schedule input file                  |
| edul | ing |         |                                              |
| e_in |     |         |                                              |
| put_ |     |         |                                              |
| file |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| ini  | dat | None    | Runs a "warm up" simulation to improve       |
| tial | eti | (no     | initial temperature values                   |
| izat | me. | i       |                                              |
| ion_ | tim | nitiali |                                              |
| time | ede | zation) |                                              |
|      | lta |         |                                              |
+------+-----+---------+----------------------------------------------+
| t    | str | None    | Use "DST" for local U.S. time zone with      |
| ime_ | ing | (no     | daylight savings, "noDST" for local U.S.     |
| zone |     | time    | time zone without daylight savings, or any   |
|      |     | zone    | time zone in pytz.all_timezones              |
|      |     | m       |                                              |
|      |     | odeled) |                                              |
+------+-----+---------+----------------------------------------------+
| v    | int | 1       | Verbosity of the outputs, from 0-9. See      |
| erbo |     |         | Outputs and Analysis for details             |
| sity |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| m    | int | 6       | Verbosity of the output metrics, from 0-9.   |
| etri |     |         | See Dwelling and Equipment Metrics for       |
| cs_v |     |         | details                                      |
| erbo |     |         |                                              |
| sity |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| out  | str | HPXML   | Path to saved output files                   |
| put_ | ing | or      |                                              |
| path |     | eq      |                                              |
|      |     | uipment |                                              |
|      |     | s       |                                              |
|      |     | chedule |                                              |
|      |     | file    |                                              |
|      |     | di      |                                              |
|      |     | rectory |                                              |
+------+-----+---------+----------------------------------------------+
| o    | b   | FALSE   | Save time series files as parquet files      |
| utpu | ool |         | (False saves as csv files)                   |
| t_to | ean |         |                                              |
| _par |     |         |                                              |
| quet |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| ex   | dat | None    | Time resolution to save results to files     |
| port | eti | (no     |                                              |
| _res | me. | inter   |                                              |
|      | tim | mediate |                                              |
|      | ede | data    |                                              |
|      | lta | export) |                                              |
+------+-----+---------+----------------------------------------------+
| save | b   | True if | Save results files, including time series    |
| _res | ool | ve      | files, metrics file, schedule output file,   |
| ults | ean | rbosity | and status file                              |
|      |     | > 0     |                                              |
+------+-----+---------+----------------------------------------------+
| s    | b   | FALSE   | Save all input arguments to json file,       |
| ave_ | ool |         | including user defined arguments. If False   |
| args | ean |         | and verbosity >= 3, the json file will only  |
| _to_ |     |         | include HPXML properties.                    |
| json |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| sav  | b   | True if | Save status file to indicate whether the     |
| e_st | ool | save_   | simulation is complete or failed             |
| atus | ean | results |                                              |
|      |     | is True |                                              |
+------+-----+---------+----------------------------------------------+
| s    | l   | Empty   | List of time series inputs to save to        |
| ave_ | ist | list    | schedule output file                         |
| sche |     |         |                                              |
| dule |     |         |                                              |
| _col |     |         |                                              |
| umns |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| sche | p   | None    | Schedule with equipment or weather data that |
| dule | and |         | overrides the schedule_input_file and the    |
|      | as. |         | equipment_schedule_file. Not required for    |
|      | Dat |         | Dwelling and some equipment                  |
|      | aFr |         |                                              |
|      | ame |         |                                              |
+------+-----+---------+----------------------------------------------+
| ext_ | dat | None    | Time resolution for external controller.     |
| time | eti |         | Required if using Duty Cycle control         |
| _res | me. |         |                                              |
|      | tim |         |                                              |
|      | ede |         |                                              |
|      | lta |         |                                              |
+------+-----+---------+----------------------------------------------+
| seed | int | HPXML   | Random seed for setting initial temperatures |
|      | or  | or      | and EV event data                            |
|      | str | eq      |                                              |
|      | ing | uipment |                                              |
|      |     | s       |                                              |
|      |     | chedule |                                              |
|      |     | file    |                                              |
+------+-----+---------+----------------------------------------------+
| m    | d   | Empty   | Dictionary that directly modifies values     |
| odif | ict | dict    | from HPXML file                              |
| y_hp |     |         |                                              |
| xml_ |     |         |                                              |
| dict |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| E    | d   | Empty   | Includes Equipment-specific arguments        |
| quip | ict | dict    |                                              |
| ment |     |         |                                              |
+------+-----+---------+----------------------------------------------+
| Enve | d   | Empty   | Includes arguments for the building Envelope |
| lope | ict | dict    |                                              |
+------+-----+---------+----------------------------------------------+

Equipment-specific Arguments
----------------------------

An Equipment model can be initialized in a very similar way to a
Dwelling. For example, to initialize a battery:

\``\`

from OCHRE import Battery

equipment = Battery(name, \**equipment_args)

\``\`

where \` equipment_args\` is a Python dictionary of Equipment arguments.
A full set of the equipment classes available are listed in this
section, by end use.

The table below lists the required arguments for creating any standalone
Equipment model. Some equipment have additional required arguments as
described in the sections below.

+----------------------------+--------------+-------------------------+
| **Argument Name**          | **Argument   | **Description**         |
|                            | Type**       |                         |
+============================+==============+=========================+
| start_time                 | datet        | Simulation start time   |
|                            | ime.datetime |                         |
+----------------------------+--------------+-------------------------+
| time_res                   | dateti       | Simulation time         |
|                            | me.timedelta | resolution              |
+----------------------------+--------------+-------------------------+
| duration                   | dateti       | Simulation duration     |
|                            | me.timedelta |                         |
+----------------------------+--------------+-------------------------+
|                            |              |                         |
+----------------------------+--------------+-------------------------+
|                            |              |                         |
+----------------------------+--------------+-------------------------+
|                            |              |                         |
+----------------------------+--------------+-------------------------+

The table below lists the optional arguments for creating any standalone
Equipment model. Some equipment have additional optional arguments as
described in the sections below.

+-------+-----+---------+---------------------------------------------+
| **Arg | *   | **      | **Description**                             |
| ument | *Ar | Default |                                             |
| N     | gum | Value** |                                             |
| ame** | ent |         |                                             |
|       | Typ |         |                                             |
|       | e** |         |                                             |
+=======+=====+=========+=============================================+
| name  | str | OCHRE   | Name of the simulation                      |
|       | ing |         |                                             |
+-------+-----+---------+---------------------------------------------+
| init  | dat | None    | Runs a "warm up" simulation to improve      |
| ializ | eti | (no     | initial temperature values                  |
| ation | me. | i       |                                             |
| _time | tim | nitiali |                                             |
|       | ede | zation) |                                             |
|       | lta |         |                                             |
+-------+-----+---------+---------------------------------------------+
| zone  | str | None    | Name of Envelope zone if envelope model     |
| _name | ing |         | exists                                      |
+-------+-----+---------+---------------------------------------------+
| enve  | oc  | None    | Envelope model for measuring temperature    |
| lope_ | hre |         | impacts (required for HVAC equipment)       |
| model | .En |         |                                             |
|       | vel |         |                                             |
|       | ope |         |                                             |
+-------+-----+---------+---------------------------------------------+
| verb  | int | 1       | Verbosity of the outputs, from 0-9. See     |
| osity |     |         | Outputs and Analysis for details            |
+-------+-----+---------+---------------------------------------------+
| o     | str | HPXML   | Path to saved output files                  |
| utput | ing | or      |                                             |
| _path |     | eq      |                                             |
|       |     | uipment |                                             |
|       |     | s       |                                             |
|       |     | chedule |                                             |
|       |     | file    |                                             |
|       |     | di      |                                             |
|       |     | rectory |                                             |
+-------+-----+---------+---------------------------------------------+
| ou    | b   | FALSE   | Save time series files as parquet files     |
| tput_ | ool |         | (False saves as csv files)                  |
| to_pa | ean |         |                                             |
| rquet |     |         |                                             |
+-------+-----+---------+---------------------------------------------+
| expor | dat | None    | Time resolution to save results to files    |
| t_res | eti | (no     |                                             |
|       | me. | inter   |                                             |
|       | tim | mediate |                                             |
|       | ede | data    |                                             |
|       | lta | export) |                                             |
+-------+-----+---------+---------------------------------------------+
| sa    | b   | True if | Save results files, including time series   |
| ve_re | ool | ve      | files, metrics file, schedule output file,  |
| sults | ean | rbosity | and status file                             |
|       |     | > 0     |                                             |
+-------+-----+---------+---------------------------------------------+
| sa    | b   | FALSE   | Save all input arguments to json file,      |
| ve_ar | ool |         | including user defined arguments. If False  |
| gs_to | ean |         | and verbosity >= 3, the json file will only |
| _json |     |         | include HPXML properties.                   |
+-------+-----+---------+---------------------------------------------+
| s     | b   | True if | Save status file to indicate whether the    |
| ave_s | ool | save_   | simulation is complete or failed            |
| tatus | ean | results |                                             |
|       |     | is True |                                             |
+-------+-----+---------+---------------------------------------------+
| s     | b   | FALSE   | Include equivalent battery model data in    |
| ave_e | ool |         | results                                     |
| bm_re | ean |         |                                             |
| sults |     |         |                                             |
+-------+-----+---------+---------------------------------------------+
| s     | l   | Empty   | List of time series inputs to save to       |
| ave_s | ist | list    | schedule output file                        |
| chedu |     |         |                                             |
| le_co |     |         |                                             |
| lumns |     |         |                                             |
+-------+-----+---------+---------------------------------------------+
| equ   | str | None    | File with equipment time series data.       |
| ipmen | ing |         | Optional for most equipment                 |
| t_sch |     |         |                                             |
| edule |     |         |                                             |
| _file |     |         |                                             |
+-------+-----+---------+---------------------------------------------+
| sch   | d   | None    | Dictionary of {file_column_name:            |
| edule | ict |         | ochre_schedule_name} to rename columns in   |
| _rena |     |         | equipment_schedule_file. Sometimes used for |
| me_co |     |         | PV                                          |
| lumns |     |         |                                             |
+-------+-----+---------+---------------------------------------------+
| s     | num | 1       | Scaling factor to normalize data in         |
| chedu | ber |         | equipment_schedule_file. Sometimes used for |
| le_sc |     |         | PV to convert units                         |
| ale_f |     |         |                                             |
| actor |     |         |                                             |
+-------+-----+---------+---------------------------------------------+
| sch   | p   | None    | Schedule with equipment or weather data     |
| edule | and |         | that overrides the schedule_input_file and  |
|       | as. |         | the equipment_schedule_file. Not required   |
|       | Dat |         | for Dwelling and some equipment             |
|       | aFr |         |                                             |
|       | ame |         |                                             |
+-------+-----+---------+---------------------------------------------+
| ex    | dat | None    | Time resolution for external controller.    |
| t_tim | eti |         | Required if using Duty Cycle control        |
| e_res | me. |         |                                             |
|       | tim |         |                                             |
|       | ede |         |                                             |
|       | lta |         |                                             |
+-------+-----+---------+---------------------------------------------+
| seed  | int | HPXML   | Random seed for setting initial             |
|       | or  | or      | temperatures and EV event data              |
|       | str | eq      |                                             |
|       | ing | uipment |                                             |
|       |     | s       |                                             |
|       |     | chedule |                                             |
|       |     | file    |                                             |
+-------+-----+---------+---------------------------------------------+

The following sections list the names and arguments for all OCHRE
equipment by end use. Many equipment types have all of their required
arguments included in the HPXML properties. These properties can be
overwritten by specifying the arguments in the \`equipment_args\`
dictionary.

HVAC Heating and Cooling
~~~~~~~~~~~~~~~~~~~~~~~~

OCHRE includes models for the following HVAC equipment:

+------------+---------------------+----------------+----------------+
| End Use    | Equipment Class     | Equipment Name | Description    |
+============+=====================+================+================+
| HVAC       | ElectricFurnace     | Electric       |                |
| Heating    |                     | Furnace        |                |
+------------+---------------------+----------------+----------------+
| HVAC       | ElectricBaseboard   | Electric       |                |
| Heating    |                     | Baseboard      |                |
+------------+---------------------+----------------+----------------+
| HVAC       | ElectricBoiler      | Electric       |                |
| Heating    |                     | Boiler         |                |
+------------+---------------------+----------------+----------------+
| HVAC       | GasFurnace          | Gas Furnace    |                |
| Heating    |                     |                |                |
+------------+---------------------+----------------+----------------+
| HVAC       | GasBoiler           | Gas Boiler     |                |
| Heating    |                     |                |                |
+------------+---------------------+----------------+----------------+
| HVAC       | HeatPumpHeater      | Heat Pump      | Air Source     |
| Heating    |                     | Heater         | Heat Pump with |
|            |                     |                | no electric    |
|            |                     |                | resistance     |
|            |                     |                | backup         |
+------------+---------------------+----------------+----------------+
| HVAC       | ASHPHeater          | ASHP Heater    | Air Source     |
| Heating    |                     |                | Heat Pump,     |
|            |                     |                | heating only   |
+------------+---------------------+----------------+----------------+
| HVAC       | MSHPHeater          | MSHP Heater    | Minisplit Heat |
| Heating    |                     |                | Pump, heating  |
|            |                     |                | only           |
+------------+---------------------+----------------+----------------+
| HVAC       | AirConditioner      | Air            | Central air    |
| Cooling    |                     | Conditioner    | conditioner    |
+------------+---------------------+----------------+----------------+
| HVAC       | RoomAC              | Room AC        | Room air       |
| Cooling    |                     |                | conditioner    |
+------------+---------------------+----------------+----------------+
| HVAC       | ASHPCooler          | ASHP Cooler    | Air Source     |
| Cooling    |                     |                | Heat Pump,     |
|            |                     |                | cooling only   |
+------------+---------------------+----------------+----------------+
| HVAC       | MSHPCooler          | MSHP Cooler    | Minisplit Heat |
| Cooling    |                     |                | Pump, cooling  |
|            |                     |                | only           |
+------------+---------------------+----------------+----------------+

The table below shows the required and optional equipment-specific
arguments for HVAC equipment.

+---------------+--------+---------+--------------+------------------+
| Argument Name | Ar     | Re      | Default      | Description      |
|               | gument | quired? | Value        |                  |
|               | Type   |         |              |                  |
+===============+========+=========+==============+==================+
| Capacity (W)  | number | Yes     | N/A          | Number: Rated    |
|               | or     |         |              | capacity         |
|               | list   |         |              |                  |
|               |        |         |              | List: Rated      |
|               |        |         |              | capacity by      |
|               |        |         |              | speed            |
+---------------+--------+---------+--------------+------------------+
| use_i         | b      | No      | True only if | Method to        |
| deal_capacity | oolean |         | time_res >=  | determine HVAC   |
|               |        |         | 5 minutes or | capacity.        |
|               |        |         | for          |                  |
|               |        |         | va           | If True, use     |
|               |        |         | riable-speed | ideal setpoint   |
|               |        |         | equipment    | method.          |
|               |        |         |              |                  |
|               |        |         |              | If False, use    |
|               |        |         |              | equipment        |
|               |        |         |              | cycling method   |
|               |        |         |              | with thermostat  |
|               |        |         |              | deadband         |
+---------------+--------+---------+--------------+------------------+
| …             |        |         |              |                  |
+---------------+--------+---------+--------------+------------------+

.. _water-heating-1:

Water Heating
~~~~~~~~~~~~~

OCHRE includes models for the following Water Heating equipment:

+-------------------+----------------------+--------------------------+
| End Use           | Equipment Class      | Equipment Name           |
+===================+======================+==========================+
| Water Heating     | ElectricR            | Electric Tank Water      |
|                   | esistanceWaterHeater | Heater                   |
+-------------------+----------------------+--------------------------+
| Water Heating     | GasWaterHeater       | Gas Tank Water Heater    |
+-------------------+----------------------+--------------------------+
| Water Heating     | HeatPumpWaterHeater  | Heat Pump Water Heater   |
+-------------------+----------------------+--------------------------+
| Water Heating     | TanklessWaterHeater  | Tankless Water Heater    |
+-------------------+----------------------+--------------------------+
| Water Heating     | Ga                   | Gas Tankless Water       |
|                   | sTanklessWaterHeater | Heater                   |
+-------------------+----------------------+--------------------------+

The table below shows the required and optional equipment-specific
arguments for Water Heating equipment.

+---+----------+---+-------+----------------+--------------------------+
| e | **       | * | **R   | **Default      | **Description**          |
| n | Argument | * | equir | Value**        |                          |
| d | Name**   | A | ed?** |                |                          |
| u |          | r |       |                |                          |
| s |          | g |       |                |                          |
| e |          | u |       |                |                          |
|   |          | m |       |                |                          |
|   |          | e |       |                |                          |
|   |          | n |       |                |                          |
|   |          | t |       |                |                          |
|   |          | T |       |                |                          |
|   |          | y |       |                |                          |
|   |          | p |       |                |                          |
|   |          | e |       |                |                          |
|   |          | * |       |                |                          |
|   |          | * |       |                |                          |
+===+==========+===+=======+================+==========================+
| W | us       | b | No    | True if        | If True, OCHRE sets      |
| a | e_ideal_ | o |       | time_res >= 5  | water heater capacity to |
| t | capacity | o |       | minutes        | meet the setpoint. If    |
| e |          | l |       |                | False, OCHRE uses        |
| r |          | e |       |                | thermostat deadband      |
| H |          | a |       |                | control                  |
| e |          | n |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | wat      | i | No    | 12 if Heat     | Number of nodes in water |
| a | er_nodes | n |       | Pump Water     | tank model               |
| t |          | t |       | Heater, 1 if   |                          |
| e |          |   |       | Tankless Water |                          |
| r |          |   |       | Heater,        |                          |
| H |          |   |       | otherwise 2    |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Capacity | n | No    | 4500           | Water heater capacity    |
| a | (W)      | u |       |                |                          |
| t |          | m |       |                |                          |
| e |          | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Ef       | n | No    | 1              | Water heater efficiency  |
| a | ficiency | u |       |                | (or supplemental heater  |
| t | (-)      | m |       |                | efficiency for HPWH)     |
| e |          | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Setpoint | n | Yes   | Taken from     | Water heater setpoint    |
| a | Tem      | u |       | HPXML file, or | temperature. Can also be |
| t | perature | m |       | 51.67          | set in schedule          |
| e | (C)      | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Deadband | n | No    | 8.17 for Heat  | Water heater deadband    |
| a | Tem      | u |       | Pump Water     | size. Can also be set in |
| t | perature | m |       | Heater,        | schedule                 |
| e | (C)      | b |       | otherwise 5.56 |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Max Tank | n | No    | 60             | Maximum water tank       |
| a | Tem      | u |       |                | temperature              |
| t | perature | m |       |                |                          |
| e | (C)      | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Mixed    | n | No    | 40.56          | Hot water temperature    |
| a | Delivery | u |       |                | for tempered water draws |
| t | Tem      | m |       |                | (sinks, showers, and     |
| e | perature | b |       |                | baths)                   |
| r | (C)      | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Initial  | n | No    | Setpoint       | Initial temperature of   |
| a | Tem      | u |       | temperature -  | the entire tank (before  |
| t | perature | m |       | 10% of         | initialization routine)  |
| e | (C)      | b |       | deadband       |                          |
| r |          | e |       | temperature    |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Max      | n | No    | None           | Maximum rate of change   |
| a | Setpoint | u |       |                | for setpoint temperature |
| t | Ramp     | m |       |                |                          |
| e | Rate     | b |       |                |                          |
| r | (C/min)  | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Tank     | n | Yes   | Taken from     | Size of water tank, in L |
| a | Volume   | u |       | HPXML file     |                          |
| t | (L)      | m |       |                |                          |
| e |          | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Tank     | n | Yes   | Taken from     | Height of water tank,    |
| a | Height   | u |       | HPXML file     | used to determine        |
| t | (m)      | m |       |                | surface area             |
| e |          | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Heat     | n | Yes   | Taken from     | Heat transfer            |
| a | Transfer | u |       | HPXML file     | coefficient of water     |
| t | Coe      | m |       |                | tank                     |
| e | fficient | b |       |                |                          |
| r | (        | e |       |                |                          |
| H | W/m^2/K) | r |       |                |                          |
| e | or UA    |   |       |                |                          |
| a | (W/K)    |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | hp_o     | b | No    | FALSE          | Disable supplemental     |
| a | nly_mode | o |       |                | heater for HPWH          |
| t |          | o |       |                |                          |
| e |          | l |       |                |                          |
| r |          | e |       |                |                          |
| H |          | a |       |                |                          |
| e |          | n |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH COP | n | Only  |                | Coefficient of           |
| a | (-)      | u | for   |                | Performance for HPWH     |
| t |          | m | Heat  |                |                          |
| e |          | b | Pump  |                |                          |
| r |          | e | Water |                |                          |
| H |          | r | H     |                |                          |
| e |          |   | eater |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH     | n | No    | 500 (for HPWH  | Capacity or rated power  |
| a | Capacity | u |       | Power)         | for HPWH                 |
| t | (W) or   | m |       |                |                          |
| e | HPWH     | b |       |                |                          |
| r | Power    | e |       |                |                          |
| H | (W)      | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH     | n | No    | 1              | Parasitic power for HPWH |
| a | Pa       | u |       |                |                          |
| t | rasitics | m |       |                |                          |
| e | (W)      | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH Fan | n | No    | 35             | Fan power for HPWH       |
| a | Power    | u |       |                |                          |
| t | (W)      | m |       |                |                          |
| e |          | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH SHR | n | No    | 0.88           | Sensible heat ratio for  |
| a | (-)      | u |       |                | HPWH                     |
| t |          | m |       |                |                          |
| e |          | b |       |                |                          |
| r |          | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH     | n | No    | 0.75 if in     | Fraction of HPWH         |
| a | Int      | u |       | Indoor Zone    | sensible gains to        |
| t | eraction | m |       | else 1         | envelope                 |
| e | Factor   | b |       |                |                          |
| r | (-)      | e |       |                |                          |
| H |          | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | HPWH     | n | No    | 0.5            | Fraction of HPWH         |
| a | Wall     | u |       |                | sensible gains to wall   |
| t | Int      | m |       |                | boundary, remainder goes |
| e | eraction | b |       |                | to zone                  |
| r | Factor   | e |       |                |                          |
| H | (-)      | r |       |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | Energy   | n | Only  | Taken from     | Water heater energy      |
| a | Factor   | u | for   | HPXML file     | factor (EF) for getting  |
| t | (-)      | m | Gas   |                | skin loss fraction       |
| e |          | b | Water |                |                          |
| r |          | e | H     |                |                          |
| H |          | r | eater |                |                          |
| e |          |   |       |                |                          |
| a |          |   |       |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+
| W | P        | n | Only  | Taken from     | Parasitic power for Gas  |
| a | arasitic | u | for   | HPXML file     | Tankless Water Heater    |
| t | Power    | m | Gas   |                |                          |
| e | (W)      | b | Tan   |                |                          |
| r |          | e | kless |                |                          |
| H |          | r | Water |                |                          |
| e |          |   | H     |                |                          |
| a |          |   | eater |                |                          |
| t |          |   |       |                |                          |
| i |          |   |       |                |                          |
| n |          |   |       |                |                          |
| g |          |   |       |                |                          |
+---+----------+---+-------+----------------+--------------------------+

Electric Vehicle
~~~~~~~~~~~~~~~~

OCHRE includes an electric vehicle (EV) model. The equipment name can be
“EV” or “Electric Vehicle”. The table below shows the required and
optional equipment-specific arguments for EVs.

+---+------------+-----+----------+------------------+--------------+
| e | **Argument | *   | **Req    | **Default        | **D          |
| n | Name**     | *Ar | uired?** | Value**          | escription** |
| d |            | gum |          |                  |              |
| u |            | ent |          |                  |              |
| s |            | Typ |          |                  |              |
| e |            | e** |          |                  |              |
+===+============+=====+==========+==================+==============+
| E | ve         | str | Yes      | BEV, if taken    | EV vehicle   |
| V | hicle_type | ing |          | from HPXML file  | type,        |
|   |            |     |          |                  | options are  |
|   |            |     |          |                  | "PHEV" or    |
|   |            |     |          |                  | "BEV"        |
+---+------------+-----+----------+------------------+--------------+
| E | char       | str | Yes      | Level 2, if      | EV charging  |
| V | ging_level | ing |          | taken from HPXML | type,        |
|   |            |     |          | file             | options are  |
|   |            |     |          |                  | "Level 1" or |
|   |            |     |          |                  | "Level 2"    |
+---+------------+-----+----------+------------------+--------------+
| E | capacity   | num | Yes      | 100 miles if     | EV battery   |
| V | or mileage | ber |          | HPXML Annual EV  | capacity in  |
|   |            |     |          | Energy < 1500    | kWh or       |
|   |            |     |          | kWh, otherwise   | mileage in   |
|   |            |     |          | 250 miles        | miles        |
+---+------------+-----+----------+------------------+--------------+
| E | enable     | b   | No       | True if          | Allows EV to |
| V | _part_load | ool |          | charging_level = | charge at    |
|   |            | ean |          | Level 2          | partial load |
+---+------------+-----+----------+------------------+--------------+
| E | ambie      | num | No       | Taken from       | Ambient      |
| V | nt_ev_temp | ber |          | schedule, or 20  | temperature  |
|   |            |     |          | C                | used to      |
|   |            |     |          |                  | estimate EV  |
|   |            |     |          |                  | usage per    |
|   |            |     |          |                  | day          |
+---+------------+-----+----------+------------------+--------------+

Battery
~~~~~~~

OCHRE includes a battery model. The table below shows the required and
optional equipment-specific arguments for batteries.

+---+----------+---+------+--------------+----------------------------+
| e | **       | * | *    | **Default    | **Description**            |
| n | Argument | * | *Req | Value**      |                            |
| d | Name**   | A | uire |              |                            |
| u |          | r | d?** |              |                            |
| s |          | g |      |              |                            |
| e |          | u |      |              |                            |
|   |          | m |      |              |                            |
|   |          | e |      |              |                            |
|   |          | n |      |              |                            |
|   |          | t |      |              |                            |
|   |          | T |      |              |                            |
|   |          | y |      |              |                            |
|   |          | p |      |              |                            |
|   |          | e |      |              |                            |
|   |          | * |      |              |                            |
|   |          | * |      |              |                            |
+===+==========+===+======+==============+============================+
| B | capa     | n | No   | 10           | Nominal energy capacity of |
| a | city_kwh | u |      |              | battery, in kWh            |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | capacity | n | No   | 5            | Max power of battery, in   |
| a |          | u |      |              | kW                         |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | ef       | n | No   | 0.98         | Battery Discharging        |
| a | ficiency | u |      |              | Efficiency, unitless       |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | e        | n | No   | 0.98         | Battery Charging           |
| a | fficienc | u |      |              | Efficiency, unitless       |
| t | y_charge | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | eff      | n | No   | 0.97         | Inverter Efficiency,       |
| a | iciency_ | u |      |              | unitless                   |
| t | inverter | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | efficie  | s | No   | "advanced"   | Efficiency calculation     |
| a | ncy_type | t |      |              | option. Options are        |
| t |          | r |      |              | "advanced", "constant",    |
| t |          | i |      |              | "curve", and "quadratic"   |
| e |          | n |      |              |                            |
| r |          | g |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | soc_init | n | No   | 0.5          | Initial State of Charge,   |
| a |          | u |      |              | unitless                   |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | soc_max  | n | No   | 0.95         | Maximum SOC, unitless      |
| a |          | u |      |              |                            |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | soc_min  | n | No   | 0.15         | Minimum SOC, unitless      |
| a |          | u |      |              |                            |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | en       | b | No   | TRUE         | If True, runs an energy    |
| a | able_deg | o |      |              | capacity degradation model |
| t | radation | o |      |              | daily                      |
| t |          | l |      |              |                            |
| e |          | e |      |              |                            |
| r |          | a |      |              |                            |
| y |          | n |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | initial  | n | No   | 50.4         | Initial open circuit       |
| a | _voltage | u |      |              | voltage, in V. Used for    |
| t |          | m |      |              | advanced efficiency and    |
| t |          | b |      |              | degradation models.        |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | v_cell   | n | No   | 3.6          | Cell voltage, in V. Used   |
| a |          | u |      |              | for advanced efficiency    |
| t |          | m |      |              | and degradation models.    |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | ah_cell  | n | No   | 70           | Cell capacity, in Ah. Used |
| a |          | u |      |              | for advanced efficiency    |
| t |          | m |      |              | and degradation models.    |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | r_cell   | n | No   | 0            | Cell resistance, in ohm.   |
| a |          | u |      |              | Used for advanced          |
| t |          | m |      |              | efficiency and degradation |
| t |          | b |      |              | models.                    |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | c        | n | No   | 9            | Schedule: Charge Start     |
| a | harge_st | u |      |              | Time, in hour of day       |
| t | art_hour | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | disc     | n | No   | 16           | Schedule: Discharge Start  |
| a | harge_st | u |      |              | Time, in hour of day       |
| t | art_hour | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | char     | n | No   | 1            | Schedule: Charge Power, in |
| a | ge_power | u |      |              | kW                         |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | dischar  | n | No   | 1            | Schedule: Discharge Power, |
| a | ge_power | u |      |              | in kW                      |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | c        | n | No   | 0            | Self-Consumption: Force    |
| a | harge_fr | u |      |              | Charge from Solar, in      |
| t | om_solar | m |      |              | boolean                    |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | impo     | n | No   | 0            | Self-Consumption: Grid     |
| a | rt_limit | u |      |              | Import Limit, in kW        |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | expo     | n | No   | 0            | Self-Consumption: Grid     |
| a | rt_limit | u |      |              | Export Limit, in kW        |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | enab     | b | No   | True only if | If True, creates 1R-1C     |
| a | le_therm | o |      | zone_name or | thermal model for battery  |
| t | al_model | o |      | envelope is  | temperature. Temperature   |
| t |          | l |      | specified    | is used in degradation     |
| e |          | e |      |              | model                      |
| r |          | a |      |              |                            |
| y |          | n |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | t        | n | No   | 0.5          | Thermal Resistance, in K/W |
| a | hermal_r | u |      |              |                            |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | t        | n | No   | 90000        | Thermal Mass, in J/K       |
| a | hermal_c | u |      |              |                            |
| t |          | m |      |              |                            |
| t |          | b |      |              |                            |
| e |          | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+
| B | Initial  | n | No   | zone         |                            |
| a | Battery  | u |      | temperature  |                            |
| t | Tem      | m |      |              |                            |
| t | perature | b |      |              |                            |
| e | (C)      | e |      |              |                            |
| r |          | r |      |              |                            |
| y |          |   |      |              |                            |
+---+----------+---+------+--------------+----------------------------+

.. _solar-pv-1:

Solar PV
~~~~~~~~

OCHRE includes a solar PV model. The table below shows the required and
optional equipment-specific arguments for PV.

+---+--------+---+--------------+-------------+----------------------+
| e | **Ar   | * | *            | **Default   | **Description**      |
| n | gument | * | *Required?** | Value**     |                      |
| d | Name** | A |              |             |                      |
| u |        | r |              |             |                      |
| s |        | g |              |             |                      |
| e |        | u |              |             |                      |
|   |        | m |              |             |                      |
|   |        | e |              |             |                      |
|   |        | n |              |             |                      |
|   |        | t |              |             |                      |
|   |        | T |              |             |                      |
|   |        | y |              |             |                      |
|   |        | p |              |             |                      |
|   |        | e |              |             |                      |
|   |        | * |              |             |                      |
|   |        | * |              |             |                      |
+===+========+===+==============+=============+======================+
| P | ca     | n | Only if      |             | PV panel capacity,   |
| V | pacity | u | use_sam is   |             | in kW                |
|   |        | m | True         |             |                      |
|   |        | b |              |             |                      |
|   |        | e |              |             |                      |
|   |        | r |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | u      | b | No           | True if     | If True, runs PySAM  |
| V | se_sam | o |              | e           | to generate PV power |
|   |        | o |              | quipment_sc | profile              |
|   |        | l |              | hedule_file |                      |
|   |        | e |              | not         |                      |
|   |        | a |              | specified   |                      |
|   |        | n |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | tilt   | n | No           | Taken from  | Tilt angle from      |
| V |        | u |              | HPXML roof  | horizontal, in       |
|   |        | m |              | pitch       | degrees. Used for    |
|   |        | b |              |             | SAM                  |
|   |        | e |              |             |                      |
|   |        | r |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | orien  | n | No           | Taken from  | Orientation angle    |
| V | tation | u |              | HPXML       | from south, in       |
|   |        | m |              | building    | degrees. Used for    |
|   |        | b |              | orientation | SAM                  |
|   |        | e |              |             |                      |
|   |        | r |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | incl   | b | No           | TRUE        | If True, outputs AC  |
| V | ude_in | o |              |             | power and            |
|   | verter | o |              |             | incorporates         |
|   |        | l |              |             | inverter efficiency  |
|   |        | e |              |             | and power            |
|   |        | a |              |             | constraints          |
|   |        | n |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | i      | n | No           | 1           | Efficiency of the    |
| V | nverte | u |              |             | inverter, unitless   |
|   | r_effi | m |              |             |                      |
|   | ciency | b |              |             |                      |
|   |        | e |              |             |                      |
|   |        | r |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | inver  | s | No           | "Var"       | PV inverter          |
| V | ter_pr | t |              |             | priority. Options    |
|   | iority | r |              |             | are "Var", "Watt",   |
|   |        | i |              |             | or "CPF" (constant   |
|   |        | n |              |             | power factor)        |
|   |        | g |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | inver  | n | No           | PV.capacity | Inverter apparent    |
| V | ter_ca | u |              |             | power capacity, in   |
|   | pacity | m |              |             | kVA (i.e., kW)       |
|   |        | b |              |             |                      |
|   |        | e |              |             |                      |
|   |        | r |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | inv    | n | No           | 0.8         | Inverter minimum     |
| V | erter_ | u |              |             | power factor,        |
|   | min_pf | m |              |             | unitless             |
|   |        | b |              |             |                      |
|   |        | e |              |             |                      |
|   |        | r |              |             |                      |
+---+--------+---+--------------+-------------+----------------------+
| P | sam_   | s | Only if      |             | Weather file in SAM  |
| V | weathe | t | use_sam is   |             | format               |
|   | r_file | r | True and     |             |                      |
|   |        | i | running      |             |                      |
|   |        | n | without a    |             |                      |
|   |        | g | Dwelling     |             |                      |
+---+--------+---+--------------+-------------+----------------------+

Gas Generator
~~~~~~~~~~~~~

OCHRE includes models for the following gas generator equipment:

+-------------------+----------------------+--------------------------+
| End Use           | Equipment Class      | Equipment Name           |
+===================+======================+==========================+
| Gas Generator     | GasGenerator         | Gas Generator            |
+-------------------+----------------------+--------------------------+
| Gas Generator     | GasFuelCell          | Gas Fuel Cell            |
+-------------------+----------------------+--------------------------+

The table below shows the required and optional equipment-specific
arguments for gas generators.

+----+-----------------+--------+---------------+---------------------+
| e  | **Argument      | **Ar   | **Required?** | **Default Value**   |
| nd | Name**          | gument |               |                     |
| u  |                 | Type** |               |                     |
| se |                 |        |               |                     |
+====+=================+========+===============+=====================+
| G  | capacity        | number | No            | 6                   |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | efficiency      | number | No            | 0.95                |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | efficiency_type | string | No            | "curve" if          |
| en |                 |        |               | GasFuelCell,        |
| er |                 |        |               | otherwise           |
| at |                 |        |               | "constant"          |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | control_type    | string | No            | "Off"               |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | ramp_rate       | number | No            | 0.1                 |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | ch              | number | No            | 9                   |
| en | arge_start_hour |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | disch           | number | No            | 16                  |
| en | arge_start_hour |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | charge_power    | number | No            | 1                   |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | discharge_power | number | No            | 1                   |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | import_limit    | number | No            | 0                   |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+
| G  | export_limit    | number | No            | 0                   |
| en |                 |        |               |                     |
| er |                 |        |               |                     |
| at |                 |        |               |                     |
| or |                 |        |               |                     |
+----+-----------------+--------+---------------+---------------------+

Other Equipment
~~~~~~~~~~~~~~~

OCHRE includes basic models for other loads, including appliances,
lighting, and miscellaneous electric and gas loads:

+-------------------+----------------------+--------------------------+
| End Use           | Equipment Class      | Equipment Name           |
+===================+======================+==========================+
| Lighting          | LightingLoad         | Lighting                 |
+-------------------+----------------------+--------------------------+
| Lighting          | LightingLoad         | Exterior Lighting        |
+-------------------+----------------------+--------------------------+
| Lighting          | LightingLoad         | Basement Lighting        |
+-------------------+----------------------+--------------------------+
| Lighting          | LightingLoad         | Garage Lighting          |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Clothes Washer           |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Clothes Dryer            |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Dishwasher               |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Refrigerator             |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Cooking Range            |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | MELs                     |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | TV                       |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Well Pump                |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Gas Grill                |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Gas Fireplace            |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Gas Lighting             |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Pool Pump                |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Pool Heater              |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Hot Tub Pump             |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Hot Tub Heater           |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Ceiling Fan              |
+-------------------+----------------------+--------------------------+
| Other             | ScheduledLoad        | Ventilation Fan          |
+-------------------+----------------------+--------------------------+
| EV                | ScheduledEV          | Scheduled EV             |
+-------------------+----------------------+--------------------------+

The table below shows the required and optional equipment-specific
arguments for other equipment.

+---+------------+-----+---------+--------------+--------------------+
| e | **Argument | *   | **Requ  | **Default    | **Description**    |
| n | Name**     | *Ar | ired?** | Value**      |                    |
| d |            | gum |         |              |                    |
| u |            | ent |         |              |                    |
| s |            | Typ |         |              |                    |
| e |            | e** |         |              |                    |
+===+============+=====+=========+==============+====================+
| O | Convective | num | No      | Taken from   | Fraction of power  |
| t | Gain       | ber |         | HPXML file,  | consumption that   |
| h | Fraction   |     |         | or 0         | is dissipated      |
| e | (-)        |     |         |              | through convection |
| r |            |     |         |              | into zone          |
| / |            |     |         |              |                    |
| L |            |     |         |              |                    |
| i |            |     |         |              |                    |
| g |            |     |         |              |                    |
| h |            |     |         |              |                    |
| t |            |     |         |              |                    |
| i |            |     |         |              |                    |
| n |            |     |         |              |                    |
| g |            |     |         |              |                    |
+---+------------+-----+---------+--------------+--------------------+
| O | Radiative  | num | No      | Taken from   | Fraction of power  |
| t | Gain       | ber |         | HPXML file,  | consumption that   |
| h | Fraction   |     |         | or 0         | is dissipated      |
| e | (-)        |     |         |              | through radiation  |
| r |            |     |         |              | into zone          |
| / |            |     |         |              |                    |
| L |            |     |         |              |                    |
| i |            |     |         |              |                    |
| g |            |     |         |              |                    |
| h |            |     |         |              |                    |
| t |            |     |         |              |                    |
| i |            |     |         |              |                    |
| n |            |     |         |              |                    |
| g |            |     |         |              |                    |
+---+------------+-----+---------+--------------+--------------------+
| O | Latent     | num | No      | Taken from   | Fraction of power  |
| t | Gain       | ber |         | HPXML file,  | consumption that   |
| h | Fraction   |     |         | or 0         | is dissipated as   |
| e | (-)        |     |         |              | latent heat into   |
| r |            |     |         |              | zone               |
| / |            |     |         |              |                    |
| L |            |     |         |              |                    |
| i |            |     |         |              |                    |
| g |            |     |         |              |                    |
| h |            |     |         |              |                    |
| t |            |     |         |              |                    |
| i |            |     |         |              |                    |
| n |            |     |         |              |                    |
| g |            |     |         |              |                    |
+---+------------+-----+---------+--------------+--------------------+

Outputs and Analysis

At the end of any OCHRE simulation, time series outputs are saved. These
time series outputs are used to calculate metrics that describe the
simulation results. The set of time series outputs depends on the
\`verbosity\` of the simulation, and the set of metrics depends on the
\`metrics_verbosity\`. The tables below describe the Dwelling and
Equipment-specific outputs and metrics that are reported.

Dwelling Time Series Outputs
----------------------------

+-----------------------+--------------------+------------------------+
| Time Series Output    | Available if       | Description            |
| Name                  | \`verbosity>=\_\`  |                        |
+=======================+====================+========================+
| Total Electric Power  | 1                  | Total dwelling real    |
| (kW)                  |                    | electric power, in kW  |
+-----------------------+--------------------+------------------------+
| …                     |                    |                        |
+-----------------------+--------------------+------------------------+

Dwelling Metrics
----------------

+-----------------------+--------------------+------------------------+
| Time Series Output    | Available if       | Description            |
| Name                  | \`metri            |                        |
|                       | cs_verbosity>=\_\` |                        |
+=======================+====================+========================+
| Total Electric Energy | 1                  | Total dwelling real    |
| (kWh)                 |                    | electric energy        |
|                       |                    | consumption, in kWh    |
+-----------------------+--------------------+------------------------+
| …                     |                    |                        |
+-----------------------+--------------------+------------------------+

Equipment-Specific Time Series Outputs
--------------------------------------

+--------------+-----------------+----------------+------------------+
| End Use      | Time Series     | Available if   | Description      |
|              | Output Name     | \`v            |                  |
|              |                 | erbosity>=\_\` |                  |
+==============+=================+================+==================+
| HVAC Heating | HVAC Heating    | 2?             | Real electric    |
|              | Electric Power  |                | power from HVAC  |
|              | (kW)            |                | heating          |
|              |                 |                | equipment, in kW |
+--------------+-----------------+----------------+------------------+
|              | …               |                |                  |
+--------------+-----------------+----------------+------------------+

Equipment-Specific Metrics
--------------------------

+-------------+-----------------+-------------------+------------------+
| End Use     | Time Series     | Available if      | Description      |
|             | Output Name     | \`metric          |                  |
|             |                 | s_verbosity>=\_\` |                  |
+=============+=================+===================+==================+
| HVAC        | HVAC Heating    | 2?                | Total electric   |
| Heating     | Electric Energy |                   | energy           |
|             | (kWh)           |                   | consumption from |
|             |                 |                   | HVAC heating     |
|             |                 |                   | equipment, in    |
|             |                 |                   | kWh              |
+-------------+-----------------+-------------------+------------------+
|             | …               |                   |                  |
+-------------+-----------------+-------------------+------------------+

Data Analysis
-------------

The \`Analysis\` module has useful data analysis functions for OCHRE
output data:

\``\`

from ochre import Analysis

# load existing ochre simulation data

df, metrics, df_hourly = Analysis.load_ochre(folder)

# calculate metrics from a pandas DataFrame

metrics = Analysis.calculate_metrics(df)

\``\`

Some analysis functions are useful for analyzing or combining results
from multiple OCHRE simulations:

\``\`

# Combine OCHRE metrics files from multiple simulations (in subfolders
of path)

df_metrics = Analysis.combine_metrics_files(path=path)

# Combine 1 output column from multiple OCHRE simulations into a single
DataFrame

results_files = Analysis.find_files_from_ending(path, ‘ochre.csv’)

df_powers = Analysis.combine_time_series_column(results_files, 'Total
Electric Power (kW)')

\``\`

Data Visualization
------------------

The \`CreateFigures\` module has useful visualization functions for
OCHRE output data:

\``\`

from ochre import Analysis, CreateFigures

df, metrics, df_hourly = Analysis.load_ochre(folder)

# Create standard HVAC output plots

CreateFigures.plot_hvac(df)

# Create stacked plot of power by end use

CreateFigures.plot_power_stack(df)

\``\`

Many functions work on any generic pandas DataFrame with a
DateTimeIndex.

Controller Integration
======================

External Control Signals
------------------------

While OCHRE can simulate a stand-alone dwelling or piece of equipment,
it is designed to integrate with external controllers and other modeling
tools. External controllers can adjust the power consumption of any
OCHRE equipment using multiple control methods.

Below is a simple example that will create a battery model and discharge
it at 5 kW.

\``\`

battery = Battery(capacity_kwh=10, # energy capacity = 10 kWh

capacity=5, # power capacity = 5 kW

soc_init=1, # Initial SOC=100%

start_time=dt.datetime(2018, 1, 1, 0, 0),

time_res=dt.timedelta(minutes=15),

duration=dt.timedelta(days=1),

)

control_signal = {'P Setpoint': -5} # Discharge at 5 kW

status = battery.update(control_signal) # Run for 1 time step with
control signal

\``\`

The following table lists the control signals available to OCHRE
equipment, by end use.

+----------------+----------------+-----------------+-----------------+
| End Uses       | Control Signal | Control Signal  | Description     |
|                | Name           | Type and Units  |                 |
+================+================+=================+=================+
| HVAC Heating,  | Setpoint       | Number, in      | Setpoint        |
| HVAC Cooling,  |                | degrees C       | temperature for |
| or Water       |                |                 | thermostat      |
| Heating        |                |                 | control         |
+----------------+----------------+-----------------+-----------------+
| …              |                |                 |                 |
+----------------+----------------+-----------------+-----------------+

External Model Signals
----------------------

OCHRE can also integrate with external models that modify default
schedule values and other settings.

The most common use case is to integrate with a grid simulator that
modifies the dwelling voltage. OCHRE includes a ZIP model for all
equipment that modifies the real and reactive electric power based on
the grid voltage.

The following code sends a voltage of 0.97 p.u. to a Dwelling model:

\``\`

status = dwelling.update(ext_model_args={‘Voltage (-)’: 0.97})

\``\`

External model signals can also modify any time series schedule values
including weather and occupancy variables. The names and units of these
variables can be found in the header of the schedule output file.
Alternatively, these variables can be reset at the beginning of the
simulation; see notebooks/… for more details.

Status Variables
----------------

The \`update\` function for equipment and dwellings returns a Python
dictionary with status variables that can be sent to the external
controller. These status variables are equivalent to the Time Series
Outputs described in Outputs and Analysis. Note that the \`verbosity\`
applies to the status variables in the same way as the outputs.

Example Use Case – Dwelling
---------------------------

The following code creates a Dwelling model and runs a simulation that
controls the HVAC heating setpoint. For more details and examples, see
bin/run_external_control.py and notebooks/…

Example Use Case – Equipment
----------------------------

The following code creates a water heater model and runs a simulation
that controls the water heater setpoint. For more details and examples,
see bin/run_external_control.py and notebooks/…

.. _co-simulation-1:

Co-simulation
-------------

Multiple OCHRE instances have been run in co-simulation using the HELICS
platform. OCHRE models can communicate with other agents via its
external control signals, external model signals, and status variables.

See the publications list for examples of co-simulation architectures
that use OCHRE. We do not currently have public code for using OCHRE in
co-simulation.

API Reference (automatically generated, low priority)
=====================================================

.. |A picture containing diagram Description automatically generated| image:: media/image1.png
   :width: 4.57271in
   :height: 1.80509in
.. |Diagram, schematic Description automatically generated| image:: media/image2.png
   :width: 2.87476in
   :height: 4.27811in
.. |image1| image:: media/image3.emf
   :width: 4.59037in
   :height: 3.80417in
