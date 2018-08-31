# MetaMSD


MetaMSD integrates proteomics results (p-values) from multiple experiments





##	Testing

Creating test output, selecting specific columns, swapping tabs for spaces and comparing using `numdiff` and very nice tools that compares the numeric contents of files with an adjustable tolerance level.

```BASH
./MetaMSD.Rscript -m Stouffer -i test/input.1 -o test/output.1.Stouffer
./MetaMSD.Rscript -m Pearson  -i test/input.1 -o test/output.1.Pearson 
./MetaMSD.Rscript -m Stouffer -i test/input.2 -o test/output.2.Stouffer
./MetaMSD.Rscript -m Pearson  -i test/input.2 -o test/output.2.Pearson 

awk 'BEGIN{FS=OFS="\t"}{i=$1;gsub(/[[:alpha:]]/,"",i);print i,$1,$17,$18,$19}'  test/output.2.Stouffer/MetaAnalysisResult.txt | sort -n | sed -e '1s/^\t//' | sed -e 's/\t/ /g' | head -2001 > test/myStoufferresult.txt

numdiff --absolute-tolerance 1e-14 test/*Stoufferresult.txt
+++  Files "test/Stoufferresult.txt" and "test/myStoufferresult.txt" are equal






awk 'BEGIN{FS=OFS="\t"}{i=$1;gsub(/[[:alpha:]]/,"",i);print i,$1,$17,$18,$19}'  test/output.2.Pearson/MetaAnalysisResult.txt | sort -n | sed -e '1s/^\t//' | sed -e 's/\t/ /g' | head -2001 > test/myPearsonresult.txt

numdiff --absolute-tolerance 1e-14 test/*Pearsonresult.txt 
+++  Files "test/Pearsonresult.txt" and "test/myPearsonresult.txt" are equal

```

