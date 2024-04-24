# Identification of DNA sequences with BLAST

Today we are going to [BLAST](https://www.nature.com/scitable/topicpage/basic-local-alignment-search-tool-blast-29096/#:~:text=BLAST%20is%20a%20computer%20algorithm,tool%20in%20ongoing%20genomic%20research.) DNA sequences. The BLAST+ algorithm can be run locally or on NCBI, and today we are going to run both versions. 

## 1. Local blast search

We have a fasta sequence for the species _Rhimphoctona megacephalus_ and we want to hopefully identify what this sequence is. I have a database of other insect sequences, and I want to blast my _R. megacephalus_ sequence to this database to see if I can identify the sequence. We can do it localy in our computesr, since the blast algorithm is already installed.

In this same github repositiory you will find the _R. megacephalus_ sequence we want to BLAST [OZ022415.1.out2.fa](./OZ022415.1.out2.fa) (in blast, this is called the **query**), and the database of insect sequences [sequences_db2.fasta](./sequences_db2.fasta) (in blast, those are called the **subjects**). Download these sequences to your local machine.

Confirm you have your sequences downloaded.

In the command line, in folder where you downloaded the sequences type:

```ls -ltrh ```

Do you see your sequences there? Good, then we can go to the next step.


### 1. Create a blast database to run your BLAST search

The first step in local blast is to create a blast database with indexes for your subjects. Run the following command to do it so:

```
makeblastdb -in sequences_db2.fasta -dbtype "nucl" -out sequences_db2

```

---
**NOTE**

If you want to know more about the blast parameters you can type ``` makeblastdb -help ``` in the command line. You can do the same for the next step, giving ``` blastn -help ```. Most programs will show a help message in the command line. Another alternative is to search for their manuals on the internet.  

---

After running the makeblastdb comand, type ``` ls -ltr ``` on your command line, in the same folder where you ran your makeblastdb command. Do you see the indexes? They will look like this:

```
sequences_db2.nto
sequences_db2.ntf
sequences_db2.nsq
sequences_db2.not
sequences_db2.njs
sequences_db2.nin
sequences_db2.nhr
sequences_db2.ndb
```

If yes, we are ready for our next step. Running blastn.

### 2. Run blastn to identify our query against our database

#### 2.1 Running blastn with default output

We are running a ```blastn``` analyses, which means we will search for **nucleotide** sequence homology (based on blast aligments) of our query against our subjects. There are different ways we can have our analyses output done, first we will generate the defaulf output for blast.

```
blastn -query OZ022415.1.out2.fa -db sequences_db2 -out result.blast_default
```

#### 2.2 Running blastn with output 7

Now we are going to run the same analyses, but we want a tabular output. We will use output format 7 and will add 2 extra columns at the end, the length of the query and the length of the subject.

```
blastn -query OZ022415.1.out2.fa -db sequences_db2 -out result2.blast7 -outfmt '7 std qlen slen'
```

### 3. Interpreting your results

CONGRATULATIONS! You have just ran local blast! 

Now that the first analyses are done, I want you to interprete the results. 

1-) Open the blast default result by doing ``` less result.blast_default ``` . Have a look at the result. To go down in your results, press the space key in your keyboard.

1.1-) What is the first blast match you see? 

1.2-) And what is the second? Soon enough you can see that looking at the default blast result, its hard to see the second blast match. And that is why we have ran it in a tabular format. Let's go to that result.


#### 3.1 Interpreting your results in tabular format

2-) Open the blast output7 result by doing ``` less result2.blast7 ``` . Now, on the 3 first lines of the file you have a description of the algorithm and of what each column on the output represents. You can also find the column ids [here](https://www.metagenomics.wiki/tools/blast/blastn-output-format-6). 

3-) Considering both results (default and tabular, which represent the same thing), answer: what is the first blast hit? 

4-) What is the percentage identity of the match?

5-) What is the length aligment of the first blast match?

6-) What do you think our query sequence is?

Once you have finish answering these questions, let Marcela know. 

---
**SECOND NOTE**

Our sequences are in [fasta format](https://en.wikipedia.org/wiki/FASTA_format). This means we can use some simple commands to manipulate our sequences and check them out. For example, if you want to see the complete headers of our subjects do:

```grep ">" sequences_db2.fasta```

This will show you:

```
>OZ023325.1_O.obscuratus mitochondrion Ophion obscuratus genome assembly, organelle: mitochondrion
>OX403633.1_C.raptor mitochondrion Campoletis raptor genome assembly, organelle: mitochondrion
>OZ022425.1_R.megacephalus mitochondrion Rhimphoctona megacephalus genome assembly, organelle: mitochondrion
```

If you want to cound the number of sequences in a multifasta file, such as our subjects, do:

```grep ">" sequences_db2.fasta | wc```

---

### 4. Finally, let's run blast on the NCBI website

Finally, copy your query sequence and blast on the [NCBI website](https://blast.ncbi.nlm.nih.gov/Blast.cgi?PROGRAM=blastn&PAGE_TYPE=BlastSearch&LINK_LOC=blasthome). 

7-) Do you have the same result as the local blast?

8-) What is the length aligment of the first blast match?

9-) Which blast result is more reliable? Why?


