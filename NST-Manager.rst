\ |nst\_manager\_icon.png| **NST Manager (Formerly: Nest Manager)**\ 

NST Manager App
===============

 This SmartThings SmartApp is the core of the Nest integration with
SmartThings. The SmartApp and Device Handlers work together to provide
integration to the SmartThings ecosystem using Nest's Official API. This
also includes automations that allow enabling different features. See
`NST Automations Info <NST_Manager#NST_Automations>`__

Features (Coming Soon)
----------------------

Screen Shots
------------

|nm\_mainpage\_1.png| |nm\_mainpage\_2.png|

| 

NST Automations App
===================

**The Available Automations:**

-  *Nest Mode (Home/Away) (built-in, user can choose to enable)*
-  *Thermostat Automations (built-in, user can choose to enable)*
-  *Watchdog Automation (built-in, always enabled)*

There are many Automations built-in to NST Manager. This makes setup and
operations much simpler as the automations are integrated both into NST
Manager, and with each other.

-  *Note*: Multiple SmartApps simultaneously use NST Manager device
   handlers, as the devices handlers comply with SmartThings Device
   Capabilities.
-  **Heads Up**: It is important to consider "who is on first" in
   regards to setting up automations. This includes schedules and
   automations built into Nest itself, as well as SmartThings
   automations.

| 

Nest Mode (Home/Away Automation)
--------------------------------

 |nm\_nestmode\_icon.png| **Automate changes to the Nest location's Home
/ Away setting**

Nest Home/Away can be updated using one of the following:

-  Based on SmartThings Location Mode(s)
-  One or more SmartThings Presence Sensors
-  SmartThings Switch Device(s)

Typically with this automation, configure its options to have it set
thermostats to ECO settings when AWAY, and return to normal operations
when HOME.

Time, ST mode, or HVAC state restrictions can be set to restrict
operations.

| 
| For information on SmartThings Location Modes, some references to
  learn about creating, and managing are:

-  `Welcome FAQ [SmartThings Community
   Page <https://community.smartthings.com/t/jds-welcome-faq/65163>`__]
-  `How to Add a new Mode [SmartThings Community
   Page <https://community.smartthings.com/t/faq-how-to-add-a-new-mode-or-manually-change-from-one-mode-to-another/15530>`__]

| 
| See Nest Home/Away Assist in the Nest Mobile App, or in the Nest Web
  interface https://home.nest.com)

***FYI: Only one instance of a Nest Home/Away automation is allowed per
SmartThings location***

| 

WatchDog Automation
-------------------

|nm\_watchdog\_icon.png| **Monitors configured Nest devices and NST
Manager for errors (This is automatically installed and configured)**

-  The sole function of this automation is send notifications when
   errors or safety settings are reached.

| 

Thermostat Automations
----------------------

|nm\_tstat\_automation\_icon.png| **Allows automation centered around
that particular thermostat with many available features**

This automation has many features that can be individually enabled: (Fan
Control, External Temp, Humidifier Control, Schedules, Remote Sensor,
Contact Watcher, Leak Watcher). If schedules are setup/enabled (Schedule
Automation below), all features that are enabled for this Nest
Thermostat share the schedule set points.

***When Nest location is set to AWAY, and thermostats are set to ECO,
temperature settings cannot be adjusted by SmartThings automations. It
is important that ECO temperature settings are properly setup in each
configured Nest thermostat.***

***NOTICE: Nest thermostats have built-in safety temperatures. These
should be properly set on each thermostats to ensure full protection.***

**NOTICE: There can be one Thermostat Automation per Nest Thermostat
(logically a Zone within the home)** Many builtin features may be
enabled within the Thermostat Automation:

| 

Schedules
~~~~~~~~~

|nm\_sched\_icon.png| **Automate temperature set points and/or HVAC mode
settings based on restrictions by time, ST Modes, motion sensors being
active**

Schedules are not required to be enabled, if enabled the following rules
should be followed:

*NOTE: Currently there can be up to 8 schedules enabled per thermostat
automation. All automations enabled within a thermostat Automation share
the schedules. (Developer can adjust this number remotely as time goes
on)*

-  The schedule precedence is the first schedule that is not restricted
   (i.e. the schedules are evaluated in order 1,2,3,4) and the first
   schedule whose restrictions match current state is set as the
   \*active\* schedule.
-  For a Schedule to become active, it **MUST** always have Temperature
   set-points configured.

   -  (Optionally) it can have:

      -  HVAC mode to set when schedule is active
      -  Restrictions for when schedule can be considered ACTIVE

         -  SmartThings Location Modes
         -  Time of Day
         -  Days of week
         -  Switch is required to be *ON* to make schedule Active.
         -  Switch that makes schedule Inactive

      -  Remote sensors to use when schedule is active (*NOTE: Only if
         the Remote Sensor automation is enabled/configured*)
      -  Motion Sensor to use to override schedule settings to motion
         settings

         -  Motion override settings include HVAC Mode, Temperature
            set-points.

| 
| A Simple Schedule Example:

-  Schedule 1 \| Heat setpoint: 72° \| SmartThings Location Mode(s):
   DAYTIME
-  Schedule 2 \| Heat setpoint: 68° \| SmartThings Location Mode(s):
   NIGHTTIME
-  Schedule 3 \| Heat Setpoint 65°

| 
| The above assumes ST Location Modes DAYTIME, NIGHTTIME (There may be
  more modes defined), and adjusts the thermostat setpoints when the ST
  Mode changes to one of these modes (schedule 1, schedule 2). Some
  Notes:

-  Because the schedules did not fill in HVAC Modes, We will use the
   current HVAC Mode that the thermostat is in at the time the
   automation runs. HVAC mode can be defined in a schedule (for example
   one of HEAT, COOL, or AUTO) to have the automation set that HVAC mode
   then set the temperature setpoints.
-  If the thermostat is OFF when the schedule is evaluated (schedule
   without HVAC mode set in schedule), the HVAC system will stay OFF as
   in the example above the schedules are not configured to change HVAC
   mode. The schedule "will be active", but it will not adjust setpoints
   as the current HVAC mode (OFF) does not allow temp changes.
-  If the HVAC mode is ECO when the schedule is evaluated (or the
   schedule sets the HVAC mode to ECO), the temperature settings of the
   schedule are "ignored", as a Nest thermostat in HVAC mode ECO (like
   OFF), adjustments to the temperature settings cannot be made. If the
   thermostat comes out of ECO mode (for example Nest Mode automation
   above or some other automation or user operation), the schedule would
   be re-evaluated and the temperature settings will take effect.

| 
| In the example above Schedule 3 is the *"catch-all"* schedule, if none
  of the other schedules matched. So if the ST Mode went from DAYTIME ->
  VACATION, or NIGHTTIME -> VACATION, the first two schedules would not
  match. Having a catchall without any time/mode restrictions LAST makes
  it clear that some schedule matches.

-  **NOTICE**: If schedule 3 was first in the list, it would ALWAYS
   match, and the schedule would set the zone to 65 degrees when the
   automation runs. ***SCHEDULE ORDER MATTERS!***

| 
| For more information on SmartThings Location Modes, here are some
  references to learn about creating and managing them:

-  `Welcome FAQ [SmartThings Community
   Page <https://community.smartthings.com/t/jds-welcome-faq/65163>`__]
-  `How to Add a new Mode [SmartThings Community
   Page <https://community.smartthings.com/t/faq-how-to-add-a-new-mode-or-manually-change-from-one-mode-to-another/15530>`__]

| 
| ***NOTE:*** The more advanced schedules will have more parameters
  and/or overrides. Additional settings include motion sensors and
  temperature settings to use if the schedule is active when motion is
  detected. When using Remote Sensor automation (below), there are
  settings to allow adjusting which temperature sensors are used when a
  schedule is active, etc. It is not required to fill in these
  additional parameters unless the automation "plan/desires" requires
  them. The same basic rules apply - first schedule that matches the
  schedule restrictions is the active schedule.

Fan Automations
~~~~~~~~~~~~~~~

|nm\_fan\_ctrl\_icon.png| **Automates Fan Operations**

There are two automations in the Fan Automation:

-  Operate an external Fan while the HVAC system is operating

   -  This automation turns on/off an external fan while the HVAC system
      is operating. This automation can be configured to track certain
      HVAC modes (heat, cool) or track hvac system fan (if HVAC system
      fan is present)

-  Circulate air using the HVAC Fan while the HVAC system is idle

   -  This automation cycles the HVAC system fan on/off at intervals
      while the HVAC system is idle

| Time, ST mode, or HVAC state restrictions can be set to restrict
  operations.

Remote Sensor
~~~~~~~~~~~~~

|nm\_remsen\_icon.png| **Use additional/alternate temperature sensors
for determining a zone's temperature in place of thermostat**

| Remote Sensors are commonly used to deal with temperature differences
  within a thermostat zone that may cause occupants to feel
  uncomfortable. By adding or using different temperature readings
  within the zone, this automation can change HVAC operation to make the
  zone more comfortable. This automation also allows creation larger
  "zones" by joining together different zones.
| Creating a virtual thermostat for the remote sensor automation, makes
  it easier to see and adjust the zone's temperatures via the
  SmartThings mobile application or other SmartApps.
| \* If multiple sensors are in use, they are averaged together to
  determine the new zone temperature

-  Automation schedules can override alternate temperature sensors used
   by Remote Sensor automation to allow for different temperature
   measurements based on schedule.

   -  Example:

      -  During Day use the downstairs temperature sensor
      -  During the evening use the upstairs temperature sensor

-  This automation allows creation of a virtual thermostat in
   SmartThings, to allow users (via SmartThings App) or other
   automations to see and adjust the set points in use on the "remote
   sensor thermostat". This is not required to use the remote sensor,
   but makes it much easier to see the operating settings remote sensor
   is using and integrate with other SmartThings automations.

-  Because the temperature sensor is commonly not the Nest Thermostat
   temperature reading, this automation adjusts the thermostat set point
   higher / lower to force the HVAC system on/off. This can cause
   confusion when one looks at the physical thermostat (or thru the
   native Nest Mobile App or Nest Web access), in that the set points
   can seem artificially high or low both during operation, and off
   times. If one looks at the virtual thermostat settings will appear
   "normal" or "as expected". This is done because the relationship of
   the physical thermostat to the remote sensors in use at this time is
   not "fixed" or "constant". The settings on the physical thermostat
   are "forcing on" or "forcing off" the HVAC system based on the
   automation's temperature measurements.

-  Temperature settings done on the virtual thermostat (either manually,
   or via another SmartApp) override the schedule in NST Manager for 4
   hours, or until the next schedule change - whichever occurs first.

| The temperature setting entered when configuring remote sensor, are
  the "last default" or "last resort" temperature settings that will be
  used if no schedule matches (see Schedules above).
| [Option descriptions/screenshots coming Soon]

Leak Detection
~~~~~~~~~~~~~~

|nm\_leak\_icon.png| **Automates turning off HVAC system if a water
sensor is WET. Commonly used to detect leaks in HVAC system or water in
basement**

-  If any monitored water sensors become WET, the automation will turn
   off the HVAC unit (connected to this thermostat) until all water
   sensors return to a dry state.

[Option descriptions/screenshots coming Soon]

| 

Contact
~~~~~~~

|nm\_conwat\_icon.png| **Automates setting Thermostat to ECO temperature
settings if a door or window contact is left open**

-  If any monitored contact sensors become open, the automation will set
   the HVAC unit to ECO (connected to this thermostat) until all contact
   sensors return to the closed state.

This automation will only return the system from ECO if it set the
system to ECO.

| Time, ST mode, or HVAC state restrictions can be set to restrict
  operations.
| [Option descriptions/screenshots coming Soon]

| 

External Temp
~~~~~~~~~~~~~

|nm\_exttmp\_icon.png| **Automates turning HVAC system to ECO
temperature settings if external and thermostat temperatures match**

This is commonly used to save energy. This automation typically relies
on the Weather device handler be enabled in NST Manager. It can be
configured to use an external temperature sensor installed at the
location (however dewpoint checks will not be available).

This automation does not consider inside temperature, just the desired
setpoint vs outside temperature.

This automation will set the HVAC to ECO (and return from ECO) if:

-  external temperature is lower than desired set point temperature with
   HVAC system set to COOL and external dewpoint is not in uncomfortable
   range
-  external temperature is higher than desired set point temperature
   with HVAC system set to HEAT and external dewpoint is not in
   uncomfortable range
-  external temperature is within low and high set points with HVAC
   system set to AUTO and dewpoint is not in uncomfortable range

This automation will only return the system from ECO if it set the
system to ECO.

| Time, ST mode, or HVAC state restrictions can be set to restrict
  operations.
| [Option descriptions/screenshots coming Soon]

| 

Humidifier Control
~~~~~~~~~~~~~~~~~~

|nst\_humauto\_icon.png| **Automates turning humidifier on/off based on
external temperatures**

| This automation turns a switch on/off to control humidifier(s). It can
  be used with external humidifiers connected to a SmartThings switch,
  or HVAC installed humidifiers if a device handler is available that
  supports SmartThings switch capabilities. See `NST Humidifier
  Info <NST_Manager#nst_humidity>`__
| This calculates the optimal humidity level based on exterior
  temperature.
  http://www.livingwithmyhome.com/201-home-tips/pillar-to-post-central-humidifier.aspx
| This automation typically relies on the Weather device handler be
  enabled in NST Manager. It can be configured to use an external
  temperature sensor installed at the location. This automation will set
  the switch on to call for humidification, and off when humidity level
  is reached/exceeded.

| Time, ST mode, or HVAC state restrictions can be set to restrict
  operations.
| [Option descriptions/screenshots coming Soon]

| 

Device Handlers
===============

Device Handlers are installed via the IDE (see `installation
instructions <NST_Manager#Installation_Instructions>`__ below) and are
created when configuring the NST Manager application. These are the
devices handlers for the physical Nest devices such as thermostat,
protects, camera, and there are virtual device handlers that can be
create for Weather, Presence, and virtual thermostats.

Nest Thermostat
---------------

|nst\_tstat\_v5\_01.png| |nst\_tstat\_v5\_02.png|
|nst\_tstat\_v5\_03.png| |nst\_tstat\_v5\_04.png|
|nst\_tstat\_v5\_05.png| |nst\_tstat\_v5\_06.png|

One thermostat device will be created for each thermostat at a Nest
location.

SmartThings SmartApps can control the following functions with this
device handler:

-  Change Temperature Set Points
-  Change Operating Mode (Off, Eco, Heat, Cool, Auto)
-  Set the Nest location to Home/Away
-  Run the HVAC Fan (*Run time length is determined in the Nest Mobile
   App*)

Each device will contain a graph with history for:

-  Set points (Today)
-  Ambient Temp (Today and Yesterday)
-  Humidity (Today)
-  Thermostat Operating modes (Today)
-  External Temperature (If Weather Device has been enabled) (Today);
   Weather is from WeatherUnderground based on the Hub's location by
   default, and can be set in NST Manager

*This device is compatible with all SmartThings standard `thermostat
capabilities <http://docs.smartthings.com/en/latest/capabilities-reference.html#thermostat>`__*

Device voice reports can be enabled for thermostats, please see
Integrations info below. `3rd Party
Integrations <NST_Manager#3rd_Party_Integrations>`__

| 

Nest Protect
------------

|nst\_prot\_v5\_01.png| |nst\_prot\_v5\_02.png|

One protect device will be created for each protect at a Nest location.

The device contains the following attributes:

-  CO and Smoke Detector for SmartThings *This device handler is
   compatible with all of SmartThings standard `Carbon
   Monoxide <http://docs.smartthings.com/en/latest/capabilities-reference.html#carbon-monoxide-detector>`__
   and `Smoke
   detector <http://docs.smartthings.com/en/latest/capabilities-reference.html#smoke-detector>`__
   capabilities*
-  Battery reporting capabilities to monitor battery status.
-  It can be integrated into Smart Home Monitor (SHM) and can trigger
   alarms based on smoke or CO2 being detected by the Protect.
   (***IMPORTANT: This does not function real-time and may be delayed
   based on ST or Nest cloud operations***)
-  Supports testing in the DTH smoke and CO2 alerts for testing
   automations in SmartThings.

Nest Protects interact with Nest thermostats when smoke or CO2 events
occur. See:
https://nest.com/support/article/Learn-how-Nest-products-work-together

| 

Nest Camera
-----------

|nst\_cam\_v5\_01.png| |nst\_cam\_v5\_02.png| |nst\_cam\_v5\_03.png|
|nst\_cam\_v5\_04.png|

One camera device will be created for each Nest Camera at a Nest
location.

SmartThings SmartApps can view / do the following with Nest Cams:

-  View the Live video stream (*This requires enabling public streaming
   on each camera in the Nest web site https://home.nest.com*)
-  View the still image of the current view
-  Take a snapshot in the device handler and view in the devices
   carousel tile
-  View the last motion event animation
-  Start and Stop camera streaming

| 
| *This device handler is compatible with all of SmartThings standard
  `Image
  Capture <http://docs.smartthings.com/en/latest/capabilities-reference.html#image-capture>`__,
  `sound
  sensor <http://docs.smartthings.com/en/latest/capabilities-reference.html#sound-sensor>`__
  and `Motion
  sensor <http://docs.smartthings.com/en/latest/capabilities-reference.html#motion-sensor>`__
  capabilities*

-  Note sound and motion sensor reports from nest are delayed by Nest
   until after the event has finished

| 

Nest Weather
------------

|nm\_weather\_ss\_1.png| |nm\_weather\_ss\_2.png|
|nm\_weather\_ss\_3.png|

-  This virtual device gathers weather data from Weather Underground and
   provides SmartThings access to this weather data. It can be used by
   External Temperature Sensor automation (below) or Humidifier
   automation to monitor external temperatures and dewpoints.
-  This device will also send local weather alerts via a SmartThings
   push notification (This can be disabled in the NST Manager app)
-  Other applications can use it also, as it is compatible with Smart
   Weather Tile capabilities.

| 

Nest Presence
-------------

.. figure:: nm_nest_pres_ss.png
   :alt: nm_nest_pres_ss.png
   :width: 281px

   nm\_nest\_pres\_ss.png

This device allows provides Nest Locations Home/Away status as a virtual
presence sensor for in any routine or SmartApp that supports the
presence sensor capability.

Nest can automatically update Home/Away with Home Away Assist
https://nest.com/support/article/How-Home-Away-Assist-decides-to-switch-your-home-to-Home-or-Away

*This virtual device is compatible with the SmartThings standard
`presence
sensor <http://docs.smartthings.com/en/latest/capabilities-reference.html#presence-sensor>`__
capabilities*

Nest Virtual Thermostat
-----------------------

|nst\_tstat\_v5\_01.png| |nst\_tstat\_v5\_02.png|
|nst\_tstat\_v5\_03.png| |nst\_tstat\_v5\_04.png|
|nst\_tstat\_v5\_05.png| |nst\_tstat\_v5\_06.png|

-  This device is the same code and has all of the same features as the
   thermostat above. With the exception that it can only be created when
   configuring Remote Sensor automation.
-  The virtual device can be used to provide easy control of the new
   virtual zone that is created by enabling the remote sensor
   automation.

| 

Project Summary
===============

**Authors**

+------------------------+--------------------+
| Name                   | Community Handle   |
+========================+====================+
| **Anthony Santilli**   | @tonesto7          |
+------------------------+--------------------+
| **Eric Schott**        | @E\_Sch            |
+------------------------+--------------------+

**Contributors**

+----------------------------------------+
| @ghesp - Thanks for all your help...   |
+----------------------------------------+
| @desertblade                           |
+----------------------------------------+

**Testers**

+---------------------------------------------------------------+
| @shmookles - Thanks for helping with testing and criticism.   |
+---------------------------------------------------------------+

| 

Version Info
------------

+-------------------+----------------+
| **SmartApps:**    | **Version:**   |
+===================+================+
| NST Manager       | *v5.1.2*       |
+-------------------+----------------+
| NST Automations   | *v5.1.2*       |
+-------------------+----------------+

+----------------+----------------+
| **Devices:**   | **Version:**   |
+================+================+
| Thermostat     | *v5.1.0*       |
+----------------+----------------+
| Protect        | *v5.1.0*       |
+----------------+----------------+
| Presence       | *v5.1.0*       |
+----------------+----------------+
| Weather        | *v5.1.0*       |
+----------------+----------------+
| Camera         | *v5.1.0*       |
+----------------+----------------+

| 

Advantages
----------

-  Support for thermostats, protects, cameras and ability to
   add/control/remove multiples devices from a single SmartApp

   -  Support latest Nest features including ECO mode

-  No need to repeatedly enter device serial number and login info in
   preferences
-  Nest Login info is not stored by the application
-  No need to use 3rd Party Polling apps for device updates

   -  Since there is only a single poll for all devices, updates are
      more often

-  Many built in automations that may be enabled without needing to
   install additional SmartApps
-  One common API and device capabilities for Nest devices; complies
   with SmartThings Device Capabilities
-  The devices look great :smile:

| 

Latest Announcements
--------------------

**Please visit this community page for latest announcements and
features:**

-  **`V5.0.9 Update
   Announcement <https://community.smartthings.com/t/release-nst-manager-v5-0/83228/341>`__**

**BETA Program:**

-  **`V5.x.x BETA
   Information <https://community.smartthings.com/t/beta-nst-manager>`__**

**Previous v5 Release Announcement Posts:**

-  **`V5.0.0 Release
   Announcement <https://community.smartthings.com/t/release-nst-manager-v5-0>`__**

**Previous v4 Release Announcement Posts:**

-  `V4.5 Update
   Announcement <https://community.smartthings.com/t/release-nest-manager-4-0/60052/648>`__
-  `V4.5.1 Update
   Announcement <https://community.smartthings.com/t/release-nest-manager-4-0/60052/691>`__

| 

Reference Links
---------------

-  `GitHub Project Issues
   Link <https://github.com/tonesto7/nest-manager/issues>`__
-  `SmartThings Community Forum
   Link <https://community.smartthings.com/t/release-nst-manager-v5-0/>`__
-  `SmartThings IDE GitHub Integration
   Instructions <http://docs.smartthings.com/en/latest/tools-and-ide/github-integration.html>`__

| 

Things to Know
--------------

Installation
~~~~~~~~~~~~

-  Please ensure **if upgrading, to closely follow the upgrade
   instructions in this document**.
-  When upgrading an installation running versions prior to V4.0 it is
   required to delete all built-in automations prior to upgrade and
   re-create them after the upgrade is complete.
-  Each install of this SmartApp will only support **One**
   location/structure and the Thermostats, Protects and Cameras within
   the Nest structure. If multiple SmartThings Locations are configured,
   NST Manager would be installed in each SmartThings location (if there
   are Nest devices in each location).
-  ''The token used with this application is using my 'Works for Nest'
   distribution *appId* and *secret*. We are currently under review by
   Nest to extend our available tokens.'' **We do not have the ability
   to see any Nest data at the location or who is using the token**
-  In the Nest mobile application, permission updates may need to
   updated for ST NST Manager in the "Works with Nest" section under
   "Account" -> "Works with Nest" -> "ST-Integration", to ensure the
   latest Nest features are integrated with NST Manager.
-  **If in the Nest Mobile app, you see multiple ST-Integration** under
   *Account* -> *Works with Nest*, and you do not have multiple Nest
   Locations, you should delete the all the *ST-Integration* items, and
   then go into the SmartThings Mobile app -> Nest Manager and
   re-authorize Nest Manager.
-  **When logging into the IDE (to install or gather IDE "Live Logging",
   ensure to login to the proper shard. We suggest to use
   http://ide.smartthings.com as it will redirect to the proper shard.
   If NST Manager is installed in the wrong shard, NST Manager will not
   show up in the mobile app as available to be configured.**
-  For folks using Celsius temperature settings, there is an optional
   step to perform during install/upgrade to ensure UIs for the
   thermostat and weather device appear correctly. This is due to a ST
   limitation that background colors and enums cannot be changed after
   compile-time for device handlers.

   -  In the 4.5 and later device handlers for weather and thermostat
      devices, make a change in method compileForC (ensure to save, and
      publish for me):

      -  OLD: def retVal = false // if using C mode, set this to true so
         that enums and colors are correct (due to ST issue of compile
         time evaluation)
      -  NEW: def retVal = true // if using C mode, set this to true so
         that enums and colors are correct (due to ST issue of compile
         time evaluation)

Device Handlers
~~~~~~~~~~~~~~~

-  Devices that use html tile (thermostat, weather) will not refresh the
   HTML portions without going out of the device and back in again when
   in the SmartThings mobile app.
-  Device names can be edited in multiple locations: NST Manager, in the
   device handler settings page, and in the SmartThings IDE. NST Manager
   by default will manage/override these settings. This can be disabled
   in NST Manager Device Customization.

Nest (Eco) Thermostat Mode
~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Nest mode "eco" is interesting in relation to SmartThings and
   SmartApps. SmartThings thermostat capabilities
   http://docs.smartthings.com/en/latest/capabilities-reference.html#thermostat
   only allows off, heat, cool, auto, emergency-heat as settings. So
   when a Nest thermostat is in ECO mode, the thermostat dth will
   display ECO state, but a SmartApp using SmartThings thermostat
   capabilities will see one of heat, cool, auto as the state. This has
   the following things to be aware of:

   -  if using CoRE or other SmartApp that is normalized to ST
      capabilities, there will not be a standard command to set eco
      mode. Create a "custom" or device specific command in CoRE to call
      eco().
   -  If this is done, when setting the thermostat back to auto (or
      heat, cool), CoRE's command optimization will look at the ST view
      of status, and if what is being set is the same, it will not send
      the command to the device to come out of ECO. This can be resolved
      for that piston by setting "Disable Command Optimizations" to ON.
      This ensures CoRE issues the command even if it "thinks" the
      device is in that state.
   -  The thermostat device does support a custom attribute
      "nestThermostatMode" which shows ECO state in addition to the
      standard ST capabilities states.

Nest Protect
~~~~~~~~~~~~

-  Nest protects report battery status binary (good/bad), there will not
   be a gradual battery drop visible (SmartThings reports battery level
   as a percent).

Nest Home/Away
~~~~~~~~~~~~~~

-  Nest home / away has similar interesting effects in relation the
   SmartThings and SmartApps

   -  Nest Thermostats (and Protects (Smoke Detector / CO2 Detector),
      and Cameras) do special things when in away mode (See Nest
      documentation as this regularly changes/improves
      https://nest.com/support/article/Learn-how-Nest-products-work-together)

      -  Key is when in ECO, (and commonly AWAY) mode, temperature
         settings cannot be changed on the thermostat until the
         thermostat is taken out of ECO mode.
      -  A Nest thermostat can be configured to automatically go to ECO
         mode when AWAY, and return to the previous mode when AWAY ends.
         (See Home/Away Assist in the Nest application/website)

   -  Automations (NestMode below) can be configured to control Nest
      home/away based on ST modes, OR
   -  in other SmartApps, create custom commands for home() and
      present() and call these based on automation needs. These commands
      are in the thermostat device, The virtual presence sensor device
      uses the API setPresence() to toggle home/away.

-  Nest Home/Away Assist has been challenging since the changes adding
   ECO mode by Nest. Many users experience the home randomly coming out
   of away mode (and therefore out of ECO mode if home / away assist is
   enabled)
   https://community.smartthings.com/t/removed-nest-manager-4-0/60052/418.
   This issue has been reported to Nest. Some have suggested that Nest
   seems to do this on some Nest schedule changes. NestMode Automation
   (below) can automate setting nest to eco when it sets Nest AWAY, and
   setting back to ON when setting Nest to HOME. If this feature of
   NestMode automation is enabled, consider what other automations are
   also adjusting Nest Home/Away on a thermostat.

Nest API Rate Limits
~~~~~~~~~~~~~~~~~~~~

-  Nest rate limits commands to their APIs based on devices and
   structures. This is done to ensure availability of their services,
   and to not impact the operation of the devices.

   -  Writes (changes of temps or modes) to Nest devices requires the
      device to wake up and synchronize its state. This can impact
      battery life so Nest implemented rate limits.
   -  Nest describes this in:
      https://developer.nest.com/documentation/cloud/data-rate-limits/
   -  How commands work with NST Manager:

      -  It is important when designing automation(s) using Nest, that
         automation(s) do not require more changes than Nest will allow
         in a period of time.
      -  NST Manager for SmartThings implements throttling to keep
         requests within Nest’s rate limits. If commands are received
         for a device that exceeds the Nest rate limits, the NST Manager
         will slow the commands to 1 per minute for the device that is
         over the limit.

   -  Nest may reject commands if the battery state of the Nest device
      is low. If this occurs, Nest will not accept any commands for the
      device.

Other Requests
~~~~~~~~~~~~~~

-  Wanting to use Nest Thermostat or Protect as a SmartThings motion
   sensor:

   -  Nest does not give us any direct access to the status of the
      motion sensor. They only may update home / away - based on Home /
      Away Assist. We cannot see from their API the motion sensor status
      for Thermostats or Protects.
   -  Some motion capabilities are available with the NestCam, however
      Nest reports these \*after\* the event has ended.

-  Want to adjust humidity settings on thermostat

   -  Nest does not give us API access to set humidity. Some folks have
      used old Nest drivers to allow this, not using approved Nest APIs.
      https://github.com/jdc0730/device-type.nest-humidity.

-  Want to use Protect as a siren device in SmartThings

   -  Nest does not provide API access to components of the smoke/CO2
      detector.

-  Better integration of Nest thermostat schedules with NST Manager

   -  Nest API does not give us access to schedule settings / times, so
      we cannot "see them" to use, or modify them.
   -  Related to this is asks for us to be able to "resume" current Nest
      schedule; Nest does not offer a resume command for temperature
      overrides, beyond the next "schedule change time"

| 

3rd-Party SmartApp Compatibility (Confirmed)
--------------------------------------------

NST Manager devices follow SmartThings Thermostat, smoke / CO2 detector,
Camera, Weather device type capabilities. These should work fine with
all SmartApps that support thermostat, smoke detector, camera, or
weather capabilities.

+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------+
| SmartApp                                                                                                                                               | Author           |
+========================================================================================================================================================+==================+
| `CoRE <https://community.smartthings.com/t/beta-milestone-1-core-communitys-own-rules-engine/48189?u=tonesto7>`__                                      | @ady624          |
+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------+
| `Ask Alexa <https://community.smartthings.com/t/release-ask-alexa>`__                                                                                  | @MichaelS        |
+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------+
| `SmartTiles <http://smarttiles.click/>`__                                                                                                              | @625alex         |
+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------+
| `Keenect <https://community.smartthings.com/t/release-keenect-v1-2-0-optional-separate-vo-settings-for-cooling-vent-obstruction-auto-clear/39119>`__   | @Mike\_Maxwell   |
+--------------------------------------------------------------------------------------------------------------------------------------------------------+------------------+

| 

3rd Party Integrations
======================

| 
| \* **`Ask Alexa <Ask_Alexa>`__** by (Michael Struck)

| 

Installation Instructions
=========================

Thanks @MichaelS for letting me borrow from Ask Alexa Install
Instructions...

Community created video walks through the install process (Based on an
older version of Nest Manager):

-  `NST-Manager Install Video
   Walkthrough <https://www.youtube.com/embed/gcmVSmoGQ7c>`__

'''Point a browser to the SmartThings IDE and **Log In**.

*https://ide.smartthings.com should redirect to the proper shard, if not
below are the current shards:*

-  US (New Accounts Since March 2016):
   https://graph-na02-useast1.api.smartthings.com/
-  US: https://graph.smartthings.com or https://ide.smartthings.com
-  Europe: https://graph-eu01-euwest1.api.smartthings.com

| 

Using Git Integration (Recommended)
-----------------------------------

*Enabling the GitHub Integration in the IDE is by far the easiest way to
install and get the latest updates for NST Manager, Automations,
Presence, Protect, Thermostat, and Weather devices.*

To enable Git integration (one time configuration) under the IDE please
visit here for instructions: ***`IDE GitHub Integration
Instructions <http://docs.smartthings.com/en/latest/tools-and-ide/github-integration.html>`__***

**NOTE: Git Integration is not currently available outside of US and
UK**

| 

Installing The Manager and Automation App
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  First, find the **Settings** button at the top of SmartThings IDE
   page (this will only appear after completing the one time integration
   with GitHub)

.. figure:: nm_ide_settings.jpg
   :alt: nm_ide_settings.jpg
   :width: 591px

   nm\_ide\_settings.jpg

-  Clicking this button will open the GitHub Repository Integration
   page.
-  To find the **NST Manager** SmartApp code, enter the information
   below:

**Owner:** tonesto7

**Name:** nest-manager

**Branch:** master

.. figure:: nm_git_integ_ss.png
   :alt: nm_git_integ_ss.png
   :width: 518px

   nm\_git\_integ\_ss.png

-  Close the GitHub Repository Integration page
-  Next, click the **Update from Repo** button at the upper-right corner
   of the IDE
-  Click on **nest-manager (master) from the drop down menu**
-  On the right-hand column labelled New (Only in Github), scroll down
   to click the apps to install. This will typically be:
   ``nest-manager.groovy``

   ``nst-automations.groovy``

-  Check the Publish box and Click the **Execute Update** in the
   bottom-right corner of the screen. When done syncing, the new apps
   should now appear in the IDE. If they ever change color, that
   indicates a new version is available.

| ***REMINDER!!!: Remember to Enable OAuth under the NST Manager's App
  Settings (Instructions Below)***

Installing the Presence, Protect, Thermostat, Camera, and Weather Device Handlers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Go to "**My Device Handlers**" in the IDE
-  Under My Device Handlers Click on ***Update from Repo*** and select
   ***nest-manager*** from the drop-down
-  Check the box next to ***nest-presence***, ***nest-protect***,
   ***nest-thermostat***, ***nest-camera*** and ***nest-weather*** then
   check the **Publish** box and click **Execute Update**

That's it in the IDE... Just install "**NST Manager**" from the
***Marketplace > MyApps*** under the mobile app.

When updates are available to the source code the Link color change from
black in the IDE.

| 

The Manual Way
--------------

| 
| === NST Manager and NST Automations Code Installation ===

The code for the SmartThings SmartApp is found on the GitHub site:

+--------------------+------------------------------------------------------------------------------------------------------------------------+
| **SmartApps:**     | **Source Code URL:**                                                                                                   |
+====================+========================================================================================================================+
| NST Manager:       | *https://github.com/tonesto7/nest-manager/blob/master/smartapps/tonesto7/nest-manager.src/nest-manager.groovy*         |
+--------------------+------------------------------------------------------------------------------------------------------------------------+
| NST Automations:   | *https://github.com/tonesto7/nest-manager/blob/master/smartapps/tonesto7/nst-automations.src/nst-automations.groovy*   |
+--------------------+------------------------------------------------------------------------------------------------------------------------+

-  While on the GitHub site, find the **Raw** button and click it.

.. figure:: nm_git_raw_ss.png
   :alt: nm_git_raw_ss.png
   :width: 1015px

   nm\_git\_raw\_ss.png

-  This will bring up a non-formatted page with just the code present.
-  Click on the text inside window one time then press (***CTRL+A***) on
   the keyboard to select all of the code. (Command A on MacOS
-  Finally press (***CTRL+C***) to copy the code to the clipboard.
   (Command C on MacOS)

**Point a browser to the SmartThings IDE** and **Log In**.

*https://ide.smartthings.com should redirect, if not below are the
current shards:*

-  US (New Accounts Since March 2016):
   https://graph-na02-useast1.api.smartthings.com/
-  US: https://graph.smartthings.com or https://ide.smartthings.com
-  Europe: https://graph-eu01-euwest1.api.smartthings.com

.. figure:: nm_ide_loginscreen.jpg
   :alt: nm_ide_loginscreen.jpg
   :width: 700px

   nm\_ide\_loginscreen.jpg

-  Once logged in, find the **My SmartApps** link on the top of the
   page. Clicking **My SmartApps** will allow creating a new SmartApp.

.. figure:: nm_mysmartapps_ss.png
   :alt: nm_mysmartapps_ss.png
   :width: 700px

   nm\_mysmartapps\_ss.png

-  Find the button on this page labeled **+New SmartApp** and click it.

.. figure:: nm_new_smartapp_btn.png
   :alt: nm_new_smartapp_btn.png

   nm\_new\_smartapp\_btn.png

-  Since the code in the clipboard, find the tab along the top section
   called **From Code**.
-  Click inside the large text box area provided, and paste the code
   copied from GitHub by pressing (***CTRL+V***). (Command V on MacOS)
-  Click **Create** in the bottom left corner of the page.

.. figure:: Nm_newSmartApp_ss.png
   :alt: Nm_newSmartApp_ss.png

   Nm\_newSmartApp\_ss.png

-  This will bring up another page, with the code now formatted within
   the IDE. If the code was copied correctly, there are no other steps
   except to save and publish the code. In the upper right corner of the
   page, find and click **Save**. Now, click **Publish (For Me)**. There
   should receive a confirmation on screen that the code has been
   published successfully.

-  Repeat the steps above for the NST Automations App.

.. figure:: nm_ide_save_publish.png
   :alt: nm_ide_save_publish.png

   nm\_ide\_save\_publish.png

***REMINDER!!!: Remember to Enable OAuth under the NST Manager's App
Settings (Instructions Below)***

Manager and Automation App's Source Code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+--------------------+---------------------------------------------------------------------------------------------------------------------+
| **SmartApp:**      | **Source Code URL:**                                                                                                |
+====================+=====================================================================================================================+
| NST Manager:       | *https://github.com/tonesto7/nest-manager/blob/master/smartapps/tonesto7/nest-manager.src/nest-manager.groovy*      |
+--------------------+---------------------------------------------------------------------------------------------------------------------+
| NST Automations:   | *https://github.com/tonesto7/nest-manager/blob/master/smartapps/tonesto7/nest-manager.src/nst-automations.groovy*   |
+--------------------+---------------------------------------------------------------------------------------------------------------------+

Nest Device Installation
~~~~~~~~~~~~~~~~~~~~~~~~

Just use the same steps as above except click on ***"My Devices"*** and
then ***"+ New Device"*** and copy paste the code for each device listed
below.

-  **FYI:** It is recommended to install all of the device handlers
   below even if all devices are not present / in use - as we check that
   they are present to avoid later configuration issues as new devices
   are added in NST Manager.

Device Source Code
^^^^^^^^^^^^^^^^^^

+--------------------+--------------------------------------------------------------------------------------------------------------------------+
| **Device Type:**   | **Source Code URL:**                                                                                                     |
+====================+==========================================================================================================================+
| Thermostat:        | *https://github.com/tonesto7/nest-manager/blob/master/devicetypes/tonesto7/nest-thermostat.src/nest-thermostat.groovy*   |
+--------------------+--------------------------------------------------------------------------------------------------------------------------+
| Protect:           | *https://github.com/tonesto7/nest-manager/blob/master/devicetypes/tonesto7/nest-protect.src/nest-protect.groovy*         |
+--------------------+--------------------------------------------------------------------------------------------------------------------------+
| Presence:          | *https://github.com/tonesto7/nest-manager/blob/master/devicetypes/tonesto7/nest-presence.src/nest-presence.groovy*       |
+--------------------+--------------------------------------------------------------------------------------------------------------------------+
| Weather:           | *https://github.com/tonesto7/nest-manager/blob/master/devicetypes/tonesto7/nest-weather.src/nest-weather.groovy*         |
+--------------------+--------------------------------------------------------------------------------------------------------------------------+
| Nest Cam:          | *https://github.com/tonesto7/nest-manager/blob/master/devicetypes/tonesto7/nest-camera.src/nest-camera.groovy*           |
+--------------------+--------------------------------------------------------------------------------------------------------------------------+

| 

Enabling OAuth
--------------

**NST Manager** requires OAuth to operate correctly.

**ONLY enable OAuth for NST Manager, DO NOT enable for NST Automations
SmartApp, as that will cause installation failures**

To enable OAuth, In the IDE, "My SmartApps" -> NST Manager" -> find and
click the **App Settings** button in the upper right corner of the page.

From here, find the **OAuth** section toward the bottom of the page.

.. figure:: nm_oauthbtn_ss.png
   :alt: nm_oauthbtn_ss.png

   nm\_oauthbtn\_ss.png

Clicking the **OAuth** link will reveal a button labeled **Enable OAuth
in Smart App**. Click this button. The screen will update giving a
unique code for the **Client ID** and **Client Secret**. These are the
foundations of the security and should be kept secret. This setup is
done once and automatically filled in, it is not required to memorize or
write down these codes.

.. figure:: nm_oauth_pref_ss.jpg
   :alt: nm_oauth_pref_ss.jpg

   nm\_oauth\_pref\_ss.jpg

The final step is to press the **Update** button at the bottom left
corner of the screen, or go back to the code by using the button in the
upper-right region of the page, then **Save**, then **Publish** the
SmartApp again.

.. figure:: nm_ide_save_publish.png
   :alt: nm_ide_save_publish.png

   nm\_ide\_save\_publish.png

Applying Updates to Existing Code
---------------------------------

**OLD RELEASES NOTICE:**

#. Due to changes to our github repo structure for v5.x.x users with
   versions v3.x.x or lower will likely have broken installs.
#. Please DO NOT attempt to update from v3.x.x or lower to v5.x.x.

   -  These upgrades haven't been tested and will not be supported. We
      have seen a few users that did not properly update from V3 to V4
      (this upgrade required automations to be deleted and re-created in
      V4). If earlier updates were not performed properly, the upgrade
      from V4.5.x to V5 will not work.
   -  Please perform a complete uninstall/reinstall

**IMPORTANT NOTE:** The update to version 5.0 requires using the
separated automations file. If there are existing automations it's
imperative to install the new automations file along side the manager
file then update all device handlers. The new manager will begin a
migration process for exist automations which will back them up and
restore them under the new file and remove the old automations. There is
no user interaction required beyond updating the files themselves
properly.

Performing updates using Git Integration is the fastest method of
updating. Just follow the same methods as the install steps above:

#. Click on ***Update from Repo***
#. Select ***nest-manager (master)*** from the dropdown
#. Once the Update from Repo page is shown look under the left column
   titled **Obsolete (updated on GitHub)** check the box(es) next to
   (SmartApp or All of Device Handlers) that show an update.
#. **Please NOTE:** If updating an install from *v4.5.x to v5.0.0* then
   please check the box next to the new **nst-automations.groovy** file
   in the **New (only in GitHub)** box to the right.
#. Once selected the necessary items check the ***publish*** box at the
   bottom right of the page.
#. Click on ***Execute Update***.

*Congratulation's, done in the IDE. The SmartApps and Devices are up to
date.*

**FYI:** These steps must be performed under *My Devices* and *My
SmartApps* respectively in order to update the manager and each of the
device handlers.

**Try to update the code in this order:**

-  All Device Handlers
-  NST Automations SmartApp
-  NST Manager SmartApp

| If Git Integration is not enabled or it's not available in the
  SmartThings region, copy/paste the code from the source links above
  into each app/device and press **Save** then **Publish** for me.

Getting NST Manager Installed and Configured
============================================

-  Open the SmartThings Mobile App:
-  Confirm location is setup correctly

   -  go to three horizontal bars (lower right)
   -  go to select a location, and select settings (gear in upper right)
   -  ensure the location is correct, and hit "Done"

-  Go to "**Marketplace**" and select "**SmartApps**" tab.

   -  Marketplace is the "building", "star" or "sunlight" icon second
      from the right at the bottom of the mobile app

-  Scroll to the bottom of the list, select "**My Apps**"
-  Select "**NST Manager**" from the list.
-  Enter Nest Login credentials when prompted.
-  Choose **Structure**
-  Choose **Thermostats**
-  Choose **Protects**
-  Choose **Cameras**
-  Choose *Add Presence Device* (Optional)
-  Choose *Add Weather Device* (Optional)
-  Tap **"Next"**
-  Review and Modify any preferences (Optional)
-  Tap on "**Done**"

| After initial setup of NST Manager and devices, setup is complete.
  Optionally enable / configure automations in NST Manager or other
  SmartApps.

Manager Preferences
===================

| ***This section is still under construction and will be slowly
  populated as time allows***
| It is important when changing parameters in the ST mobile app to hit
  "Done" for the parameters to take effect. Hitting the back button may
  cause settings to not be properly applied. If you change anything, hit
  "Done" all "the way out".

Notification Preferences
------------------------

Notifications send message(s) when a certain action occurs.

Contact Book
~~~~~~~~~~~~

**The "*Send Notifications to*" input will not be displayed for users
whose accounts do not have contact book enabled. If contact book isn't
available it cannot be enabled in the mobile app until SmartThings
decides to add the toggle feature again. If the Contact book is still
not available, there will be a toggle that will allow sending Push
Messages instead of selecting individual users.**

--------------

Enable Contact-Book Option on SmartThings Account (Safe Hack)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is not the official method and is consider a hack. This should not
cause any harm.

-  Log into the IDE
-  Browse to
   `1 <https://graph.api.smartthings.com/account/list>`__\ (https://graph.api.smartthings.com/account/list)
-  Click on the link for the Name of your account
-  In a web browsers URL bar
   notice\`https://graph.api.smartthings.com/account/show/%My\_Unique\_ID%\`
-  Just replace the \`account/show\` section with \`contact\`
-  So it looks like this
   \`https://graph.api.smartthings.com/contact/%My\_Unique\_ID%\`
-  Select +New Contact or Either of the Import Buttons to proceed.
-  Add one contact to the account for contact book to be enabled. Now
   contacts can be managed from the Mobile App under the Slide out
   settings menu.

--------------

| 

Issues/Troubleshooting
======================

Issues
------

| ***For issues, please let us know by heading over to project's issues
  page on GitHub. If the issue is not reported please help us improve by
  openning a new issue and provide as much detail as possible. IDE logs
  are appreciated.***
| `Submit Your Issues Here [GitHub Issues
  Page <https://github.com/tonesto7/st-nest-unofficial/issues>`__]

Known Issues
------------

-  Device handlers with HTML content won't reload under Android client.
   This issue is being addressed by ST and an issue has been opened with
   the android developer.

| 
| \* SmartThings health status shows device offline. Going into the
  device in the SmartThings mobile app, hit settings (gear is upper
  right) and hit done. This should reset the health status.

Troubleshooting
---------------

| **Tip:** *The most common issue is forgetting to enable oAuth for NST
  Manager SmartApp under SmartThings*
| **Note:** *Do not enable OAuth for the NST Automations Smartapp*
| **Tip:** *The next common issue is not installing in the proper
  SmartThings Shard*
| If you are experiencing issues start by performing the following:

-  Verify the software is the most current SmartApp and Device handler
   code .
-  Review installation and configuration instructions for items that may
   not have been followed.
-  Take a look at the IDE logs to see any warning or error messages:

   -  This is done by going to the "Live Logging" tab in the IDE, and
      leave that window open for a few minutes
   -  Try to perform actions with the Nest devices in the SmartThings
      Mobile app (NST Manager, or another SmartApp), and look out for
      any warnings and/or error messages.

| ***NOTE:*** If you see 401 status errors in the IDE logs, these are
  authentication issues; revoke and re-enable the Nest Token in the NST
  Manager App.

FAQ (Frequently Asked Questions)
--------------------------------

| This section obviously needs some work. Feel free to help make this
  better

Feature Requests
================

-  We love new ideas so please head on over to GitHub and open an issue
   for the feature. This will help prioritize what is important and what
   is not.
-  There is a feedback mechanism built into the NST Manager App under
   *Help, Info, Instructions and More*

| Do read `Other Requests <NST_Manager#Other_Requests>`__ section above

Donations
=========

-  While donations are not required they are very much appreciated.
-  Here is donation link ***`donation
   link <https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=2CJEVN439EAWS>`__***

.. figure:: nm_donation_qr_img.png
   :alt: nm_donation_qr_img.png
   :width: 150px

   nm\_donation\_qr\_img.png

| 

`Category:Unpublished SmartApps <Category:Unpublished_SmartApps>`__

.. |nst\_manager\_icon.png| image:: nst_manager_icon.png
   :width: 120px
.. |nm\_mainpage\_1.png| image:: nm_mainpage_1.png
   :width: 281px
.. |nm\_mainpage\_2.png| image:: nm_mainpage_2.png
   :width: 281px
.. |nm\_nestmode\_icon.png| image:: nm_nestmode_icon.png
   :width: 80px
.. |nm\_watchdog\_icon.png| image:: nm_watchdog_icon.png
   :width: 80px
.. |nm\_tstat\_automation\_icon.png| image:: nm_tstat_automation_icon.png
   :width: 80px
.. |nm\_sched\_icon.png| image:: nm_sched_icon.png
   :width: 80px
.. |nm\_fan\_ctrl\_icon.png| image:: nm_fan_ctrl_icon.png
   :width: 80px
.. |nm\_remsen\_icon.png| image:: nm_remsen_icon.png
   :width: 80px
.. |nm\_leak\_icon.png| image:: nm_leak_icon.png
   :width: 80px
.. |nm\_conwat\_icon.png| image:: nm_conwat_icon.png
   :width: 80px
.. |nm\_exttmp\_icon.png| image:: nm_exttmp_icon.png
   :width: 80px
.. |nst\_humauto\_icon.png| image:: nst_humauto_icon.png
   :width: 80px
.. |nst\_tstat\_v5\_01.png| image:: nst_tstat_v5_01.png
   :width: 281px
.. |nst\_tstat\_v5\_02.png| image:: nst_tstat_v5_02.png
   :width: 281px
.. |nst\_tstat\_v5\_03.png| image:: nst_tstat_v5_03.png
   :width: 281px
.. |nst\_tstat\_v5\_04.png| image:: nst_tstat_v5_04.png
   :width: 281px
.. |nst\_tstat\_v5\_05.png| image:: nst_tstat_v5_05.png
   :width: 281px
.. |nst\_tstat\_v5\_06.png| image:: nst_tstat_v5_06.png
   :width: 281px
.. |nst\_prot\_v5\_01.png| image:: nst_prot_v5_01.png
   :width: 281px
.. |nst\_prot\_v5\_02.png| image:: nst_prot_v5_02.png
   :width: 281px
.. |nst\_cam\_v5\_01.png| image:: nst_cam_v5_01.png
   :width: 281px
.. |nst\_cam\_v5\_02.png| image:: nst_cam_v5_02.png
   :width: 281px
.. |nst\_cam\_v5\_03.png| image:: nst_cam_v5_03.png
   :width: 281px
.. |nst\_cam\_v5\_04.png| image:: nst_cam_v5_04.png
   :width: 281px
.. |nm\_weather\_ss\_1.png| image:: nm_weather_ss_1.png
   :width: 281px
.. |nm\_weather\_ss\_2.png| image:: nm_weather_ss_2.png
   :width: 281px
.. |nm\_weather\_ss\_3.png| image:: nm_weather_ss_3.png
   :width: 281px