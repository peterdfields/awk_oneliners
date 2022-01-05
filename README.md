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

#### Fix paired reads that are no longer properly sorted (see https://www.biostars.org/p/59707/)
```
mkfifo tmp
awk 'NR%4==1{n=$1}NR%4==2{s=$1}NR%4==0{print n,s,$1}' r1.fq | sort -S 2G > tmp &
awk 'NR%4==1{n=$1}NR%4==2{s=$1}NR%4==0{print n,s,$1}' r2.fq | sort -S 2G | join -a1 -a2 tmp - | awk 'NF==5{print $1"\n"$2"\n+\n"$3 >"x1.fq";print $1"\n"$4"\n+\n"$5 >"x2.fq"}NF==3{print $1"\n"$2"\n+\n"$3>"orphan.fq"}'
```

#### Add text at the beginning of lines 1-10, inplace (see https://stackoverflow.com/questions/9533679/how-to-insert-a-text-at-the-beginning-of-a-file)
`sed -i '1,10s/^/<added text> /' file`

#### Add line at the beginning of file, inplace
`sed -i '1s/^/<added text> \n/' file`

#### Transpose columns and rows in a text file (see https://unix.stackexchange.com/questions/169995/rows-to-column-conversion-of-file)
```
awk '{ for (i=1; i<=NF; i++) RtoC[i]= (RtoC[i]!=""? RtoC[i] FS $i: $i) } 
    END{ for (i in RtoC) print RtoC[i] }' infile
```

#### Merge two files by column and select a subset of columns in resultant file (see https://theglassicon.com/tip-of-the-day/awk-script-merge-columns-files/)
#### Here there are two files, both two columns, and we merge column two from the first file with column one from the second.
`pr -m -t -s\  file1 file2 | awk '{print $2,$3}' > out_file.txt`

#### subset file by specific row number (see https://stackoverflow.com/questions/6491532/how-to-subset-a-file-select-a-numbers-of-rows-or-columns)
`cat largefile | awk 'NR >= 10000  && NR <= 100000 { print }'`
