# Bash_forBeginner
this repository contains all the bash commands a beginner in bioinformatics needs to know when starting out 

Unix is a computer operating system best known for its powerful command-line interface, which allows users to interact with the system by typing commands. Instead of clicking and pressing buttons, as you would with a graphical user interface (GUI), when using Unix, you enter words and symbols that act as commands and instruct the computer to perform various processes. It may seem archaic to use a keyboard to issue commands today, but it’s much easier to automate keyboard tasks than mouse tasks.

Unix is widely used in bioinformatics because of its flexibility, scalability, and powerful command-line tools. Many bioinformatics software tools and pipelines are designed to run in a Unix environment, and the command-line interface, often provided by the Bash shell, allows bioinformaticians to perform complex data analysis and manipulation tasks efficiently. In this tutorial, I’ll provide a crash course on basic Bash commands for bioinformatics, including an overview of essential Bash commands to navigate a file system and move, copy, edit files, and more.

HOW TO WORK WITH FILES AND DIRECTORIES
use `mkdir` to make directory/folder and `rmdir` to remove directory/folder
```bash```
```mkdir NameOfFolder```
```mkdir Salmon```

use `wget` to download files, reference genome, scripts, software, batch download of files within loops 
```wget PasteLinkOfYourfiles/ReferenceGenome```
```wget  https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_45/gencode.v45.annotation.gtf.gz```
```for i in {1..10}; do```
    ```wget http://example.com/project_A/sample_${i}.fastq.gz```
```done```
