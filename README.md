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





