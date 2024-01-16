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
Raw fastq files for NPCs can be found at on of the hard drives that Salvör has, called Salvor-phd2 at this location:
```
"E:\decode_230116\20230118_Fastq_files\20230116_temperature_fastq_files"
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
bamCoverage --bam control.bam -o control_depthnorm.bw -p max --binSize 5 --normalizeUsing RPGC --effectiveGenomeSize  2652783500 --ignoreForNormalization chrX --extendReads
```
