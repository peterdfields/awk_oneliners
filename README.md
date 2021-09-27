# awk_oneliners

#### Find unique values between two files (see https://stackoverflow.com/questions/4717250/extracting-unique-values-between-2-sets-files).

`awk 'FNR==NR {a[$0]++; next} !($0 in a)' file1 file2`


#### Convert fasta headers to numbers (see https://www.biostars.org/p/53212/).

`awk '/^>/{print ">" ++i; next}{print}' file.fasta > file.header_mod.fasta`

#### Convert fasta headers to numbers w/a prefix, 'chromosome' here (see https://www.biostars.org/p/53212/).

`awk '/^>/{print ">chromosome" ++i; next}{print}' < file.fasta`
