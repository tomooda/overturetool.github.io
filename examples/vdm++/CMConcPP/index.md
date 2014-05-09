---
layout: default
title: CMConc
---

~~~
This example is used in the guidelines for developing distributed 
~~~
###BaseThread.vdmpp

{% raw %}
~~~
class BaseThread
types
public static ThreadDef ::
instance variables
protected period : nat1 := 1;
protected registeredSelf : BaseThread;
operations
protected BaseThread : BaseThread ==> BaseThread
Step : () ==> ()
thread
 (if isPeriodic
end BaseThread
~~~{% endraw %}

###environment.vdmpp

{% raw %}
~~~

class Environment is subclass of GLOBAL, BaseThread
types
public InputTP   = (Time * seq of inline);
public inline  = EventId * MissileType * Angle * Time;
instance variables
-- access to the VDMTools stdio
-- the input file to process
-- the output file to print
-- maintain a link to all sensors
busy : bool := true;
-- Amount of time we want to simulate
operations
public Environment: seq of char * [ThreadDef] ==> Environment
  if tDef <> nil
public addSensor: Sensor ==> ()
private createSignal: () ==> () 
public handleEvent: EventId * FlareType * Angle * Time * Time ==> ()
public showResult: () ==> ()
public isFinished : () ==> ()
public Step : () ==> ()
sync
mutex (handleEvent);
end Environment

~~~{% endraw %}

###fighteraircraft.vdmpp

{% raw %}
~~~

class CM
instance variables
  -- maintain a link to the detector
  public static sensor0 : Sensor := new Sensor(detector,0);
  public static controller0 : FlareController := new FlareController(0, nil);
  public static dispenser0 : FlareDispenser := new FlareDispenser(0, nil);
  public static dispenser4 : FlareDispenser := new FlareDispenser(0, nil);
  public static dispenser8 : FlareDispenser := new FlareDispenser(0, nil);
end CM

~~~{% endraw %}

###flarecontroller.vdmpp

{% raw %}
~~~

class FlareController is subclass of GLOBAL, BaseThread
instance variables
-- the left hand-side of the working angle
-- maintain a link to each dispenser
-- the relevant events to be treated by this controller
-- the status of the controller
operations
public FlareController: Angle * [ThreadDef] ==> FlareController
  if tDef <> nil
public addDispenser: FlareDispenser ==> ()
-- get the left hand-side start point and opening angle
-- addThreat is a helper operation to modify the event
-- getThreat is a local helper operation to modify the event list
public isFinished: () ==> ()
Step: () ==> ()
sync
-- addThreat and getThreat modify the same instance variables
-- getThreat is used as a 'blocking read' from the main
end FlareController

~~~{% endraw %}

###flaredispenser.vdmpp

{% raw %}
~~~

class FlareDispenser is subclass of GLOBAL, BaseThread
values
responseDB : map MissileType to Plan =
missilePriority : map MissileType to nat =
types
public Plan = seq of PlanStep;
public PlanStep = FlareType * Time;
instance variables
public curplan : Plan := [];
operations
public FlareDispenser: Angle * [ThreadDef] ==> FlareDispenser
  if tDef <> nil
public GetAngle: () ==> nat
public addThreat: EventId * MissileType * Time ==> ()
private Step: () ==> ()
private releaseFlare: EventId * FlareType * Time * Time ==> ()
public isFinished: () ==> ()

sync
mutex (Step);
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
public Time = nat;
operations
public canObserve: Angle * Angle * Angle ==> bool
end GLOBAL

~~~{% endraw %}

###missiledetector.vdmpp

{% raw %}
~~~

class MissileDetector is subclass of GLOBAL, BaseThread
-- the primary task of the MissileDetector is to
instance variables
-- maintain a link to each controller
-- collects the observations from all attached sensors
-- status of the missile detector
operations
public MissileDetector: [ThreadDef] ==> MissileDetector
-- addController is only used to instantiate the model
-- addThreat is a helper operation to modify the event
-- getThreat is a local helper operation to modify the event list
public isFinished: () ==> ()
Step: () ==> ()
sync
mutex (Step);
-- addThreat and getThreat modify the same instance variables
-- getThreat is used as a 'blocking read' from the main

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

###TimeStamp.vdmpp

{% raw %}
~~~

class TimeStamp
values
public stepLength : nat = 1;
instance variables
currentTime  : nat   := 0;
operations
-- private constructor (singleton pattern)
-- public operation to get the singleton instance
public RegisterThread : BaseThread ==> ()
public UnRegisterThread : BaseThread ==> ()
public IsInitialising: () ==> bool
public DoneInitialising: () ==> ()
public WaitRelative : nat ==> ()
public WaitAbsolute : nat ==> ()
BarrierReached : () ==> ()
AddToWakeUpMap : nat * [nat] ==> ()
public NotifyThread : nat ==> ()
public GetTime : () ==> nat
Awake: () ==> ()
public ThreadDone : () ==> ()
sync
  mutex (IsInitialising);
  mutex (AddToWakeUpMap);
  mutex (AddToWakeUpMap, NotifyThread);
  mutex (AddToWakeUpMap, NotifyThread, BarrierReached);
end TimeStamp
~~~{% endraw %}

###world.vdmpp

{% raw %}
~~~

class World
instance variables
public static timerRef : TimeStamp := TimeStamp`GetInstance();
operations
public World: () ==> World
   env.addSensor(CM`sensor0);
   -- add the first controller with four dispensers
   -- add the second controller with four dispensers
   -- add the third controller with four dispensers
-- the run function blocks the user-interface thread
end World

~~~{% endraw %}
