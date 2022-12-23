# nodered-flow-lk-modbus
Node-red flow to interact with LK ICS.2 Room Temperature Control System from LK Systems using modbus and output the result to MQTT for easy integration into Home Assistant.

The flow will scan your ICS.2 system and discover control units and zones and add them in a hiearchy representing your system setup. The ICS.2 system supports up to eight control units with a maximum of eight room thermostats totaling 64 possible zones, or rooms.

By default the flow will add control units, zones and climate controls for each zone to MQTT to be automatically discovered by Home Assistant. You will also get status on you system with a sensor per possible error code in the system. The flow comes with an example of how you can send a notice to a phone if an error occurs.

All entities will have default names but you can easily change name in Home Assistant to make it more user friendly.

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
