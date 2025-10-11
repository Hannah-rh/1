Data Wrangling 1 - Data Import
================

Import -\> Tidy -\> Transform —-\> 之后的操作

- default behavior 默认行为

- data frame -\> tibble  
  tib_df(): like a
  console控制台，只显示前几行（可读性）；列明必须是合法变量名（安全性）

- 创建repository的时候不用add gitignore，
  RStudio创建本地项目时会自动生成，最后能够直接push到repository

- 安装包：library(包名) 用于加载已安装的R包  
  tidyverse：包含dplyr、readr、tidyr、ggplot2等数据科学工具包  
  dplyer包  
  readr包：import data
  set（用于读取CSV文件（虽然tidyverse已包含，但显示加载更清晰））  
  haven包：import data set from SAS、Stata  
  readxl包：非常方便读取excel文件

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.2     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

# Let’s import a dataset.

``` r
litters_df = 
    read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

read_csv() 读取CSV文件（不要用read.csv！）

# Look at the data.

``` r
names(litters_df)
```

    ## [1] "Group"             "Litter Number"     "GD0 weight"       
    ## [4] "GD18 weight"       "GD of Birth"       "Pups born alive"  
    ## [7] "Pups dead @ birth" "Pups survive"

name() 显示数据框中所有列的名称

# Update the names in “litters_df”

``` r
litters_df =
  janitor::clean_names(litters_df)
```

janitor：一个R包，专门用于数据清洗和探索性数据分析（EDA）的初步阶段
::双冒号：从左边的包中，调用右边的函数
clean_names()：对数据框的列名进行清洗或标准化（将空格替换为下划线，移除特殊字符，将所有字母转换为小写）
