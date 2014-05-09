---
layout: default
title: CMSeq
---

~~~
This example is used in the guidelines for developing distributed 
~~~
###CM.vdmpp

{% raw %}
~~~

class CM
instance variables
-- maintain a link to the detector
public static sensor0 : Sensor := new Sensor(detector,0);
public static controller0 : FlareController := new FlareController(0);
public static dispenser0 : FlareDispenser := new FlareDispenser(0);
public static dispenser4 : FlareDispenser := new FlareDispenser(0);
public static dispenser8 : FlareDispenser := new FlareDispenser(0);
end CM

~~~{% endraw %}

###environment.vdmpp

{% raw %}
~~~

class Environment is subclass of GLOBAL
types
public inline  = EventId * MissileType * Angle * Time;
instance variables
-- access to the VDMTools stdio
-- the input file to process
-- the output file to print
-- maintain a link to all sensors
-- information about the latest event that has arrived
busy : bool := true;
operations
public Environment: seq of char ==> Environment
public addSensor: Sensor ==> ()
public Run: () ==> ()
private createSignal: () ==> [EventId]
public handleEvent: EventId * FlareType * Angle * Time * Time ==> ()
public showResult: () ==> ()
public isFinished : () ==> bool
end Environment

~~~{% endraw %}

###flarecontroller.vdmpp

{% raw %}
~~~

class FlareController is subclass of GLOBAL
instance variables
-- the left hand-side of the working angle
-- maintain a link to each dispenser
-- the relevant events to be treated by this controller
-- the status of the controller
operations
public FlareController: Angle ==> FlareController
public addDispenser: FlareDispenser ==> ()
public Step: () ==> ()
-- get the left hand-side start point and opening angle
-- addThreat is a helper operation to modify the event
-- getThreat is a local helper operation to modify the event list
public isFinished: () ==> bool
end FlareController

~~~{% endraw %}

###flaredispenser.vdmpp

{% raw %}
~~~

class FlareDispenser is subclass of GLOBAL
values
responseDB : map MissileType to Plan =
missilePriority : map MissileType to nat =
types
public Plan = seq of PlanStep;
public PlanStep = FlareType * Time;
instance variables
public curplan : Plan := [];
operations
public FlareDispenser: nat ==> FlareDispenser
public Step: () ==> ()
public GetAngle: () ==> nat
public addThreat: EventId * MissileType * Time ==> ()
private releaseFlare: EventId * FlareType * Time * Time ==> ()
public isFinished: () ==> bool
end FlareDispenser

~~~{% endraw %}

###global.vdmpp

{% raw %}
~~~

class GLOBAL
values
public SENSOR_APERTURE = 90;
types
-- there are three different types of missiles
-- there are nine different flare types, three per missile
-- the angle at which the missile is incoming
public EventId = nat;
public Time = nat
operations
public canObserve: Angle * Angle * Angle ==> bool
public getAperture: () ==> Angle * Angle
end GLOBAL

~~~{% endraw %}

###missiledetector.vdmpp

{% raw %}
~~~

class MissileDetector is subclass of GLOBAL
-- the primary task of the MissileDetector is to
instance variables
-- maintain a link to each controller
-- collects the observations from all attached sensors
-- status of the missile detector
operations
-- addController is only used to instantiate the model
public Step: () ==> ()
-- addThreat is a helper operation to modify the event
-- getThreat is a local helper operation to modify the event list
public isFinished: () ==> bool
end MissileDetector

~~~{% endraw %}

###sensor.vdmpp

{% raw %}
~~~

class Sensor is subclass of GLOBAL
instance variables
-- the missile detector this sensor is connected to
-- the left hand-side of the viewing angle of the sensor
operations
public Sensor: MissileDetector * Angle ==> Sensor
-- get the left hand-side start point and opening angle
-- trip is called asynchronously from the environment to
end Sensor

~~~{% endraw %}

###timer.vdmpp

{% raw %}
~~~

class Timer
instance variables
currentTime : nat := 0;
values
stepLength : nat = 10;
operations
private Timer: () ==> Timer
public static GetInstance: () ==> Timer
public StepTime : () ==> ()
public GetTime : () ==> nat
end Timer

~~~{% endraw %}

###world.vdmpp

{% raw %}
~~~

class World
instance variables
-- maintain a link to the environment
operations
public World: () ==> World
   -- add the first controller with four dispensers
   -- add the second controller with four dispensers
   -- add the third controller with four dispensers
-- the run function blocks the user-interface thread
end World

~~~{% endraw %}
