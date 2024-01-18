# utl-wps-meta-data-dictionaries
WPS meta data dictionaries 
    %let pgm=utl-wps-meta-data-dictionaries;

    %stop_submission; /* while developing stops acidental submission of entire program */

    WPS meta data dictionaries

    https://github.com/rogerjdeangelis/utl-wps-meta-data-dictionaries

    SOLUTIONS  (distionaries)

      1 wps vlibnam
      2 wps vtable subset
      3 wps vtable all
      4 wps vcolumn

    /*                        _ _      _   _                        _
    __      ___ __  ___    __| (_) ___| |_(_) ___  _ __   __ _ _ __(_) ___  ___
    \ \ /\ / / `_ \/ __|  / _` | |/ __| __| |/ _ \| `_ \ / _` | `__| |/ _ \/ __|
     \ V  V /| |_) \__ \ | (_| | | (__| |_| | (_) | | | | (_| | |  | |  __/\__ \
      \_/\_/ | .__/|___/  \__,_|_|\___|\__|_|\___/|_| |_|\__,_|_|  |_|\___||___/
             |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* LIBNAME    MEMNAME     MEMTYPE  NVAR SUBSET OF USEFULL VARIABLES                                                       */
    /*                                                                                                                        */
    /* SASHELP    VTABLE       VIEW     27  libname memname memtype memlabel typemem crdate modate nobs obslen                */
    /*                                      nvar compress npage filesize pcompress delobs nlobs maxvar maxlabel               */
    /*                                      indxtype datarep sortname sorttype datarepname encoding num_character             */
    /*                                      num_numeric pointobs                                                              */
    /*                                                                                                                        */
    /* SASHELP    VCOLUMN      VIEW     18  libname memname memtype name type length npos varnum label                        */
    /* SASHELP    VFORMAT      VIEW     13  libname memname path objname fmtname fmttype source minw mind maxw maxd defw defd */
    /* SASHELP    VEXTFL       VIEW      3  fileref xpath xengine                                                             */
    /* SASHELP    VMACRO       VIEW      5  scope name offset value readonly                                                  */
    /* SASHELP    VGOPT        VIEW      6  optname opttype setting optdesc level group                                       */
    /* SASHELP    VTITLE       VIEW      3  type number text                                                                  */
    /* SASHELP    VOPTION      VIEW      6  optname opttype setting optdesc level group                                       */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* SASHELP    VLIBNAM      VIEW     10  libname engine path  readonly sequential                                          */
    /* SASHELP    VCATALG      VIEW      9  libname memname memtype objname objtype objdesc                                   */
    /* SASHELP    VCFORMAT     VIEW     13  libname memname path objname fmtname fmttype source                               */
    /* SASHELP    VDCTNRY      VIEW     10  memname memlabel name type length npos varnum label format informat               */
    /* SASHELP    VDEST        VIEW      2  destination style                                                                 */
    /* SASHELP    VINDEX       VIEW      9  libname memname memtype name idxusage indxname indxpos nomiss unique              */
    /* SASHELP    VMEMBER      VIEW      6  libname memname memtype engine index path                                         */
    /* SASHELP    VVIEW        VIEW      4  libname memname memtype engine                                                    */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* SASHELP    VSACCES      VIEW      2  libname memname                                                                   */
    /* SASHELP    VSCATLG      VIEW      2  libname memname                                                                   */
    /* SASHELP    VSELIB       VIEW      4  libname engine level path                                                         */
    /* SASHELP    VSEMEM       VIEW      4  libname memname memtype path                                                      */
    /* SASHELP    VSLIB        VIEW      2  libname path                                                                      */
    /* SASHELP    VSTABLE      VIEW      2  libname memname                                                                   */
    /* SASHELP    VSTABVW      VIEW      3  libname memname memtype                                                           */
    /* SASHELP    VSVIEW       VIEW      2  libname memname                                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    proc datasets lib=sd1 nolist mt=data mt=view nodetails;delete class class_sas; run;quit;

    libname sd1 "d:/sd1";

    data sd1.class_sas;
      set sashelp.class;
    run;quit;

    proc contents data=sd1.class_sas position;
    run;quit;

    /**************************************************************************************************************************/
    /*                               _____ _         _       _                                                                */
    /*  ___  __ _ ___   ___  __ _ __|___  | |__   __| | __ _| |_                                                              */
    /* / __|/ _` / __| / __|/ _` / __| / /| `_ \ / _` |/ _` | __|                                                             */
    /* \__ \ (_| \__ \ \__ \ (_| \__ \/ / | |_) | (_| | (_| | |_                                                              */
    /* |___/\__,_|___/ |___/\__,_|___/_/  |_.__/ \__,_|\__,_|\__|                                                             */
    /*                                                                                                                        */
    /* Data Set Name   SD1.CLASS_SAS    Observations    19                                                                    */
    /* Member Type     DATA             Variables        5                                                                    */
    /* Encoding        wlatin1  Western (Windows)                                                                             */
    /* Engine          V9                                                                                                     */
    /*                                                                                                                        */
    /*  Variables in Creation Order                                                                                           */
    /*                                                                                                                        */
    /* #    Variable    Type    Len                                                                                           */
    /*                                                                                                                        */
    /* 1    NAME        Char      8                                                                                           */
    /* 2    SEX         Char      1                                                                                           */
    /* 3    AGE         Num       8                                                                                           */
    /* 4    HEIGHT      Num       8                                                                                           */
    /* 5    WEIGHT      Num       8                                                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    %utl_submit_wps64x("
    options validvarname=any;
    libname wpd wpd 'd:/wpd';
    libname sd1 sas7bdat 'd:/sd1';
     data wpd.class_wpd;
       set sd1.class_sas;
     run;quit;
     proc contents data=wpd.cl ass_wpd position;
     run;quit;
    ");

    /**************************************************************************************************************************/
    /*                     _                                                                                                  */
    /* __      ___ __   __| |                                                                                                 */
    /* \ \ /\ / / `_ \ / _` |                                                                                                 */
    /*  \ V  V /| |_) | (_| |                                                                                                 */
    /*   \_/\_/ | .__/ \__,_|                                                                                                 */
    /*          |_|                                                                                                           */
    /*                                                                                                                        */
    /* The WPS System                                                                                                         */
    /*                                                                                                                        */
    /* The CONTENTS Procedure                                                                                                 */
    /*                                                                                                                        */
    /* Data Set Name           CLASS_WPD                                                                                      */
    /* Member Type             DATA                                                                                           */
    /* Engine                  WPD                                                                                            */
    /* Variables               5                                                                                              */
    /* Observations            19                                                                                             */
    /* Encoding                wlatin1 Windows-1252 Western                                                                   */
    /*                                                                                                                        */
    /* Variables in Creation Order                                                                                            */
    /*                                                                                                                        */
    /* Number    Variable    Type  Len    Pos                                                                                 */
    /* ______________________________________                                                                                 */
    /*      1    NAME        Char    8     24                                                                                 */
    /*      2    SEX         Char    1     32                                                                                 */
    /*      3    AGE         Num     8      0                                                                                 */
    /*      4    HEIGHT      Num     8      8                                                                                 */
    /*      5    WEIGHT      Num     8     16                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*                              _ _ _
    / | __      ___ __  ___  __   _| (_) |__  _ __   __ _ _ __ ___
    | | \ \ /\ / / `_ \/ __| \ \ / / | | `_ \| `_ \ / _` | `_ ` _ \
    | |  \ V  V /| |_) \__ \  \ V /| | | |_) | | | | (_| | | | | | |
    |_|   \_/\_/ | .__/|___/   \_/ |_|_|_.__/|_| |_|\__,_|_| |_| |_|
                 |_|
    */

    %utl_submit_wps64x("
    options validvarname=any;
    libname wpd wpd 'd:/wpd';
    libname sd1 sas7bdat 'd:/sd1';
    proc sql;
      create
         table sd1.vlibnam_sas as
      select
         *
      from
        sashelp.vlibnam
      &where
     ;quit;
     proc print;
     run;quit;

     proc print data=sd1.vlibnam_meta ;
     run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* WPS System                                                                                                             */
    /*                                                                                                                        */
    /*  LIBNAME   ENGINE                    PATH                                                                              */
    /*                                                                                                                        */
    /*  SASHELP  WPD       C:\progra~1\worldp~1\wpsana~1\4\sashelp                                                            */
    /*  SASUSER  WPD       d:\wpsEtc                                                                                          */
    /*  SD1      SAS7BDAT  d:\sd1                                                                                             */
    /*  WORK     WPD       d:\wpsWrk\t_XXXXXXX                                                                                */
    /*  WPD      WPD       d:\wpd                                                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*___                               _        _     _                  _              _
    |___ \  __      ___ __  ___  __   _| |_ __ _| |__ | | ___   ___ _   _| |__  ___  ___| |_
      __) | \ \ /\ / / `_ \/ __| \ \ / / __/ _` | `_ \| |/ _ \ / __| | | | `_ \/ __|/ _ \ __|
     / __/   \ V  V /| |_) \__ \  \ V /| || (_| | |_) | |  __/ \__ \ |_| | |_) \__ \  __/ |_
    |_____|   \_/\_/ | .__/|___/   \_/  \__\__,_|_.__/|_|\___| |___/\__,_|_.__/|___/\___|\__|
                     |_|
    */

    %utl_submit_wps64x("
    options validvarname=any;
    libname wpd wpd 'd:/wpd';
    libname sd1 sas7bdat 'd:/sd1';
    options validvarname=any;
    proc sql;
      create
         table sd1.vtable_class_sas as
      select
         libname
        ,memname
        ,nvar
        ,nlobs
      from
        sashelp.vtable
      where
        memname eqt 'CLASS_'
     ;quit;

     proc print;
     run;quit;
    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS System  (SAS DATASET_                                                                                          */
    /*                                                                                                                        */
    /* Obs    libname     memname     nvar    nlobs                                                                           */
    /*                                                                                                                        */
    /*  1       SD1      CLASS_SAS      5       19   SAS Dataset                                                              */
    /*  2       WPD      CLASS_WPD      5       19   WPS Dataset                                                              */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                              _        _     _              _ _
    |___ /  __      ___ __  ___  __   _| |_ __ _| |__ | | ___    __ _| | |
      |_ \  \ \ /\ / / `_ \/ __| \ \ / / __/ _` | `_ \| |/ _ \  / _` | | |
     ___) |  \ V  V /| |_) \__ \  \ V /| || (_| | |_) | |  __/ | (_| | | |
    |____/    \_/\_/ | .__/|___/   \_/  \__\__,_|_.__/|_|\___|  \__,_|_|_|
                     |_|
    */

    %utl_submit_wps64x("
    options validvarname=any;
    libname wpd wpd 'd:/wpd';
    libname sd1 sas7bdat 'd:/sd1';
    options label;
    proc sql;
      create
         table sd1.vtable_sasWpd as
      select
         *
      from
        sashelp.vtable
      where upcase(memname) eqt 'CLASS_' and libname in ('SD1','WPD')
     ;quit;
     proc print;
     run;quit;
    ");


    /**************************************************************************************************************************/
    /*        _        _     _                                                                                                */
    /* __   _| |_ __ _| |__ | | ___                                                                                           */
    /* \ \ / / __/ _` | `_ \| |/ _ \                                                                                          */
    /*  \ V /| || (_| | |_) | |  __/                                                                                          */
    /*   \_/  \__\__,_|_.__/|_|\___|                                                                                          */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* SD1.VTABLE_sasWpd total obs=27                                                                                         */
    /*                                                                                                                        */
    /* Obs    NAME              SAS7BDAT                        WPD                                                           */
    /*                                                                                                                        */
    /*   1    libname           SD1                             WPD                                                           */
    /*   2    memname           CLASS_SAS                       CLASS_WPD                                                     */
    /*   3    memtype           DATA                            DATA                                                          */
    /*   4    memlabel                                                                                                        */
    /*   5    typemem                                           DATA                                                          */
    /*   6    crdate            18JAN24:12:43:46                18JAN24:12:43:47                                              */
    /*   7    modate            18JAN24:12:43:46                18JAN24:12:43:47                                              */
    /*   8    nobs              19                              19                                                            */
    /*   9    obslen            40                              33                                                            */
    /*  10    nvar              5                               5                                                             */
    /*  11    compress          NO                              NO                                                            */
    /*  12    npage             1                               2                                                             */
    /*  13    filesize          131072                          8192                                                          */
    /*  14    pcompress         .                               .                                                             */
    /*  15    delobs            0                               0                                                             */
    /*  16    nlobs             19                              19                                                            */
    /*  17    maxvar            6                               6                                                             */
    /*  18    maxlabel          0                               0                                                             */
    /*  19    indxtype                                                                                                        */
    /*  20    datarep           NATIVE                          NATIVE                                                        */
    /*  21    sortname                                                                                                        */
    /*  22    sorttype                                                                                                        */
    /*  23    datarepname       WINDOWS_64                      Little endian, IEEE Windows                                   */
    /*  24    encoding          wlatin1 Windows-1252 Western    wlatin1 Windows-1252 Western                                  */
    /*  25    num_character     2                               2                                                             */
    /*  26    num_numeric       3                               3                                                             */
    /*  27    pointobs          NO                              NO                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                                         _
    | || |   __      ___ __  ___  __   _____ ___ | |_   _ _ __ ___  _ __
    | || |_  \ \ /\ / / `_ \/ __| \ \ / / __/ _ \| | | | | `_ ` _ \| `_ \
    |__   _|  \ V  V /| |_) \__ \  \ V / (_| (_) | | |_| | | | | | | | | |
       |_|     \_/\_/ | .__/|___/   \_/ \___\___/|_|\__,_|_| |_| |_|_| |_|
                      |_|
    */

    %utl_submit_wps64x("
    options validvarname=any;
    libname wpd wpd 'd:/wpd';
    libname sd1 sas7bdat 'd:/sd1';
    options label;
    proc sql;
      create
         table sd1.vcolumn_sasWpd as
      select
         *
      from
        sashelp.vcolumn
      where upcase(memname) eqt 'CLASS_' and libname in ('SD1','WPD')
      order by name libname
     ;quit;
     proc print;
     run;quit;
    ");


    /**************************************************************************************************************************/
    /*                 _                                                                                                      */
    /* __   _____ ___ | |_   _ _ __ ___  _ __                                                                                 */
    /* \ \ / / __/ _ \| | | | | `_ ` _ \| `_ \                                                                                */
    /*  \ V / (_| (_) | | |_| | | | | | | | | |                                                                               */
    /*   \_/ \___\___/|_|\__,_|_| |_| |_|_| |_|                                                                               */
    /*                                                                                                                        */
    /* SD1.VCOLUMN_SASWPD                                                                                                     */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* Obs    NAME      ATTRIBUTE     SAS7BDAT     WPD                                                                        */
    /*                                                                                                                        */
    /*   1    AGE       libname       SD1          WPD                                                                        */
    /*   2    AGE       memname       CLASS_SAS    CLASS_WPD                                                                  */
    /*   3    AGE       memtype       DATA         DATA                                                                       */
    /*   4    AGE       name          AGE          AGE                                                                        */
    /*   5    AGE       type          num          num                                                                        */
    /*   6    AGE       length        8            8                                                                          */
    /*   7    AGE       npos          9            9                                                                          */
    /*   8    AGE       varnum        3            3                                                                          */
    /*   9    AGE       label                                                                                                 */
    /*  10    AGE       format                                                                                                */
    /*  11    AGE       informat                                                                                              */
    /*  12    AGE       idxusage                                                                                              */
    /*  13    AGE       sortedby      0            0                                                                          */
    /*  14    AGE       xtype                                                                                                 */
    /*  15    AGE       notnull                                                                                               */
    /*  16    AGE       precision     .            .                                                                          */
    /*  17    AGE       scale         .            .                                                                          */
    /*  18    AGE       transcode     YES          YES                                                                        */
    /* ...                                                                                                                    */
    /* ...                                                                                                                    */
    /*  73    WEIGHT    libname       SD1          WPD                                                                        */
    /*  74    WEIGHT    memname       CLASS_SAS    CLASS_WPD                                                                  */
    /*  75    WEIGHT    memtype       DATA         DATA                                                                       */
    /*  76    WEIGHT    name          WEIGHT       WEIGHT                                                                     */
    /*  77    WEIGHT    type          num          num                                                                        */
    /*  78    WEIGHT    length        8            8                                                                          */
    /*  79    WEIGHT    npos          25           25                                                                         */
    /*  80    WEIGHT    varnum        5            5                                                                          */
    /*  81    WEIGHT    label                                                                                                 */
    /*  82    WEIGHT    format                                                                                                */
    /*  83    WEIGHT    informat                                                                                              */
    /*  84    WEIGHT    idxusage                                                                                              */
    /*  85    WEIGHT    sortedby      0            0                                                                          */
    /*  86    WEIGHT    xtype                                                                                                 */
    /*  87    WEIGHT    notnull                                                                                               */
    /*  88    WEIGHT    precision     .            .                                                                          */
    /*  89    WEIGHT    scale         .            .                                                                          */
    /*  90    WEIGHT    transcode     YES          YES                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
