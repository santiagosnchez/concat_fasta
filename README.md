# concat_fasta.pl
Concatenates multiple FASTA alignments into a single super-matrix

Concatenates FASTA files given a suffix present in all target files (e.g. "XXX.fasta"). By default the output format is FASTA, but the "-n" and the "-p" flags will produce either a NEXUS or a PHYLIP formatted file. Labels for the same "taxon" should be the same on all FASTA files, but can be unordered. The number of sequences on each file can also be different. In this case, an empty sequence will be added (e.g. "NNNN.."). It will also print a layout of the partitions to the screen. If the "-p" flag is given the partitions are printed in "raxml" style.

The script also has filtering capabilities. You can provide a pattern (e.g. "sp1") after the "--filter" flag or a file with a list of label patterns to include. If you wish to filter out sequences, but avoid concatenation you can pass the "--no-concat" flag. This will produce individual gene files that only include sequences that match your filter pattern. This is particularly useful if you have phased allelic sequences that cannot be concatenated, or unequal per gene sampling.

## Installation

    git clone https://github.com/santiagosnchez/concat_fasta
    cd concat_fasta
    chmod +x concat_fasta.pl
    sudo cp concat_fasta.pl /usr/local/bin

## Running the code

Use the `-h` flag for more details:

    perl concat_fasta.pl -h
    
    Try:
    perl concat_fasta.pl [ --suffix | --prefix ] your_pattern --outfile output [ --filter filter_pattern ] [ -n | -p ]
    
         --suffix, --prefix         A string of characters present only in the FASTA files you wish to concatenate.
                                    An example would be ".fasta" or ".fas" (without quotation marks) in the case of the suffix,
                                    or "xxx" or "sample" at the begining of the file in the case of the prefix.
         --outfile                  The name of file where you are saving the concatenated data.
                                    By default the format is FASTA, unless the following flags are stated.
         --filter    [Optional]     Will include only the terminals that include the pattern.
                                    This can also be a text file with a list of filter patterns.
         --no-concat                Use only if you just want to filter records while keeping individual gene alignments.
         -n          [Optional]     The output format is NEXUS.
                                    The partitions will be printed at the end of the file in NEXUS style.
         -p          [Optional]     The output format is PHYLIP.
                                    Partitions are printed to the screen or can be printed to a file by using ">"

    Example:
    
    perl concat_fasta.pl --suffix .fasta --outfile concat.phylip --filter sp3 -p > part.txt)

