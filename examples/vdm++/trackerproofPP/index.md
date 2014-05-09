---
layout: default
title: trackerproof
---

~~~

This VDM++ model is a direct transformation from the 
#******************************************************
~~~
###tracker.vdmpp

{% raw %}
~~~
class TRACKER
types
 public Tracker :: containers : ContainerInfo
 public ContainerInfo = map ContainerId to Container;
 public PhaseInfo = map PhaseId to Phase;
 public Container :: fiss_mass : real
 public Phase :: contents           : set of ContainerId
 public ContainerId = token;
 public PhaseId = token;
 public Material = token
functions
  -- introduce a new container to the plant (map union)
  Introduce : Tracker * ContainerId * real * Material -> Tracker
  -- permission to move (simple Boolean function)
  Permission: Tracker * ContainerId * PhaseId  ->  bool
  -- move a known container between two phases
  Move : Tracker * ContainerId * PhaseId * PhaseId -> Tracker
  -- remove a container from the contents of a phase
  Remove: Tracker * ContainerId * PhaseId -> Tracker
  -- delete a container from the plant
  Delete: Tracker * ContainerId * PhaseId  ->  Tracker
  -- Auxiliary functions defined for inv-Tracker
Consistent: ContainerInfo * PhaseInfo -> bool
  PhasesDistinguished: PhaseInfo -> bool
 MaterialSafe: ContainerInfo * PhaseInfo -> bool

end TRACKER
~~~{% endraw %}
