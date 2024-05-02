# Factera
How to install Factera on your linux. x86_64:

First go to the https://factera.stanford.edu/download.php website and make an account.
Navigate to Download section and follow the steps:

Download factera version 1.4.4 from website.
open the terminal and type: 

cd factera/

In orderr to able to run factera you have to be sure that you installed the requirements correctly.
Requiremnets:

1. perl:
   sudo cpan Statistics::Descriptive
   It should be installed in /usr/bin/perl

2. Download hg19.bit throgh this link: https://hgdownload.cse.ucsc.edu/goldenpath/hg19/bigZips/

3. twoBitToFa suitable to your system. My system is linux (red hat) x86_64: So:
   rsync -aP rsync://hgdownload.soe.ucsc.edu/genome/admin/exe/linux.x86_64/twoBitToFa ./
   Also, add twoBitToFa to /usr/bin/
   You can download it manually also by going to website http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/ and search for twoBitToFa and click on it. 
   you can check the installation by running:
   /usr/bin/twoBitToFa hg19.2bit test.fa

4. Last, you need to install blast. Downlod the ncbi-blast-2.15.0+-3.x86_64.rpm file throgh this link https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/
   then run:
   rpm -ivh ncbi-blast-2.15.0+-3.x86_64.rpm to install it.

   after that add blastn and makeblastdb to /usr/bin/.
   In orther to be sure you installed all correctely, first you can write "whereis blastn" and it should be in /usr/bin/.
   also, when you type makeblastdb in should type sth like:

   USAGE
  makeblastdb [-h] [-help] [-in input_file] [-input_type type]
    -dbtype molecule_type [-title database_title] [-parse_seqids]
    [-hash_index] [-mask_data mask_data_files] [-mask_id mask_algo_ids]
    [-mask_desc mask_algo_descriptions] [-gi_mask]
    [-gi_mask_name gi_based_mask_names] [-out database_name]
    [-blastdb_version version] [-max_file_sz number_of_bytes]
    [-metadata_output_prefix ] [-logfile File_Name] [-taxid TaxID]
    [-taxid_map TaxIDMapFile] [-oid_masks oid_masks] [-version]

DESCRIPTION
   Application to create BLAST databases, version 2.15.0+

Use '-help' to print detailed descriptions of command line arguments
========================================================================

Error: Argument "dbtype". Mandatory value is missing:  `String, `nucl', `prot''
Error:  (CArgException::eNoArg) Argument "dbtype". Mandatory value is missing:  `String, `nucl', `prot''



When you did all, now you can sure the installation by downloading and running the example data in the website:
perl factera.pl -o test HCC78.bam exons.bed hg19.2bit targets.bed

If you get almost the same output (2 fusion), you are good to go with your own data. 
mkdir output

You need the bam files, an output directory, exons.bed which is in inside the facter folder and your target bed file. 
Keep in mind that all is for hgq9, so you need the "chr" written in bam files and bed files. 

make a text file in the factera directory which contains all your patient id. example:
sample1.bam
sample2.bam

then run these:
file=$(cat bamid.txt)
for i in $file; do echo $i; /usr/bin/perl factera.pl -o output /data/matin/BAM/chr/$i exons.bed hg19.2bit target_EXONS_chr.bed; done

Now you should see the running! bravo :)



   


   


