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
References: 
Multifwn manual
	- input file 3.21
	- centroids distance theory 3.21.4
	- centroids distance example 4.18.4
## Prepare the files:
Two files are necessary:
- the file containing basis function and molecular orbital information
	- for ORCA users this information is contained in .gbw file. You have to convert the gbw file info molden file, using orca_2mkl. If the .gbw is named Test.gbw: 
	```
	orca_2mkl Test -molden
	```
- the file cointaining configuration coefficient of excited states
    - for ORCA users it is important to set ```tprint 1E-8``` whitin the %tddft block


## Generate the file (.fch file)
Boot up Multiwfn. 
- input 
```
path\file.input.molden
```
- 18 // Electron excitation analysis
- 6 // Generate NTOs
- ```path\file.out```
- 1 for singles 3 for triplets
- type the state
-  2 Output NTO orbitals to .fch file
- ``` path\file.fch ```
- 2 save as .fch file
- path\file.fch
0 0 for visualizing



## Calculate distance
- Boot up Multiwfn and input 
``` path\file.fch ```
- 18 // Electron excitation analysis
- 4 // Calculate delta r index ``` path\file.out ```
- 1-5 // Assume that we want to calculate  r index for all the five calculated singlet excited states
- Immediately, the results are printed on screen:
