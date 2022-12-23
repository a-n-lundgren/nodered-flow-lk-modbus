# nodered-flow-lk-modbus
Node-red flow to interact with LK ICS.2 Room Temperature Control System from LK Systems using Modbus RS485/RTU and output the result to MQTT for easy integration into Home Assistant.

The flow will scan your ICS.2 system and discover control units and zones and add them in a hiearchy representing your system setup. The ICS.2 system supports up to eight control units with a maximum of eight room thermostats totaling 64 possible zones, or rooms.

By default the flow will add control units, zones and climate controls for each zone to MQTT to be automatically discovered by Home Assistant. You will also get status on you system with a sensor per possible error code in the system. The flow comes with an example of how you can send a notice to a phone if an error occurs.

All entities will have default names but you can easily change name in Home Assistant to make it more user friendly. If you have multiple control units connected the first control unit is named Section 1 and will contain Zones 1-8 and Actuators 1-8. The second section will contain Zones 9-16, Actuators 9-16 and so on.

The hierarcy that you will get in Home Assistant looks like this:
 * Section 1
   * Climate Control entities for defined zones with current temperature, temperature setpoint, heating status and possibility to change the temperature
   * Error status sensors
   * Actuator 1
     * Error status sensors
   * Actuator 2
   * Actuator N
   * Zone 1 (Room sensor)
     * Error status sensors
     * Battery status
     * Floor target temperature
     * Floor temperature
     * Heating status
     * Link quality
     * Preset mode
     * Regulation output
     * Room target temperature
     * Room temperature
   * Zone 2
   * Zone N
 * Section 2
 * Section N

## Known bugs and limitations
These are known bugs and limitations currently in this project.
 * Climate controls in Home Assistant will use room temperature and room temperature setpoint and not floor temperature and floor temperature setpoint by the simple fact that I do not have access to a system that uses floor sensors.
 * Actuator to zone mapping is missing. The data is there but the mapping is not performed as of today.
 * Presets is not enabled in climate controls yet, had some problems getting it to work properly and will take a look at it later on.
 * All control units are assumed to have 8 zones, the smaller units are not currently supported
