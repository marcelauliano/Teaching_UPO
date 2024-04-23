# Identification of DNA sequences with BLAST

Today we are going to identify DNA sequences with [BLAST](https://www.nature.com/scitable/topicpage/basic-local-alignment-search-tool-blast-29096/#:~:text=BLAST%20is%20a%20computer%20algorithm,tool%20in%20ongoing%20genomic%20research.). The BLAST+ algorithm can be run locally or on NCBI, and we are going to run both versions today. 

## 1. Local blast search

We have a fasta sequence for the species _Rhimphoctona megacephalus_ and we want to identify what this sequence is. I have a database of other insect sequences, and I want to blast my _R. megacephalus_ sequence to this database to see if I can identify the sequence. I can do it localy in my computer, since the blast algorithm is already installed.

In this same github repositiory you will find the _R. megacephalus_ sequence we want to identify (xx) (this is the query), and the database of insect seqquences (subject). Download this sequences to your local machine.

### 1. Create a blast database to run your BLAST search

Now that you have your sequences downloaded, the first step to run a local blast search is to 

```
makeblastdb -in sequences_db2.fasta -dbtype "nucl" -out sequences_db2

```






