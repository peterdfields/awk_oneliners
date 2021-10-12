# awk oneliners

#### Find unique values between two files (see https://stackoverflow.com/questions/4717250/extracting-unique-values-between-2-sets-files).

`awk 'FNR==NR {a[$0]++; next} !($0 in a)' file1 file2`


#### Convert fasta headers to numbers (see https://www.biostars.org/p/53212/).

`awk '/^>/{print ">" ++i; next}{print}' file.fasta > file.header_mod.fasta`

#### Convert fasta headers to numbers w/a prefix, 'chromosome' here (see https://www.biostars.org/p/53212/).

`awk '/^>/{print ">chromosome" ++i; next}{print}' < file.fasta`

#### Remove vcf header (see https://www.biostars.org/p/49660/)

`awk '! /\#/' variants.VCF > no_header.VCF`

#### Get the average of a column, here column 2 (see https://stackoverflow.com/questions/19149731/use-awk-to-find-average-of-a-column)
`awk -v N=2 '{ sum += $N } END { if (NR > 0) print sum / NR }'`
