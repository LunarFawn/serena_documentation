# Serena RNA Analysis Suite

    This is the webiste for information on the Serena Suite of RNA analysis tools and algorithms. This includes software documentation and thought/reasons for doing things certain ways.

## System Requirments
    This software was developed to run on Ubuntu 22.04 LTS and Python 3.9. Python 3.9 is used due to the fact that the NUPACK version I currenlty use 4.0.0.28 will not build with any python versions after 3.9. 

## Algorithms, Tools, and Framework

    Currently Ensemble Variation and Local Minima Variation are the only algorithms with tools fully coded up and unit tested from the list of algorithms presented at the annual RNA design conference Eternacon9 at Stanford University. These utilize a new software framework I developed that enabled the processing and shuttling around of information on RNA stuctural ensembles. These ensembles are determined through thermodynamic modeling using University research software tools such as Nupack4 and Vienna2. 

### Framework
    The entry point into the framework is the Sara2SecondaryStructure. This object contains all the information known about a single secondary structure found in the ensemble of a RNA sequence. This includes the structure in dot parentheses notation, total free energy, stack energy, RNA sequence and number of nucleotides. The full ensemble of a RNA sequence with all its seperate secondary structures is then represented through the Sara2StructureList to start with.

    I very purposfully chose my words when I said "full ensemble of a RNA sequence". This is because the shape RNA takes should not be thought of as the MFE structure only, as it currently taught in schoolm as the best approximation of the shape it will take. This is becuase the MFE is only the shape that it will exhibit at the lowest and strongest negative free energy. The RNA in actuallity will jump around and you really need to look at the entire ensemble over a large span of energy from the MFE toward the positive direction of energy. 

    One major reason 