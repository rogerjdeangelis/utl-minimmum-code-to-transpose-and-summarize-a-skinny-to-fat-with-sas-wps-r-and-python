# utl-minimmum-code-to-transpose-and-summarize-a-skinny-to-fat-with-sas-wps-r-and-python
Minimmum code_to transpose and summarize a skinny to fat numeric array with sas wps r and python 
    %let pgm=utl-minimmum-code-to-transpose-and-summarize-a-skinny-to-fat-with-sas-wps-r-and-python;

    Minimmum code_to transpose and summarize a skinny to fat numeric array with sas wps r and python

    github
    https://tinyurl.com/2j3w66ds
    https://github.com/rogerjdeangelis/utl-minimmum-code-to-transpose-and-summarize-a-skinny-to-fat-with-sas-wps-r-and-python

        All of these create output datasets, including report, tabulate and freq, where the dataset has a fat structure.
        SAS does not honor ODS with report, tabulate and freq

           1. wps/sas proc corresp (same output in sas and wps)
           2. wps/sas proc report (same output in sas and wps)
           3. wps/sas datastep (same output in sas and wps)
           4. wps/sas summary transpose
           5. wps/sas tabulate (same output in sas and wps)
           6. wps/sas hash transpose (same output in sas and wps)
           7. wps/sas proc freq (same output in sas and wps)
           8. wps/python pivot
           9. wps/python crosstab
          10. wps/r tidyverse
          11. sas sql no dosubl and arrays
          12  wps sql no nosubl and arrays (dosubl not supported in wps yet)
          13  wps sql dosubl and arrays
          14  wps sql arrays
          15  wps r sql
          16  python sql


    StakOverflow Python
    https://tinyurl.com/38hvyaxs
    https://stackoverflow.com/questions/47152691/how-can-i-pivot-a-dataframe

    options validvarname=upcase;
    data have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    /**************************************************************************************************************************/
    /*                                       |                    |                                                           */
    /*                                       |                    |                                                           */
    /*  HAVE total obs=20                    |   RULES SUMMARIZE  |  OUTPUT TRANSPOSED                                        */
    /*                                       |                    |                                                           */
    /*  Obs    ROW     COL     VAL0          |   SUMS             |   LABEL    COL0    COL1    COL2    COL3    COL4           */
    /*                                       |                    |                                                           */
    /*    1    row0    col1    0.51          |                    |   row0     0.00    0.55    0.40    1.02    0.00           */
    /*    2    row0    col1    0.04          |   0.55             |   row1     0.96    0.32    0.23    0.00    0.00           */
    /*                                       |                    |   row2     1.26    0.00    1.05    1.06    0.00           */
    /*    3    row0    col2    0.26          |                    |   row3     0.03    0.00    0.00    0.00    0.12           */
    /*    4    row0    col2    0.14          |   0.40             |   row4     0.00    0.00    0.63    0.00    0.79           */
    /*                                       |                    |                                                           */
    /*    5    row0    col3    0.52          |                    |                                                           */
    /*    6    row0    col3    0.50          |   1.02             |                                                           */
    /*                                       |                    |                                                           */
    /*    7    row1    col0    0.96          |   0.96             |                                                           */
    /*    8    row1    col1    0.32          |   0.32             |                                                           */
    /*    9    row1    col2    0.23          |   0.23             |                                                           */
    /*                                       |                    |                                                           */
    /*   10    row2    col0    0.51          |                    |                                                           */
    /*   11    row2    col0    0.74          |                    |                                                           */
    /*   12    row2    col0    0.01          |   1.26             |                                                           */
    /*                                       |                    |                                                           */
    /*   13    row2    col2    0.80          |                    |                                                           */
    /*   14    row2    col2    0.25          |   1.05             |                                                           */
    /*                                       |                    |                                                           */
    /*   15    row2    col3    0.37          |                    |                                                           */
    /*   16    row2    col3    0.69          |   1.06             |                                                           */
    /*                                       |                    |                                                           */
    /*   17    row3    col0    0.03          |   0.03             |                                                           */
    /*   18    row3    col4    0.12          |   0.12             |                                                           */
    /*   19    row4    col2    0.63          |   0.63             |                                                           */
    /*   20    row4    col4    0.79          |   0.79             |                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                           __
    / |   __      ___ __  ___   / /__  __ _ ___    ___ ___  _ __ _ __ ___  ___ _ __
    | |   \ \ /\ / / `_ \/ __| / / __|/ _` / __|  / __/ _ \| `__| `__/ _ \/ __| `_ \
    | |_   \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | (_| (_) | |  | | |  __/\__ \ |_) |
    |_(_)   \_/\_/ | .__/|___/_/ |___/\__,_|___/  \___\___/|_|  |_|  \___||___/ .__/
                   |_|                                                        |_|
    */
    proc datasets lib=work nodetails nolist; delete want; run;quit;

    ods exclude all;
    ods output observed=want ;
    proc corresp data=have dim=1 observed;
       table row, col;
       weight val0;
    run;quit;
    ods select all;

    /*----                      WPS                                          ----*/

    %let _pth=%sysfunc(pathname(work));
    %utl_submit_wps64("
    libname wrk '&_pth';
    proc datasets lib=wrk nodetails nolist; delete want; run;quit;
    ods exclude all;
    ods output observed=wrk.want ;
    proc corresp data=wrk.have dim=1 observed;
       tables row, col;
       weight val0;
    run;quit;
    ods select all;
    proc print data=wrk.want;
    run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Up to 40 obs from WANT total obs=6 05JUN2023:13:58:18                                                                 */
    /*                                                                                                                        */
    /*  Obs    LABEL    COL0    COL1    COL2    COL3    COL4     SUM                                                          */
    /*                                                                                                                        */
    /*   1     row0     0.00    0.55    0.40    1.02    0.00    1.97                                                          */
    /*   2     row1     0.96    0.32    0.23    0.00    0.00    1.51                                                          */
    /*   3     row2     1.26    0.00    1.05    1.06    0.00    3.37                                                          */
    /*   4     row3     0.03    0.00    0.00    0.00    0.12    0.15                                                          */
    /*   5     row4     0.00    0.00    0.63    0.00    0.79    1.42                                                          */
    /*                                                                                                                        */
    /*   6     Sum      2.25    0.87    2.31    2.08    0.91    8.42                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                            __                                         _
    |___ \    __      ___ __  ___   / /__  __ _ ___   _ __ ___ _ __   ___  _ __| |_
      __) |   \ \ /\ / / `_ \/ __| / / __|/ _` / __| | `__/ _ \ `_ \ / _ \| `__| __|
     / __/ _   \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | | |  __/ |_) | (_) | |  | |_
    |_____(_)   \_/\_/ | .__/|___/_/ |___/\__,_|___/ |_|  \___| .__/ \___/|_|   \__|
                       |_|                                    |_|
    */

    proc datasets lib=work nodetails nolist; delete want; run;quit;

    proc report data=have nowd missing  out=want (drop=_break_ rename=(
    _C2_=col0 _C3_=col1 _C4_=col2 _C5_=col3 _C6_=col5));
    format _numeric_ 5.3;
    column row col , val0 ;
    define row / Group;
    define col / across;
    define val0 / sum f=6.3;
    run;quit;
    proc print data=want;
    run;quit;

    /*----                      WPS                                          ----*/

    %let _pth=%sysfunc(pathname(work));
    %utl_submit_wps64("
    libname wrk '&_pth';

    proc datasets lib=wrk nodetails nolist; delete want; run;quit;

    proc report data=wrk.have nowd missing  out=wrk.want(drop=_break_ rename=(
       _C2_=col0 _C3_=col1 _C4_=col2 _C5_=col3 _C6_=col4));
    format _numeric_ 5.3;
    column row col , val0 ;
    define row / Group;
    define col / across;
    define val0 / sum f=6.3;
    run;quit;
    proc print data=wrk.want;
    run;quit;

    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Up to 40 obs from WANT total obs=5 05JUN2023:16:34:27                                                                  */
    /*                                                                                                                        */
    /* Obs    ROW     COL0    COL1    COL2    COL3    COL5                                                                    */
    /*                                                                                                                        */
    /*  1     row0     0      0.55    0.40    1.02     0                                                                      */
    /*  2     row1    0.96    0.32    0.23     0       0                                                                      */
    /*  3     row2    1.26     0      1.05    1.06     0                                                                      */
    /*  4     row3    0.03     0       0       0      0.12                                                                    */
    /*  5     row4     0       0      0.63     0      0.79                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                          __                   _       _            _
    |___ /   __      ___ __  ___   / /__  __ _ ___    __| | __ _| |_ __ _ ___| |_ ___ _ __
      |_ \   \ \ /\ / / `_ \/ __| / / __|/ _` / __|  / _` |/ _` | __/ _` / __| __/ _ \ `_ \
     ___) |   \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | (_| | (_| | || (_| \__ \ ||  __/ |_) |
    |____(_)   \_/\_/ | .__/|___/_/ |___/\__,_|___/  \__,_|\__,_|\__\__,_|___/\__\___| .__/
                      |_|                                                            |_|

    */
    proc datasets lib=work nodetails nolist; delete want; run;quit;

     data want (keep=rows col0-col4);

       retain rows rowsum 0;

       do until (dne);
         set have end=dne;
           by row col;
           if first.col then rowsum=0;
           rowSum=sum(rowSum,val0);
         if last.col;
         array xpo[0:4,0:4] _temporary_ ;
         i=input(substr(row,4),best.);
         j=input(substr(col,4),best.);
         xpo[i,j] = rowSum;
         put row= col= i= j= rowsum= xpo[i,j]=;
      end;

      array cols[0:4] col0-col4;
      do rows=0 to 4;
        do j=0 to 4;
           cols[j]=xpo[rows,j];
           put i= j= xpo[rows,j]=;
        end;
      output;
      end;
      stop;

    run;quit;

    /*----                      WPS                                          ----*/

    %let _pth=%sysfunc(pathname(work));

    %utl_submit_wps64("

    libname wrk '&_pth';

    proc datasets lib=wrk nodetails nolist; delete want; run;quit;

     data wrk.want(keep=rows col0-col4);

       retain rows rowsum 0;

       do until (dne);
         set wrk.have end=dne;
           by row col;
           if first.col then rowsum=0;
           rowSum=sum(rowSum,val0);
         if last.col;
         array xpo[0:4,0:4] _temporary_ ;
         i=input(substr(row,4),best.);
         j=input(substr(col,4),best.);
         xpo[i,j] = rowSum;
         put row= col= i= j= rowsum= xpo[i,j]=;
      end;

      array cols[0:4] col0-col4;
      do rows=0 to 4;
        do j=0 to 4;
           cols[j]=xpo[rows,j];
           put i= j= xpo[rows,j]=;
        end;
      output;
      end;
      stop;

     run;quit;
     proc print data=wrk.want;
     run;quit;

    ");


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Up to 40 obs from last table WORK.WANT total obs=5 06JUN2023:08:33:39                                                 */
    /*                                                                                                                        */
    /*  Obs    ROWS    COL0    COL1    COL2    COL3    COL4                                                                   */
    /*                                                                                                                        */
    /*   1       0      0      0.55    0.40    1.02     0                                                                     */
    /*   2       1     0.96    0.32    0.23     0       0                                                                     */
    /*   3       2     1.26     0      1.05    1.06     0                                                                     */
    /*   4       3     0.03     0       0       0      0.12                                                                   */
    /*   5       4      0       0      0.63     0      0.79                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                            __
    | || |    __      ___ __  ___   / /__  __ _ ___   ___ _   _ _ __ ___  _ __ ___   __ _ _ __ _   _
    | || |_   \ \ /\ / / `_ \/ __| / / __|/ _` / __| / __| | | | `_ ` _ \| `_ ` _ \ / _` | `__| | | |
    |__   _|   \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ \__ \ |_| | | | | | | | | | | | (_| | |  | |_| |
       |_|(_)   \_/\_/ | .__/|___/_/ |___/\__,_|___/ |___/\__,_|_| |_| |_|_| |_| |_|\__,_|_|   \__, |
                       |_|                                                                     |___/
    */
    proc datasets lib=work nodetails nolist; delete want; run;quit;

    proc summary data=have nway;
    class row col;
    var val0;
    output out=havSmy idgroup(out[5](val0 )=) sum=val0;
    run;

    proc transpose data=havSmy out=want;
    by row;
    id col;
    var val0;
    run;quit;

    proc print data=want;
    run;quit;

    /*----                      WPS                                          ----*/

    %let _pth=%sysfunc(pathname(work));

    %utl_submit_wps64("

    libname wrk '&_pth';

    proc datasets lib=wrk nodetails nolist; delete want; run;quit;

    proc summary data=wrk.have nway;
    class row col;
    var val0;
    output out=wrk.havSmy idgroup(out[5](val0 )=) sum=val0;
    run;

    proc transpose data=wrk.havSmy out=wrk.want;
    by row;
    id col;
    var val0;
    run;quit;

    proc print data=wrk.want;
    run;quit;

    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS System                                                                                                         */
    /*                                                                                                                        */
    /* Obs    ROW     _NAME_    col0    col1    col2    col3    col4                                                          */
    /*                                                                                                                        */
    /*  1     row0     val0      .       .55    0.40    1.02     .                                                            */
    /*  2     row1     val0     0.96     .32    0.23     .       .                                                            */
    /*  3     row2     val0     1.26     .      1.05    1.06     .                                                            */
    /*  4     row3     val0     0.03     .       .       .       .12                                                          */
    /*  5     row4     val0      .       .      0.63     .       .79                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
     /*
     ____                          __               _        _           _       _
    | ___|  __      ___ __  ___   / /__  __ _ ___  | |_ __ _| |__  _   _| | __ _| |_ ___
    |___ \  \ \ /\ / / `_ \/ __| / / __|/ _` / __| | __/ _` | `_ \| | | | |/ _` | __/ _ \
     ___) |  \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | || (_| | |_) | |_| | | (_| | ||  __/
    |____/    \_/\_/ | .__/|___/_/ |___/\__,_|___/  \__\__,_|_.__/ \__,_|_|\__,_|\__\___|
                      |_|
    */

    proc datasets lib=work nodetails nolist; delete want; run;quit;

    %utl_odstbx(setup,intermediate=_temp_);
    proc tabulate data=have;
      title "|Row|col0|col1|col2|col3|col4|";
      class row col;
      table row,col*(val0*sum)/rts=8;
      var val0;
    run;quit;
    %utl_odstbx(want);
    proc print data=want;
    run;quit;

    /*----                      WPS                                          ----*/

    libname sd1 "d:/sd1";

    data sd1.have;
      set have;
    run;quit;

    %utl_submit_wps64('

    libname sd1 "d:/sd1";

    options sasautos=("c:/otowps");

    %utl_odstbx(setup,intermediate=_temp_);
    proc tabulate data=sd1.have;
      title "|Row|col0|col1|col2|col3|col4|";
      class row col;
      table row,col*(val0*sum)/rts=8;
      var val0;
    run;quit;
    %utl_odstbx(want);
    proc print data=want;
    run;quit;
    ',resolve=N);

    /*__                           __               _               _       _
     / /_   __      ___ __  ___   / /__  __ _ ___  | |__   __ _ ___| |__   | |_ _ __ __ _ _ __  ___ _ __   ___  ___  ___
    | `_ \  \ \ /\ / / `_ \/ __| / / __|/ _` / __| | `_ \ / _` / __| `_ \  | __| `__/ _` | `_ \/ __| `_ \ / _ \/ __|/ _ \
    | (_) |  \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | | | | (_| \__ \ | | | | |_| | | (_| | | | \__ \ |_) | (_) \__ \  __/
     \___/    \_/\_/ | .__/|___/_/ |___/\__,_|___/ |_| |_|\__,_|___/_| |_|  \__|_|  \__,_|_| |_|___/ .__/ \___/|___/\___|
                     |_|                                                                           |_|
    */

    data _null_ ;

     dcl hash H (ordered: "A") ;
     h.definekey ("ROW","COL") ;
     h.definedata ("ROW", "COL", "SUM") ;
     h.definedone () ;

     dcl hash U () ;
     u.definekey ("ROW","COL","VAL0") ;
     u.definedone () ;

     do until (dne) ;
     set have end = dne ;
     if h.find() ne 0 then call missing (SUM) ;
     SUM = sum (SUM, VAL0) ;
     u.add() ;
     h.replace() ;

    end;
    h.output (dataset: "havSum") ;
    rc = dosubl('
          proc transpose data=havSum out=want;
            by row;
            id col;
            var sum;
          ;quit;
        ');
    stop ;
    run ;
    proc print data=want;
    run;quit;


    /*----                      WPS                                          ----*/


    libname sd1 "d:/sd1";

    data sd1.have;
      set have;
    run;quit;

    %utl_submit_wps64("

    libname sd1 'd:/sd1';

    proc datasets lib=work nodetails nolist; delete want; run;quit;

    data _null_ ;
     dcl hash H (ordered: 'A') ;
     h.definekey ('ROW','COL') ;
     h.definedata ('ROW', 'COL', 'SUM') ;
     h.definedone () ;

     dcl hash U () ;
     u.definekey ('ROW','COL','VAL0') ;
     u.definedone () ;

     do until (dne) ;
     set sd1.have end = dne ;
     if h.find() ne 0 then call missing (SUM) ;
     SUM = sum (SUM, VAL0) ;
     u.add() ;
     h.replace() ;

    end;
    h.output (dataset: 'havSum') ;
    rc = dosubl('
          proc transpose data=havSum out=want;
            by row;
            id col;
            var sum;
          ;quit;
        ');
    stop ;
    run ;
    proc print data=want;
    run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Note col0 is out of order for both SAS and WPS                                                                        */
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  Obs    ROW     _NAME_    col1    col2    col3    col0    col4                                                         */
    /*                                                                                                                        */
    /*   1     row0     SUM       .55    0.40    1.02     .       .                                                           */
    /*   2     row1     SUM       .32    0.23     .      0.96     .                                                           */
    /*   3     row2     SUM       .      1.05    1.06    1.26     .                                                           */
    /*   4     row3     SUM       .       .       .      0.03     .12                                                         */
    /*   5     row4     SUM       .      0.63     .       .       .79                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*____                         __                __
    |___  | __      ___ __  ___   / /__  __ _ ___   / _|_ __ ___  __ _
       / /  \ \ /\ / / `_ \/ __| / / __|/ _` / __| | |_| `__/ _ \/ _` |
      / /_   \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ |  _| | |  __/ (_| |
     /_/(_)   \_/\_/ | .__/|___/_/ |___/\__,_|___/ |_| |_|  \___|\__, |
                     |_|                                            |_|
    */
    proc datasets lib=work nodetails nolist; delete want; run;quit;

    %utl_odsfrq(setup);
    proc freq data=sd1.have ;
    tables row*col / norow nocol nopercent;
    weight val0;
    run;quit;
    %utl_odsfrq(want);
    proc print data=want(keep=frequency--total);
    run;quit;

    /*----                      WPS                                          ----*/

    libname sd1 "d:/sd1";

    data sd1.have;
      set have;
    run;quit;

    /*---- I editied my autocall macros to use only double quotes            ----*/

    %utl_submit_wps64('

    options sasautos="c:/otowps");
    libname sd1 "d:/sd1";

    proc datasets lib=work nodetails nolist; delete want; run;quit;

    %utl_odsfrq(setup);
    proc freq data=sd1.have ;
    tables row*col /missing norow nocol nopercent;
    weight val0;
    run;quit;
    %utl_odsfrq(want);
    proc print data=_temp_;
    format _numeric_ 8.2;
    run;quit;
    proc print data=want(keep=frequency--total);
    format _numeric_ 8.2;
    run;quit;
    ',resolve=N);

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  WPS System (you may have change single quotes to double quotes in utl_odsfrq)                                         */
    /*                                                                                                                        */
    /*  Obs    FREQUENCY        COL0        COL1        COL2        COL3        COL4       TOTAL                              */
    /*                                                                                                                        */
    /*   1      row0            0.00        0.55        0.40        1.02        0.00        1.97                              */
    /*   2      row1            0.96        0.32        0.23        0.00        0.00        1.51                              */
    /*   3      row2            1.26        0.00        1.05        1.06        0.00        3.37                              */
    /*   4      row3            0.03        0.00        0.00        0.00        0.12        0.15                              */
    /*   5      row4            0.00        0.00        0.63        0.00        0.79        1.42                              */
    /*                                                                                                                        */
    /*   6      Total           2.25        0.87        2.31        2.08        0.91        8.42                              */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                           __           _   _                         _            _
     ( _ )   __      ___ __  ___   / / __  _   _| |_| |__   ___  _ __    _ __ (_)_   _____ | |_
     / _ \   \ \ /\ / / `_ \/ __| / / `_ \| | | | __| `_ \ / _ \| `_ \  | `_ \| \ \ / / _ \| __|
    | (_) |   \ V  V /| |_) \__ \/ /| |_) | |_| | |_| | | | (_) | | | | | |_) | |\ V / (_) | |_
     \___(_)   \_/\_/ | .__/|___/_/ | .__/ \__, |\__|_| |_|\___/|_| |_| | .__/|_| \_/ \___/ \__|
                      |_|           |_|    |___/                        |_|

    */

    options validvarname=upcase;
    data have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;

    %let _pth=%sysfunc(pathname(work));

    %utl_submit_wps64("

    libname wrk '&_pth';

    proc python;
    export data=wrk.have python=have;
    submit;
    import numpy as np;
    import pandas as pd;
    want=pd.pivot_table(have,values ='VAL0', index='ROW', columns='COL',aggfunc='sum',fill_value=0);
    print(want);
    endsubmit;
    ");

    /*___                           __           _   _                        _        _
     / _ \   __      ___ __  ___   / / __  _   _| |_| |__   ___  _ __   __  _| |_ __ _| |__
    | (_) |  \ \ /\ / / `_ \/ __| / / `_ \| | | | __| `_ \ / _ \| `_ \  \ \/ / __/ _` | `_ \
     \__, |   \ V  V /| |_) \__ \/ /| |_) | |_| | |_| | | | (_) | | | |  >  <| || (_| | |_) |
       /_(_)   \_/\_/ | .__/|___/_/ | .__/ \__, |\__|_| |_|\___/|_| |_| /_/\_\\__\__,_|_.__/
                      |_|           |_|    |___/
    */


    %let _pth=%sysfunc(pathname(work));

    %utl_submit_wps64("

    libname wrk '&_pth';

    proc python;
    export data=wrk.have python=have;
    submit;
    import numpy as np;
    import pandas as pd;
    want=pd.crosstab(have['ROW'], have['COL'], have['VAL0'], aggfunc='sum', margins=True);
    want=want.fillna(0);
    print(want);
    endsubmit;
    ");

    /*  ___                           __      _   _     _
    / |/ _ \   __      ___ __  ___   / / __  | |_(_) __| |_   ___   _____ _ __ ___  ___
    | | | | |  \ \ /\ / / `_ \/ __| / / `__| | __| |/ _` | | | \ \ / / _ \ `__/ __|/ _ \
    | | |_| |   \ V  V /| |_) \__ \/ /| |    | |_| | (_| | |_| |\ V /  __/ |  \__ \  __/
    |_|\___(_)   \_/\_/ | .__/|___/_/ |_|     \__|_|\__,_|\__, | \_/ \___|_|  |___/\___|
                        |_|                               |___/
    */


    proc datasets lib=work nodetails nolist; delete want; run;quit;

    %let _pth=%sysfunc(pathname(work));

    %utl_submit_wps64("

    libname wrk '&_pth';

    proc r;
    export data=wrk.have r=have;
    submit;
    library(tidyverse);
    want<-have %>%
      group_by(ROW, COL) %>%
      summarize(value = sum(VAL0, na.rm = T)) %>%
      pivot_wider(names_from = COL);
      want <- want %>% replace(is.na(.), 0);
      want;
    endsubmit;
    import data=wrk.want r=want;
    proc print data=wrk.want;
    run;quit;
    endsubmit;
    ");

    proc print data=want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                          |                                                                             */
    /*                                          |                                                                             */
    /*                                          |                                                                             */
    /* The WPS R System                         |  WPS/SAS                                                                    */
    /*                                          |                                                                             */
    /* # A tibble: 5 x 6                        |  Obs    ROW     COL1    COL2    COL3    COL0    COL4                        */
    /* # Groups:   ROW [5]                      |                                                                             */
    /*   ROW    col1  col2  col3  col0  col4    |   1     row0     .55    0.40    1.02    0.00     .00                        */
    /*   <chr> <dbl> <dbl> <dbl> <dbl> <dbl>    |   2     row1     .32    0.23    0.00    0.96     .00                        */
    /* 1 row0   0.55  0.4   1.02  0     0       |   3     row2     .00    1.05    1.06    1.26     .00                        */
    /* 2 row1   0.32  0.23  0     0.96  0       |   4     row3     .00    0.00    0.00    0.03     .12                        */
    /* 3 row2   0     1.05  1.06  1.26  0       |   5     row4     .00    0.63    0.00    0.00     .79                        */
    /* 4 row3   0     0     0     0.03  0.12    |                                                                             */
    /* 5 row4   0     0.63  0     0     0.79    |                                                                             */
    /*                                          |                                                                             */
    /**************************************************************************************************************************/

    /* _                               _
    / / |    ___  __ _ ___   ___  __ _| |  _ __   ___     __ _ _ __ _ __ __ _ _   _
    | | |   / __|/ _` / __| / __|/ _` | | | `_ \ / _ \   / _` | `__| `__/ _` | | | |
    | | |_  \__ \ (_| \__ \ \__ \ (_| | | | | | | (_) | | (_| | |  | | | (_| | |_| |
    |_|_(_) |___/\__,_|___/ |___/\__, |_| |_| |_|\___/   \__,_|_|  |_|  \__,_|\__, |
                                    |_|                                       |___/
    */

    options validvarname=upcase;
    data have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;

    proc datasets lib=work nolist nodetails mt=data mt=view ;
     delete want havSumVue havRowVue ;
    run;quit;

    options missing='0';
    proc sql;
      create
         view havSumVue as
      select
         col
        ,row
        ,sum(val0) as val0Sum
      from
         have
      group
         by row, col
    ;
     create
        view havRowVue as
     select
        distinct row as rowUnq
     from
        havSumVue
    ;
     create
         table havXpo as
     select
         rows.rowUnq as row
        ,c0.val0Sum as col0
        ,c1.val0Sum as col1
        ,c2.val0Sum as col2
        ,c3.val0Sum as col3
        ,c4.val0Sum as col4
     from
           havRowVue as rows
            left join havSumVue as c0 on rows.rowUnq = c0.Row and c0.col='col0'
            left join havSumVue as c1 on rows.rowUnq = c1.Row and c1.col='col1'
            left join havSumVue as c2 on rows.rowUnq = c2.Row and c2.col='col2'
            left join havSumVue as c3 on rows.rowUnq = c3.Row and c3.col='col3'
            left join havSumVue as c4 on rows.rowUnq = c4.Row and c4.col='col4'
    ;quit;

     /**************************************************************************************************************************/
     /*                                                                                                                        */
     /*  INTERMEDIATE DATASETS                                                                                                 */
     /*                                                                                                                        */
     /*  UHAVSUMVUE total obs=13 11JUN2023:09:59:09                                                                            */
     /*                                                                                                                        */
     /*       Obs    COL     ROW     VAL0SUM                                                                                   */
     /*                                                                                                                        */
     /*         1    col1    row0      0.55                                                                                    */
     /*         2    col2    row0      0.40                                                                                    */
     /*         3    col3    row0      1.02                                                                                    */
     /*         4    col0    row1      0.96                                                                                    */
     /*         5    col1    row1      0.32                                                                                    */
     /*         6    col2    row1      0.23                                                                                    */
     /*         7    col0    row2      1.26                                                                                    */
     /*         8    col2    row2      1.05                                                                                    */
     /*         9    col3    row2      1.06                                                                                    */
     /*        10    col0    row3      0.03                                                                                    */
     /*        11    col4    row3      0.12                                                                                    */
     /*        12    col2    row4      0.63                                                                                    */
     /*        13    col4    row4      0.79                                                                                    */
     /*                                                                                                                        */
     /* HAVROWVUE total obs=5 11JUN2023:10:00:16                                                                               */
     /*                                                                                                                        */
     /*       Obs    ROWUNQ                                                                                                    */
     /*                                                                                                                        */
     /*         1     row0                                                                                                     */
     /*         2     row1                                                                                                     */
     /*         3     row2                                                                                                     */
     /*         4     row3                                                                                                     */
     /*         5     row4                                                                                                     */
     /*                                                                                                                        */
     /*  FINAL OUTPUT                                                                                                          */
     /*                                                                                                                        */
     /*  HAVXPO total obs=5 11JUN2023:10:01:49                                                                                 */
     /*                                                                                                                        */
     /*  Obs    ROW     COL0    COL1    COL2    COL3    COL4                                                                   */
     /*                                                                                                                        */
     /*   1     row0     0      0.55    0.40    1.02     0                                                                     */
     /*   2     row1    0.96    0.32    0.23     0       0                                                                     */
     /*   3     row2    1.26     0      1.05    1.06     0                                                                     */
     /*   4     row3    0.03     0       0       0      0.12                                                                   */
     /*   5     row4     0       0      0.63     0      0.79                                                                  */
     /*                                                                                                                        */
     /**************************************************************************************************************************/

    /* ____
    / |___ \    __      ___ __  ___   _ __   ___     __ _ _ __ _ __ __ _ _   _
    | | __) |   \ \ /\ / / `_ \/ __| | `_ \ / _ \   / _` | `__| `__/ _` | | | |
    | |/ __/ _   \ V  V /| |_) \__ \ | | | | (_) | | (_| | |  | | | (_| | |_| |
    |_|_____(_)   \_/\_/ | .__/|___/ |_| |_|\___/   \__,_|_|  |_|  \__,_|\__, |
                         |_|                                             |___/
    */

    libname sd1 "d:/sd1";

    options validvarname=upcase;
    data sd1.have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;


    %utl_wpsbegin;
    parmcards4;

    options validvarname=any;

    libname sd1 "d:/sd1";

    proc datasets lib=work nolist nodetails mt=data mt=view ;
     delete want havSumVue havRowVue havXpoWps;
    run;quit;

    options missing='0';
    proc sql;
      create
         view havSumVue as
      select
         col
        ,row
        ,sum(val0) as val0Sum
      from
         sd1.have
      group
         by row, col
    ;
     create
        view havRowVue as
     select
        distinct row as rowUnq
     from
        havSumVue
    ;
     create
         table havXpoWps as
     select
         rows.rowUnq as row
        ,c0.val0Sum as col0
        ,c1.val0Sum as col1
        ,c2.val0Sum as col2
        ,c3.val0Sum as col3
        ,c4.val0Sum as col4
     from
           havRowVue as rows
            left join havSumVue as c0 on rows.rowUnq = c0.Row and c0.col='col0'
            left join havSumVue as c1 on rows.rowUnq = c1.Row and c1.col='col1'
            left join havSumVue as c2 on rows.rowUnq = c2.Row and c2.col='col2'
            left join havSumVue as c3 on rows.rowUnq = c3.Row and c3.col='col3'
            left join havSumVue as c4 on rows.rowUnq = c4.Row and c4.col='col4'
    ;quit;
    proc print data=havXpoWps;
    run;quit;
    ;;;;
    %utl_wpsend;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS System                                                                                                        */
    /*                                                                                                                        */
    /*  Obs    row     col0    col1    col2    col3    col4                                                                   */
    /*                                                                                                                        */
    /*   1     row0     0       .55    0.40    1.02     0                                                                     */
    /*   2     row1    0.96     .32    0.23     0       0                                                                     */
    /*   3     row2    1.26     0      1.05    1.06     0                                                                     */
    /*   4     row3    0.03     0       0       0       .12                                                                   */
    /*   5     row4     0       0      0.63     0       .79                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /* _____                              _
    / |___ /    ___  __ _ ___   ___  __ _| |   __ _ _ __ _ __ __ _ _   _ ___
    | | |_ \   / __|/ _` / __| / __|/ _` | |  / _` | `__| `__/ _` | | | / __|
    | |___) |  \__ \ (_| \__ \ \__ \ (_| | | | (_| | |  | | | (_| | |_| \__ \
    |_|____(_) |___/\__,_|___/ |___/\__, |_|  \__,_|_|  |_|  \__,_|\__, |___/
                                       |_|                         |___/
    */

    options validvarname=upcase;
    data have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;

    %symdel rowUnq rowUnq / nowarn;

    proc datasets lib=work nolist nodetails mt=data mt=view ;
     delete want havSumVue havRowVue havXpo;
    run;quit;

    %arraydelete(_v);

    /*----     Make sure the _v array does not exist                         ----*/
    /*----     Since rowUnq = colUnq=5 we only need one indes                ----*/

    %put check exitance of third element = &_v3 ;
    /*----  WARNING: Apparent symbolic reference _V3 not resolved.           ----*/

    proc sql;

      %dosubl('proc sql;select distinct input(substr(col,4),best.) into :_v1- from have;quit;%let _vn=&sqlobs;')
      %dosubl('proc sql;create view havRowVue as select distinct row as rowUnq from have;quit;')

      create
         view havSumVue as
      select
         col
        ,row
        ,sum(val0) as val0Sum
      from
         have
      group
         by row, col
    ;
    quit;

    %put &=_v3; /*---- 2                                                     ----*/
    %put &=_vn; /*---- 5                                                     ----*/

    options missing='0';
    proc sql;
     create
         table havXpo as
     select
         rows.rowUnq as row
       , %do_over(_v,phrase=c?.val0Sum as col?,between=comma)
     from
           havRowVue as rows
           %do_over(_v,phrase=%str(
            left join havSumVue as c? on rows.rowUnq = c?.Row and c?.col="col?"))
    ;quit;

    /*----  If you want the generated code                                   ----*/

    data _null_;
       %do_over(_v,phrase=%str(put "c?.val0Sum as col?";));
    run;quit;

    c0.val0Sum as col0
    c1.val0Sum as col1
    c2.val0Sum as col2
    c3.val0Sum as col3
    c4.val0Sum as col4

    data _null_;
       %do_over(_v,phrase=%str(put "left join havSumVue as c? on rows.rowUnq = c?.Row and c?.col='col?'";))
    run;quit;

    left join havSum as c0 on rows.rowUnq = c0.Row and c0.col='col0'
    left join havSum as c1 on rows.rowUnq = c1.Row and c1.col='col1'
    left join havSum as c2 on rows.rowUnq = c2.Row and c2.col='col2'
    left join havSum as c3 on rows.rowUnq = c3.Row and c3.col='col3'
    left join havSum as c4 on rows.rowUnq = c4.Row and c4.col='col4'


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  HAVXPO total obs=5 11JUN2023:10:52:53                                                                                 */
    /*                                                                                                                        */
    /*  Obs    ROW     COL0    COL1    COL2    COL3    COL4                                                                   */
    /*                                                                                                                        */
    /*   1     row0     0      0.55    0.40    1.02     0                                                                     */
    /*   2     row1    0.96    0.32    0.23     0       0                                                                     */
    /*   3     row2    1.26     0      1.05    1.06     0                                                                     */
    /*   4     row3    0.03     0       0       0      0.12                                                                   */
    /*   5     row4     0       0      0.63     0      0.79                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /* _  _                                     _
    / | || |    __      ___ __  ___   ___  __ _| |   __ _ _ __ _ __ __ _ _   _ ___
    | | || |_   \ \ /\ / / `_ \/ __| / __|/ _` | |  / _` | `__| `__/ _` | | | / __|
    | |__   _|   \ V  V /| |_) \__ \ \__ \ (_| | | | (_| | |  | | | (_| | |_| \__ \
    |_|  |_|(_)   \_/\_/ | .__/|___/ |___/\__, |_|  \__,_|_|  |_|  \__,_|\__, |___/
                         |_|                 |_|                         |___/
    */

    libname sd1 "d:/sd1";

    options validvarname=upcase;
    data sd1.have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;

    %utl_wpsbegin;
    parmcards4;

    options validvarname=any;

    libname sd1 "d:/sd1";

    %symdel rowUnq rowUnq / nowarn;

    proc datasets lib=work nolist nodetails mt=data mt=view ;
     delete want havSumVue havRowVue havXpo;
    run;quit;

    /*----     Make sure the _v array does not exist                         ----*/
    /*----     Since rowUnq = colUnq=5 we only need one indes                ----*/

    %put check exitance of third element = &_v3 ;
    /*----  WARNING: Apparent symbolic reference _V3 not resolved.           ----*/

    proc sql;

      select
          distinct input(substr(col,4),best.) into :_v1-
      from
          sd1.have
      ;
      %let _vn=&sqlobs;

      create
          view havRowVue as
      select
          distinct row as rowUnq
      from
          sd1.have
      ;
      create
         view havSumVue as
      select
         col
        ,row
        ,sum(val0) as val0Sum
      from
         sd1.have
      group
         by row, col
    ;
    quit;

    %put &=_v3; /*---- 2                                                     ----*/
    %put &=_vn; /*---- 5                                                     ----*/

    options missing='0';
    proc sql;
     create
         table havXpo as
     select
         rows.rowUnq as row
       , %do_over(_v,phrase=c?.val0Sum as col?,between=comma)
     from
           havRowVue as rows
           %do_over(_v,phrase=%str(
            left join havSumVue as c? on rows.rowUnq = c?.Row and c?.col="col?"))
    ;quit;
    proc print data=havXpo;
    run;quit;
    ;;;;
    %utl_wpsend;



    /*----  If you want the generated code                                   ----*/

    data _null_;
       %do_over(_v,phrase=%str(put "c?.val0Sum as col?";));
    run;quit;

    c0.val0Sum as col0
    c1.val0Sum as col1
    c2.val0Sum as col2
    c3.val0Sum as col3
    c4.val0Sum as col4

    data _null_;
       %do_over(_v,phrase=%str(put "left join havSumVue as c? on rows.rowUnq = c?.Row and c?.col='col?'";))
    run;quit;

    left join havSum as c0 on rows.rowUnq = c0.Row and c0.col='col0'
    left join havSum as c1 on rows.rowUnq = c1.Row and c1.col='col1'
    left join havSum as c2 on rows.rowUnq = c2.Row and c2.col='col2'
    left join havSum as c3 on rows.rowUnq = c3.Row and c3.col='col3'
    left join havSum as c4 on rows.rowUnq = c4.Row and c4.col='col4'


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  HAVXPO total obs=5 11JUN2023:10:52:53                                                                                 */
    /*                                                                                                                        */
    /*  Obs    ROW     COL0    COL1    COL2    COL3    COL4                                                                   */
    /*                                                                                                                        */
    /*   1     row0     0      0.55    0.40    1.02     0                                                                     */
    /*   2     row1    0.96    0.32    0.23     0       0                                                                     */
    /*   3     row2    1.26     0      1.05    1.06     0                                                                     */
    /*   4     row3    0.03     0       0       0      0.12                                                                   */
    /*   5     row4     0       0      0.63     0      0.79                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /* ____                                           _
    / | ___|   __      ___ __  ___   _ __   ___  __ _| |
    | |___ \   \ \ /\ / / `_ \/ __| | `__| / __|/ _` | |
    | |___) |   \ V  V /| |_) \__ \ | |    \__ \ (_| | |
    |_|____(_)   \_/\_/ | .__/|___/ |_|    |___/\__, |_|
                        |_|                        |_|
    */
    libname sd1 "d:/sd1";

    options validvarname=upcase;
    data sd1.have;informat
    ROW $4.
    COL $4.
    VAL0 8.3
    VAL1 8.3
    ;input
    ROW COL VAL0 VAL1;
    cards4;
    row0 col1 0.51 0.38
    row0 col1 0.04 0.44
    row0 col2 0.26 0.82
    row0 col2 0.14 0.87
    row0 col3 0.52 0.72
    row0 col3 0.5 0.85
    row1 col0 0.96 0.53
    row1 col1 0.32 0.69
    row1 col2 0.23 0.21
    row2 col0 0.51 0.42
    row2 col0 0.74 0.62
    row2 col0 0.01 0.82
    row2 col2 0.8 0.64
    row2 col2 0.25 0.39
    row2 col3 0.37 0.43
    row2 col3 0.69 0.37
    row3 col0 0.03 0.55
    row3 col4 0.12 0.33
    row4 col2 0.63 0.38
    row4 col4 0.79 0.64
    ;;;;
    run;quit;

    %utl_wpsbegin;
    parmcards4;
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;

    library(sqldf);
    library(dplyr);

    havSumVue<-sqldf('
      select
         col
        ,row
        ,sum(val0) as val0Sum
      from
         have
      group
         by row, col
    ');
    havSumVue;
    havRowVue<-sqldf('
     select
        distinct row as rowUnq
     from
        havSumVue
    ');
    havRowVue;
    havXpoWps<-sqldf('
     select
         rows.rowUnq as row
        ,c0.val0Sum as col0
        ,c1.val0Sum as col1
        ,c2.val0Sum as col2
        ,c3.val0Sum as col3
        ,c4.val0Sum as col4
     from
           havRowVue as rows
            left outer join havSumVue as c0 on rows.rowUnq = c0.Row and c0.col=\'col0\'
            left outer join havSumVue as c1 on rows.rowUnq = c1.Row and c1.col=\'col1\'
            left outer join havSumVue as c2 on rows.rowUnq = c2.Row and c2.col=\'col2\'
            left outer join havSumVue as c3 on rows.rowUnq = c3.Row and c3.col=\'col3\'
            left outer join havSumVue as c4 on rows.rowUnq = c4.Row and c4.col=\'col4\'
    ');
    havXpoWps <- havXpoWps %>% replace(is.na(.), 0);
    havXpoWps;
    endsubmit;
    import data=sd1.havXpoWps r=havXpoWps;
    ;;;;
    %utl_wpsend;

    proc print data=sd1.havXpoWps;
    run;quit;

    /**************************************************************************************************************************/
    /*                                    |                                                                                   */
    /*  R                                 |    SD1.HAVXPOWPS total obs=5 11JUN2023:11:44:41                                   */
    /*                                    |                                                                                   */
    /*     row col0 col1 col2 col3 col4   |    Obs    ROW     COL0    COL1    COL2    COL3    COL4                            */
    /*                                    |                                                                                   */
    /*  1 row0 0.00 0.55 0.40 1.02 0.00   |     1     row0    0.00    0.55    0.40    1.02    0.00                            */
    /*  2 row1 0.96 0.32 0.23 0.00 0.00   |     2     row1    0.96    0.32    0.23    0.00    0.00                            */
    /*  3 row2 1.26 0.00 1.05 1.06 0.00   |     3     row2    1.26    0.00    1.05    1.06    0.00                            */
    /*  4 row3 0.03 0.00 0.00 0.00 0.12   |     4     row3    0.03    0.00    0.00    0.00    0.12                            */
    /*  5 row4 0.00 0.00 0.63 0.00 0.79   |     5     row4    0.00    0.00    0.63    0.00    0.79                            */
    /*                                    |                                                                                   */
    /**************************************************************************************************************************/

    /*  __                  _   _                             _
    / |/ /_     _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
    | | `_ \   | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
    | | (_) |  | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |_|\___(_) | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
               |_|    |___/                                |_|
    */

    %utl_pybegin;
    parmcards4;
    from os import path
    import pandas as pd
    import xport
    import xport.v56
    import pyreadstat
    import numpy as np
    from pandasql import sqldf
    mysql = lambda q: sqldf(q, globals())
    from pandasql import PandaSQL
    pdsql = PandaSQL(persist=True)
    sqlite3conn = next(pdsql.conn.gen).connection.connection
    sqlite3conn.enable_load_extension(True)
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll')
    mysql = lambda q: sqldf(q, globals())
    have, meta = pyreadstat.read_sas7bdat("d:/sd1/have.sas7bdat")
    havSumVue = pdsql("""
      select
         col
        ,row
        ,sum(val0) as val0Sum
      from
         have
      group
         by row, col
    """);
    print(havSumVue);
    havRowVue=pdsql("""
     select
        distinct row as rowUnq
     from
        havSumVue
    """);
    print(havRowVue);
    havXpoWps=sqldf("""
     select
         rows.rowUnq as row
        ,c0.val0Sum as col0
        ,c1.val0Sum as col1
        ,c2.val0Sum as col2
        ,c3.val0Sum as col3
        ,c4.val0Sum as col4
     from
           havRowVue as rows
            left outer join havSumVue as c0 on rows.rowUnq = c0.Row and c0.col=\'col0\'
            left outer join havSumVue as c1 on rows.rowUnq = c1.Row and c1.col=\'col1\'
            left outer join havSumVue as c2 on rows.rowUnq = c2.Row and c2.col=\'col2\'
            left outer join havSumVue as c3 on rows.rowUnq = c3.Row and c3.col=\'col3\'
            left outer join havSumVue as c4 on rows.rowUnq = c4.Row and c4.col=\'col4\'
    """);
    havXpoWps=havXpoWps.fillna(0);
    print(havXpoWps);
    ds = xport.Dataset(havXpoWps, name='want')
    with open('d:/xpt/havXpoWps.xpt', 'wb') as f:
        xport.v56.dump(ds, f)
    ;;;;
    %utl_pyend;

    libname pyxpt xport "d:/xpt/havXpoWps.xpt";

    proc contents data=pyxpt._all_;
    run;quit;

    proc print data=pyxpt.want;
    run;quit;

    data want;
       set pyxpt.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Up to 40 obs from last table WORK.WANT total obs=5 11JUN2023:12:04:27                                                  */
    /*                                                                                                                        */
    /* Obs    ROW     COL0    COL1    COL2    COL3    COL4                                                                    */
    /*                                                                                                                        */
    /*  1     row0    0.00    0.55    0.40    1.02    0.00                                                                    */
    /*  2     row1    0.96    0.32    0.23    0.00    0.00                                                                    */
    /*  3     row2    1.26    0.00    1.05    1.06    0.00                                                                    */
    /*  4     row3    0.03    0.00    0.00    0.00    0.12                                                                    */
    /*  5     row4    0.00    0.00    0.63    0.00    0.79                                                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
