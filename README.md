# utl-excel-hiding-columns-height-and-weight-in-sheet-class
Excel hiding columns height and weight in sheet class.

    Excel hiding columns age, height and weight in sheet class

    SAS/IML/R

    github
    https://tinyurl.com/yak4mmtg
    https://github.com/rogerjdeangelis/utl-excel-hiding-columns-height-and-weight-in-sheet-class

    sas forum
    https://tinyurl.com/yaxhf8va
    https://communities.sas.com/t5/ODS-and-Base-Reporting/create-excel-with-collapse-expand-columns-function/m-p/515092

    excel repos
    https://tinyurl.com/ybnm6azh
    https://github.com/rogerjdeangelis?utf8=%E2%9C%93&tab=repositories&q=excel+in%3Aname&type=&language=

    INPUT
    =====

     SASHELP.CLASS total obs=19

      NAME       SEX    AGE    HEIGHT    WEIGHT

      Alfred      M      14     69.0      112.5
      Alice       F      13     56.5       84.0
      Barbara     F      13     65.3       98.0
     ...
      Ronald      M      15     67.0      133.0
      Thomas      M      11     57.5       85.0
      William     M      15     66.5      112.0


    EXAMPLE OUTPUT
    ==============

     d:/xls/tabs/xlsx
                               ** C,D,E Hidden **
       +---------------------------------------------------------------+
       |     A     |    B       |    F       |    G       |    H       |
       +---------------------------------------------------------------+
    1  |   NAME    |   SEX      |            |            |            |
       +-----------+------------+------------+------------+------------+
    2  |  Alfred   |    M       |            |            |            |
       +-----------+------------+------------+------------+------------+
        ...
       +-----------+------------+------------+------------+------------+
    19 |  William  |    M       |            |            |            |
       +-----------+------------+------------+------------+------------+


    PROCESS
    =======

    %utl_submit_r64('
    library(openxlsx);
    library(haven);
    have<-read_sas("d:/sd1/have.sas7bdat");
    wb <- createWorkbook();
    addWorksheet(wb, "class");
    writeData(wb, sheet = "class", x = have);
    setColWidths(wb, sheet = "class", cols = 3:5, widths = "auto",hidden=rep(TRUE));
    saveWorkbook(wb, "d:/xls/hidecolumns.xlsx", overwrite = TRUE);
    ');

    OUTPUT
    =====

    see above

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      set sashelp.class;
    run;quit;

