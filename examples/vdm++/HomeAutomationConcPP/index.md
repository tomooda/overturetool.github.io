---
layout: default
title: HomeAutomationConc
---

~~~

#******************************************************
~~~
###Actuator.vdmpp

{% raw %}
~~~
class Actuator
instance variables
protected ID   : nat;
operations
public GetID: () ==> nat
public GetType: () ==> NetworkTypes`nodeType
protected GetCorr: () ==> NetworkTypes`correction
end Actuator
~~~{% endraw %}

###BaseThread.vdmpp

{% raw %}
~~~
class BaseThread
instance variables
protected period : nat1 := 1;
operations
protected BaseThread : () ==> BaseThread
Step : () ==> ()
thread
end BaseThread
~~~{% endraw %}

###Environment.vdmpp

{% raw %}
~~~
class Environment is subclass of BaseThread
instance variables
--private ha       : HA;
private finished : bool := false;
types
-- Input file: Temp, Humid, Time
operations
public Environment: seq of char * nat1 * bool ==> Environment
  def mk_ (-,mk_(t,input)) = io.freadval[nat * seq of inline](fname) 
private CreateSignal: () ==> ()
public IsFinished: () ==> ()
public Finish: () ==> ()
Step: () ==> ()
sync
  per IsFinished => finished;
--thread
--    World`timerRef.WaitRelative(1);
end Environment
~~~{% endraw %}

###HomeAutomation.vdmpp

{% raw %}
~~~

class HA
instance variables
public static Sur		: Surroundings := new Surroundings();
end HA
~~~{% endraw %}

###HostController.vdmpp

{% raw %}
~~~

class HostController is subclass of BaseThread
instance variables
private finished    : bool := false;
private TargetTemp  : nat;
private NodeList    : map nat to NetworkTypes`nodeType := { |-> };

types   
private algType	= <THTW> | <TTW> | <TT> | <TW> | <HW> | <NONE>;

operations
public HostController: nat * nat * nat1 * bool ==> HostController
private UpdateValues: () ==> ()
private Algorithm: () ==> ()
private THTWAlgo: () ==> ()
private TTWAlgo: () ==> ()
private TTAlgo: () ==> ()
private TWAlgo: () ==> ()
private HWAlgo: () ==> ()
private UpdateAlgorithm: () ==> ()
private printStr: seq of char ==> ()
public AddNode: nat * NetworkTypes`nodeType ==> ()
public RemoveNode: nat * NetworkTypes`nodeType ==> ()
public IsFinished: () ==> ()
public Finish: () ==> ()
Step: () ==> ()
sync
per IsFinished => finished;

--thread
end HostController
~~~{% endraw %}

###HumidSensor.vdmpp

{% raw %}
~~~
class HumidSensor is subclass of Sensor, BaseThread
instance variables
finished	: bool := false;
operations
public HumidSensor: nat * NetworkTypes`nodeType * nat * Surroundings * nat1 * bool ==> HumidSensor
public Finish: () ==> ()
public IsFinished: () ==> ()
Step: () ==> ()
sync
  per IsFinished => finished;
--thread
--  while true 
end HumidSensor
~~~{% endraw %}

###NetworkTypes.vdmpp

{% raw %}
~~~
class NetworkTypes
types   
public nodeType   = <TEMPSENSOR> | <HUMIDSENSOR> | <WINDOW> | <THERMOSTAT> | <HOSTCONTROL> | <NONE>;
end NetworkTypes
~~~{% endraw %}

###Sensor.vdmpp

{% raw %}
~~~
class Sensor
instance variables
protected ID	: nat;
operations
public GetID: () ==> nat
public GetType: () ==> NetworkTypes`nodeType
public ReadValue: () ==> nat
end Sensor
~~~{% endraw %}

###Surroundings.vdmpp

{% raw %}
~~~
class Surroundings
instance variables
private envTemp	 : nat;
operations
public Surroundings: () ==> Surroundings
public SetTemp: nat ==> ()
public SetHumid: nat ==> ()
public ReadTemp: () ==> nat
public IncTemp: () ==> ()
public DecTemp: () ==> ()
public ReadHumid: () ==> nat
public IncHumid: () ==> ()
public DecHumid: () ==> ()
sync
  mutex(IncTemp);
end Surroundings
~~~{% endraw %}

###TemperatureSensor.vdmpp

{% raw %}
~~~
class TemperatureSensor is subclass of Sensor, BaseThread
instance variables
finished	: bool := false;
operations
public TemperatureSensor: nat * NetworkTypes`nodeType * nat * Surroundings * nat1 * bool ==> TemperatureSensor
public Finish: () ==> ()
public IsFinished: () ==> ()
Step: () ==> ()
sync
  per IsFinished => finished;
--thread
--  while true 
end TemperatureSensor
~~~{% endraw %}

###Thermostat.vdmpp

{% raw %}
~~~

class Thermostat is subclass of Actuator, BaseThread
instance variables
finished	: bool := false;

operations
public Thermostat: nat * NetworkTypes`nodeType * Surroundings * nat1 * bool ==> Thermostat
public SetCorrection: NetworkTypes`correction ==> ()
public Finish: () ==> ()
public IsFinished: () ==> ()
Step: () ==> ()
  if tempCorr = <INC>
sync
  per IsFinished => finished;
--thread
--  while true 
--    if tempCorr = <INC>
--    World`timerRef.WaitRelative(5);--World`timerRef.stepLength);
end Thermostat
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
public TimeStamp : nat ==> TimeStamp
public RegisterThread : BaseThread ==> ()
public UnRegisterThread : () ==> ()
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
mutex(IsInitialising);
  mutex(AddToWakeUpMap, NotifyThread);
  mutex(AddToWakeUpMap, NotifyThread, BarrierReached);
end TimeStamp
~~~{% endraw %}

###Window.vdmpp

{% raw %}
~~~
class Window is subclass of Actuator, BaseThread
instance variables
finished	: bool := false;
operations
public Window: nat * NetworkTypes`nodeType * Surroundings * nat1 * bool ==> Window
public SetCorrection: NetworkTypes`correction ==> ()
public Finish: () ==> ()
public IsFinished: () ==> ()
Step: () ==> ()
sync
  per IsFinished => finished;
--thread
--  while true 
end Window
~~~{% endraw %}

###World.vdmpp

{% raw %}
~~~
class World
instance variables
private env				: Environment;
operations
public World: () ==> World
  ha.Host.AddNode(ha.TempNode.GetID(), ha.TempNode.GetType());
  -- End the initialisation phase of system threads
public Run: () ==> ()
end World
~~~{% endraw %}
