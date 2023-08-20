This is the webiste for information on the Serena Suite of RNA analysis tools and algorithms. This includes software documentation and thought/reasons for doing things certain ways.

# System Requirments
This software was developed to run on Ubuntu 22.04 LTS and Python 3.9. Python 3.9 is used due to the fact that the NUPACK version I currenlty use 4.0.0.28 will not build with any python versions after 3.9. 

# Installation 
The package is pip installable so currently from the root of the project pass:

    pip install .

# Algorithms, Tools, and Framework

Currently Ensemble Variation and Local Minima Variation are the only algorithms with tools fully coded up and unit tested from the list of algorithms presented at the annual RNA design conference Eternacon9 at Stanford University. These utilize a new software framework I developed that enabled the processing and shuttling around of information on RNA stuctural ensembles. These ensembles are determined through thermodynamic modeling using University research software tools such as Nupack4 and Vienna2. 

## Framework
The entry point into the framework is the Sara2SecondaryStructure. This object contains all the information known about a single secondary structure found in the ensemble of a RNA sequence. This includes the structure in dot parentheses notation, total free energy, stack energy, RNA sequence and number of nucleotides. The full ensemble of a RNA sequence with all its seperate secondary structures is then represented through the Sara2StructureList to start with.

I very purposfully chose my words when I said "full ensemble of a RNA sequence". This is because the shape RNA takes should not be thought of as the MFE structure only, as it currently taught in schoolm as the best approximation of the shape it will take. This is becuase the MFE is only the shape that it will exhibit at the lowest and strongest negative free energy. The RNA in actuallity will jump around and you really need to look at the entire ensemble over a large span of energy from the MFE toward the positive direction of energy. 

One major reason for this is that Temperature is one of the variables that goes into the Partiton Function for the ensemble that is calculated. It is impossible to hold the temperature in a state that there is zero variation and as such when the temperature fluctuates even a fraction of a degree, the partition function will change. The partition function then will feed back into how the secondary structures for the ensemble that is generated. Any change that would affect the partition function then would change how the enemble would look. Taking this a step further, when you predict the fold of a RNA and thus the MFE structure using a package such as Nupack, you have to enter the temperature at time of the fold. This gives you a MFE tied to only that exact temperature and does represent the MFE at different temperatures. We can however do a single fold at the target temperature and analyze the ensemble out some span form MFE, as the ensemble structures are predictions of what structures will appear at what total energy levels for that sequence and one of the things that affects energy is Temperature. We can thus use this information to determine stability of the RNA, as well as the prefered beavhiours the RNA sequence wants to take. In order to make more sense of the ensemble i have found it is best to break it up into chunks to better understand the transitions of each energy level in 1 degree increments. You can then get a feel for how stable the RNA is even across any generalized stability. You can also see if there are echoes of the ability to be a RNA riboswitch and how well it would do if different oligos were present.

The Sara2StructureList is thus a list of each Sara2SecondaryStructure in the ensemble in order found. When populated the oject is able to give you inromation on min and max energy levels, mfe structure, num of structures in list, as well as teh list of strucures. Each 1 kcal energy group has a Sara2StructureList generated for it which is used to make a unique SingleEnsembleGroup. The SingleEnsembleGroup is an object that is used to hold increasing amounts of information about chuncks of the ensemble and includes information used for switch analyis. Each SingleEnsembleGroup is then feed into a single MultipleEnsembleGroups which is an object that holds all the ensemble groups information broken down by kcal range for those structures.

A Sara2StructureList object is then feed into the Ensemble Variation Algotithm to determine general stability of a RNA sequence across the the descret range of teh ensemble. The value generated is a unit of measurment and Ensemble Variation or EV is the unit. A MultipleEnsembleGroups object is fed into the Local Minima Variation algorithm to get results for that various flavors of LMV that represent different aspect of the stabilty of the ensemble using the ensemble variation metric and unit of measure. To see examples of this implementation check out the unit tests for the nupack interface as it has teh entire process coded up.

### How to call
After installation you can access Serena's EV and LMV tools from python via:

    from serena.ensemble_variation import RunEnsembleVariation

or

    from serena.local_minima_variation import  LocalMinimaVariation

# API Reference

[Sara2 Structures](/docs/src/serena/utilities/ensemble_structures.html)



