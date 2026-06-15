# EXFOR Plot File (CX4)
The EXFOR Plot File is the [EXFOR Entry File](https://nds.iaea.org/nrdc/exfor-master/entry/) converted to the CX4 (Compact EXFOR) format via the [EXFOR JSON File (J4)](https://nds.iaea.org/nrdc/exfor-master/j4/) by the [ForEXy](https://pypi.org/project/forexy/) package [1]. The CX4 format has ($x, \Delta x, y, \Delta y$) structure, and its table structure is suitable for plotting. Each CX4 file is provided with a sample plot pdf file. See [2] for the original EXFOR Library.

**Download**

- download individual files of the current version from the [EXFOR Plot File](https://nds.iaea.org/nrdc/exfor-master/cx4/) website, or
- download the full repository of the current version by using the terminal command:
```
git clone https://github.com/iaea-nrdcnetwork/exfor-plot-file.git
```

**Directory structure**
```
    +--+--x4_makcxl.log   # update log file
       +--x4_makcxl.txt   # index file
       |
       +--cx4
          |
          +--0            # spantaneous fissoin
          |  |
          |  +--Bk249       # Bk249(sf)
          |  ...
          |
          +--Ac215        # Ac-215 induced reaction
          ...
          +--a            # alpha-particle induced reactoin
          |  |
          |  +--Ag          # Ag+a
          |     |
          |     +--el         # Ag(a,a0)
          |        |
          |        +--adxc      # Ag(a,a0) dsigma/dOmega(cm)
          |        |  +--a-Ag-..._F0700.004.1.cx4 # EXFOR F0700.004.1 (CX4)
          |        |  +--a-Ag-..._F0700.004.1.pdf # EXFOR F0700.004.1 (PDF)
          |        |  +--a-Ag-..._F0700.004.2.cx4 # EXFOR F0700.004.2 (CX4)
          |        |  +--a-Ag-..._F0700.004.2.pdf # EXFOR F0700.004.2 (PDF)
          |        |  ...
          |        |
          |        +--adxl      # Ag(a,a0) dsigma/dOmega(lab)
          |           +--a-Ag-..._F1116.002.cx4 # EXFOR F1116.002 (CX4)
          |           +--a-Ag-..._F1116.002.pdf # EXFOR F1116.002 (PDF)
          ...
         
```

**Contents**

The following quantities are within the scope of these libraries:

* cross section (incl. gamma production)
* angular differential cross section (incl. gamma production)
* energy differential cross section (incl. gamma production)
* double differential cross section
* fission neutron multiplicity
* fission product yield

for any projectiles and reactions not leaving two or more heavy (A>4) nuclides.


Experimental data in 

* 4 columns (x,dx,y,dy) for a dataset as a function of the
  * incident energy (excation function - "excfun"),
  * outgoing angle (angular distribution - "angdisc" and "angdisl"),
  * outgoing energy (energy distribution - "enedisc" and "enedisl"), or
  * level energy (level distribution - "lvldis")

* 3 columns (x,y,dy) for a dataset as a function of the
  * product nuclide (nuclide distirbution - "nucdis")
    N.B. the nuclide is give as a real number (e.g., 46109.9 for 109Pd).

* 2 columns (y,dy) for 
  * neutron multiplicities for spontaneous fissions ("sponnu").

CX4 files are stroed in the following directory structure:
`$projectile/$target/$reaction/$quantity`

*Examples*
* `a/Ni/x/sig/a-Ni-x-sig-excfun-mon-prodCu64_Takacs_2020_D4408.005.cx4`:
Ni(a,x)64Cu production cross section as a function of the incident energy (excfun), published by Takacs in 2020 and compiled in EXFOR D4408.005.

* `n/Fe56/el/adxc/n-Fe56-el-adxc-angdisc-mon-einc5.050E+06_prodFe56_Boschung_1971_10037.024.cx4`:
56Fe(n,n0)56Fe angular differential cross sections in the c.m. system (adxc) at the incident energy (einc) of 5.05 MeV as a function of the c.m.  angle (angdisc), published by Boschung in 1971 and compiled in EXFOR 10037.024.

* `p/Bi209/xn/ddxl/p-Bi209-xn-ddxl-enedisl-mon-einc9.000E+07_angl20_Kalend_1983_C0841.008.cx4`:
209Bi(p,n+x) double differential cross section in the lab. system (ddxl) at the incident energy (einc) of 90 MeV and outgoing angle in the lab. system (angl) at 20 deg as a function of the outgoing neutron energy in the lab. system (enedisl), published by Kalend in 1983 and compiled in EXFOR C0841.008.

## Abbreviations in CX4 file names
### Isomeric state
An isomeric state is indicated by

* g: ground state production (G)
* m: first metastable state production (M or M1)
* n: second metastable state production (M2)
* p: ground + first metastable state production (G+M1)
* q: ground + second metastable state production (G+M2)
* r: first + second metastable state production (M1+M2)

*Example*
 "Au196n" is for 196m2Au (9.6 h) while "Au196p" is for the sum of 196gAu (6.2 d) and 196g1Au (8.1 s).


### Physical quantity
* adxc: angular differential cross section in c.m. system
* adxl: angular differential cross section in lab. system
* ddxc: double differential cross section in c.m. system
* ddxl: double differential cross section in lab. system
* edxc: energy differential cross seciton in c.m. system
* edxl: energy differential cross seciton in lab. system
* sig:  cross section
* sigc: cross section (cumulative)
* fyc:  fission product yield (cumulative)
* fyi:  fission product yield (independent)
* nud:  fission neutron multiplicity (delayed)
* nup:  fission neutron multiplicity (prompt)
* nut:  fission neutron multiplicity (total)


### Distribution (running variable)
* angdisc: c.m. angle dependence
* angdisl: lab. angle dependence
* enedisc: c.m. outgoing energy dependence
* enedisl: lab. outgoing energy dependence
* excfun:  incident energy dependence
* lvldis:  level energy dependence
* nucdis:  product nuclide dependence
* othdis:  other distribution (probably indication of processing error!)
* sponnu:  spontaneous fission neutron multiplicity


### Incident particle spectrum
* brs:  bremsstrahlung spectrum average and unfolded
* fis:  fission neutron spectrum field
* mon:  mono energetic field
* mxw:  Maxwellian field
* sdt:  slow-down time spectrometer field
* spa:  averaged over a spectrum with  <E>~0.0253 eV or narrow energy width


### Constant
* angc: c.m. angle
* angl: lab. angle
* elvl: excitation energy (of product)
* enec: c.m. outgoing energy
* enel: lab. outgoing energy
* prod: product


### Author name
A blank and "-" in author's name are replaced by "%" and "+" in the file name (e.g., "Abd%El+Kariem" for "Abd El-Kariem".)


## References
1. N. Otuka, V. Devi, O. Iwamoto, [Appl. Radiat. Isot. 225 (2025) 111903](https://doi.org/10.1016/j.apradiso.2025.111903) [[pdf](https://doi.org/10.48550/arXiv.2505.03758)].
2. N. Otuka et al., [Nucl. Data Sheets 120 (2014) 272](http://dx.doi.org/10.1016/j.nds.2014.07.065) [[pdf](https://doi.org/10.48550/arXiv.2002.07114)].
