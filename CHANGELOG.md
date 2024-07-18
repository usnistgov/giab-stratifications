All updates are summarized here. For exact versions and provenance information,
see the configuration file at `config/all.yml`.

# 3.5

## NEW - Better READMEs

Versions since 3.1 had relatively little documentation. 

This version adds both top-level readmes for each reference as well as
stratification level readmes to explain the meaning of each bed file and how
they were generated. Provenance information for all source files is also
captured in these readmes (including urls and hashes).

## NEW - BigBeds Now Included

BedBed versions of each stratification are now included. The .bb version can be
found next to its corresponding .bed.gz file in each stratification directory.

The .bb files are also denoted in `<ref>-all-bb-stratifications.tsv`, and they
are separately tarballed in `genome-stratifications-bb-<ref>.tar.gz`.

## NEW - Smaller HG002 Diploid Het/Hom distances

In the previous release, each of the diploid het/hom region bed files was
created with relatively large region sizes on either side (meaning the distance
from a het was relatively large for these regions). The distances we used were
5,000-100,000bp.

In this release we added shorter distances, with the intended use case being to
identify regions for which a short(ish) read would be able to (or not) map to
the correct haplotype. The distances added to create these were 100, 250, 500,
and 1000 base pairs which reflect some common short read lengths as well as
insert sizes.

This created the following new bed files:

* `HG002.X_het_regions_100.bed.gz`
* `HG002.X_het_regions_250.bed.gz`
* `HG002.X_het_regions_500.bed.gz`
* `HG002.X_het_regions_1000.bed.gz`
* `HG002.X_het_SNVorSV_regions_100.bed.gz`
* `HG002.X_het_SNVorSV_regions_250.bed.gz`
* `HG002.X_het_SNVorSV_regions_500.bed.gz`
* `HG002.X_het_SNVorSV_regions_1000.bed.gz`
* `HG002.X_hom_regions_100.bed.gz`
* `HG002.X_hom_regions_250.bed.gz`
* `HG002.X_hom_regions_500.bed.gz`
* `HG002.X_hom_regions_1000.bed.gz`
* `HG002.X_hom_SNVorSV_regions_100.bed.gz`
* `HG002.X_hom_SNVorSV_regions_250.bed.gz`
* `HG002.X_hom_SNVorSV_regions_500.bed.gz`
* `HG002.X_hom_SNVorSV_regions_1000.bed.gz`

where `X` denotes `pat` or `mat` (see below for new naming conventions)

## Other Changes

### CHM13 with masked Y PAR

GRCh37/38 both have the Y PAR masked (filled with Ns) to reflect the fact that
this region behaves like a diploid region in a haploid reference. Previous
stratifications used the unmasked CHM13 reference; this version uses the masked
reference to standardize it with GRCh37/38.

This slightly altered nearly all the stratifications (basically anything with
regions on the Y chromosome). Full changes can be found in
`validation/CHM13@all`.

### Diploid Naming Convention

Rather than use "hap1" and "hap2" we now use "pat" and "mat" respectively which
will be more clear to users.

### Off-by-one errors

Some stratifications (such as those in `Functional`) were created from GFF files
which are 1-indexed. In previous versions the GFF file was treated as 0-indexed,
which led to each stratification being shifted to 3' 1 base pair. This has been
fixed, and the following stratifications were affected (for each ref):

* `Functional/GRCh37_notinrefseq_cds.bed.gz`
* `Functional/GRCh37_refseq_cds.bed.gz`
* `OtherDifficult/GRCh37_VDJ.bed.gz`
* `Functional/GRCh38_notinrefseq_cds.bed.gz`
* `Functional/GRCh38_refseq_cds.bed.gz`
* `OtherDifficult/GRCh38_VDJ.bed.gz`
* `Functional/CHM13_notinrefseq_cds.bed.gz`
* `Functional/CHM13_refseq_cds.bed.gz`
* `OtherDifficult/CHM13_VDJ.bed.gz`

### GenomeSpecific Name Correction (GRCh37/38 only)

This:

`GRCh3X_HG00Y_v4.2.1_snpswithin10bp_slop50.bed.gz`

was renamed to:

`GRCh3X_HG00Y_v4.2.1_complexsnp10bp_slop50.bed.gz`

for GRCh37/38 and HG001-HG007

This name change better reflects what this file represents and keeps
nomenclature consistent.

# 3.4

## NEW - HG002 Diploid Stratifications

The major addition to this update is the inclusion of stratifications for
the HG002 T2T Q100 assemblies. Since this is a diploid assembly, two sets of
stratifications for each haplotype are included in two separate directories.
`HG002.hap1` corresponds to paternal and `HG002.hap2` corresponds to maternal.
The stratifications in each of these are analogous to those for the three
previous haploid references.

Additionally, HG002 includes a new groups of
stratifications under the `Diploid` directory which includes the following
(where `X` is either `1` or `2`):

* `Diploid/HG002.hapX_het_regions_5k.bed.gz`
* `Diploid/HG002.hapX_het_regions_10k.bed.gz`
* `Diploid/HG002.hapX_het_regions_25k.bed.gz`
* `Diploid/HG002.hapX_het_regions_50k.bed.gz`
* `Diploid/HG002.hapX_het_regions_100k.bed.gz`
* `Diploid/HG002.hapX_het_SNVorSV_regions_5k.bed.gz`
* `Diploid/HG002.hapX_het_SNVorSV_regions_10k.bed.gz`
* `Diploid/HG002.hapX_het_SNVorSV_regions_25k.bed.gz`
* `Diploid/HG002.hapX_het_SNVorSV_regions_50k.bed.gz`
* `Diploid/HG002.hapX_het_SNVorSV_regions_100k.bed.gz`
* `Diploid/HG002.hapX_hom_regions_5k.bed.gz`
* `Diploid/HG002.hapX_hom_regions_10k.bed.gz`
* `Diploid/HG002.hapX_hom_regions_25k.bed.gz`
* `Diploid/HG002.hapX_hom_regions_50k.bed.gz`
* `Diploid/HG002.hapX_hom_regions_100k.bed.gz`
* `Diploid/HG002.hapX_hom_SNVorSV_regions_5k.bed.gz`
* `Diploid/HG002.hapX_hom_SNVorSV_regions_10k.bed.gz`
* `Diploid/HG002.hapX_hom_SNVorSV_regions_25k.bed.gz`
* `Diploid/HG002.hapX_hom_SNVorSV_regions_50k.bed.gz`
* `Diploid/HG002.hapX_hom_SNVorSV_regions_100k.bed.gz`

The `het` bed files cover regions that are within k base pairs of a het variant
relative to the other haplotype. The `het_SNVorSV` bed files are a subtype of
this which only considers SNV or SV (>50bp variants or alignment breaks)
variants. These may be useful for troubleshooting assembly errors which use SNVs
or SVs for phasing.

To be more concrete, the `HG002.hap1_het_regions_10k` file includes regions that
are within 10 kb of a SNV, INDEL, or SV on hap1 (paternal) relative to hap2
(paternal).

The `hom` bed files are simply complements of the analogous `het` bed files.

## CHM13, GRCh38, GRCh38

These assemblies received no major updates in this release. 

Mappabilty and union changed slightly due to the non-determinism in GEM. This
resulted in at most ~200 base pairs being changed depending on the reference.
This affected the following bed files:

* `Mappability/<ref>_lowmappabilityall.bed.gz`
* `Mappability/<ref>_nonunique_l100_m2_e1.bed.gz`
* `Mappability/<ref>_notinlowmappabilityall.bed.gz`
* `Union/<ref>_alllowmapandsegdupregions.bed.gz`
* `Union/<ref>_notinalllowmapandsegdupregions.bed.gz`

Additionally, the GFF files used to create the refseq CDS region files received
updates in late 2023, resulting in the following gains to
`Functional/<ref>_refseq_cds.bed.gz` (and equal corresponding loss in
`Functional/<ref>_notinrefseq_cds.bed.gz`) for each of the three references:

* GRCh37: -134 bp
* GRCh38: -128 bp
* CHM13: 164651 bp

# 3.3

## Small fixes

- Fixed minor bugs relating to tarball structure
- Fixed bug that prevent validation files from uploading

## Stratification updates

Only CHM13 was changed in this release.

### Low complexity

Low complexity inputs ([repeat
masker](https://hgdownload.soe.ucsc.edu/gbdb/hs1/t2tRepeatMasker/chm13v2.0_rmsk.bb),
[simple repeats](https://hgdownload.soe.ucsc.edu/gbdb/hs1/bbi/simpleRepeat.bb),
and [censat](https://hgdownload.soe.ucsc.edu/gbdb/hs1/censat/censat.bb)) are now
sourced from UCSC tracks.

In summary this vastly expanded the size of many of the low complexity
stratifications in terms of coverage (in some cases by 3x). See the comparison
b/t 3.2 and 3.3 under `validation/CHM13/diagnostics.tsv` for the exact changes.
Some of these stratitifications also removed a few existing regions, but this
was miniscule compared to what was added.

Affected stratifications:

* `LowComplexity/CHM13_AllTandemRepeats.bed.gz`
* `LowComplexity/CHM13_AllTandemRepeats_201to10000bp_slop5.bed.gz`
* `LowComplexity/CHM13_AllTandemRepeats_51to200bp_slop5.bed.gz`
* `LowComplexity/CHM13_AllTandemRepeats_ge10001bp_slop5.bed.gz`
* `LowComplexity/CHM13_AllTandemRepeats_ge101bp_slop5.bed.gz`
* `LowComplexity/CHM13_AllTandemRepeats_le50bp_slop5.bed.gz`
* `LowComplexity/CHM13_AllTandemRepeatsandHomopolymers_slop5.bed.gz`
* `LowComplexity/CHM13_notinAllTandemRepeatsandHomopolymers_slop5.bed.gz`
* `LowComplexity/CHM13_notinallTandemRepeats.bed.gz`

Additionally, these union stratifications inherited the expansions to the
low complexity regions above:

`Union/CHM13_alldifficultregions.bed.gz`
`Union/CHM13_notinalldifficultregions.bed.gz`

### Mappability

Some mappability stratifications (and the union stratifications that depend on
them) changed slightly due to non-determinism in GEM. These changes are
miniscule and amount to several hundred bases total. They are documented here
for completion:

* `Mappability/CHM13_lowmappabilityall.bed.gz`
* `Mappability/CHM13_nonunique_l100_m2_e1.bed.gz`
* `Mappability/CHM13_notinlowmappabilityall.bed.gz`
* `Union/CHM13_alllowmapandsegdupregions.bed.gz`
* `Union/CHM13_notinalllowmapandsegdupregions.bed.gz`

# 3.2


### Changes to naming convention

For all strats and references, the naming convention was updated (and files
presented in subsequent sections are in terms of the new names).

* all directory names are now capitalized for consistency
* `FunctionalTechnicallyDifficultRegions` was shortened to
  `FunctionalTechnicallyDifficult`
* `FunctionalRegions` was shortened to `Functional`
* `LowComplexity` base pair lengths are now more consistent. Specifically,
  `XtoY` now means "X through Y" (this meaning was not consistent previously)
  and `geX` now means "greater than or equal to X" (before it said `gtX` which
  gave the erroneous impression that this length did not include `X`)
* (CHM13 only) - each stratification file now is prefixed with `CHM13` rather
  than `CHM13v2.0` for simplicity.
* (CHM13 only) - `SegDups` in the segmental duplications strats was lowercased
  to `segdups` to be consistent with the other references.

### Additions

#### Low Complexity

Homopolymer stratifications now have GC or AT-only analogues:

* `LowComplexity/*_SimpleRepeat_homopolymer_4to6_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_4to6_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_7to11_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_7to11_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_ge12_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_ge12_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_ge21_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_homopolymer_ge21_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_imperfecthomopolge11_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_imperfecthomopolge11_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_imperfecthomopolge21_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_imperfecthomopolge21_GC_slop5.bed.gz`

#### Telomeres (CHM13 only)

CHM13 now has a telomeres stratification:

* `Telomeres/CHM13_telomeres.bed.gz`

#### Functional, GCcontent, Mappability (CHM13 only)

CHM13 now has these stratifications analogously to GRCh37/38:

* `Functional/CHM13_notinrefseq_cds.bed.gz`
* `Functional/CHM13_refseq_cds.bed.gz`

* `GCcontent/CHM13_gc15_slop50.bed.gz`
* `GCcontent/CHM13_gc15to20_slop50.bed.gz`
* `GCcontent/CHM13_gc20to25_slop50.bed.gz`
* `GCcontent/CHM13_gc25to30_slop50.bed.gz`
* `GCcontent/CHM13_gc30to55_slop50.bed.gz`
* `GCcontent/CHM13_gc55to60_slop50.bed.gz`
* `GCcontent/CHM13_gc60to65_slop50.bed.gz`
* `GCcontent/CHM13_gc65to70_slop50.bed.gz`
* `GCcontent/CHM13_gc70to75_slop50.bed.gz`
* `GCcontent/CHM13_gc75to80_slop50.bed.gz`
* `GCcontent/CHM13_gc80to85_slop50.bed.gz`
* `GCcontent/CHM13_gc85_slop50.bed.gz`
* `GCcontent/CHM13_gclt25orgt65_slop50.bed.gz`
* `GCcontent/CHM13_gclt30orgt55_slop50.bed.gz`

* `Mappability/CHM13_lowmappabilityall.bed.gz`
* `Mappability/CHM13_nonunique_l100_m2_e1.bed.gz`
* `Mappability/CHM13_nonunique_l250_m0_e0.bed.gz`
* `Mappability/CHM13_notinlowmappabilityall.bed.gz`

#### Other Difficult (CHM13 only)

These stratifications were lifted from GRCh38 onto the CHM13 assembly and are
now included:

* `OtherDifficult/CHM13_KIR.bed.gz`
* `OtherDifficult/CHM13_MHC.bed.gz`
* `OtherDifficult/CHM13_VDJ.bed.gz`

Note that the VDJ strats were made using the refseq annotations as updated for
the other references (see below).

### Removals

#### Segmental duplications

Self chain stratifications were removed from both GRCh37 and GRCh38:

* `SegmentalDuplications/*_chainSelf.bed.gz`
* `SegmentalDuplications/*_chainSelf_gt10kb.bed.gz`
* `SegmentalDuplications/*_notinchainSelf.bed.gz`
* `SegmentalDuplications/*_notinchainSelf_gt10kb.bed.gz`

Additionally, the 99 percent identity file was removed:

* `SegmentalDuplications/*_gt5segdups_gt10kb_gt99percidentity.bed.gz`

### Revisions to regions

#### All references

##### Low Complexity

For low complexity stratifications, the di/tri/quad simple repeat
stratifications are now constructed with an upper limit of 150bp in the highest
bracket instead of 200bp. This was to better match a common short-read length
(150bp) and to include more meaningful regions, as some of these stratifications
were totally empty with the previous upper limit.

Affected files:

* `LowComplexity/*_SimpleRepeat_diTR_50to149_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_diTR_50to149_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_diTR_50to149_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_quadTR_50to149_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_quadTR_50to149_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_quadTR_50to149_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_triTR_50to149_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_triTR_50to149_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_triTR_50to149_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_diTR_ge150_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_diTR_ge150_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_diTR_ge150_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_quadTR_ge150_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_quadTR_ge150_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_quadTR_ge150_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_triTR_ge150_AT_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_triTR_ge150_GC_slop5.bed.gz`
* `LowComplexity/*_SimpleRepeat_triTR_ge150_slop5.bed.g`

##### VDJ

The VDJ stratifications are now created using the refseq annotations. Note that
for CHM13 this is a totally new stratification, and for the other references
this replaces the previous version.

Furthermore, the old VDJ stratifications for GRCh37/38 did not include the three
T cell loci on chromosomes 7 (2 loci) and 14 (1 locus). These were also added.

#### GRCh37

##### Updated source file versions

Functional regions were updated with the latest feature table and GFF files from
refseq. This resulted in minor changes to the boundaries of these regions:

* `Functional/GRCh37_notinrefseq_cds.bed.gz`
* `Functional/GRCh37_refseq_cds.bed.gz`

Segmental duplications were made using a more updated version of the superdups
database from UCSC. This also resulted in minor boundary changes:

* `SegmentalDuplications/GRCh37_notinsegdups.bed.gz`
* `SegmentalDuplications/GRCh37_notinsegdups_gt10kb.bed.gz`
* `SegmentalDuplications/GRCh37_segdups.bed.gz`
* `SegmentalDuplications/GRCh37_segdups_gt10kb.bed.gz`

##### Mappability

Previous mappability files were constructed with a slightly different reference
(with different decoy regions) and possibly without merging nearby regions with
`mergeBed ... -d 100`. This resulted in ~1.5% and ~17.0% increases in the number
of covered bases in `l250_m0_e0` and `l100_m2_e1` in v3.2 vs 3.1.

Affected files:

* `Mappability/GRCh37_lowmappabilityall.bed.gz`
* `Mappability/GRCh37_nonunique_l100_m2_e1.bed.gz`
* `Mappability/GRCh37_nonunique_l250_m0_e0.bed.gz`
* `Mappability/GRCh37_notinlowmappabilityall.bed.gz`

##### Union

These stratifications changed slightly since they are aggregated from GCcontent,
SegDup, and Mappability strats. Affected files:

* `Union/GRCh37_alldifficultregions.bed.gz`
* `Union/GRCh37_alllowmapandsegdupregions.bed.gz`
* `Union/GRCh37_notinalldifficultregions.bed.gz`
* `Union/GRCh37_notinalllowmapandsegdupregions.bed.gz`

##### Gaps

The gaps stratification is now made from the gaps track from UCSC. Unlike the
previous gaps source file, this no longer includes small (sometimes single bp)
gaps, nor does it include centromeres. For the latter we provide the `satellite`
stratification file from `LowComplexity`.

Affected file:

* `OtherDifficult/GRCh37_gaps_slop15kb.bed.gz`

##### Correcting missing slop

Low complexity homopolymers were originally created without adding slop (despite
the filename). This has been corrected. As a consequence, some regions are now
in different length brackets, since length was computed before as if slop were
already added. Affected files:

* `LowComplexity/GRCh37_AllTandemRepeats_201to10000bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_51to200bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeatsandHomopolymers_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_ge10001bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_ge101bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_le50bp_slop5.bed.gz`
* `LowComplexity/GRCh37_notinAllTandemRepeatsandHomopolymers_slop5.bed.gz`
* `LowComplexity/GRCh37_notinallTandemRepeats.bed.gz`

##### X Chromosome

The PAR and XTR regions were updated since v3.1. Affected files:

* `XY/GRCh37_chrX_nonPAR.bed.gz`
* `XY/GRCh37_chrX_PAR.bed.gz`
* `XY/GRCh37_chrX_XTR.bed.gz`

##### Changes to Y pseudoautosomal region

The boundaries of the PAR on the Y chromosome was updated since v3.1. This
affected both the Y PAR-specific stratifications themselves as well as any other
stratifications that intersected with the old/new PAR regions (for most
stratifications we subtract off the Y PAR).

Affected XY stratifications:

* `XY/GRCh37_chrY_nonPAR.bed.gz`
* `XY/GRCh37_chrY_PAR.bed.g`

Affected non-XY stratifications:

* `GCcontent/GRCh37_gc15to20_slop50.bed.gz`
* `GCcontent/GRCh37_gc20to25_slop50.bed.gz`
* `GCcontent/GRCh37_gc25to30_slop50.bed.gz`
* `GCcontent/GRCh37_gc30to55_slop50.bed.gz`
* `GCcontent/GRCh37_gc55to60_slop50.bed.gz`
* `GCcontent/GRCh37_gc60to65_slop50.bed.gz`
* `GCcontent/GRCh37_gc65to70_slop50.bed.gz`
* `GCcontent/GRCh37_gclt25orgt65_slop50.bed.gz`
* `GCcontent/GRCh37_gclt30orgt55_slop50.bed.gz`
* `GenomeSpecific/GRCh37_HG001_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG001_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG002_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG002_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG003_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG003_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG004_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG004_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG005_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG005_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG006_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG006_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG007_v4.2.1_complexandSVs_alldifficultregions.bed.gz`
* `GenomeSpecific/GRCh37_HG007_v4.2.1_notin_complexandSVs_alldifficultregions.bed.gz`
* `LowComplexity/GRCh37_AllHomopolymers_ge7bp_imperfectge11bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_201to10000bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_51to200bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeatsandHomopolymers_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_ge10001bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_ge101bp_slop5.bed.gz`
* `LowComplexity/GRCh37_AllTandemRepeats_le50bp_slop5.bed.gz`
* `LowComplexity/GRCh37_notinAllHomopolymers_ge7bp_imperfectge11bp_slop5.bed.gz`
* `LowComplexity/GRCh37_notinAllTandemRepeatsandHomopolymers_slop5.bed.gz`
* `LowComplexity/GRCh37_notinallTandemRepeats.bed.gz`
* `LowComplexity/GRCh37_notinsatellites_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_diTR_10to49_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_homopolymer_4to6_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_homopolymer_7to11_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_homopolymer_ge12_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_homopolymer_ge21_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_imperfecthomopolge11_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_imperfecthomopolge21_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_quadTR_19to49_slop5.bed.gz`
* `LowComplexity/GRCh37_SimpleRepeat_triTR_14to49_slop5.bed.gz`
* `Mappability/GRCh37_lowmappabilityall.bed.gz`
* `Mappability/GRCh37_nonunique_l100_m2_e1.bed.gz`
* `Mappability/GRCh37_nonunique_l250_m0_e0.bed.gz`
* `Mappability/GRCh37_notinlowmappabilityall.bed.gz`
* `OtherDifficult/GRCh37_allOtherDifficultregions.bed.gz`
* `OtherDifficult/GRCh37_gaps_slop15kb.bed.gz`
* `OtherDifficult/GRCh37_hg38_minimap2_asm20_N10_nocovgt1kb.bed.gz`
* `OtherDifficult/GRCh37_hs37d5_decoy_alignments.bed.gz`
* `SegmentalDuplications/GRCh37_notinsegdups.bed.gz`
* `SegmentalDuplications/GRCh37_notinsegdups_gt10kb.bed.gz`
* `SegmentalDuplications/GRCh37_segdups.bed.gz`
* `SegmentalDuplications/GRCh37_segdups_gt10kb.bed.gz`
* `Union_GRCh37/alldifficultregions.bed.gz`
* `Union_GRCh37/alllowmapandsegdupregions.bed.gz`
* `Union_GRCh37/notinalldifficultregions.bed.gz`
* `Union_GRCh37/notinalllowmapandsegdupregions.bed.gz`

#### GRCh38

##### Updated source file versions

Functional regions and segmental duplications now use updated source files
(analogously to GRCh37, see above). Affected files:

* `Functional/GRCh38_notinrefseq_cds.bed.gz`
* `Functional/GRCh38_refseq_cds.bed.gz`
* `SegmentalDuplications/GRCh38_notinsegdups.bed.gz`
* `SegmentalDuplications/GRCh38_notinsegdups_gt10kb.bed.gz`
* `SegmentalDuplications/GRCh38_segdups.bed.gz`
* `SegmentalDuplications/GRCh38_segdups_gt10kb.bed.gz`

##### Mappability

Very minor changes (~400bp total) occurred b/t v3.1 and v3.2 due to not including
the EBV alternative contig in the newer pass. Affected files:

* `Mappability/GRCh38_lowmappabilityall.bed.gz`
* `Mappability/GRCh38_nonunique_l100_m2_e1.bed.gz`
* `Mappability/GRCh38_nonunique_l250_m0_e0.bed.gz`
* `Mappability/GRCh38_notinlowmappabilityall.bed.gz`

##### Union

Changes to mappability and segmental duplications strats affected the union
strats (which are aggregated from the former). Affected files:

* `Union_GRCh38_alldifficultregions.bed.gz`
* `Union_GRCh38_alllowmapandsegdupregions.bed.gz`
* `Union_GRCh38_notinalldifficultregions.bed.gz`
* `Union_GRCh38_notinalllowmapandsegdupregions.bed.gz`

##### Gaps

The gaps file was updated analogously to GRCh37 (see above). Affected file:

* `OtherDifficult/GRCh38_gaps_slop15kb.bed.gz`

#### CHM13

Segmental duplications are now created using the
[SEDEF](https://genome.ucsc.edu/cgi-bin/hgTables?db=hub_3671779_hs1&hgta_group=varRep&hgta_track=hub_3671779_sedefSegDups&hgta_table=hub_3671779_sedefSegDups&hgta_doSchema=describe+table+schema)
track from UCSC. Affected stratifications:

* `SegmentalDuplications/CHM13_notinsegdups.bed.gz`
* `SegmentalDuplications/CHM13_segdups.bed.gz`

The existing `Union` stratifications have been revised to incorporate
new mappability stratifications. Affected files:

* `Union/CHM13_alldifficultregions.bed.gz`
* `Union/CHM13_notinalldifficultregions.bed.gz`

# Pre v3.1 Releases

## 3.1 - 2022-07-08

### New Stratifications

All stratifications for CHM13v2.0 new and include stratifications for:

- Union
- LowComplexity
- SegmentalDuplications
- XY
- OtherDifficult

LowComplexity

- added satellite regions and union of all tandem repeats
    - GRCh3X_satellites.bed.gz
    - GRCh3X_notinsatellites.bed.gz
    - GRCh3X_allTandemRepeats.bed.gz
    - GRCh3X_notinallTandemRepeats.bed.gz

XY

- Added regions specific to chromosomes X and Y.
    - GRCh3X_allTandemRepeats.bed.gz
    - GRCh3X_notinallTandemRepeats.bed.gz
    - GRCh3X_AllAutosomes.bed.gz
    - GRCh3X_chrX_PAR.bed.gz
    - GRCh3X_chrX_ampliconic.bed.gz
    - GRCh3X_chrX_XTR.bed.gz
    - GRCh3X_chrX_nonPAR.bed.gz
    - GRCh3X_chrY_PAR.bed.gz
    - GRCh3X_chrY_ampliconic.bed.gz
    - GRCh3X_chrY_XTR.bed.gz
    - GRCh3X_chrY_nonPAR.bed.gz
	
### Revised Stratifications

LowComplexity
- The following LowComplexity stratifications were revised for both GRCh37 and
  GRCh38 to to include satellite regions
    - GRCh3X_AllTandemRepeats_201to10000bp_slop5.bed.gz
    - GRCh3X_AllTandemRepeats_51to200bp_slop5.bed.gz
    - GRCh3X_AllTandemRepeats_gt10000bp_slop5.bed.gz
    - GRCh3X_AllTandemRepeats_gt100bp_slop5.bed.gz
    - GRCh3X_AllTandemRepeats_lt51bp_slop5.bed.gz
    - GRCh3X_AllTandemRepeatsandHomopolymers_slop5.bed.gz
    - GRCh3X_notinAllTandemRepeatsandHomopolymers_slop5.bed.gz
    - All other LowComplexity stratifications were regenerated as part of code in
    - new GRCh3X_LowComplexity.ipynb however are unchanged.

Segmental Duplications
- PAR-X was found to be incorrectly annotated in the following files and
  therefore PAR-X regions removed from these files.
    - GRCh38_chainSelf.bed.gz
    - GRCh38_chainSelf_gt10kb.bed.gz
    - GRCh38_notinchainSelf.bed.gz
    - GRCh38_notinchainSelf_gt10kb.bed.gz
    - GRCh37_chainSelf.bed.gz
    - GRCh37_chainSelf_gt10kb.bed.gz
    - GRCh37_notinchainSelf.bed.gz
    - GRCh37_notinchainSelf_gt10kb.bed.gz
    - GRCh37_notinsegdups.bed.gz
    - GRCh37_notinsegdups_gt10kb.bed.gz
    - GRCh37_segdups.bed.gz
    - GRCh37_segdups_gt10kb.bed.gz
	
Union
- The following Union stratifications were revised for both GRCh37 and GRCh38 to
  include satellites, chrX/Y XTR and ampliconic regions.
    - GRCh38_alldifficultregions.bed.gz
    - GRCh38_notinalldifficultregions.bed.gz
- The following Union stratifications were revised for both GRCh37 and GRCh38 to
  include satellites, chrX/Y XTR and ampliconic regions and removal of PAR-X
  regions from SegDups file.
    - GRCh37_alldifficultregions.bed.gz
    - GRCh37_notinalldifficultregions.bed.gz
    - GRCh37_alllowmapandsegdupregions.bed.gz  
    - GRCh37_notinalllowmapandsegdupregions.bed.gz
	
### Removed Stratifications

None 

## v3.0 - 2021-10-20

### New Stratifications

Ancestry
- Regions with inferred local ancestry in GRCh38 from the T2T-consortium
    - GRCh38_ancestry_AFR.bed.gz
    - GRCh38_ancestry_AMR.bed.gz
    - GRCh38_ancestry_EAS.bed.gz
    - GRCh38_ancestry_EUR.bed.gz
    - GRCh38_ancestry_Neanderthal.bed.gz
    - GRCh38_ancestry_SAS.bed.gz 

FunctionalTechnicallyDifficult
- Regions generated as part of the Challenging Medically Revelant Genes
  benchmark (v1.00) evaluation that identified duplicated regions. (GRCh37 and
  GRCh38)
    - GRCh3*_CMRGv1.00_duplicationinKMT2C.bed.gz
    - GRCh3*_CMRGv1.00_falselyduplicatedgenes.bed.gz

GenomeSpecific
- Stratifications for genomes HG001, HG003, HG004, HG005, HG006 and HG007 are
  new as of this version of stratifications and utilize GIAB v4.2.1 benchmark.
  (GRCh37 and GRCh38)
- New HG002 stratification:
    - GRCh3*_HG002_hifiasmv0.11_ComplexVar_in_TRgt100.bed.gz from development of
      Challenging Medically Relevant Gene benchmark (v1.00) development. (GRCh37
      and GRCh38)

LowComplexity
- Regions identified during manual curation of Challenging Medically Relevant
  Gene benchmark (v1.00) and accounted for a majority of false negatives and
  false positives for both SNPs and INDELs. (GRCh37 and GRCh38)
    - GRCh3*_SimpleRepeat_homopolymer_gt20_slop5.bed.gz
    - GRCh3*_SimpleRepeat_imperfecthomopolgt20_slop5.bed.gz

OtherDifficult
- Regions from the T2T-consortium for GRCh38 only
    - GRCh38_false_duplications_correct_copy.bed.gz
    - GRCh38_false_duplications_incorrect_copy.bed.gz
    - GRCh38_collapsed_duplication_FP_regions.bed.gz
    - GRCh38_population_CNV_FP_regions.bed.gz
    - GRCh38_LD_discordant_haplotypes_slop5bp.bed.gz
    - GRCh38_gnomAD_InbreedingCoeff_slop1bp_merge1000bp.bed.gz
	
- Regions from GIAB v4.2.1 benchmark development (GRCh37 and GRCh38)
    - GRCh3*_KIR.bed.gz
	
### Revised Stratifications

FunctionalRegions
- corrected filename error, GRCh37_notinrefseq_union_cds.bed.gz to
  GRCh37_notinrefseq_cds.bed.gz

FunctionalTechnicallyDifficult
- corrected filename error, GRCh3*_BadPromters.gz to GRCh3*_BadPromters.bed.gz

GenomeSpecific
- Stratifications for HG002 utilized benchmark v4.2.1. (GRCh37 and GRCh38)

OtherDifficult
- GRCh38_allOtherDifficultregions.bed.gz now includes new T2T-based
  stratifications and used newer version of bedtools (v2.30.0).
- GRCh37_allOtherDifficultregions.bed.gz no additional regions were merged
  rather file was just reproduced with newer version of bedtools (v2.30.0) to be
  consistent with GRCh38 file.

Union
- now includes new T2T-based stratifications and used newer version of bedtools
  (v2.30.0) (GRCh38 only)
    - GRCh38_alldifficultregions.bed.gz
    - GRCh38_notinalldifficultregions.bed.gz
- no additional regions were merged rather file was just reproduced with newer
  version of bedtools (v2.30.0) (GRCh37 and GRCh38)
    - GRCh3*_alllowmapandsegdupregions.bed.gz
    - GRCh3*_notinalllowmapandsegdupregions.bed.gz
    - GRCh37_alldifficultregions.bed.gz
    - GRCh37_notinalldifficultregions.bed.gz
	
### Removed Statifications

GenomeSpecific
- All stratifications that utilized GIAB v3.3.2 and v4.1 benchmark.  All files
  were updated to using GIAB v4.2.1 benchmark. 

## v2.0 - 2020-03-11

### New Stratifications

FunctionalRegions
- addition of GRCh38 files
    - GRCh38_refseq_cds.bed.gz
    - GRCh38_notinrefseq_cds.bed.gz
	
FunctionalTechnicallyDifficult
- addition of GRCh38 file
    - GRCh38_BadPromoters.bed.gz

GCcontent
- addition of GRCh38 files
    - GRCh38_gc15_slop50.bed.gz
    - GRCh38_gc15to20_slop50.bed.gz
    - GRCh38_gc20to25_slop50.bed.gz
    - GRCh38_gc25to30_slop50.bed.gz
    - GRCh38_gc30to55_slop50.bed.gz
    - GRCh38_gc55to60_slop50.bed.gz
    - GRCh38_gc60to65_slop50.bed.gz
    - GRCh38_gc65to70_slop50.bed.gz
    - GRCh38_gc75to80_slop50.bed.gz
    - GRCh38_gc80to85_slop50.bed.gz
    - GRCh38_gc85_slop50.bed.gz
    - GRCh38_gclt25orgt65_slop50.bed.gz
    - GRCh38_gclt30orgt55_slop50.bed.gz

GenomeSpecific
- new files utilizing GIAB v3.3.2 and v4.1 benchmarks for GRCh37
    - GRCh37_HG001_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh37_HG001_GIABv3.3.2_RTG_PG_v3.3.2_SVs_alldifficultregions.bed.gz
    - GRCh37_HG001_GIABv3.3.2_RTG_PG_v3.3.2_SVs_notin_alldifficultregions.bed.gz
    - GRCh37_HG002_expanded_150__Tier1plusTier2_v0.6.1.bed.gz
    - GRCh37_HG002_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG002_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh37_HG002_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG002_GIABv4.1_CNV_CCSandONT_elliptical_outlier.bed.gz
    - GRCh37_HG002_GIABv4.1_CNV_gt2assemblycontigs_ONTCanu_ONTFlye_CCSCanu.bed.gz
    - GRCh37_HG002_GIABv4.1_CNV_mrcanavarIllumina_CCShighcov_ONThighcov_intersection.bed.gz
    - GRCh37_HG002_GIABv4.1_CNVsandSVs.bed.gz
    - GRCh37_HG002_GIABv4.1_comphetindel10bp_slop50.bed.gz
    - GRCh37_HG002_GIABv4.1_comphetsnp10bp_slop50.bed.gz
    - GRCh37_HG002_GIABv4.1_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG002_GIABv4.1_complexandSVs.bed.gz
    - GRCh37_HG002_GIABv4.1_complexindel10bp_slop50.bed.gz
    - GRCh37_HG002_GIABv4.1_inversions_slop25percent.bed.gz
    - GRCh37_HG002_GIABv4.1_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG002_GIABv4.1_othercomplexwithin10bp_slop50.bed.gz
    - GRCh37_HG002_GIABv4.1_snpswithin10bp_slop50.bed.gz
    - GRCh37_HG002_Tier1plusTier2_v0.6.1.bed.gz
    - GRCh37_HG003_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG003_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh37_HG003_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG004_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG004_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh37_HG004_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG005_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh37_HG005_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh37_HG005_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
- addition of GRCh38 files
    - GRCh38_HG001_GIABv3.2.2_compoundhet_slop50.bed.gz
    - GRCh38_HG001_GIABv3.2.2_varswithin50bp.bed.gz
    - GRCh38_HG001_GIABv3.3.2_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG001_GIABv3.3.2_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG001_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh38_HG001_GIABv3.3.2_complexindel10bp_slop50.bed.gz
    - GRCh38_HG001_GIABv3.3.2_RTG_PG_v3.3.2_SVs_alldifficultregions.bed.gz
    - GRCh38_HG001_GIABv3.3.2_RTG_PG_v3.3.2_SVs_notin_alldifficultregions.bed.gz
    - GRCh38_HG001_GIABv3.3.2_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG001_PacBio_MetaSV.bed.gz
    - GRCh38_HG001_PG2016-1.0_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG001_PG2016-1.0_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG001_PG2016-1.0_complexindel10bp_slop50.bed.gz
    - GRCh38_HG001_PG2016-1.0_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG001_RTG_37.7.3_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG001_RTG_37.7.3_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG001_RTG_37.7.3_complexindel10bp_slop50.bed.gz
    - GRCh38_HG001_RTG_37.7.3_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG002_expanded_150_Tier1plusTier2_v0.6.1.bed.gz
    - GRCh38_HG002_GIABv3.2.2_compoundhet_slop50.bed.gz
    - GRCh38_HG002_GIABv3.2.2_varswithin50bp.bed.gz
    - GRCh38_HG002_GIABv3.3.2_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv3.3.2_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG002_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh38_HG002_GIABv3.3.2_complexindel10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG002_GIABv3.3.2_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv4.1_CNV_CCSandONT_elliptical_outlier.bed.gz
    - GRCh38_HG002_GIABv4.1_CNV_gt2assemblycontigs_ONTCanu_ONTFlye_CCSCanu.bed.gz
    - GRCh38_HG002_GIABv4.1_CNV_mrcanavarIllumina_CCShighcov_ONThighcov_intersection.bed.gz
    - GRCh38_HG002_GIABv4.1_CNVsandSVs.bed.gz
    - GRCh38_HG002_GIABv4.1_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv4.1_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv4.1_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG002_GIABv4.1_complexandSVs.bed.gz
    - GRCh38_HG002_GIABv4.1_complexindel10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv4.1_inversions_slop25percent.bed.gz
    - GRCh38_HG002_GIABv4.1_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG002_GIABv4.1_othercomplexwithin10bp_slop50.bed.gz
    - GRCh38_HG002_GIABv4.1_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG002_HG003_HG004_allsvs.bed.gz
    - GRCh38_HG002_Tier1plusTier2_v0.6.1.bed.gz
    - GRCh38_HG003_GIABv3.3.2_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG003_GIABv3.3.2_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG003_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG003_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh38_HG003_GIABv3.3.2_complexindel10bp_slop50.bed.gz
    - GRCh38_HG003_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG003_GIABv3.3.2_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG004_GIABv3.3.2_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG004_GIABv3.3.2_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG004_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG004_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh38_HG004_GIABv3.3.2_complexindel10bp_slop50.bed.gz
    - GRCh38_HG004_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG004_GIABv3.3.2_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG005_GIABv3.3.2_comphetindel10bp_slop50.bed.gz
    - GRCh38_HG005_GIABv3.3.2_comphetsnp10bp_slop50.bed.gz
    - GRCh38_HG005_GIABv3.3.2_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG005_GIABv3.3.2_complexandSVs.bed.gz
    - GRCh38_HG005_GIABv3.3.2_complexindel10bp_slop50.bed.gz
    - GRCh38_HG005_GIABv3.3.2_notin_complexandSVs_alldifficultregions.bed.gz
    - GRCh38_HG005_GIABv3.3.2_snpswithin10bp_slop50.bed.gz
    - GRCh38_HG005_HG006_HG007_MetaSV_allsvs.bed.gz
	
LowComplexity
- new additions for GRCh37
    - GRCh37_AllHomopolymers_gt6bp_imperfectgt10bp_slop5.bed.gz
    - GRCh37_AllTandemRepeats_gt10000bp_slop5.bed.gz
    - GRCh37_notinAllHomopolymers_gt6bp_imperfectgt10bp_slop5.bed.gz
    - GRCh37_notinAllTandemRepeatsandHomopolymers_slop5.bed.gz
    - GRCh37_SimpleRepeat_homopolymer_4to6_slop5.bed.gz
- addition of GRCh38 files
    - GRCh38_AllHomopolymers_gt6bp_imperfectgt10bp_slop5.bed.gz
    - GRCh38_AllTandemRepeats_201to10000bp_slop5.bed.gz
    - GRCh38_AllTandemRepeats_51to200bp_slop5.bed.gz
    - GRCh38_AllTandemRepeats_gt10000bp_slop5.bed.gz
    - GRCh38_AllTandemRepeats_gt100bp_slop5.bed.gz
    - GRCh38_AllTandemRepeats_lt51bp_slop5.bed.gz
    - GRCh38_AllTandemRepeatsandHomopolymers_slop5.bed.gz
    - GRCh38_notinAllHomopolymers_gt6bp_imperfectgt10bp_slop5.bed.gz
    - GRCh38_notinAllTandemRepeatsandHomopolymers_slop5.bed.gz
    - GRCh38_SimpleRepeat_diTR_11to50_slop5.bed.gz
    - GRCh38_SimpleRepeat_diTR_51to200_slop5.bed.gz
    - GRCh38_SimpleRepeat_diTR_gt200_slop5.bed.gz
    - GRCh38_SimpleRepeat_homopolymer_4to6_slop5.bed.gz
    - GRCh38_SimpleRepeat_homopolymer_7to11_slop5.bed.gz
    - GRCh38_SimpleRepeat_homopolymer_gt11_slop5.bed.gz
    - GRCh38_SimpleRepeat_imperfecthomopolgt10_slop5.bed.gz
    - GRCh38_SimpleRepeat_quadTR_20to50_slop5.bed.gz
    - GRCh38_SimpleRepeat_quadTR_51to200_slop5.bed.gz
    - GRCh38_SimpleRepeat_quadTR_gt200_slop5.bed.gz
    - GRCh38_SimpleRepeat_triTR_15to50_slop5.bed.gz
    - GRCh38_SimpleRepeat_triTR_51to200_slop5.bed.gz
    - GRCh38_SimpleRepeat_triTR_gt200_slop5.bed.gz
	
mappability
- addition of GRCh38 files
    - GRCh38_lowmappabilityall.bed.gz
    - GRCh38_nonunique_l100_m2_e1.bed.gz
    - GRCh38_nonunique_l250_m0_e0.bed.gz
    - GRCh38_notinlowmappabilityall.bed.gz

OtherDifficult
- all stratifications new for v2.0 (GRCh37 and GRCh38)
    - GRCh37_allOtherDifficultregions.bed.gz
    - GRCh37_contigs_lt500kb.bed.gz 
    - GRCh37_gaps_slop15kb.bed.gz
    - GRCh37_hg38_minimap2_asm20_N10_gt1contig_gt1kb.bed.gz
    - GRCh37_hg38_minimap2_asm20_N10_nocovgt1kb.bed.gz
    - GRCh37_hs37d5_decoy_alignments.bed.gz
    - GRCh37_L1H_gt500.bed.gz
    - GRCh37_MHC.bed.gz
    - GRCh37_missing_and_multiple_alignments_of_GRCh38.bed.gz
    - GRCh37_VDJ.bed.gz
    - GRCh38_allOtherDifficultregions.bed.gz
    - GRCh38_contigs_lt500kb.bed.gz 
    - GRCh38_gaps_slop15kb.bed.gz
    - GRCh38_L1H_gt500.bed.gz
    - GRCh38_MHC.bed.gz
    - GRCh38_VDJ.bed.gz

SegmentalDuplications
- new additions for GRCh37
    - GRCh37_gt5segdups_gt10kb_gt99percidentity.bed.gz
    - GRCh37_notinchainSelf_gt10kb.bed.gz
    - GRCh37_notinchainSelf.bed.gz
    - GRCh37_notinsegdups_gt10kb.bed.gz
    - GRCh37_segdups_gt10kb.bed.gz
- addition of GRCh38 files
    - GRCh38_chainSelf_gt10kb.bed.gz
    - GRCh38_chainSelf.bed.gz
    - GRCh38_gt5segdups_gt10kb_gt99percidentity.bed.gz
    - GRCh38_notinchainSelf_gt10kb.bed.gz
    - GRCh38_notinchainSelf.bed.gz
    - GRCh38_notinsegdups_gt10kb.bed.gz
    - GRCh38_notinsegdups.bed.gz
    - GRCh38_segdups_gt10kb.bed.gz
    - GRCh38_segdups.bed.gz
	
Union
- all stratifications new for v2.0 (GRCh37 and GRCh38)
    - GRCh37_alldifficultregions.bed.gz
    - GRCh37_alllowmapandsegdupregions.bed.gz
    - GRCh37_notinalldifficultregions.bed.gz
    - GRCh37_notinalllowmapandsegdupregions.bed.gz
    - GRCh38_alldifficultregions.bed.gz
    - GRCh38_alllowmapandsegdupregions.bed.gz
    - GRCh38_notinalldifficultregions.bed.gz
    - GRCh38_notinalllowmapandsegdupregions.bed.gz

### Revised Stratifications

FunctionalRegions
-  bug in the code used to identify the coding regions was corrected. V1.0
   functional region stratifications only includes chromosomes 1-9. (GRCh37)
   
   - GRCh37_notinrefseq_union_cds.bed.gz
   - GRCh37_refseq_cds.bed.gz

LowComplexity
- RepeatMasker and TRF_SimpleRepeats downloaded from UCSC for hg19 and hg38 on
  7/22/19. These replace the TRDB repeats that were used in the 2015 version,
  since the 2015 version missed some long, imperfect tandem repeats. (GRCh37 and
  GRCh38)
  
- Exact repeats with fewer than 5 copies of the tandem repeat unit (e.g., <15bp
  total length for trinucleotide STRs) were now ignored, since these tend to
  have low sequencing error rates. (GRCh37 and GRCh38)
  
- Homopolymer lengths were incorrectly labeled, 1bp lower than the actual size,
  in the previous version. (GRCh37 and GRCh38)
  
- Fixed the SimpleRepeat_imperfecthomopolgt10_slop5.bed.gz to only merge
  adjacent homopolymers if they had the same base repeated. (GRCh37 and GRCh38)
  
- All beds have 5bp slop added on each side to capture variants at the edge of
  the repeats (sometimes insertions were not captured properly before in
  stratifications). (GRCh37 and GRCh38)
  
    - GRCh37_AllTandemRepeats_201to10000bp_slop5.bed.gz
    - GRCh37_AllTandemRepeats_51to200bp_slop5.bed.gz
    - GRCh37_AllTandemRepeats_gt100bp_slop5.bed.gz
    - GRCh37_AllTandemRepeats_lt51bp_slop5.bed.gz
    - GRCh37_AllTandemRepeatsandHomopolymers_slop5.bed.gz
    - GRCh37_SimpleRepeat_diTR_11to50_slop5.bed.gz
    - GRCh37_SimpleRepeat_diTR_51to200_slop5.bed.gz
    - GRCh37_SimpleRepeat_diTR_gt200_slop5.bed.gz
    - GRCh37_SimpleRepeat_homopolymer_7to11_slop5.bed.gz
    - GRCh37_SimpleRepeat_homopolymer_gt11_slop5.bed.gz
    - GRCh37_SimpleRepeat_imperfecthomopolgt10_slop5.bed.gz
    - GRCh37_SimpleRepeat_quadTR_20to50_slop5.bed.gz
    - GRCh37_SimpleRepeat_quadTR_51to200_slop5.bed.gz
    - GRCh37_SimpleRepeat_quadTR_gt200_slop5.bed.gz
    - GRCh37_SimpleRepeat_triTR_15to50_slop5.bed.gz
    - GRCh37_SimpleRepeat_triTR_51to200_slop5.bed.gz
    - GRCh37_SimpleRepeat_triTR_gt200_slop5.bed.gz

Mappability
- To reduce the total number of stratifications for V2.0 of the stratifications
  only two mappability files (parameter sets: l-100, m-2, e-1; and l-250, m-0,
  e-0) are included. These stratifications represent the most (l-250, m-0, e-0)
  and least (l-100, m-2, e-1) stringent stratifications. (GRCh37 and GRCh38-new)
    - GRCh37_lowmappabilityall.bed.gz
    - GRCh37_notinlowmappabilityall.bed.gz
	
SegmentalDuplications
    - GRCh37_chainSelf_gt10kb.bed.gz
    - GRCh37_chainSelf.bed.gz
    - GRCh37_notinsegdups.bed.gz
    - GRCh37_segdups.bed.gz

## v1.0 - 2017

- initial release (https://github.com/ga4gh/benchmarking-tools/tree/d88448a68a79ed322837bc8eb4d5a096a710993d/resources/stratification-bed-files)
