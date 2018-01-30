# utl_map_counties_within_one_state_choropleth_map
Mapping Counties within One State Choropleth Map.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.
    Mapping Counties within One State Choropleth Map

    This is a somewhat dated solution.  There are several more recent R mapping packages.

    See output Graphic
    https://goo.gl/2oHj6Q
    https://github.com/rogerjdeangelis/utl_map_counties_within_one_state_choropleth_map/blob/master/utl_map_counties_within_one_state_choropleth_map

    inspired by
    https://stackoverflow.com/questions/33112514/counties-within-one-state-choropleth-map


    https://goo.gl/pLBtG9
    https://communities.sas.com/t5/SAS-Visual-Analytics/How-to-create-custom-regional-maps-in-SAS-Visual-Analytics-8-2/m-p/431422


    INPUT
    =====

     SD1.HAVE total obs=99

        county     Income

         19001    31024.38
         19003    28921.47
         19005    19654.91
         19007    30681.83
         19009    35218.69
         19011    46424.57
        ...
         19193    44299.209395
         19195    32510.908988
         19197    49540.494079

    PROCESS (working code)
    ======================

        png("d:/png/utl_map_counties_within_one_state_choropleth_map.png");
        county_choropleth(county, "Iowa", state_zoom = "iowa") + scale_fill_brewer("Iowa",palette="Blues") ;
        county_choropleth(county, "Iowa", state_zoom = "iowa", num_colors = 1) +
        scale_fill_gradient2(high = "blue",
               low = "red",
               na.value = "grey90",
               breaks = pretty(county$value, n = 10),
               label = scales::dollar_format());

    OUTPUT
    ======

    Output Graphic
    https://goo.gl/2oHj6Q

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

    options validvarname=v7;
    libname sd1 "d:/sd1";
    data sd1.have;
     input region @@;
     value=50000*uniform(5731);;
    cards4;
    19001 19003 19005 19007 19009 19011 19013 19015 19017 19019 19021 19023 19025
    19027 19029 19031 19033 19035 19037 19039 19041 19043 19045 19047 19049 19051
    19053 19055 19057 19059 19061 19063 19065 19067 19069 19071 19073 19075 19077
    19079 19081 19083 19085 19087 19089 19091 19093 19095 19097 19099 19101 19103
    19105 19107 19109 19111 19113 19115 19117 19119 19121 19123 19125 19127 19129
    19131 19133 19135 19137 19139 19141 19143 19145 19147 19149 19151 19153 19155
    19157 19159 19161 19163 19165 19167 19169 19171 19173 19175 19177 19179 19181
    19183 19185 19187 19189 19191 19193 19195 19197
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname sd1 sas7bdat "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    libname hlp sas7bdat "C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    library(haven);
    library(choroplethr);
    library(ggplot2);
    county<-read_sas("d:/sd1/have.sas7bdat");
    png("d:/png/utl_map_counties_within_one_state_choropleth_map.png");
    county_choropleth(county, "Iowa", state_zoom = "iowa") + scale_fill_brewer("Iowa",palette="Blues") ;
    county_choropleth(county, "Iowa", state_zoom = "iowa", num_colors = 1) +
    scale_fill_gradient2(high = "blue",
      low = "red",
      na.value = "grey90",
      breaks = pretty(county$value, n = 10),
      label = scales::dollar_format());
    endsubmit;
    run;quit;
    ');

