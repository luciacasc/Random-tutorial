# Calculating $\Delta r$
The $\Delta r$ index is a quantitative indicator for measuring charge transfer (CT) length of electron excitation, 
larger $\Delta r$ index implies longer CT distance. \\
The original paper of $\Delta r$ suggests using 2.0 Å as criterion for distinguishing LE and CT excitations.

pag 223: \\
| Excitation type     | Index D |
|---------------------|---------|
| LE                  | small   |
| Single direction CT | large   |
| Centrosymmetric CT  | small   |



# How to visualize NTOs using Multiwfn (for ORCA users)
References:\ 
Multifwn manual
- input file 3.21 (3 Input files)
- centroids distance theory 3.21.4
- centroids distance example 4.18.4

## Prepare the files:
Two files are necessary:
- the file containing basis function and molecular orbital information
	- for ORCA users this information is contained in .gbw file. You have to convert the gbw file info molden file, using orca_2mkl. If the .gbw is named Test.gbw: 
	```
	orca_2mkl Test -molden
	```
- the file cointaining configuration coefficient of excited states (.out)
    - for ORCA users it is important to set ```tprint 1E-8``` whitin the %tddft block



## Calculate distance
- Boot up Multiwfn and input 
``` path\file.molden ```
- 18 // Electron excitation analysis
- 4 // Calculate delta r index 	``` path\file.out ```
- 1 // 1 singlet 3 triplets. This step is not shown if there are omly siglets
- 3 // Assume that we want to calculate $\Delta r$ index for third calculated singlet excited state. Immediately, the results are printed on screen: ``` Excited state 3: Delta_r = 1.499249 Bohr, 0.793368 Angstrom (..)  ```
- y  // Print orbital pair contributions
- 0.01 // Only the orbital pairs having contribution larger than 0.01 Å will be printed


  continua a leggere da pag 671
