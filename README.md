
# compass
Improving assembly contiguity by using locally mapped reads to bridge gaps via De Bruijn graphs.   

* Version: 0.1
* Authors: Andre Corvelo, Jennifer Shelton [New York Genome Center](https://www.nygenome.org)

## Requirements

* Python2
* GEM mapper and indexer. To get the required GEM binaries, run the following commands: 
```
cd bin/
wget -q -O - "https://downloads.sourceforge.net/project/gemlibrary/gem-library/Binary%20pre-release%203/GEM-binaries-Linux-x86_64-core_i3-20130406-045632.tbz2" | tar -jxv GEM-binaries-Linux-x86_64-core_i3-20130406-045632/bin/gem-mapper --strip-components 2
wget -q -O - "https://downloads.sourceforge.net/project/gemlibrary/gem-library/Binary%20pre-release%203/GEM-binaries-Linux-x86_64-core_i3-20130406-045632.tbz2" | tar -jxv GEM-binaries-Linux-x86_64-core_i3-20130406-045632/bin/gem-indexer --strip-components 2
```


## Usage message

```                                                                     
Usage: 
compass options

Options:
  --version            show program's version number and exit
  -h, --help           show this help message and exit

  Input (MANDATORY one of the following: -i, -f or (-1 and -2) and -g:
    -i STR             Input command (use absolute paths!). Quoted, with
                       interleaved FASTQ on STDOUT [Mandatory | -f | (-1 &
                       -2)]
    -f CSV_FILE_LIST   Input .fq, .fastq, .fq.gz or .fastq.gz files.
                       Interleaved [Mandatory | -i | (-1 & -2)]
    -1 CSV_FILE_LIST   Input .fq, .fastq, .fq.gz, .fastq.gz read 1 file. In
                       sync with, and of the same sort as, -2 input file
                       [Mandatory | -i | -f]
    -2 CSV_FILE_LIST   Input .fq, .fastq, .fq.gz, .fastq.gz read 2 file. In
                       sync with, and of the same sort as, -1 input file
                       [Mandatory | -i | -f]
    -g FILE            Input genome FASTA file [Mandatory]
    -b FILE            Input target .bed file []

  Target parameters:
    -s INT             Target slop [15]
    -a INT             Anchor length [100]
    -m INT             Maximum fragment length [800]
    -l STR             Library type. PE or MP [PE]
    --include-targets  Include targets in probe [False]

  Gap Filling:
    -e FLOAT           Maximum mapping edit distance [0.02]
    --unique-mapping   Unique mapping reads only [False]
    -k CSV_INT_LIST    K-mers. CSV ['91,81,71,61,51,41,31']
    -c INT             Minimum coverage [2]
    -v FLOAT           Minimum frequency [0.4]

  Output and miscellaneous:
    -p STR             Sample prefix [random 8-char UUID]
    -o DIR             Output directory ['.']
    -t INT             Number of threads [16]
    -Q QUEUE           Cluster queue/partition []
    -S INT             Cluster slots [16]
    --dry              Dry run [False]
```


## Example invocation

```
compass \
    -f reads.interleaved.fq \
    -g assembly.w_gaps.fa \
    -k 117,107,97,87,77,67,57,47,37 \
    -a 200 \
    -p mysample \
    -e 0.01 ;
```

