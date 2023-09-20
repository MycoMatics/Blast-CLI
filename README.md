# Blast-CLI  

## Intro  

The BLAST algorithm, which stands for **B**asic **L**ocal **A**lignment **S**earch **T**ool, is a widely used and highly effective algorithm in bioinformatics and computational biology. It is used to compare biological sequences, such as DNA, RNA, or protein sequences, to identify regions of similarity or homology.  
The primary goal of the BLAST algorithm is to find local alignments between a query sequence and a database of sequences, which can help researchers identify genes, functional domains, and evolutionary relationships between sequences. Blast can be run at the [NCBI website](https://blast.ncbi.nlm.nih.gov/Blast.cgi).
Or a **C**ommand **L**ine **I**nterface can be downloaded to your own system.

Here are the key components and steps of the BLAST algorithm:
  1. **Query Sequence**: BLAST starts with a query sequence provided by the user, which is the sequence you want to compare against a database of other sequences.
  2. **Database**: BLAST searches against a database containing a collection of sequences. This can be a database of known genes, genomes, proteins, or any other         relevant biological sequences.  
  3. **Scoring System**: BLAST uses a scoring system to assign a numerical score to alignments between the query sequence and sequences in the database. Common           scoring systems include the substitution matrix (e.g., BLOSUM or PAM matrices) for protein sequences and scoring schemes like match/mismatch scores and gap          penalties for nucleotide sequences.
  4. **Seed Search**: BLAST starts by identifying short, exact matches (seeds) between the query sequence and sequences in the database. These seeds serve as             starting points for potential alignments.
  5. **Extension**: Once seeds are identified, BLAST extends these seed matches in both directions along the sequences, using dynamic programming techniques to           find the optimal alignment that maximizes the alignment score. The algorithm also considers gap penalties to account for insertions and deletions.
  6. **Scoring and Filtering**: BLAST scores the extended alignments based on the chosen scoring system. It then applies a statistical significance threshold             (usually based on E-values) to filter out alignments that could occur by chance.
  7. **Reporting Hits**: BLAST reports the significant alignments, known as "hits," to the user. These hits represent regions of similarity between the query             sequence and sequences in the database.

BLAST is highly configurable, allowing users to adjust parameters such as the scoring system, gap penalties, and statistical significance thresholds to customize the search based on their specific needs. There are different versions of BLAST, including BLASTn (for nucleotide sequences), BLASTp (for protein sequences), BLASTx (translating nucleotide sequences to proteins), and more, each tailored to different types of sequence data.  

Overall, BLAST is an essential tool for sequence comparison and is widely used in genomics, proteomics, and other areas of biological research. It enables researchers to quickly and effectively identify similarities between sequences and gain insights into the functional and evolutionary relationships of biological molecules.  

Check out the [NCBI-blast page](https://blast.ncbi.nlm.nih.gov/Blast.cgi) for more information (and online applications)

## Get Blast ready on your local system

For more info take a look at the [Download section](https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) @ NCBI website.

### Software installation  

Running blast form the [webinterface](https://blast.ncbi.nlm.nih.gov/Blast.cgi) has it's limitations.  
If you want to include your blast analysis in your own pipelines, Blast+ is the way to go.  
You can [download the Blast+ executables](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) and install them on your own machine.  

  1. [Download the latest executable](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/)
  2. Unpack the download file:  
```bash
tar xzvf yourfile.tar.gz
```
**NOTE**: It is always good pracktice to install bioinformatic software (if installed from source) to a designated **bioinfo** folder i.e. **/usr/local/bionfo**.  
          From here you can create a symlink to a folder in your $PATH f.i. /usr/local/bin
          
### Database Download

BLAST databases are updated daily and may be downloaded via [FTP](https://ftp.ncbi.nlm.nih.gov/blast/db/).
Database sets may be retrieved automatically with update_blastdb.pl, which is part of the BLAST+ suite. (run this command in working directory, probably best in same directory at your $PATH of the database.)

Please refer to the [BLAST database documentation](https://ftp.ncbi.nlm.nih.gov/blast/documents/blastdb.html) for more details.

  1. Pre-fromatted BLAST db are archived [here](https://ftp.ncbi.nlm.nih.gov/blast/db/)
  2. Get all numbered files for a database with the same base name:
      Each of these files represents a subset (volume) of that database,
      and all of them are needed to reconstitute the database.
  3. After extraction, there is no need to concatenate the resulting files:
      Call the database with the base name, for nr database files, use "-db nr".

**NOTE**:For easy download, use the update_blastdb.pl script from the blast+ package.
     Run following command in your db folder:
```bash
perl update_blastdb.pl --decompress nt # or any other prefix for you db of coice
```
**NOTE**:if the ncbi server runs slow, the update command could rise connection issues.
  Sometimes it is easier to download manually from the [ftp db website](https://ftp.ncbi.nlm.nih.gov/blast/db/):
```bash
wget https://ftp.ncbi.nlm.nih.gov/blast/db/nt.???.tar.gz
wget https://ftp.ncbi.nlm.nih.gov/blast/db/nt.???.tar.gz.md5
```

### Build Local DB (DYI)  

If you want to build your own database based on fasta sequences take a look [here](https://www.ncbi.nlm.nih.gov/books/NBK569841/) for more details.  

### Configuration blast (set env)  

Make a configuration file named .ncbirc (on Unix-like platforms) or ncbi.ini (on Windows) in your home directory  

```bash  
touch ~/.ncbirc &&
echo [BLAST] >> ~/.ncbirc
echo [BLASTDB]=/path/to/databases >> ~/.ncbirc
```
  
More available parameters can be set in the config file.
More detailed info on configurateion can be found [here](https://www.ncbi.nlm.nih.gov/books/NBK569858/) 

## Run blast on command line  

### Quick run

```bash
blastn –db nt –query nt.fsa –out results.out
```

### Personalized outputformat

```bash
blastn -db nt \
  -query /path/to/fastafiles \
  -out /path/to/output/out \
  -outfmt ""6 qseqid sseqid pident length mismatch gapopen qstart qend sstart send evalue bitscore staxids sscinames sskingdoms qcovs" \
  -num_trheads $(THREADS)
```

## Setup Blast @ HPC-UGent  

Blast modules are available on the HPC. 
Databases on the other hand are installed **'localy**.  
**ALERT!**: don't install databases locally, they take up a lot of space. Please contact Pieter if you need a database which is not installed yet.

### DB location  

A dedicated folder is available for our VO where we can 'locally' make pre installed databases available for us all. 
If you need another database, please avoid installing it into your own account folder, it will take up a lot of space and others who are part of our VO cannot access.  

  **Location**: /data/gent/vo/001/gvo00142/data_share_group/databases_blast/   
  **Configuration db**: Create a ncbirc file (see above for instructions) and save in your home folder (/user/gent/433/**yourvscnumber**)  
  
  **Alternative**: add this line to your .bashrc file:  
    
```bash
export BLASTDB=/data/gent/vo/001/gvo00142/data_share_group/databases_blast/
``` 

### Updates  

Instllation dates are always part of the folder where you can find the databasefiles, if you feel it is not up to date, give a shout out to Pieter or make an update yourself if you know how to.
When you need another type of db wchich you frequently use and others might benefit from, ask for a local installation.  

### Usage  

  1. Make sure your env value for $BLASTDB is set correctly.  
```console
vsc43352@node3206:~$echo $BLASTDB                                                    
/data/gent/vo/001/gvo00142/data_share_group/databases_blast/db
```
  2. Use **ml spider blast** to list the installed blast modules
  3. Use the latest module installed in your jobscript
  4. run blast following the blast module (for instpiration look to section **Quick run** above)
     or [RTFM](https://www.ncbi.nlm.nih.gov/books/NBK279690/).
