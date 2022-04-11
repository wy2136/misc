# TC track analysis on the tiger machine at Princeton University
* Wenchang Yang 
* Department of Geosciences, Princeton University
* 2022-04-11

### Steps
1. Tracker.
2. Sorter.
3. Netcdf converter.
4. Tracks analyzer.

### 1. Tracker.
* /tigress/gvecchi/ANALYSIS/LUCAS_TRACKER/CODE/bin/track_gav.exe
* input: yyyy0101.atmos_4xdaily.nc (GCM output data on lon/lat grid in nc format)
* output: lmh_TCtrack_ts_4x.dat (storm track points records), e.g.
    
      head /tigress/wenchang/MODEL_OUT/AM2.5C360/CTL2010s_tigercpu_intelmpi_18_1080PE/analysis_lmh/cyclones_gav_ro110_330k/atmos_101_101/Harris.TC/lmh_TCtrack_ts_4x.dat

       1   101   1   1   6       1       323.70       -53.57       950.86        23.73         0.00         0.00         0.00   -.47E-03       0      -1.00     10507233.00
       2   101   1   1   6       2       319.34        46.76       960.14        27.39         0.00         0.00         0.00   0.63E-03       0     238.03      6217283.00
       3   101   1   1   6       3        34.91       -56.02       964.30        21.39         0.00         0.00         0.00   -.59E-03       0      -1.00       565125.62
       4   101   1   1   6       4       280.34       -56.82       966.62        13.28         0.00         0.00         0.00   -.71E-03       0      -1.00        17734.06
       5   101   1   1   6       5        20.47       -64.05       966.94        15.38         0.00         0.00         0.00   -.17E-03       0      -1.00      1788048.12
       6   101   1   1   6       6       271.01       -55.41       967.51        16.41         0.00         0.00         0.00   -.34E-03       0      -1.00       133170.69
       7   101   1   1   6       7       191.36        52.76       971.38        23.05         0.00         0.00         0.00   0.42E-03       0      -1.00      3967469.25
       8   101   1   1   6       8       344.17        63.68       973.78        15.46         0.00         0.00         0.00   0.28E-03       0      -1.00       298288.88
       9   101   1   1   6       9       339.42        69.40       976.04        14.08         0.00         0.00         0.00   0.33E-03       0      -1.00        52045.19
      10   101   1   1   6      10       108.85       -61.59       976.28        13.93         0.00         0.00         0.00   -.21E-03       0      -1.00      3924457.50
     
### 2. Sorter.
* /tigress/wenchang/analysis/TC/track_sorter_FLOR_fix99.py
* input: lmh_TCtrack_ts_4x.dat
* output: lmh_TCtrack_ts_4x.dat.warm.\*.txt, e.g. lmh_TCtrack_ts_4x.dat.warm.h29_25.TS.world.20010101-20020101.txt
 
      head -n32 /tigress/wenchang/MODEL_OUT/AM2.5C360/CTL2010s_tigercpu_intelmpi_18_1080PE/analysis_lmh/cyclones_gav_ro110_330k/atmos_101_101/Harris.TC/lmh_TCtrack_ts_4x.dat.warm.h29_25.TS.world.20010101-20020101.txt
      
      00001++++++++++++++++++++00001   000024         44.5900   968   28
          2001010106  131.37   9.15   993.28    31.55  264.13
          2001010112  129.41   8.83   986.52    27.49  261.42
          2001010118  126.83   9.34   968.77    37.32  266.32
          2001010200  125.32   9.66   975.74    44.59  265.90
          2001010206  123.36  10.60   973.96    36.42  263.59
          2001010212  121.92  10.67   969.43    40.47  262.92
          2001010218  120.93  11.14   980.15    31.88  260.95
          2001010300  119.79  11.87   979.55    32.27  264.40
          2001010306  118.73  12.41   977.98    30.77  261.37
          2001010312  117.68  12.74   982.96    28.18  260.09
          2001010318  117.18  12.89   988.19    23.68  259.50
          2001010400  116.83  13.98   988.77    25.15  261.13
          2001010406  116.37  14.94   989.23    25.83   -1.00
          2001010412  115.89  15.78   992.80    23.00   -1.00
          2001010418  115.43  16.16   994.61    18.85  258.82
          2001010500  115.71  16.29   994.58    21.95  258.24
          2001010506  116.38  16.59   990.42    24.99  260.38
          2001010512  117.18  17.11   990.89    25.02  259.23
          2001010518  117.50  17.10   996.33    18.35   -1.00
          2001010600  118.28  17.02   998.15    18.45   -1.00
          2001010606  118.96  17.04   997.41    18.32   -1.00
          2001010612  119.48  16.46   999.82    18.28   -1.00
          2001010618  119.89  15.82  1001.03    14.63   -1.00
          2001010700  120.23  15.13  1003.61    14.04   -1.00
          2001010706  120.09  14.68  1003.65    13.95   -1.00
          2001010712  119.55  13.85  1004.92    14.36   -1.00
          2001010718  118.62  12.87  1005.43    14.16   -1.00
          2001010800  117.13  12.06  1005.96    17.87   -1.00
      00002++++++++++++++++++++00002   000029         32.4300   969   16
          2001010106  120.86 -15.10  998.32    24.79  260.01
          2001010112  120.39 -15.57  995.28    25.24  260.14
          
### 3. Netcdf converter.
* tc_tracks in /tigress/wenchang/wython/xtc/tracks.py
* input: experiment name, years, ensemble members, etc.
* output: tc_tracks.TS.\*.nc, e.g. tc_tracks.TS.0101-0150.nc
      
      ncdump -h /tigress/wenchang/analysis/TC/AM2.5C360/CTL2010s_tigercpu_intelmpi_18_1080PE/netcdf/tc_tracks.TS.0101-0150.nc

      netcdf tc_tracks.TS.0101-0150 {
      dimensions:
	      storm = 200 ;
	      stage = 120 ;
	      year = 50 ;
      variables:
	      int storm(storm) ;
	      int stage(stage) ;
		      stage:units = "hours from genesis" ;
	      float lat(year, storm, stage) ;
		      lat:_FillValue = NaNf ;
		      lat:long_name = "latitude" ;
		      lat:units = "degree north" ;
	      float lon(year, storm, stage) ;
		      lon:_FillValue = NaNf ;
		      lon:long_name = "longitude" ;
		      lon:units = "degree east" ;
	      float windmax(year, storm, stage) ;
		      windmax:_FillValue = NaNf ;
		      windmax:long_name = "max wind speed" ;
		      windmax:units = "m/s" ;
	      float slp(year, storm, stage) ;
		      slp:_FillValue = NaNf ;
		      slp:long_name = "sea level pressure" ;
		      slp:units = "hPa" ;
	      float tm(year, storm, stage) ;
		      tm:_FillValue = NaNf ;
		      tm:long_name = "300-500hPa air temperature" ;
		      tm:units = "K" ;
	      int month(year, storm, stage) ;
	      int day(year, storm, stage) ;
	      int hour(year, storm, stage) ;
	      int year(year) ;

      // global attributes:
		      :note = "CTL2010s_tigercpu_intelmpi_18_1080PE, years=0101-0150, ens=None, model=AM2.5C360, storm_type=TS, track_tag=cyclones_gav_ro110_330k" ;
      }
 
 ### 4. Tracks analyzer.
 * Python package /tigress/wenchang/wython/xtc
 * input: TC tracks in netcdf format, e.g. tc_tracks.TS.0101-0150.nc
 * output: TC counts, tracks/genesis density, ACE, etc. e.g. tc_counts.TS17.0101-0200.nc, tc_density.TS17.0101-0150.nc.

### Example scripts.
* step 1 and step 2: /tigress/wenchang/analysis/TC/AM2.5C360/CTL2010s_tigercpu_intelmpi_18_1080PE
  - AM2.5C360.CTL2010s_tigercpu_intelmpi_18_1080PE.lmh_TCtrack_ts_4x_gav_ro110_330k_yr.csh
  - loop.AM2.5C360.CTL2010s_tigercpu_intelmpi_18_1080PE.lmh_TCtrack_ts_4x_gav_ro110_330k_yr.sh
  - slurm.AM2.5C360.CTL2010s_tigercpu_intelmpi_18_1080PE.lmh_TCtrack_ts_4x_gav_ro110_330k_yr.sh
* step 3 and 4: /tigress/wenchang/analysis/TC/AM2.5C360/CTL2010s_tigercpu_intelmpi_18_1080PE/tc_save2netcdf.py

