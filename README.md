# Blast-CLI  

## Intro  

The BLAST algorithm, which stands for **B**asic **L**ocal **A**lignment **S**earch **T**ool, is a widely used and highly effective algorithm in bioinformatics and computational biology. It is used to compare biological sequences, such as DNA, RNA, or protein sequences, to identify regions of similarity or homology.  
The primary goal of the BLAST algorithm is to find local alignments between a query sequence and a database of sequences, which can help researchers identify genes, functional domains, and evolutionary relationships between sequences.

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

## Installation  

[Download section](https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html)  

### Software installation  

Running blast form the [webinterface](https://blast.ncbi.nlm.nih.gov/Blast.cgi) has it's limitations.  
If you want to include your blast analysis in your own pipelines, Blast+ is the way to go.  
You can [download the Blast+ executables](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) and install them on your own machine.  

  1. [Download the latest executable](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/)
  2. Unpack the download file:  
```bash
tar xvf yourfile.tar.gz
```
**NOTE**: It is always good pracktice to install bioinformatic software (if from source) to a designated **bioinfo** folder i.e. **/usr/local/bionfo**.  
          From here you can create a symlink to a folder in your $PATH f.i. /usr/local/bin
          
### Database installation
## Build Database  

## Run blast on command line  

## Output tab format  

