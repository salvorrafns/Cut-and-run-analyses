# Cut-and-run-analyses

## Demultiplexing bcl files from sequencer from Decode

Here is the sample sheet we used for demultiplexing: [sample sheet](20230118_AHN2FNDSX2_sample_sheet.csv)

This is the command used on Elja for demultiplexing:
```
bcl2fastq --sample-sheet 20230118_AHN2FNDSX2_sample_sheet.csv --runfolder-dir 230111_A00845_0709_AHN2FNDSX2/  -o 20230118_fastq  --ignore-missing-control --ignore-missing-positions --ignore-missing-filter
```
## Raw data location:

Raw data can be found on Elja at this location:
```
/hpcdata/Mimir/kimberl/20230116_Decode_CutandRun_decode_230116/20230118_fastq/20230116_temperature_cutandrun
```
Fastq-files for NPC, all rep (missing NPC_rep1_H3K36_32 /[]_37), are located on the Salvor_phd2 hard drive at the location:
```
/decode_230116/20230118_Fastq_files/20230116_temperature_fastq_files
```
NPC rep 3 and 4 were excluded as Sara did IF staining and most of the cells in NPC rep 3 and 4 were astrocytes. Fastq-files for HEK293, all reps, and NPC, rep 3 and 4m are located on the Salvor_phd2 hard drive at the location:
```
/20230116_temperature_cutandrun/20230116_temperature_fastq_files
```
Fastq-files for NPC, NPC_rep1_H3K36_32 /[]_37, canbe found at Salvor_phd2 hard drive at the location:
```
/geo_submission_june_smyd5/cut&run
```

## Alignment and remaining processing

Here is a workflow that we used: 
(https://kimberleya.github.io/Cut-and-run-analyses/analysis)

## Creating bigWig files 

Making bigWig files normalised to genome coverage for visualising with UCSC browser or some other tool. You can do something like this using samTools and deepTools:

```
#Making bigWig files from bam files for visualisation on genome browser, normalised to 1x coverage of mouse genome
#First we need to index our merged bam files
samtools index SMYD5_FLAG_merge.bam
bamCoverage --bam SMYD5_FLAG_merge.bam -o SMYD5_FLAG_merge_depthnorm.bw -p max --binSize 5 --normalizeUsing RPGC --effectiveGenomeSize  2652783500 --ignoreForNormalization chrX --extendReads

samtools index control.bam
bamCoverage --bam control.bam -o control_depthnorm.bw -p max --binSize 5 --normalizeUsing RPGC --effectiveGenomeSize  2652783500 --ignoreForNormalization chrX --extendReads #RPCG normalized
bamCoverage --bam [filename].bam -o [filename]_ecoli.bw --binSize 5  --scaleFactor [1/%E.Coli aligned reads of total reads in BAM file] --numberOfProcessors 64 # E.coli normalized
```
## Merge the e. coli normalized bigwig files 
Using bigWigMerge from UCSC tools for visualization for the figures 
see: https://www.biostars.org/p/209443/
```
```

## MACS3 peak calling
Followed protocol: https://macs3-project.github.io/MACS/docs/callpeak.html

Preprocessing
1. Filter out all duplicates, for all files: H3K36me3, SMYD5 and IgG
2. 
```
macs3 filterdup -i NPC_rep1_32_H3K36_S48.bam --keep-dup=1 -o NPC_rep1_32_H3K36_filterdup.bam

```
