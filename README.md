# Bash_forBeginner
this repository contains all the bash commands a beginner in bioinformatics needs to know when starting out 

Unix is a computer operating system best known for its powerful command-line interface, which allows users to interact with the system by typing commands. Instead of clicking and pressing buttons, as you would with a graphical user interface (GUI), when using Unix, you enter words and symbols that act as commands and instruct the computer to perform various processes. It may seem archaic to use a keyboard to issue commands today, but it’s much easier to automate keyboard tasks than mouse tasks.

Unix is widely used in bioinformatics because of its flexibility, scalability, and powerful command-line tools. Many bioinformatics software tools and pipelines are designed to run in a Unix environment, and the command-line interface, often provided by the Bash shell, allows bioinformaticians to perform complex data analysis and manipulation tasks efficiently. In this tutorial, I’ll provide a crash course on basic Bash commands for bioinformatics, including an overview of essential Bash commands to navigate a file system and move, copy, edit files, and more.

HOW TO WORK WITH FILES AND DIRECTORIES

use `mkdir` to make directory/folder and `rmdir` to remove directory/folder

```bash
   mkdir NameOfFolder
   mkdir Salmon
```

use `wget` to download files, reference genome, scripts, software, batch download of files within loops 

```bash
   wget PasteLinkOfYourfiles/ReferenceGenome  #format
   wget  https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_45/gencode.v45.annotation.gtf.gz
   for i in {1..10}; do
       wget http://example.com/project_A/sample_${i}.fastq.gz
   done
```
use `awk` for pattern matching and data manipulation
cheat code for awk 

```bash
  1. awk options 'pattern {action}' file_name
```
  #options:
        -F field separator
        -v var=value
        -f file

```   Print the chromosome and position from a VCF file      #Extracting Specific Columns
    awk '{print $1, $2}' variants.vcf
```
 Filter for variants with a Quality score > 50         #Filtering Based on Conditions
   ```
    awk '$6 > 50' variants.vcf                            #Filtering by value
```
   Print lines that contain the word "gene"
```
  awk '/gene/' annotation.gff                          #Filtering by pattern
```

 2. echo “Hello” | awk options ‘pattern {action}’
   #options:
      -F field separator
      -v var=value
      -f file
```bash
   to look at gtf file
   zless -S gencode.v45.annotation.gtf.gz | grep -v "#" | awk '$3=="gene"' | cut -f9 | head -3

   zcat gencode.v45.basic.annotation.gtf.gz |awk -F "\t" '$3 == "transcript" { print $9 }'| tr -s ";" " "   |cut -d " " -f2,4|  sed 's/\"//g' | awk '{print $1"."$2}' > genes.txt
```
cheat code for awk https://github.com/genesNi/Bash_forBeginner/blob/main/AWK%20Scripting.pdf
    

