00\_filesystem-practice\_jenny.R
================
bvegetabile
Wed Jan 31 14:06:13 2018

``` r
## First attempt: Just get it to work ----

list.files("~/Desktop/day1_s1_explore-libraries")
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R"

``` r
list.files("~/Desktop/day1_s1_explore-libraries", pattern = "\\.R$")
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R"

``` r
list.files(
  "~/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)
```

    ## [1] "/Users/bvegetabile/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R"  
    ## [2] "/Users/bvegetabile/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R"  
    ## [3] "/Users/bvegetabile/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R"

``` r
from_files <- list.files(
  "~/Desktop/day1_s1_explore-libraries",
  pattern = "\\.R$",
  full.names = TRUE
)

(to_files <- basename(from_files))
```

    ## [1] "01_explore-libraries_comfy.R"   "01_explore-libraries_jenny.R"  
    ## [3] "01_explore-libraries_spartan.R"

``` r
file.copy(from_files, to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "00_filesystem-practice_jenny.html"    
    ## [2] "00_filesystem-practice_jenny.R"       
    ## [3] "00_filesystem-practice_jenny.spin.R"  
    ## [4] "00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "01_explore-libraries_comfy.R"         
    ## [6] "01_explore-libraries_jenny.R"         
    ## [7] "01_explore-libraries_spartan.R"       
    ## [8] "explore-libraries.Rproj"              
    ## [9] "README.md"

``` r
## Clean it out, so we can refine ----
file.remove(to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "00_filesystem-practice_jenny.html"    
    ## [2] "00_filesystem-practice_jenny.R"       
    ## [3] "00_filesystem-practice_jenny.spin.R"  
    ## [4] "00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "explore-libraries.Rproj"              
    ## [6] "README.md"

``` r
## Copy again, tighter code ----
from_dir <- file.path("~", "Desktop", "day1_s1_explore-libraries")
from_files <- list.files(from_dir, pattern = "\\.R$", full.names = TRUE)
to_files <- basename(from_files)
file.copy(from_files, to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "00_filesystem-practice_jenny.html"    
    ## [2] "00_filesystem-practice_jenny.R"       
    ## [3] "00_filesystem-practice_jenny.spin.R"  
    ## [4] "00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "01_explore-libraries_comfy.R"         
    ## [6] "01_explore-libraries_jenny.R"         
    ## [7] "01_explore-libraries_spartan.R"       
    ## [8] "explore-libraries.Rproj"              
    ## [9] "README.md"

``` r
## Clean it out, so we can use fs ----
file.remove(to_files)
```

    ## [1] TRUE TRUE TRUE

``` r
list.files()
```

    ## [1] "00_filesystem-practice_jenny.html"    
    ## [2] "00_filesystem-practice_jenny.R"       
    ## [3] "00_filesystem-practice_jenny.spin.R"  
    ## [4] "00_filesystem-practice_jenny.spin.Rmd"
    ## [5] "explore-libraries.Rproj"              
    ## [6] "README.md"

``` r
## Copy again, using fs ----
library(fs)
(from_dir <- path_home("Desktop", "day1_s1_explore-libraries"))
```

    ## /Users/bvegetabile/Desktop/day1_s1_explore-libraries

``` r
(from_files <- dir_ls(from_dir, glob = "*.R"))
```

    ## /Users/bvegetabile/Desktop/day1_s1_explore-libraries/01_explore-libraries_comfy.R
    ## /Users/bvegetabile/Desktop/day1_s1_explore-libraries/01_explore-libraries_jenny.R
    ## /Users/bvegetabile/Desktop/day1_s1_explore-libraries/01_explore-libraries_spartan.R

``` r
(to_files <- path_file(from_files))
```

    ## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
    ## 01_explore-libraries_spartan.R

``` r
(out <- file_copy(from_files, to_files))
```

    ## 01_explore-libraries_comfy.R   01_explore-libraries_jenny.R   
    ## 01_explore-libraries_spartan.R

``` r
dir_ls()
```

    ## 00_filesystem-practice_jenny.R
    ## 00_filesystem-practice_jenny.html
    ## 00_filesystem-practice_jenny.spin.R
    ## 00_filesystem-practice_jenny.spin.Rmd
    ## 01_explore-libraries_comfy.R
    ## 01_explore-libraries_jenny.R
    ## 01_explore-libraries_spartan.R
    ## README.md
    ## explore-libraries.Rproj

``` r
dir_info()
```

    ##                                    path type    size permissions
    ## 1        00_filesystem-practice_jenny.R file   1.72K   rw-r--r--
    ## 2     00_filesystem-practice_jenny.html file 729.53K   rw-r--r--
    ## 3   00_filesystem-practice_jenny.spin.R file   1.72K   rw-r--r--
    ## 4 00_filesystem-practice_jenny.spin.Rmd file   1.82K   rw-r--r--
    ## 5          01_explore-libraries_comfy.R file   1.12K   rw-r--r--
    ## 6          01_explore-libraries_jenny.R file   1.54K   rw-r--r--
    ## 7        01_explore-libraries_spartan.R file     850   rw-r--r--
    ## 8                             README.md file     177   rw-r--r--
    ## 9               explore-libraries.Rproj file     205   rw-r--r--
    ##     modification_time        user group device_id hard_links
    ## 1 2018-01-31 14:06:13 bvegetabile staff  16777220          1
    ## 2 2018-01-31 13:55:46 bvegetabile staff  16777220          1
    ## 3 2018-01-31 14:06:13 bvegetabile staff  16777220          1
    ## 4 2018-01-31 14:06:13 bvegetabile staff  16777220          1
    ## 5 2018-01-31 09:57:02 bvegetabile staff  16777220          1
    ## 6 2018-01-31 09:57:02 bvegetabile staff  16777220          1
    ## 7 2018-01-31 09:57:02 bvegetabile staff  16777220          1
    ## 8 2018-01-31 13:46:09 bvegetabile staff  16777220          1
    ## 9 2018-01-31 13:31:32 bvegetabile staff  16777220          1
    ##   special_device_id     inode block_size blocks flags generation
    ## 1                 0 224505241       4096      8     0          0
    ## 2                 0 224505361       4096   1464     0          0
    ## 3                 0 224505481       4096      8     0          0
    ## 4                 0 224505482       4096      8     0          0
    ## 5                 0 224505489       4096      8     0          0
    ## 6                 0 224505490       4096      8     0          0
    ## 7                 0 224505491       4096      8     0          0
    ## 8                 0 224505156       4096      8     0          0
    ## 9                 0 224503353       4096      8     0          0
    ##           access_time         change_time          birth_time
    ## 1 2018-01-31 14:06:13 2018-01-31 14:06:13 2018-01-31 13:49:16
    ## 2 2018-01-31 13:58:58 2018-01-31 13:55:46 2018-01-31 13:55:45
    ## 3 2018-01-31 14:06:13 2018-01-31 14:06:13 2018-01-31 14:06:13
    ## 4 2018-01-31 14:06:13 2018-01-31 14:06:13 2018-01-31 14:06:13
    ## 5 2018-01-31 14:06:13 2018-01-31 14:06:13 2018-01-31 09:57:02
    ## 6 2018-01-31 14:06:13 2018-01-31 14:06:13 2018-01-31 09:57:02
    ## 7 2018-01-31 14:06:13 2018-01-31 14:06:13 2018-01-31 09:57:02
    ## 8 2018-01-31 13:46:18 2018-01-31 13:46:09 2018-01-31 13:46:09
    ## 9 2018-01-31 13:40:42 2018-01-31 13:31:32 2018-01-31 13:31:31

``` r
## Sidebar: Why does Jenny name files this way? ----
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 2.2.1     ✔ purrr   0.2.4
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.4
    ## ✔ tidyr   0.7.2     ✔ stringr 1.2.0
    ## ✔ readr   1.1.1     ✔ forcats 0.2.0

    ## ── Conflicts ─────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
ft <- tibble(files = dir_ls(glob = "*.R"))
ft
```

    ## # A tibble: 5 x 1
    ##   files                              
    ##   <fs::path>                         
    ## 1 00_filesystem-practice_jenny.R     
    ## 2 00_filesystem-practice_jenny.spin.R
    ## 3 01_explore-libraries_comfy.R       
    ## 4 01_explore-libraries_jenny.R       
    ## 5 01_explore-libraries_spartan.R

``` r
ft %>%
  filter(str_detect(files, "explore"))
```

    ## # A tibble: 3 x 1
    ##   files                         
    ##   <fs::path>                    
    ## 1 01_explore-libraries_comfy.R  
    ## 2 01_explore-libraries_jenny.R  
    ## 3 01_explore-libraries_spartan.R

``` r
ft %>%
  mutate(files = path_ext_remove(files)) %>%
  separate(files, into = c("i", "topic", "flavor"), sep = "_")
```

    ## # A tibble: 5 x 3
    ##   i     topic               flavor    
    ## * <chr> <chr>               <chr>     
    ## 1 00    filesystem-practice jenny     
    ## 2 00    filesystem-practice jenny.spin
    ## 3 01    explore-libraries   comfy     
    ## 4 01    explore-libraries   jenny     
    ## 5 01    explore-libraries   spartan

``` r
dirs <- dir_ls(path_home("Desktop"), type = "directory")
(dt <- tibble(dirs = path_file(dirs)))
```

    ## # A tibble: 5 x 1
    ##   dirs                     
    ##   <fs::path>               
    ## 1 2017-Oct-Desktop         
    ## 2 Jobs                     
    ## 3 day1_s1_explore-libraries
    ## 4 day1_s2_copy-files       
    ## 5 explore-libraries

``` r
dt %>%
  separate(dirs, into = c("day", "session", "topic"), sep = "_")
```

    ## Warning: Too few values at 3 locations: 1, 2, 5

    ## # A tibble: 5 x 3
    ##   day               session topic            
    ## * <chr>             <chr>   <chr>            
    ## 1 2017-Oct-Desktop  <NA>    <NA>             
    ## 2 Jobs              <NA>    <NA>             
    ## 3 day1              s1      explore-libraries
    ## 4 day1              s2      copy-files       
    ## 5 explore-libraries <NA>    <NA>

``` r
## Principled use of delimiters --> meta-data can be recovered from filename

## Clean it out, so we reset for workshop ----
file_delete(to_files)
dir_ls()
```

    ## 00_filesystem-practice_jenny.R
    ## 00_filesystem-practice_jenny.html
    ## 00_filesystem-practice_jenny.spin.R
    ## 00_filesystem-practice_jenny.spin.Rmd
    ## README.md
    ## explore-libraries.Rproj
