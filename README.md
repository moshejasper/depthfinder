This is a test package to examine read depth code functions (see src/depthfinder).

To install run the command: 

`python -m pip install "depthfinder @ git+https://github.com/moshejasper/depthfinder.git"`

Then adapt the supplied `example.py` script to run on an appropriate `.vcf` file


## Example Usage ##


```
# setup

from depthfinder import depthfinder as dpf

vcf_files = ["my_vcf",] # suffix currently assumed to be ".vcf.gz" - would make more robust if needed... also presumes list of files

outname = "test_standard_depths"

dpf.get_depth_outliers_parallel(
    fixlist=vcf_files,              # list of vcf file prefixes (.vcf.gz)
    outfix=outname,                 # prefix of outfiles (for R processing)
    window=10_000,                  # genome window size
    n_jobs=1,                       # how many parallel threads to use
    min_miss_frac=0.5,              # ignore sites with more than 0.xx missing data (higher = more missing)
    threshold_frac = 0.05,          # proportion of samples lying outside confidence intervals to flag window (must be at least this amount above and/or at least this amount below)
    alpha = dpf.alpha_from_sd(2),   # alpha for confidence intervals - here scaled to align with prior paper i.e. alpha corresponding to mean +/- 2xSD
    min_sites=1000,                 # window must have at least X usable sites to process
    window_depth_thresh=5,          # window must have mean/median depth >= this to process
    use_median=False,               # if True, use median/absolute deviation, if False, use mean/standard deviation (default & aligns with prior work)
    min_spread=0.01,                # if deviation is 0, increase to this as bare minimum
    transform="none",               # whether to rescale 'normalized' means before calculation 'none' (default) or alternately 'sqrt' or 'log' (affects confidence interval distributions)
    write=True                      # whether to write output files
)




```
