Reproduceable Research Project
================

-   [Files](#files)
    -   [File parsing problems](#file-parsing-problems)

This is data from Anthony (FRH Chinook). The point of this project is to be able to play around in R and GitHub with data types we typically use in lab. Currently we have two files as follows:

Files
-----

**baseline\_genotypes.csv**: typical two column genotype file with columns as follows:

*column 1* = analysis ID

*column 2* = GSI ID

*col 3-192* = 2 column genotypes with assay order as follows (keep in mind that the data is in 2 column format, so each of these assay names will appear 2 times in a row): c("Ots\_94857-232", "Ots\_102213-210", "Ots\_104569-86", "Ots\_107285-93", "Ots\_110495-380", "Ots\_112419-131", "Ots\_118175-479", "Ots\_128302-57", "Ots\_131906-141", "Ots\_AsnRs-60", "Ots\_mybp-85", "Ots\_TAPBP", "Ots\_96222-525", "Ots\_102414-395", "Ots\_105105-613", "Ots\_107806-821", "Ots\_110551-64", "Ots\_112820-284", "Ots\_118205-61", "Ots\_128693-461", "AldB1-122", "Ots\_aspat-196", "Ots\_myoD-364", "Ots\_u07-07.161", "Ots\_96500-180", "Ots\_102420-494", "Ots\_105132-200", "Ots\_108007-208", "Ots\_112876-371", "Ots\_118938-325", "Ots\_128757-61", "AldoB4-183", "Ots\_CD59-2", "Ots\_Ots311-101x", "Ots\_u07-49.290", "Ots\_97077-179", "Ots\_102457-132", "Ots\_105401-325", "Ots\_108390-329", "Ots\_111312-435", "Ots\_113242-216", "Ots\_122414-56", "Ots\_129144-472", "Myc-366", "Ots\_CD63", "Ots\_PGK-54", "Ots\_u4-92", "Ots\_99550-204", "Ots\_102801-308", "Ots\_105407-117", "Ots\_108735-302", "Ots\_111666-408", "Ots\_113457-40", "Ots\_123048-521", "Ots\_129170-683", "OTALDBINT1-SNP1", "Ots\_EP-529", "Ots\_Prl2", "OTSBMP-2-SNP1", "Ots\_100884-287", "Ots\_102867-609", "Ots\_106499-70", "Ots\_109693-392", "Ots\_111681-657", "Ots\_117043-255", "Ots\_123921-111", "Ots\_129458-451", "OTNAML12\_1-SNP1", "Ots\_GDH-81x", "Ots\_RFC2-558", "OTSTF1-SNP1", "Ots\_101119-381", "Ots\_103041-52", "Ots\_106747-239", "Ots\_110064-383", "Ots\_112208-722", "Ots\_117242-136", "Ots\_124774-477", "Ots\_130720-99", "Ots\_ARNT-195", "Ots\_HSP90B-385", "Ots\_SClkF2R2-135""S71-336", "Ots\_101704-143", "Ots\_104063-132", "Ots\_107074-284", "Ots\_110201-363", "Ots\_112301-43", "Ots\_117432-409", "Ots\_127236-62", "Ots\_131460-584", "Ots\_RAG3", "Ots\_MHC1", "Ots\_SWS1op-182", "unk\_526")

**"baseline\_metadata.csv"** = typical metadata file, columns are as follows:

c("NMFS\_DNA\_ID", "BOX\_ID", "BOX\_POSITION", "PLATE", "PLATE\_POS", "Sort", "SAMPLE\_ID", "ANALYSIS\_ID", "BATCH\_ID", "PROJECT\_NAME", "GENUS", "SPECIES", "LENGTH", "WEIGHT", "SEX", "AGE", "REPORTED\_LIFE\_STAGE", "PHENOTYPE", "HATCHERY\_MARK", "TAG\_NUMBER", "COLLECTION\_DATE", "ESTIMATED\_DATE", "PICKER", "PICK\_DATE", "LEFTOVER\_SAMPLE", "SAMPLE\_COMMENTS", "NMFS\_DNA\_ID", "STATE\_F", "COUNTY\_F", "WATERSHED", "TRIB\_1", "TRIB\_2", "WATER\_NAME", "REACH\_SITE", "LATITUDE\_F", "LONGITUDE\_F", "HATCHERY", "STRAIN", "LOCATION\_COMMENTS\_F")

*NMFS\_ID* appears twice in this dataset--both columns should be the same and refer to a unique sample ID.

*Sample\_ID* refers to the original ID the sample was given, which may not be unique.

*Length* is in milimeters.

*Weight* is in grams.

Both files were read into R as follows:

``` r
library(tidyverse)
```

    ## Loading tidyverse: ggplot2
    ## Loading tidyverse: tibble
    ## Loading tidyverse: tidyr
    ## Loading tidyverse: readr
    ## Loading tidyverse: purrr
    ## Loading tidyverse: dplyr

    ## Conflicts with tidy packages ----------------------------------------------

    ## filter(): dplyr, stats
    ## lag():    dplyr, stats

``` r
genos <- read_csv("data/baseline_genotypes.csv")
```

    ## Warning: Duplicated column names deduplicated: 'Ots_94857-232' =>
    ## 'Ots_94857-232_1' [4], 'Ots_102213-210' => 'Ots_102213-210_1' [6],
    ## 'Ots_104569-86' => 'Ots_104569-86_1' [8], 'Ots_107285-93' =>
    ## 'Ots_107285-93_1' [10], 'Ots_110495-380' => 'Ots_110495-380_1' [12],
    ## 'Ots_112419-131' => 'Ots_112419-131_1' [14], 'Ots_118175-479' =>
    ## 'Ots_118175-479_1' [16], 'Ots_128302-57' => 'Ots_128302-57_1' [18],
    ## 'Ots_131906-141' => 'Ots_131906-141_1' [20], 'Ots_AsnRs-60' =>
    ## 'Ots_AsnRs-60_1' [22], 'Ots_mybp-85' => 'Ots_mybp-85_1' [24], 'Ots_TAPBP'
    ## => 'Ots_TAPBP_1' [26], 'Ots_96222-525' => 'Ots_96222-525_1' [28],
    ## 'Ots_102414-395' => 'Ots_102414-395_1' [30], 'Ots_105105-613' =>
    ## 'Ots_105105-613_1' [32], 'Ots_107806-821' => 'Ots_107806-821_1' [34],
    ## 'Ots_110551-64' => 'Ots_110551-64_1' [36], 'Ots_112820-284' =>
    ## 'Ots_112820-284_1' [38], 'Ots_118205-61' => 'Ots_118205-61_1' [40],
    ## 'Ots_128693-461' => 'Ots_128693-461_1' [42], 'AldB1-122' =>
    ## 'AldB1-122_1' [44], 'Ots_aspat-196' => 'Ots_aspat-196_1' [46],
    ## 'Ots_myoD-364' => 'Ots_myoD-364_1' [48], 'Ots_u07-07.161' =>
    ## 'Ots_u07-07.161_1' [50], 'Ots_96500-180' => 'Ots_96500-180_1' [52],
    ## 'Ots_102420-494' => 'Ots_102420-494_1' [54], 'Ots_105132-200' =>
    ## 'Ots_105132-200_1' [56], 'Ots_108007-208' => 'Ots_108007-208_1' [58],
    ## 'Ots_112876-371' => 'Ots_112876-371_1' [60], 'Ots_118938-325' =>
    ## 'Ots_118938-325_1' [62], 'Ots_128757-61' => 'Ots_128757-61_1' [64],
    ## 'AldoB4-183' => 'AldoB4-183_1' [66], 'Ots_CD59-2' => 'Ots_CD59-2_1' [68],
    ## 'Ots_Ots311-101x' => 'Ots_Ots311-101x_1' [70], 'Ots_u07-49.290' =>
    ## 'Ots_u07-49.290_1' [72], 'Ots_97077-179' => 'Ots_97077-179_1' [74],
    ## 'Ots_102457-132' => 'Ots_102457-132_1' [76], 'Ots_105401-325' =>
    ## 'Ots_105401-325_1' [78], 'Ots_108390-329' => 'Ots_108390-329_1' [80],
    ## 'Ots_111312-435' => 'Ots_111312-435_1' [82], 'Ots_113242-216' =>
    ## 'Ots_113242-216_1' [84], 'Ots_122414-56' => 'Ots_122414-56_1' [86],
    ## 'Ots_129144-472' => 'Ots_129144-472_1' [88], 'Myc-366' =>
    ## 'Myc-366_1' [90], 'Ots_CD63' => 'Ots_CD63_1' [92], 'Ots_PGK-54' =>
    ## 'Ots_PGK-54_1' [94], 'Ots_u4-92' => 'Ots_u4-92_1' [96], 'Ots_99550-204'
    ## => 'Ots_99550-204_1' [98], 'Ots_102801-308' => 'Ots_102801-308_1' [100],
    ## 'Ots_105407-117' => 'Ots_105407-117_1' [102], 'Ots_108735-302' =>
    ## 'Ots_108735-302_1' [104], 'Ots_111666-408' => 'Ots_111666-408_1' [106],
    ## 'Ots_113457-40' => 'Ots_113457-40_1' [108], 'Ots_123048-521' =>
    ## 'Ots_123048-521_1' [110], 'Ots_129170-683' => 'Ots_129170-683_1' [112],
    ## 'OTALDBINT1-SNP1' => 'OTALDBINT1-SNP1_1' [114], 'Ots_EP-529' =>
    ## 'Ots_EP-529_1' [116], 'Ots_Prl2' => 'Ots_Prl2_1' [118], 'OTSBMP-2-SNP1'
    ## => 'OTSBMP-2-SNP1_1' [120], 'Ots_100884-287' => 'Ots_100884-287_1' [122],
    ## 'Ots_102867-609' => 'Ots_102867-609_1' [124], 'Ots_106499-70' =>
    ## 'Ots_106499-70_1' [126], 'Ots_109693-392' => 'Ots_109693-392_1' [128],
    ## 'Ots_111681-657' => 'Ots_111681-657_1' [130], 'Ots_117043-255' =>
    ## 'Ots_117043-255_1' [132], 'Ots_123921-111' => 'Ots_123921-111_1' [134],
    ## 'Ots_129458-451' => 'Ots_129458-451_1' [136], 'OTNAML12_1-SNP1' =>
    ## 'OTNAML12_1-SNP1_1' [138], 'Ots_GDH-81x' => 'Ots_GDH-81x_1' [140],
    ## 'Ots_RFC2-558' => 'Ots_RFC2-558_1' [142], 'OTSTF1-SNP1' => 'OTSTF1-
    ## SNP1_1' [144], 'Ots_101119-381' => 'Ots_101119-381_1' [146],
    ## 'Ots_103041-52' => 'Ots_103041-52_1' [148], 'Ots_106747-239' =>
    ## 'Ots_106747-239_1' [150], 'Ots_110064-383' => 'Ots_110064-383_1' [152],
    ## 'Ots_112208-722' => 'Ots_112208-722_1' [154], 'Ots_117242-136' =>
    ## 'Ots_117242-136_1' [156], 'Ots_124774-477' => 'Ots_124774-477_1' [158],
    ## 'Ots_130720-99' => 'Ots_130720-99_1' [160], 'Ots_ARNT-195' =>
    ## 'Ots_ARNT-195_1' [162], 'Ots_HSP90B-385' => 'Ots_HSP90B-385_1' [164],
    ## 'Ots_SClkF2R2-135' => 'Ots_SClkF2R2-135_1' [166], 'S71-336' =>
    ## 'S71-336_1' [168], 'Ots_101704-143' => 'Ots_101704-143_1' [170],
    ## 'Ots_104063-132' => 'Ots_104063-132_1' [172], 'Ots_107074-284' =>
    ## 'Ots_107074-284_1' [174], 'Ots_110201-363' => 'Ots_110201-363_1' [176],
    ## 'Ots_112301-43' => 'Ots_112301-43_1' [178], 'Ots_117432-409' =>
    ## 'Ots_117432-409_1' [180], 'Ots_127236-62' => 'Ots_127236-62_1' [182],
    ## 'Ots_131460-584' => 'Ots_131460-584_1' [184], 'Ots_RAG3' =>
    ## 'Ots_RAG3_1' [186], 'Ots_MHC1' => 'Ots_MHC1_1' [188], 'Ots_SWS1op-182' =>
    ## 'Ots_SWS1op-182_1' [190], 'unk_526' => 'unk_526_1' [192]

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_integer(),
    ##   ANALYSIS_ID = col_character(),
    ##   GSISIM_ID = col_character()
    ## )

    ## See spec(...) for full column specifications.

``` r
meta <- read_csv("data/baseline_metadata.csv")
```

    ## Warning: Duplicated column names deduplicated: 'NMFS_DNA_ID' =>
    ## 'NMFS_DNA_ID_1' [27]

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   Sort = col_integer(),
    ##   LENGTH = col_integer(),
    ##   TAG_NUMBER = col_integer()
    ## )
    ## See spec(...) for full column specifications.

    ## Warning: 893 parsing failures.
    ##  row        col   expected     actual
    ## 1060 TAG_NUMBER an integer CWT# 42910
    ## 1061 TAG_NUMBER an integer CWT# 56303
    ## 1079 TAG_NUMBER an integer CWT# 56301
    ## 1080 TAG_NUMBER an integer CWT# 56302
    ## 1081 TAG_NUMBER an integer CWT# 56341
    ## .... .......... .......... ..........
    ## See problems(...) for more details.

Both files had at lease one occurance of duplicate column names (see file notes above). R obviously complains about this, but changes the second occurance of the column name to "(Column Name)\_1" to give each column a unique ID.

### File parsing problems

There were a few problems in parsing the file. The cool thing is that the `problems()` function sends them back as a tibble so you can easily analyze them. First note that there were not obvious problems with genos:

``` r
problems(genos)
```

    ## # A tibble: 0 × 4
    ## # ... with 4 variables: row <int>, col <int>, expected <chr>, actual <chr>

`meta` had some problems. Let's categorize them by column and type of problem, using `dplyr`!!

``` r
problems(meta) %>%
  group_by(col, expected) %>%
  tally()
```

    ## Source: local data frame [3 x 3]
    ## Groups: col [?]
    ## 
    ##          col               expected     n
    ##        <chr>                  <chr> <int>
    ## 1     LENGTH no trailing characters    77
    ## 2 TAG_NUMBER             an integer   196
    ## 3 TAG_NUMBER no trailing characters   620

OK, that looks like three different types of problems in two different types of columns.

Ellen! Your mission today is to solve those problems using what we learned in the readr chapter!
