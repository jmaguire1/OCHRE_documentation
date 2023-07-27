Modeling Approach
=================

The overall approach in OCHRE is to try to strike a balance between the computational complexity and model accuracy, using EnergyPlus as a benchmark. OCHRE is designed to be a fully white box model, with inputs fully based on physics and no calibration or tuning of the results. Descriptions of the approach taken to modeling different aspects of the building are detailed below.

Envelope
--------
The envelope uses an RC modeling approach
Figures of RCs
Description of state space approach.

HVAC
----

The following technologies can be modeled in OCHRE:

- Furnace
- Boiler
- Air source heat pump (ASHP)
- Minispit heat pump (MSHP)
- Electric baseboards
- Central air conditioner (AC)
- Room air conditioner

The models vary a bit in their complexity depending on how the technology works. Furnaces and baseboards are modeled as having a constant efficiency equal to the rated efficiency (AFUE for furnaces). Baseboard have an efficiency of 1 by fiat.
Air conditioners and heat pumps are modeled using performance curves. For consistency with other NREL tools, OCHRE takes the same approach as EnergyPlus of using performance curves that affect the efficiency and capacity of the unit as a function of the indoor wet bulb temperature and outdoor dry bulb temperature.

Note that some of the HVAC models available in ResStock and BEopt can not be modeled in OCHRE. This includes PTAC/PTHP systems, combi systems, desuperheaters, and ground source heat pumps. These technologies may be integrated at some point in the future.


Ducts are modeled using the DSE approach specified in `ASHRAE 152 <https://webstore.ansi.org/standards/ashrae/ansiashrae1522004>`_. Sugi, can you fill this in with more details about the implementation?

Water Heating
-------------

The following technologies can be modeled in OCHRE:

- Tank water heater
- Tankless water heater
- Heat pump water heater (HPWH)

OCHRE is able to model the most common water heater technologies in the U.S. For tankless water heaters, a constant efficiency for the water heater is assumed. A 8% derate is applied to the rated efficiency of the tankless water heater to account for cycling losses.

For tank water heaters, there are a couple of options with different levels of complexity depending on the application. The tank can either be modeled as fully mixed (ie a single tank temperature) or use a multinode tank model. The multinode model better captures stratification within the tank

Note that solar water heaters are not currently supported in OCHRE.

Batteries
---------

Electric Vehicles
-----------------

Photovoltaics (PV)
------------------

Other Loads
-----------
