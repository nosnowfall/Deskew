# Deskew Accesory Info
This project comes from my research in HF/MHz switch-mode power and radio amplifiers, and my lab losing their only OEM deskew fixture. The design is copied from an [EEVblog forum post](https://www.eevblog.com/forum/testgear/scope-probe-deskew-fixture-pcb-project/), specifically the board made by Ribster.

## Background
The goal is to synchonronize propagation delays between different probes to get sensible readings or a good V*I power measurement. For example, uncorrected passive probes are ~15ns faster than Teledyne LeCroy CP031A current probes. The idea of the fixture is to generate in-phase voltage and current pulses with fast rise time, so the user can manually synchronize the probes.

## Design
To prevent any effects of current-measurement coil inductance, the voltage is measured on the low side of the coil across burden resistors with a low-inductance return path. Deskew fixtures use a second current path switched with a fast transistor to avoid any ringing or inductive turn-off effects in the measurement side. The transistor must have Rds(on) much lower than the burden resistance to prevent significant residual current in the measurement path during the off pulse. Clock frequency is not terribly important so long as rise time is high and ~50% duty cycle can be maintained. 

The default clock on this board is ~100kHz from a 555-style timer. Version A accepted alternate clocks through an SMA connector, but this was removed in version B. The clock is buffered by a MCP1415 driver to the MOSFET, a BSS214NW with 0.7nC gate charge and <140mOhm Rds(on). 

The upper resistors and burden resistance are both 20 Ohm (from 5 x 100 Ohm, for power rating), yielding a convenient 125mA measurement current step at 5Vdc. For probes with lower sensitivity, multiple loops of wire between the high and low coil terminals may artificially increase the sensed current. A direct SMA output for voltage sense is provided, but be aware that using 50 Ohm input on a scope will change behavior significantly. 

The accessory derives power either from a 5V USB or DC power supply, drawing ~1 W on average (1.25 W max, during transistor on time).

## Sourcing, DIY, etc.
Full schematics, layout, fab files, and BOM will be available once the design is finalized.
