# lab-notebook-GEN-711

## LAB NOTEBOOK 4-21-2023 

Made directories for github project in ron

<path to github directory>/fastp.sh <1.poly-g length> <1.path to fastq directory>  <3.path to your output directory>

made directory for fastqs
mkdir trimmed_fastqs

Chose project
/tmp/gen711_project_data/FMT_3/fmt-tutorial-demux-1

fastp.sh 150 /tmp/gen711_project_data/FMT_3/fmt-tutorial-demux-1 trimmed_fastqs
   
   cp /tmp/gen711_project_data//fastp-single.sh ~/fastp-signle.sh 
   chmod +x ~/fastp-single.sh
   ./fastp.sh 150 /tmp/gen711_project_data/FMT/fastqs trimmed_fastqs/

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
--i-data </home/mxn1000/trimmed_fastqs> \
--o-visualization  <path to an output directory>/<a name for the output files>.qzv 

absolute path
## realpath data/ref_genome/ecoli_rel606.fasta*
## realpath results/bam/SRR2584866.aligned.sorted.bam*

## run fastp for trimming
conda activate genomics

## run any of the qiime commands
conda activate qiime2-2022.8

/tmp/gen711_project_data/FMT_3/sample-metadata.tsv

cp /tmp/gen711_project_data/fastp-single.sh fastp-single.sh chmod +x <path to github directory>/fastp-single.sh




qiime dada2 denoise-single --i-demultiplexed-seqs trimmed_fastqs --p-trunc-len <trunc len> --p-trim-left 0 --p-n-threads 4 --o-denoising-stats denoising-stats.qza --o-table feature_table.qza --o-representative-sequences rep-seqs.qza

qiime metadata tabulate --m-input-file denoising-stats.qza  --o-visualization denoising-stats.qzv

qiime feature-table tabulate-seqs --i-data rep-seqs.qza --o-visualization rep-seqs.qzv

qiime feature-table merge-seqs --i-data rep-seqs.qza --i-data rep-seqs2.qza --o-merged-data merged.rep-seqs.qza

qiime feature-classifier classify-sklearn --i-classifier /tmp/gen711_project_data/reference_databases/classifier.qza --i-reads merged.rep-seqs.qza --o-classification FMT-taxonomy.qza

qiime taxa barplot --i-table feature_table.qza --i-taxonomy FMT-taxonomy.qza --o-visualization barplot-1.qzv

qiime taxa barplot --i-table feature_table2.qza --i-taxonomy FMT-taxonomy.qza --o-visualization barplot-2.qzv

qiime taxa barplot --i-table feature_table.qza --m-metadata-file sample-metadata.tsv --i-taxonomy FMT-taxonomy.qza --o-visualization my-barplot.qzv





















