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
use `awk` for pattern matching and data manipulation only for formatted data like CSV or TSV etc
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

use `sed` for filtering, editing (rename, change, delete, add) anything in your file. it works on any type of data , it works line by line. it is similar to awk

syntax : sed 'expression' filename 
```bash  
sed 's/ .*//' sequences.fasta        (t uses substitution (s/) to find the first space (     ) and everything after it (.*), and replaces it with nothing.)          
```
This command uses the pattern ^> to match lines that start with the FASTA header indicator (>)
```
sed -n '/^>/p' sequences.fasta
```
it has many use cases , check this cheat code https://github.com/genesNi/Bash_forBeginner/blob/main/SED%20Commands.pdf

use `grep` for filtering

syntax: `grep [options] pattern [files]`

use cases for grep ;

case insensitive
`grep -i "UNix" geekfile.txt`

count natches
`grep -c "unix" geekfile.txt`

show line numbers
`grep -n "unix" geekfile.txt`

specify expression with e option
`grep –e "Agarwal" –e "Aggarwal" –e "Agrawal" geekfile.txt`

to Use -f to Read Patterns from a File
`grep –f pattern.txt  geekfile.txt`

# USE OF SPECIAL CHARACTERS AND SYMBOLS

. Dot - it represents the current directory
example ` ls ./ `  ls for list so list files in current directory

. . double dot - represents parent directory (one level up )
example ` cd . . /` moves you one directory up in the hierarchy

- hyphen - Precedes a short option or flag for a command.
  example `ls -l ` Lists files in long format

-- double hyphen - Precedes a long option or flag for a command.
example `grep --color=auto` Enables colorized output for grep

" " double quotes - Used for weak quoting. Prevents the shell from interpreting most special characters (like * or ?), but still allows for variable expansion (like $HOME).
example `echo "The path is $HOME" ` Prints the full path, as $HOME is expanded. which means we used $ sign before home so this is used to show variable so full path of home directory will be printed.

' ' single quotes - Used for strong quoting. Prevents the shell from interpreting all special characters, including variable expansion. The text inside is treated literally.
example `echo 'The path is $HOME'` Prints literally: The path is $HOME. here even the variable is not expanded, everything inside quotes printed as such.

/ forward slash - Used as the directory separator in a path and represents the root directory.
example `cd /etc/ `  Changes directory to the etc directory under the root.

{} braces - Used for brace expansion (generating arbitrary strings).
example `touch file_{a,b,c}.txt `  Creates three files: file_a.txt, file_b.txt, and file_c.txt.
# touch command is used to create an empty file

[] brackets - Used for globbing (pathname expansion) to match a range or a set of characters. Also used in test commands.
example- `ls file_[0-9].txt `  Matches files like file_1.txt, file_2.txt, etc. 

\ back slash - Used as an escape character. It tells the shell to treat the next character literally, removing its special meaning.
example- `echo This is a space\ with\ special\ meaning`   Escapes the spaces so the entire string is treated as one argument. anything after slash for exmaple it is blank space here so it is ignored. this is often used whenever we want to write our big code not in single line otherwise we have to used arrow key to move to left or right , so we rather use \ after half code then write in next line, but the whole code is treated as one not 2 separate codes.

| pipe operator- used to pipe the standard output of the command on the left into the standard input of the command on the right, connecting them.
example- ` ls -l | grep .txt `   it means the output of list command will be input for grep command. 
` ls /usr/local/bin | grep fastqc `  

~ tilde - Represents the current user's home directory.
example `cd ~ `  Changes directory to the user's home directory, e.g., /home/user/

> greater than - Redirects the standard output (STDOUT) of a command to a file, overwriting the file if it already exists.
example - `echo "Hello" > output.txt`    Puts "Hello" into output.txt, replacing any previous content.  this means it put hello inside a txt file which has name output.txt, now if file exist and has something else written so now it will change to hello. but if no txt file of this name exists a new txt file of this name is created and hello is written on it.

>> append redirect output - Redirects the standard output (STDOUT) of a command to a file, appending to the file's existing content.
example - `echo "World" >> output.txt`   Adds "World" to the end of output.txt. this means it does not overwrite the file, it adds the word World on the last.

$ dollar sign- Used to indicate a variable. The shell replaces the variable name with its value (variable expansion).
example - `echo $USER`   Prints the name of the current user.

^ caret symbol- Start-of-Line Anchor- Requires the pattern that follows it to occur immediately after the newline character (i.e., at the start of the line).
example- `grep "^>" genome.fa`   Search for lines that start with the > symbol.   (.fa )or (.fasta) - same things

# - hash- it is used to show comments , like if you want to explain about some command or section in your code so you write comments.

# File Management Commands

Command to move your or rename files or directories (folders)
Syntax-  `mv old_file_name new_file_name `    this one is used for renaming 
example-  `mv Aligned.out.bam SRR12345_Aligned.bam `

Syntax- `mv source_file_name destination_path `    this one is used to move file from source to any destination
example- `mv geeksforgeeks /home/jayeshkumar/jkj/ `

#command to copy files or directories 
Syntax- `cp sourcefile destination`   it either creates a new file or overwrite the older one 
example- `cp /references/hg38.fa .` You have a crucial, large reference genome file (hg38.fa) in a shared directory (/references) and need a local copy in your project folder (/project_A) to prevent accidental changes.

cat - Concatenate files and print contents to the terminal- You have two quality control report files (R1_report.txt and R2_report.txt) and want to quickly view them as one combined stream of text to search for a specific error message.
example- `cat R1_report.txt R2_report.txt | less` 


# File Inspection and Manipulation

wc - Word Count (tells you lines, words, and bytes).
example- `wc -l raw_reads.fastq`  (Divide result by 4 to get read count)-  ou need to count the total number of reads (lines) in your raw FASTQ file to verify that the sequencing run produced the expected output. (FASTQ files have 4 lines per read).

head - Display the start of a file (first n lines). 
example- `head file_name `  it will show first 10 lines by default
if you add `head -n 5  megha.txt`  it will show first 5 lines of file megha.txt

tail - Display the end of a file (last 10 lines by default, or specify -n) 
Syntax- `tail file_name` or `tail -n number_of_lines file_name` 
example- `tail star_log.txt`  Check the end of a long log file (star_log.txt) to confirm the final alignment summary statistics and ensure the run completed successfully.

sort- Sorts the lines of a text file alphabetically or numerically.
Syntax- `sort [OPTION]... [FILE]...` options can be -k (Sorts a table based on a specific column number.) or -r (Sorts data in reverse order (descending).)
example- `sort -k1,1 diff_genes.tsv`  You have a file containing a list of differentially expressed genes and their Log2 Fold Change values. You want to sort the entire file by the gene name (the first column).

uniq- Reports or filters out repeated lines. (Often used after sort).
Syntax- `uniq [OPTIONS] [INPUT_FILE [OUTPUT_FILE]]`
example- `sort gene_list.txt | uniq > unique_genes.txt`  You extracted a list of all gene names from a GFF annotation file, but the list contains duplicates because genes often span multiple entries (exons, UTRs). You want a clean, unique list of gene IDs.

# working with compressed sequencing data

zless- Interactive Paging of Compressed Files.
example- `zless sample_R1.fastq.gz `  (Allows you to scroll, search (/), and quit (q) just like less).
You need to inspect the quality scores of your raw sequencing data (sample_R1.fastq.gz) without waiting for the 50GB file to fully decompress.

zcat- Concatenation and Streaming of Compressed Files.
example- `zcat sample_R1.fastq.gz | fastqc `  (The - tells FastQC to read the data being streamed from zcat).
You need to pass the contents of your compressed FASTQ file directly to a quality control tool like FastQC, which expects a stream of uncompressed data, without saving an intermediate uncompressed file.

clear- to clean the terminal 
