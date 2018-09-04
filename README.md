# MetaMSD


MetaMSD integrates proteomics results (p-values) from multiple experiments



## Installation

`MetaMSD.Rscript` is a single, self contained R script that is being developed in a OS X / Linux environment with R version 3.5.0, although it should run in Windows just the same.

R is available from a number of sources, but its primary is https://www.r-project.org. It can be installed from a number of package managers like MacPorts, Homebrew, APT (for Advanced Package Tool), Yellowdog Updater, Modified (YUM), or explicitly compiled from source code.

While not a requirement, I manage some personal settings for convenience. I create a folder to hold my installed packages.

```BASH
mkdir ~/.R
```

I then tell R to use this folder when installing and updating any packages by editing my `~/.Renviron`

```BASH
R_LIBS=~/.R
R_LIBS_USER=~/.R
```






Once `MetaMSD.Rscript`, has been acquired, it may require changing the mode of the file to enable execute permission.

```BASH
chmod a-x MetaMSD.Rscript
```

The script should now run. The first time this script is run, it will check for the presence of its required packages and attempt to install them should they not already be. This could take a few minutes. In addition, some of these R packages may have some system specific dependencies which you may need to install in order to successfully run this script.

Currently, this Rscript requires "ROCR", "stats", "gridExtra", "gtable", "optparse" and "qvalue". If there are problems with the script running for the first time, open R and try installing them manually.

```BASH
source("https://bioconductor.org/biocLite.R")
biocLite( c("ROCR","stats","gridExtra","gtable","optparse","qvalue"))
```
or
```BASH
install.packages(c("ROCR","stats","gridExtra","gtable","optparse","qvalue"))
```

Once the dependent packages have successfully been installed, try running the script again with the `-h` option.


```BASH
MetaMSD.Rscript  -h


MetaMSD (Meta Analysis for Mass Spectrometry Data)

Usage: MetaMSD.Rscript [options]


Options:
	-m CHARACTER, --metaanalysis=CHARACTER
		Specify a meta-analysis test. Either Stouffer or Pearson. [ default = Stouffer ]

	-c NUMBER, --cutoff=NUMBER
		Specify a q-value cut off. [ default = 0.05 ]

	-t NUMBER, --top=NUMBER
		Specify the number of proteins in Top-N differential protein list. [ default = 15 ]

	-i CHARACTER, --input=CHARACTER
		Specify the input folder name. [ default = input ]

	-o CHARACTER, --output=CHARACTER
		Specify the output folder name. [ default = output ]

	-h, --help
		Show this help message and exit
```

##	Example Run

```BASH
> find input

input/Dataset1.txt
input/Dataset2.txt
input/Dataset3.txt
input/Dataset4.txt
input/Dataset5.txt
```

```BASH
> head Dataset1.txt 

Protein Sign Pvalue
Protein1 -1.62923381934141 0.147221053632276
Protein2 -1.06793602882333 0.310734315752896
Protein3 NA NA
Protein4 NA NA
Protein5 -2.37671095632394 0.0389897160751429
Protein6 NA NA
Protein7 -2.89636264377984 0.0191722774908164
Protein8 -1.51486831001556 0.18547816059573
Protein9 0.188369920348748 0.855631734879989
```

```BASH
./MetaMSD.Rscript
```


```BASH
> find output

output/Diagnosis.txt
output/MetaAnalysisResult.txt
output/Summary.pdf
output/Summary.txt
output/TopDifferentialProteins.pdf
output/TopDifferentialProteins.txt
output/qplot.pdf
```


```BASH
> cat Diagnosis.txt 
Meta-Analysis Evaluation
Integration-driven Discovery Rate (IDR)	22.4 %
Integration-driven Revision Rate (IRR)	5.97 %

> cat Summary.txt 
# of detected proteins
Meta Analysis	2545
Single Analysis 1	900
Single Analysis 2	950
Single Analysis 3	1060
Single Analysis 4	1115
Single Analysis 5	1065
Intersection among Single Analyses	195
Union among Single Analyses	2150

> cat TopDifferentialProteins.txt Rank	Protein	Sign	Pvalue	Qvalue
1	1	Protein2447	-	2.63029115506893e-37	4.37273649289114e-34
2	2	Protein4447	-	2.63029115506893e-37	4.37273649289114e-34
3	3	Protein447	-	2.63029115506893e-37	4.37273649289114e-34
4	4	Protein6447	-	2.63029115506893e-37	4.37273649289114e-34
5	5	Protein8447	-	2.63029115506893e-37	4.37273649289114e-34
6	6	Protein2575	+	4.05954092797942e-36	3.37439882386244e-33
7	7	Protein4575	+	4.05954092797942e-36	3.37439882386244e-33
8	8	Protein575	+	4.05954092797942e-36	3.37439882386244e-33
9	9	Protein6575	+	4.05954092797942e-36	3.37439882386244e-33
10	10	Protein8575	+	4.05954092797942e-36	3.37439882386244e-33
11	11	Protein2523	+	2.02685447274028e-32	1.12318370809141e-29
12	12	Protein4523	+	2.02685447274028e-32	1.12318370809141e-29
13	13	Protein523	+	2.02685447274028e-32	1.12318370809141e-29
14	14	Protein6523	+	2.02685447274028e-32	1.12318370809141e-29
15	15	Protein8523	+	2.02685447274028e-32	1.12318370809141e-29

> head MetaAnalysisResult.txt
Protein	Sign.set1	pvalue.set1	qvalue.set1	Sign.set2	pvalue.set2	qvalue.set2	Sign.set3	pvalue.set3	qvalue.set3	Sign.set4	pvalue.set4	qvalue.set4	Sign.set5	pvalue.set5	qvalue.set5	Sign.meta	pvalue.meta	qvalue.meta
Protein1	-1	0.147221053632276	0.386002199317461	-1	0.0696116003878634	0.232354739425274	NA	NA	NA	1	0.518470182778413	0.586232081710312	NA	NA	NA	-1	0.130639516659494	0.293489337292437
Protein10	-1	0.09615329752224	0.296996240811491	-1	0.0245123200968932	0.109906162178047	-1	0.166127173012038	0.302227940651484	-1	0.0311097689544789	0.116738083504362	-1	0.00898390775995153	0.0465831185398761	-1	6.74435166737771e-06	3.90276182506736e-05
Protein100	-1	0.627948623080076	0.710354871417672	-1	0.111869440721791	0.312619042821373	1	0.887622682495521	0.600579347466967	NA	NA	NA	NA	NA	NA	-1	0.264377440913484	0.477733888538508
Protein1000	-1	0.945014909586666	0.78463102938301	-1	0.92141789414091	0.783473770681269	-1	0.140698119434682	0.273947049937385	-1	0.80131549752656	0.691027234000638	NA	NA	NA	-1	0.344031976789505	0.549939550026999
Protein10000	NA	NA	NA	1	0.291348206077409	0.520973332194634	NA	NA	NA	0.285159383896807	0.453330799934054	1	0.708046329311736	0.665554170316468	1	0.149166664032119	0.323737113411566
Protein1001	1	0.741635008577038	0.743407672989336	-1	0.509949047262865	0.664612157498626	-1	0.708983149277487	0.574980984448962	-1	0.776599880782423	0.679740555335955	NA	NA	NA	-1	0.621940898979742	0.713799819638344
Protein1002	-1	0.533402079887067	0.672719801726766	-1	0.920581003514001	0.783473770681269	1	0.13583437183381	0.272355103513066	-1	0.487328199267165	0.571582663834896	NA	NA	NA	1	0.970326830087737	0.830900473553751
Protein1003	-1	0.578953213094243	0.692898850468948	NA	NA	NA	NA	NA	NA	-1	0.882493227428588	0.712118550653194	NA	NA	NA	-1	0.619259056648539	0.713299706729408
Protein1004	1	0.549422339931358	0.682144306530344	1	0.856354965054217	0.77370063364739	NA	NA	NA	-1	0.153051869148448	0.333331184998575	1	0.623955687609639	0.633333713356406	-1	0.936658634996219	0.822836983443449
```
