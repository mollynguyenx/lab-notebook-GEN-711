# lab-notebook-GEN-711

## LAB NOTEBOOK 4-21-2023 

Made directories for github project in ron

<path to github directory>/fastp.sh <1.poly-g length> <1.path to fastq directory>  <3.path to your output directory>

made directory for fastqs
mkdir trimmed_fastqs

Chose project
/tmp/gen711_project_data/FMT_3/fmt-tutorial-demux-1

fastp.sh 150 /tmp/gen711_project_data/FMT_3/fmt-tutorial-demux-1 trimmed_fastqs

waiting for joe to fix whatever he messed up so now we just write commands 

cp /tmp/gen711_project_data/fastp-single.sh ~/fastp-signle.sh

./fastp-signle.sh 150 /tmp/gen_711_project_data/FMT/fastqs trimmmed_fastqs/

qiime tools import \
   --type "SampleData[PairedEndSequencesWithQuality]"  \
   --input-format CasavaOneEightSingleLanePerSampleDirFmt \
   --input-path <trimmed_fastqs> \
   --output-path </home/mxn1000/trimmed_fastqs>/<trimmed_fastqs> \
   
   qiime cutadapt trim-paired \
    --i-demultiplexed-sequences <path to the file from step 2> \
    --p-cores 4 \
    --p-front-f <TACGTATGGTGCA> \
    --p-front-r <> \
    --p-discard-untrimmed \
    --p-match-adapter-wildcards \
    --verbose \
    --o-trimmed-sequences <path to an output directory>/<name for the output files>.qza

qiime demux summarize \
--i-data <path to the file from step above> \
--o-visualization  <path to an output directory>/<a name for the output files>.qzv 

