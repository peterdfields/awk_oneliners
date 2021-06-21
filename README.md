# awk_oneliners

#### Find unique values between two files.

`awk 'FNR==NR {a[$0]++; next} !($0 in a)' file1 file2`
