# How to calculate centriods distance using Multiwfn (for ORCA users)
This function is used to calculate overlap and centroid distance between two orbitals. 

In this example, we use a NTO file.

References: 
Multifwn manual
- input file 3.21
- centroids distance par 3.100.11 (Calculate overlap and centroid distance between two orbitals)


## Prepare the files:
Two files are necessary:
- the file containing basis function and molecular orbital information
	- for ORCA users this information is contained in .gbw file. You have to convert the gbw file info molden file, using orca_2mkl. If the .gbw is named Test.gbw: 
	```
	orca_2mkl Test -molden
	```
- the file cointaining configuration coefficient of excited states
    - for ORCA users it is important to set ```tprint 1E-8``` whitin the %tddft block


## Generate the NTO file (.fch file)
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



## Calculate centriods distance
- Boot up Multiwfn and input 
``` path\file.fch ```
- 100 //  Other functions (Part 1)
- 11 //  Calculate overlap and centroid distance between two orbitals
-  enter number of orbitals (check!)
-  y // add dummy atoms
-  0
Output example:
 X/Y/Z of centroid of electron density (Angstrom)
 Orbital   147:   -3.318173    1.801150   -3.319016 
 Orbital   148:   -3.484404    0.793266   -4.452829
 Centroid distance between the two orbitals:    2.883919 Angstrom
 Overlap integral of norm of the two orbitals:    0.6571412334
 Overlap integral of square of the two orbitals:    0.0019639334

## Script example 

This script runs over all fch file and calculates the centroids distance between orbitals 147-148 
(occupied NTO -> virtual NTO). 
The output file contains two columns: the id_file and the centroid distance between the two orbitals (Angstrom).

```
for i in *fch
do
cat << EOF > radius.txt
C:\Multiwfn_3.7\axial\\$i
100
11
147,148
y
0
q
EOF
/mnt/c/Multiwfn_3.7/Multiwfn.exe > radius.log < radius.txt


r="$(grep 'Centroid distance between the two orbitals:' radius.log | tail -1)"

echo ${i}       ${r} | tee -a ./fileradius.dat

done
rm radius.log

```
