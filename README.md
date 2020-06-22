## FastQTL

This repository contains a modified version of the [FastQTL](http://fastqtl.sourceforge.net/) QTL mapping software, with the following enhancements:

1. Options for filtering by minor allele frequency and minor allele sample count
2. Python wrapper for multi-threaded execution
3. Calculation of q-values (Storey) for FDR estimation (requires R)
4. Minor allele information reported in output

For documentation and the original version, see: http://fastqtl.sourceforge.net/

#### Running multi-threaded analyses

Nominal pass:
```bash
run_FastQTL_threaded.py ${genotypes}.vcf.gz ${phenotypes}.bed.gz ${prefix} --covariates ${covariates}.txt.gz --window 1e6 --ma_sample_threshold 10 --maf_threshold 0.01 --chunks 100 --threads 10
```
Permutation pass:
```bash
run_FastQTL_threaded.py ${genotypes}.vcf.gz ${phenotypes}.bed.gz ${prefix} --covariates ${covariates}.txt.gz --permute 1000 10000 --window 1e6 --ma_sample_threshold 10 --maf_threshold 0.01 --chunks 100 --threads 10
```
These minor allele filters result in inclusion of genotypes with minor allele frequency ≥ 0.01 and with at least 10 samples containing the minor allele.

## Output format (header of the columns)
Check [here](Options_list.txt) for full options.

## Output format (header of the columns)
Nominal pass:
```
'phynotype_id', 'variant_id', 'geno_phyno_distance', 'ma_samples', 'ma_count', 'maf', 'pval_nominal', 'slope', 'slope_se'
```

Permutation pass:
```
'phynotype_id', 'num_var', 'beta_shape1', 'beta_shape2', 'true_df', 'pval_true_df',
            'variant_id', 'geno_phyno_distance', 'ma_samples', 'ma_count', 'maf', 'ref_factor',
            'pval_nominal', 'slope', 'slope_se', 'pval_perm', 'pval_beta'
```
