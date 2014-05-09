---
layout: default
title: Tracker
---

~~~
The tracker example is used in the mapping chapter of the VDM-SL
J.S. Fitzgerald and C.B. Jones, Proof in VDM: Case Studies, 
~~~
###testtracker.vdmsl

{% raw %}
~~~
values
glass = mk_token("Glass");
liquid = mk_token("liquid");
metal = mk_token("metal");
plastic = mk_token("plastic");
all_material = {glass,liquid,metal,plastic};
unpacking_inital = mk_Phase({},all_material,5);
sorting_inital = mk_Phase({},all_material,6);
assay_inital = mk_Phase({},all_material,5);
compaction_inital = mk_Phase({},{glass,metal,plastic},3);
storage_inital = mk_Phase({},{glass,metal,plastic},50);
coninfo_inital = {|->};
cid1 : ContainerId = mk_token(42);
phases_inital = {mk_token("Unpacking") |-> unpacking_inital,
tracker_inital = mk_Tracker(coninfo_inital,phases_inital)
functions
SetUp: () -> Tracker

~~~{% endraw %}

###tracker.vdmsl

{% raw %}
~~~
types
Tracker :: containers : ContainerInfo
ContainerInfo = map ContainerId to Container;
PhaseInfo = map PhaseId to Phase;
Container :: fiss_mass : real
Phase :: contents          : set of ContainerId
ContainerId = token;
PhaseId = token;
Material = token
functions

-- introduce a new container to the plant (map union)
  Introduce : Tracker * ContainerId * real * Material -> Tracker
-- permission to move (simple Boolean function)
Permission: Tracker * ContainerId * PhaseId  ->  bool
-- Remove a container from the contents of a phase
Remove: Tracker * ContainerId * PhaseId -> Tracker
-- move a known container between two phases
Move: Tracker * ContainerId * PhaseId * PhaseId -> Tracker
-- delete a container from the plant
Delete: Tracker * ContainerId * PhaseId  ->  Tracker
-- Auxiliary functions defined for inv-Tracker
  PhasesDistinguished: PhaseInfo -> bool
  MaterialSafe: ContainerInfo * PhaseInfo -> bool

~~~{% endraw %}
