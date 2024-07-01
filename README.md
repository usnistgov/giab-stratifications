# GIAB Stratifications

This repository contains the pipeline and configuration used for generating and
evaluating the Genome-in-a-Bottle stratifications. The stratification files were
developed with the Global Alliance for Genomic Health (GA4GH) Benchmarking Team,
the [Genome in a Bottle Consortium
(GIAB)](https://www.nist.gov/programs-projects/genome-bottle) and the
[Telomere-to-Telomere Consortium
(T2T)](https://sites.google.com/ucsc.edu/t2tworkinggroup). They are intended as
a standard resource of BED files for use in stratifying true positive, false
positive and false negative variant calls in challenging and targeted regions of
the the genome.

The stratification BED files are only accessible on the [GIAB FTP
site](https://ftp-trace.ncbi.nlm.nih.gov/ReferenceSamples/giab/release/genome-stratifications/).
These files can be used as a standard resource of BED files for use with GA4GH
benchmark tools such as [hap.py](https://github.com/Illumina/hap.py).

Note that this pipeline applies to stratification versions starting with v3.2.
Older pipelines and scripts can be found
[here](https://github.com/genome-in-a-bottle/genome-stratifications).

Within this repository, further details (including all source files) can be
found in the configuration at `config/all.yml`. The pipeline itself is
maintained in a separate, reference agnostic repository
[here](https://github.com/usnistgov/giab-stratifications-pipeline). Please refer
to this pipeline for specific, methodological information regarding how these
files are produced.

Currently, this pipeline is set up to build stratifications for the following
references:
* GRCh37
* GRCh38
* CHM13
* HG002 (Q100 diploid assembly)

## Versioning

Version tags follow the format `X.Y-Z` where `X` will be incremented for removal
of old stratifications and/or large deletions, `Y` will be incremented for
additions and minor revisions, and `Z` will be incremented for documentation
updates in this repository. Note that `X.Y` (without `Z`) corresponds to the
versions located in [the FTP
site](https://ftp-trace.ncbi.nlm.nih.gov/ReferenceSamples/giab/release/genome-stratifications/).

For those looking for precise differences between each stratification version,
see [the stratdiff tool](https://github.com/usnistgov/giab-stratdiff).

## General Information

Author Information
- Principal Investigator: Justin Zook, NIST, jzook@nist.gov
- Nate Olson, NIST, nathanael.olson@nist.gov
- Justin Wagner, NIST, justin.wagner@nist.gov
- Jennifer McDaniel, NIST, jennifer.mcdaniel@nist.gov
- Nate Dwarshuis, NIST, nathan.dwarshuis@nist.gov

## Sharing/Access Information

Licenses/restrictions placed on the data, or limitations of reuse:
Publicly released data are freely available for reuse without embargo.

Citations for stratifications are located in the associated READMEs.

If stratifications were used in benchmarking with GA4GH/GIAB best practices or
hap.py please reference:

	Krusche, P., Trigg, L., Boutros, P.C. et al. 
	Best practices for benchmarking germline small-variant calls in human genomes. 
	Nat Biotechnol 37, 555-560 (2019). https://doi.org/10.1038/s41587-019-0054-x
    
### Links to publicly accessible locations of the data:

[GIAB FTP URL](https://ftp-trace.ncbi.nlm.nih.gov/ReferenceSamples/giab/release/genome-stratifications/)
- Individual stratification BED files as well as zipped directories (tar.gz) of files
- stratification READMEs
- .tsvs for benchmarking with hap.py
- MD5 checksums

## Summary Of Stratifications

Stratifications can be binned into several types: Low Complexity, Functional
Technically Difficult, Genome Specific, Functional Regions, GC content,
mappability, Other Difficult, Segmental Duplications, Union, Ancestry,
Telomeres, and XY. General information for stratification types are provided
below.

These categories are present for all indicated references unless otherwise
noted.

### Low Complexity

Regions with different types and sizes of low complexity sequence, e.g.,
homopolymers, STRs, VNTRs and other locally repetitive sequences.

### Segmental Duplications

Regions with segmental duplications (generally defined as repeated regions >1kb
with >90% similarity).

### XY

Chomosome XY specific regions such as PAR, XTR or ampliconic.

### Functional Regions

Regions to stratify variants inside and outside coding regions.

### GC Content

Regions with different ranges (%) of GC content.

### Mappability

Regions where short read mapping can be challenging.

### Telomeres

Telomeric regions. These are included for CHM13 only.

### Union

Regions with different general types of difficult regions or any type of
difficult region or complex variant. For example, performance can be measured in
just "easy" or "all difficult" regions of the genome.

### Ancestry

Regions with inferred patterns of local ancestry.

These only exist for GRCh38.

### Genome Specific (GIAB benchmark v4.2.1)

Difficult regions due to potentially difficult variation in a NIST/GIAB sample,
including 1) regions containing putative compound heterozygous variants 2) small
regions containing multiple phased variants, 3) regions with potential
structural or copy number variation.

These only exist for GRCh37/8.

### Functional Technically Difficult

Functional, or potentially functional, regions that are also likely to be
technically difficult to sequences.

These only exist for GRCh37/8.

### Other Difficult

These regions that are difficult to sequences for miscellaneous reasons. In the
case of GRCh37/38, these include regions near gaps or errors in the reference or
regions that are known to be expanded/collapsed relative to most other genomes.

This category also includes highly polymorphic regions such as those coding the
major histocompatibility complex (MHC), the VDJ regions, and regions coding the
killer-cell immunoglobulin-like receptor (KIR). These are all highly polymorphic
in nature and thus difficult to sequence.

Finally, in the case of CHM13, this category also includes the rDNA arrays.

## Data-Use Policy 

This data/work was created by employees of the National Institute of Standards
and Technology (NIST), an agency of the Federal Government. Pursuant to title 17
United States Code Section 105, works of NIST employees are not subject to
copyright protection in the United States. This data/work may be subject to
foreign copyright.

The data/work is provided by NIST as a public service and is expressly provided
AS IS. NIST MAKES NO WARRANTY OF ANY KIND, EXPRESS, IMPLIED OR
STATUTORY, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTY OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NON-INFRINGEMENT AND DATA
ACCURACY. NIST does not warrant or make any representations regarding the use of
the data or the results thereof, including but not limited to the correctness,
accuracy, reliability or usefulness of the data. NIST SHALL NOT BE LIABLE AND
YOU HEREBY RELEASE NIST FROM LIABILITY FOR ANY INDIRECT, CONSEQUENTIAL, SPECIAL,
OR INCIDENTAL DAMAGES (INCLUDING DAMAGES FOR LOSS OF BUSINESS PROFITS, BUSINESS
INTERRUPTION, LOSS OF BUSINESS INFORMATION, AND THE LIKE), WHETHER ARISING IN
TORT, CONTRACT, OR OTHERWISE, ARISING FROM OR RELATING TO THE DATA (OR THE USE
OF OR INABILITY TO USE THIS DATA), EVEN IF NIST HAS BEEN ADVISED OF THE
POSSIBILITY OF SUCH DAMAGES.

To the extent that NIST may hold copyright in countries other than the United
States, you are hereby granted the non-exclusive irrevocable and unconditional
right to print, publish, prepare derivative works and distribute the NIST data,
in any medium, or authorize others to do so on your behalf, on a royalty-free
basis throughout the world.

You may improve, modify, and create derivative works of the data or any portion
of the data, and you may copy and distribute such modifications or works.
Modified works should carry a notice stating that you changed the data and
should note the date and nature of any such change. Please explicitly
acknowledge the National Institute of Standards and Technology as the source of
the data: Data citation recommendations are provided at
https://www.nist.gov/open/license.

Permission to use this data is contingent upon your acceptance of the terms of
this agreement and upon your providing appropriate acknowledgments of NISTâ€™s
creation of the data/work.

## Running this pipeline

This repository's existence on Github is primarily for documentation purposes,
as the runtime is defined in terms of NIST-specific resources.

However, for those wishing to run the pipeline themselves, there are several
options. Both require cloning this repo with submodules and setting up the
conda env:

```
git clone --recurse-submodules https://github.com/usnistgov/giab-stratifications.git
cd giab-stratifications
conda env create -f env.yml
conda activate giab-strats-production
```

### No Cluster Environment

Just call the pipeline directly using snakemake:

```
snakemake --cores 20 --configfile=config/all.yml all
```

Note that most rules in the pipeline require 12MB of memory or less with the
exception of mappability (which runs GEM) and requires ~32GB for size of the
references here.

### Cluster Environment

First, create a profile from that located at
`workflow/profiles/nisaba/config.yml` (which is designed for a NIST-specific
cluster which runs Slurm).

Then run snakemake with this profile:

```
snakemake --cores 20 --configfile=config/all.yml --profile=workflow/profiles/yerprofile all
```
