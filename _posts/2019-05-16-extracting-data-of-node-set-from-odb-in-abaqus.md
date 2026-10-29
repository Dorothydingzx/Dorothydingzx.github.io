---
title: "Extracting data of node set from odb in ABAQUS"
date: 2019-05-16 11:33:08
categories:
- "ABAQUS"
redirect_from:
- /archives/ghj43h.html
---

I want to extract reaction force and displacement of a certain point, which is a reference point established in INTERACTION module and set as a geometry set named ‘SET-3’. The error information will pop up when using the codes I often use, as ‘KeyError: SET-3’, which can be seen in the second code part.

<!-- more -->

I searched the [Abaqus Scripting Reference Guide](http://ivt-abaqusdoc.ivt.ntnu.no:2080/v6.14/books/ker/default.htm) for ode objects (34.23), the methods to use node sets from Part, Assembly and Instance modules are listed below.

```python
session.odbs[name].parts[name].NodeSet                   
session.odbs[name].rootAssembly.instances[name].NodeSet                   
session.odbs[name].rootAssembly.NodeSet
```

To eliminate the effect of coupling, I established another two node sets, ‘SET-4’ and ‘SET-5’, in Assembly module, and used ‘SET-4’ to establish another coupling. The model was re-analyzed and the information was printed as follows.

```python
>>> odbname
'10fixed-pin-elastic-L100-sine-u-v.odb'
>>> session.odbs[odbname].rootAssembly.nodeSets
session.openOdb(r'D:/Temp/10fixed-pin-elastic-L100-sine-u-v.odb').rootAssembly.nodeSets
# print the node sets in odb assembly
>>> print session.odbs[odbname].rootAssembly.nodeSets
{' ALL NODES': 'OdbSet object', 'SET-1': 'OdbSet object', 'SET-2': 'OdbSet object'}
>>> print session.odbs['10fixed-pin-elastic-L-100-sine-u-v.odb'].rootAssembly.nodeSets
{' ALL NODES': 'OdbSet object', 'ASSEMBLY_CONSTRAINT-2_REFERENCE_POINT': 'OdbSet object', 'ASSEMBLY_COUPLING-1_REFERENCE_POINT': 'OdbSet object', 'SET-1': 'OdbSet object', 'SET-2': 'OdbSet object', 'SET-3': 'OdbSet object', 'SET-4': 'OdbSet object', 'WarnNodeBCInactiveDof': 'OdbSet object'}
# compare the different use of odbname
>>> session.odbs[odbname].rootAssembly.nodeSets['SET-3']
KeyError: SET-3
>>> session.odbs['10fixed-pin-elastic-L-100-sine-u-v.odb'].rootAssembly.nodeSets['SET-3']
session.openOdb(r'D:/Temp/10fixed-pin-elastic-L-100-sine-u-v.odb').rootAssembly.nodeSets['SET-3']
```

‘SET-5’ is not involved in rootAssembly, which is just a single reference point with no contribution to the model. There is something strange and confusing for me. As can be seen in the above codes, when I use the whole name of odb, ‘SET-3’ and ‘SET-4’ can be printed out, while only ‘SET-1’ and ‘SET-2’ appear when using odbname. The codes are the same in essence and the only difference lies in the way you use odbname, which puzzling me a lot.

Finally, I find what is going on! That is a minor mistake, but cost me so much time! The odbname is actually not the same, ’10fixed-pin-elastic-L100-sine-u-v.odb’ and ’10fixed-pin-elastic-L-100-sine-u-v.odb’. The latter is right with ‘-‘ after ‘L’. After modifying the odbname, it works. Since I have tested some models, the names are very similar with just little difference to differentiate the different settings in models. In the first model, there are only two node sets and the printed results are right.

```python
>>> odbname
'10fixed-pin-elastic-L-100-sine-u-v.odb'
# compare the different use of odbname
>>> session.odbs[odbname].rootAssembly.nodeSets['SET-3']
session.openOdb(r'D:/Temp/10fixed-pin-elastic-L-100-sine-u-v.odb').rootAssembly.nodeSets['SET-3']
>>> session.odbs['10fixed-pin-elastic-L-100-sine-u-v.odb'].rootAssembly.nodeSets['SET-3']
session.openOdb(r'D:/Temp/10fixed-pin-elastic-L-100-sine-u-v.odb').rootAssembly.nodeSets['SET-3']
```

Just use this blog to remind myself to be more careful. Cautiousness improves efficiency, as well as thinking the problem over and sorting it out.
