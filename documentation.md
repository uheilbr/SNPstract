---
title: "SNPstract_0.5 Documentation"
author: "Urs Heilbronner"
date: "October 17th 2017"
output: html_document
---
Version 0.5

Email:      urs.heilbronner@med.uni-muenchen.de


###1. What is SNPstract?

SNPstract is a simple shell script to extract single nucleotide polymorphism (SNP) data from PLINK v1.07 (http://zzz.bwh.harvard.edu/plink/) dataformats (.ped/.map or .bed/.bim/.fam files, *see below*). It works on GNU/Linux operating systems (i.e. not on Microsoft Windows) and requires a working installation of PLINK v1.07 (*see below*).

SNPstract extracts SNP data using PLINK and reformats the output as a comma-separated values (.csv) text file in which the alleles of each individual and each SNP of interest are contained. This .csv file can then be easily imported to more user-friendly spreadsheet programs such as Microsoft Excel or LibreOffice Calc. 


###2. "*You can actually do this with PLINK alone, so what's the purpose?*"

The output of a PLINK v1.07 SNP extraction procedure are .ped/.map files. These files require several formatting steps in order to obtain a file that people not familiar with PLINK can use. Especially when several SNPs are to be extracted simultaneously, the process is a bit cumbersome. 

The main motivation for writing this script was that I am sometimes asked to extract data used in candidate SNP studies from PLINK files and to provide this data to colleagues not familiar with PLINK. I found this process both time-consuming and error-prone when done manually. 

I am aware that newer beta versions of PLINK offer a much more flexible approach and also a variety of output formats. Therefore, there are most probably better and simpler ways to achieve the goal. 


###3. Notes

####3.1 Computer environment

This script works on Ubuntu Linux 16.04 with PLINK v1.07 installed. All commands below work on an Ubuntu 16.04 system. 

Note that in Ubuntu Linux 16.04, the command for PLINK 1.07 is `p-link`. If your PLINK command is different, `p-link` has to be replaced by the appropriate command (e.g. `plink`) in the script.

####3.2 Installation (Terminal)

The easiest way is to create a directory called `SNPstract` in your home folder and to copy SNPstract_0.5 to this folder. The following example assumes that SNPstract_0.5 is in located the `Downloads` folder in your home directory:

```
cd
mkdir SNPstract
cp ~/Downloads/SNPstract_0.5 ~/SNPstract_0.5
```

Make SNPstact_0.5 executable:

```
cd SNPstract
chmod +x SNPstract_0.5
```

Now, SNPstract_0.5 can be run by typing `sh ~/SNPstract/SNPstract_0.5` (*see below*).

###4. Usage

Assuming the file containig the SNPs to extract (*see below*) is named `SNPs2extract.txt` and the genotype files (*see below*) are called `OmniExpress.bed/.bim/.fam`, all files located in a directory called `stuff`, the command to extract the SNPs is:

```
cd ~/stuff
sh ~/SNPstract/SNPstract_0.5 SNPs2extract.txt OmniExpress
```

**NB: SNPstract_0.5 will write all output files to the directory from which it is started.**

You can also start SNPstract_0.5 without input arguments. You will be required to specify both the file containing the SNPs as well as the genotype files when prompted by SNPstract_0.5.

####4.1 File paths

If files are located in different folder, the full path to the files (e.g. `/home/urs/morestuff/SNPs2extract.txt` or `/home/urs/lessstuff/PsychChip`) can be used.

####4.2 Types of PLINK (.bed/.bim/.fam or .ped/.map) files

To obtain human readable allele names, SNPs should to be extracted from whole-genome non-binary (.ped/.map) files. SNPstract can use both binary (.bed/.bim/.fam) and non-binary PLINK files as input. If both binary and non-binary files are present (i.e. both OmniExpress.bed/.bim/.fam and OmniExpress.ped/.map exist in the same directory), SNPs will be extracted from the non-binary fileset by default.

If binary files are used, SNPstract includes an additional recoding step (performed by PLINK). The recoded files are not deleted after SNPstract_0.5 has finished the extraction process. A logfile from this optional recoding step is preserved (see *Output files*).

####4.3 Input arguments

As described above, SNPstract_0.5 takes either two or zero input arguments. In the case of two input arguments:

* Names of the SNPs to extract must be writtten to a text file (*SNPfile*), one SNP (e.g. rs10774035) per line. This must be the first input argument to SNPstract_0.5.

* The name of genotype files (without extention [.bed/.bim/.fam]; *GENOfiles*). This must be the second input argument to SNPstract_0.5.

####4.4 Output files
As described above, SNPstract_0.5 will write all output files to the directory from which it is started. After running SNPstract_0.5 successfully, there will be two new files in this directory:

* A .csv file whose filename contains date, name of the SNPfile and name of the GENOfiles (without extention). This file contains the extracted SNP data.

* A log file from the PLINK SNP extraction operation. The filename contains date, name of the SNPfile, name of the GENOfiles (without extention) and ends with *EXTRACT.PLINK.log*.

* Optionally, if binary PLINK files were recoded to non-binary PLINK files, a log file from the PLINK recoding operation is also included. This filename also contains date, name of the SNPfile, name of the GENOfiles (without extention) and ends with *RECODE.PLINK.log*. The recoded PLINK files are not deleted.

Please note that SNPstract_0.5 deletes the .ped/.map files resulting from the extraction process.


###5. Disclaimer

I have written this script for myself to easily and rapidly extract genotype information from PLINK datasets. I have tested the script and it does what it is supposed to. However, I am not a professional programmer and I can not be held responsible for any damage that may occur by using this script.  
