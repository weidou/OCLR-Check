Welcome to OCLR-Check
==========

OCLR-Check is a toolset to perform offline checking of *OCLR* properties on system execution traces. The toolset has been developed by Wei Dou (http://people.svv.lu/dou), at the SVV lab (http://www.svv.lu) of the University of Luxembourg (http://wwwen.uni.lu).
More information on OCLR-Check is available in this technical report:

> Wei Dou, Domenico Bianculli, and Lionel Briand. __A model-based approach to trace checking of temporal properties with OCL__. Technical Report TR-SnT-2014-5, SnT Centre - University of Luxembourg, September 2014.  Available online at http://hdl.handle.net/10993/16112

*OCLR* is a temporal extension of OCL (Object Constraint Language, http://www.omg.org/spec/OCL) which allows users to express temporal properties using property specification patterns (http://patterns.projects.cis.ksu.edu). *OCLR* has been introduced in this paper:

> Wei Dou, Domenico Bianculli, and Lionel Briand. __OCLR: a more expressive, pattern-based temporal extension of OCL__. In Proceedings of the 2014 European Conference on Modelling Foundations and Applications (ECMFA 2014), York, United Kingdom, volume 8569 of Lecture Notes in Computer Science, pages 51-66. Springer, July 2014. Available online  at http://dx.doi.org/10.1007/978-3-319-09195-2_4

Requirements
---
* Mac OS X / Linux
* Xtext framework (http://xtext.org) 2.5.0+
* Java 1.6.0_65
* Eclipse OCL 4.1.0

Content of the distribution
---
The OCLR-Check distribution contains two modules:

###Checker (*checker* folder)
The offline trace checker is comprised of four parts: the OCLR-Check main programs, the models, the DSLs, and the mapping from *OCLR* to OCL.
  * In the *main* folder, *OfflineCheck.java* is the main program for checking *OCLR* properties. The other Java program *ConstraintFactory.java* is an auxiliary class for building OCL constraints and/or queries.
  * The *models* folder contains three Ecore models: a *trace* model, an *OCLR* meta model, and a *check* model. By using the three models, we generate the corresponding Java code and check the traces with our *checker* programs.
  * the *DSLs* folder contains the Xtext definitions (*Trace.xtext* and *Oclr.xtext*) of the trace model and of the *OCLR* meta model. It also contains the programs for building XMI instances of the two models.
  * The *oclr2ocl* folder contains the definition of the translation that maps *OCLR* constraints into OCL constraints on the trace model.

###Evaluation
This module contains the artifacts used to perform the evaluation described in the aforementioned technical report:
the *OCLR* properties and the trace generators used to generate the traces.

* #####Properties
We provide 38 *OCLR* properties, both as DSL specifications (under the *OCLR-DSL-specifications* folder) and as XMI instances (under the *OCLR-XMI-instances* folder) conforming to the *OCLR* meta model. These XMI instances are generated from the DSL specifications by using the program: "/checker/DSLs/OCLRInstanceFactory.java".

* #####Trace Generators
Traces generator programs implement various generation strategies, depending on the type of property that one wants to check on the trace being generated.
Generators are Python programs named after the type of property for which they generate traces;  e.g., *trace_generator_globally.py* is the trace generator to generate the trace for the properties with the ```globally``` scope.
A trace generator needs 4 parameters:
  1. scope (```--scope/-s SCOPE```);
  2. pattern (```--pattern/-p PATTERN```);
  3. property id (```--id/-i ID```);
  4. (maximum) trace length (```--length/-l LENGTH```).
  For instance:
  ```./trace_generator_globally.py -s 'globally' -p  'always a' -i p1 -l 1000000```
  corresponds to generating traces with various trace lengths - 100K, 200K, ..., 1M (determined by the given maximum trace length) for the property with id ```p1``` which has the scope ```globally``` and the pattern ```always a```.
We also provide the shell scripts used to generate the traces for the 38 properties contained in the releases.

* #####Traces
For each property to check, we provide several traces both in CSV and XMI formats. The XMI traces were generated by the trace generators introduced below, and the CSV traces were automatically transformed from the XMI ones. To keep the size of the repository small, we provide the traces in separate releases (https://github.com/weidou/OCLR-Check/releases/tag/v1.0-csv and https://github.com/weidou/OCLR-Check/releases/tag/v1.0-xmi).
#Usage
Please read the [usage guide on the Wiki](https://github.com/weidou/OCLR-Check/wiki/Usage).