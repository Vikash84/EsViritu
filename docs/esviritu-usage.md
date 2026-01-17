
# Optional helpers
mamba install -n EsViritu -c bioconda filtlong porechop -y

# (Recommended) regenerate ONT index
minimap2 -d virus_db_ont.mmi virus_pathogen_database.fna   # ONT-friendly index build  [9](https://lh3.github.io/minimap2/minimap2.html)

# Run in ONT mode
EsViritu \
  --platform ont \
  -r sample.fastq.gz \
  -s S1 \
  -o out_dir \
  -q True -f True \
  --filter_db filter_seqs/filter_seqs.fna \
  --ont-preset map-ont \
  --ont-min-len 500 --ont-min-prop 0.60 --ont-min-acc 0.75 \
  -p unpaired -t 8
