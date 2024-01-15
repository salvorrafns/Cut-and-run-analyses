# Cut-and-run-analyses

## Demultiplexing bcl files from sequencer from Decode

Here is the sample sheet we used for demultiplexing: [a relative link](20230118_AHN2FNDSX2_sample_sheet.csv)

This is the command used on Elja for demultiplexing:
```
bcl2fastq --sample-sheet 20230118_AHN2FNDSX2_sample_sheet.csv --runfolder-dir 230111_A00845_0709_AHN2FNDSX2/  -o 20230118_fastq  --ignore-missing-control --ignore-missing-positions --ignore-missing-filter
```
## Alignment and remaining processing

Here is a workflow that we used: 
[a relative link](CutandRun.html)
