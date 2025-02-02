# utl-select-fruits-purchased-and-not-purchased--from-old-macdonalds-farm-excel-r-sql
Select fruits purchased and not purchased from old macdonalds farm excel r sql
    %let pgm=utl-select-fruits-purchased-and-not-purchased--from-old-macdonalds-farm-excel-r-sql;

    Select fruits purchased and not purchased from old macdonalds farm excel r sql

    excel output
    https://tinyurl.com/6bh5df4j
    https://github.com/rogerjdeangelis/utl-select-fruits-purchased-and-not-purchased--from-old-macdonalds-farm-excel-r-sql/blob/main/wantxl.xlsx

    github
    https://tinyurl.com/59rnt8ab
    https://github.com/rogerjdeangelis/utl-select-fruits-purchased-and-not-purchased--from-old-macdonalds-farm-excel-r-sql

    stackoverflow excel
    https://tinyurl.com/2mvntycv
    https://stackoverflow.com/questions/79401121/need-help-aligning-a-table-to-a-column-based-on-similar-values-in-one-table-fiel

    Basically I simple left join


    /*************************************************************************************************************************/
    /*                                   |                   |                                                               */
    /*                                   |                   |                                                               */
    /*               INPUT               |      PROCESS      |                           OUTPUT                              */
    /*                                   |    left join      |                                                               */
    /*                                   |    on ref2=ref1   |                                                               */
    /*                                   |                   |                                                               */
    /*                                   |                   |                                                               */
    /* ------------------+               | R SQL             | --------------------+            <---- ADDED COLUMNS ------>  */
    /* | A1|fx | ID      |               |                   | | A1| fx  | ID      |            <-- MATCH KEYS --->          */
    /* --------------------------------- | select            | ------------------------------------------------------------  */
    /* [_] | A |    B   |   C|    E    | |    l.ref2         | [_] | A |   B   |  C |    D    |E|   F     |  G    |H | I  |  */
    /* --------------------------------- |   ,r.ref1         | ------------------------------------------------------------  */
    /*  1  |ID |  REF1  |MISC|  REF2   | |   ,r.id           |  1  |ID | REF1  |MISC|  REF2   | |REF2     | REF1  |ID|MISC|  */
    /*  -- |---+--------+----+---------+ |   ,r.misc         |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  2  | 3 | apple  | a  | orange  | | from              |  2  | 3 |apple  | a  | orange  | | apple   |apple  | 3| a  |  */
    /*  -- |---+--------+----+---------+ |   (select         |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  3  | 7 | banana | b  | grape   | |      ref2         |  3  | 7 |banana | b  | grape   | | apricot |apricot|10| c  |  */
    /*  -- |---+--------+----+---------+ |    from           |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  4  | 10| apricot| c  | banana  | |      have) as l   |  4  | 10|apricot| c  | banana  | | banana  |banana | 7| b  |  */
    /*  -- |---+--------+----+---------+ | left join         |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  5  | 12| bean   | d  | apple   | |    have as r      |  5  | 12|bean   | d  | apple   | | bean    |bean   |12| a  |  */
    /*  -- |---+--------+----+---------+ |  on               |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  6  | . |        |    | bluebery| |    l.ref2 = r.ref1|  6  | . |       |    | bluebery| | bluebery|       | .|    |  */
    /*  -- |---+--------+----+---------+ |  order            |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  7  | . |        |    | strabery| |    by l.ref2      |  7  | . |       |    | strabery| | grape   |       | .|    |  */
    /*  -- |---+--------+----+---------+ |                   |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  8  | . |        |    | bean    | |                   |  8  | . |       |    | bean    | | orange  |       | .|    |  */
    /*  -- |---+--------+----+---------+ |                   |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /*  9  | . |        |    | apricot | |                   |  9  | . |       |    | apricot | | strabery|       | .|    |  */
    /*  -- |---+--------+----+---------+ |                   |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /* 10  | . |        |    | strabery| |                   | 10  | . |       |    | strabery| | strabery|       | .|    |  */
    /*  -- |---+--------+----+---------+ |                   |  -- |---+-------+----+---------+-|---------+-------+--+----+  */
    /* [HAVE}                            |                   |  [HAVE}                                                       */
    /*                                   |                   |                                                               */
    /*                                   | ACCEPTED ANSWER   |                                                               */
    /*                                   |                   |                                                               */
    /*                                   | =LET(base,E2:E9,  |                                                               */
    /*                                   | look,B2:B5,       |                                                               */
    /*                                   | table,A2:C5,      |                                                               */
    /*                                   | render,IF(        |                                                               */
    /*                                   |    ISNUMBER(      |                                                               */
    /*                                   |    MATCH(base     |                                                               */
    /*                                   |     ,look,0))     |                                                               */
    /*                                   |  ,CHOOSEROWS(table|                                                               */
    /*                                   |  ,IFERROR(        |                                                               */
    /*                                   |   MATCH(base      |                                                               */
    /*                                   |   ,look,0),1))    |                                                               */
    /*                                   |   ,""),           |                                                               */
    /*                                   | HSTACK(render     |                                                               */
    /*                                   |  ,base))          |                                                               */
    /*                                   |                   |                                                               */
    /*************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     input ID Ref1$ Misc$ ref2$;
    cards4;
    3 apple a  orange
    7 banana b  grape
    10 apricot c banana
    12 bean d apple
    . . . bluebery
    . . . strabery
    . . . bean
    . . . apricot
    . . . strabery
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  ID    REF1       MISC    REF2                                                                                         */
    /*                                                                                                                        */
    /*   3    apple       a      orange                                                                                       */
    /*   7    banana      b      grape                                                                                        */
    /*  10    apricot     c      banana                                                                                       */
    /*  12    bean        d      apple                                                                                        */
    /*   .                       bluebery                                                                                     */
    /*   .                       strabery                                                                                     */
    /*   .                       bean                                                                                         */
    /*   .                       apricot                                                                                      */
    /*   .                       strabery                                                                                     */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                 _                    _
      _____  _____ ___| |  _ __   ___  __ _| |
     / _ \ \/ / __/ _ \ | | `__| / __|/ _` | |
    |  __/>  < (_|  __/ | | |    \__ \ (_| | |
     \___/_/\_\___\___|_| |_|    |___/\__, |_|
     _                   _         _     |_|       _
    (_)_ __  _ __  _   _| |_   ___| |__   ___  ___| |_
    | | `_ \| `_ \| | | | __| / __| `_ \ / _ \/ _ \ __|
    | | | | | |_) | |_| | |_  \__ \ | | |  __/  __/ |_
    |_|_| |_| .__/ \__,_|\__| |___/_| |_|\___|\___|\__|
            |_|
    */

    %utlfkil(d:/xls/wantxl.xlsx);

    %utl_rbeginx;
    parmcards4;
    library(openxlsx)
    library(sqldf)
    library(haven)
    have<-read_sas("d:/sd1/have.sas7bdat")
    wb <- createWorkbook()
    addWorksheet(wb, "have")
    writeData(wb, sheet = "have", x = have)
    saveWorkbook(
        wb
       ,"d:/xls/wantxl.xlsx"
       ,overwrite=TRUE)
    ;;;;
    %utl_rendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*    ------------------+                                                                                                 */
    /*    | A1|fx | ID      |                                                                                                 */
    /*    ---------------------------------                                                                                   */
    /*    [_] | A |    B   |   C|    E    |                                                                                   */
    /*    ---------------------------------                                                                                   */
    /*     1  |ID |  REF1  |MISC|  REF2   |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     2  | 3 | apple  | a  | orange  |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     3  | 7 | banana | b  | grape   |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     4  | 10| apricot| c  | banana  |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     5  | 12| bean   | d  | apple   |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     6  | . |        |    | bluebery|                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     7  | . |        |    | strabery|                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     8  | . |        |    | bean    |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*     9  | . |        |    | apricot |                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*    10  | . |        |    | strabery|                                                                                   */
    /*     -- |---+--------+----+---------+                                                                                   */
    /*    [HAVE}                                                                                                              */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(openxlsx)
    library(sqldf)
    source("c:/oto/fn_tosas9x.R")
     wb<-loadWorkbook("d:/xls/wantxl.xlsx")
     have<-read.xlsx(wb,"have")
     addWorksheet(wb, "want")
     want<-sqldf('
      select
         l.ref2
        ,r.ref1
        ,r.id
        ,r.misc
      from
        (select
           ref2
         from
           have) as l
         left join
           have as r
         on
           l.ref2 = r.ref1
         order
           by l.ref2
      ')
     print(want)
     writeData(wb, sheet = "have", x = want, startRow = 1, startCol = 6)
     saveWorkbook(
         wb
        ,"d:/xls/wantxl.xlsx"
        ,overwrite=TRUE)
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;


    /*************************************************************************************************************************/
    /*                                                                                                                      */
    /*                                                                                                                      */
    /*                           OUTPUT                                                                                     */
    /*                                                                                                                      */
    /*                                                                                                                      */
    /*                                                                                                                      */
    /*                                                                                                                      */
    /* --------------------+            <---- ADDED COLUMNS ------>                                                         */
    /* | A1| fx  | ID      |            <-- MATCH KEYS --->                                                                 */
    /* ------------------------------------------------------------                                                         */
    /* [_] | A |   B   |  C |    D    |E|   F     |  G    |H | I  |                                                         */
    /* ------------------------------------------------------------                                                         */
    /*  1  |ID | REF1  |MISC|  REF2   | |REF2     | REF1  |ID|MISC|                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  2  | 3 |apple  | a  | orange  | | apple   |apple  | 3| a  |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  3  | 7 |banana | b  | grape   | | apricot |apricot|10| c  |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  4  | 10|apricot| c  | banana  | | banana  |banana | 7| b  |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  5  | 12|bean   | d  | apple   | | bean    |bean   |12| a  |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  6  | . |       |    | bluebery| | bluebery|       | .|    |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  7  | . |       |    | strabery| | grape   |       | .|    |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  8  | . |       |    | bean    | | orange  |       | .|    |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  9  | . |       |    | apricot | | strabery|       | .|    |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /* 10  | . |       |    | strabery| | strabery|       | .|    |                                                         */
    /*  -- |---+-------+----+---------+-|---------+-------+--+----+                                                         */
    /*  [HAVE}                                                                                                              */
    /*                                                                                                                      */
    /*************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
