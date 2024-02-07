# **About Dataset**

*Data collected from [https://divvy-tripdata.s3.amazonaws.com/index.html](https://divvy-tripdata.s3.amazonaws.com/index.html) which is Chicago's 
public bike trip data. The data compiled corresponds to 12 months, namely the period from May 2022 through April 2023.* 

**Cyclistic/Divvy Data**

Cyclistic is a fictional company, the original datasets have the name Divvy. This data consists of public historical bike trip data from the city of Chicago.

The data has been made available by Motivate International Inc. under [this license](https://divvybikes.com/data-license-agreement)

This is public data that you can use to explore how different customer types are using Cyclistic bikes. But note that data-privacy issues prohibit you from using riders’ personally identifiable information. This means that you won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

# **BACKGROUND**

 **Case Study: How Does a Bike-Share Navigate Speedy Success?**

Imagine fictional company Cyclistic a bike-share company in Chicago. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

 **About the company**

In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and returned to any other station in the system anytime.
Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments. One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes, and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members.

Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic program and have chosen Cyclistic for their mobility needs.

Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.

**The task is to figure out:**
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

colnames(all_trips)
 [1] "ride_id"            "rideable_type"      "started_at"         "ended_at"           "start_station_name"
 [6] "start_station_id"   "end_station_name"   "end_station_id"     "start_lat"          "start_lng"         
[11] "end_lat"            "end_lng"            "member_casual"     
> glimpse(all_trips)
Rows: 5,859,061
Columns: 13
$ ride_id            <chr> "EC2DE40644C6B0F4", "1C31AD03897EE385", "1542FBEC830415CF", "6FF59852924528F8", "483C52CAAE12E3AC…
$ rideable_type      <chr> "classic_bike", "classic_bike", "classic_bike", "classic_bike", "classic_bike", "classic_bike", "…
$ started_at         <dttm> 2022-05-23 23:06:58, 2022-05-11 08:53:28, 2022-05-26 18:36:28, 2022-05-10 07:30:07, 2022-05-10 1…
$ ended_at           <dttm> 2022-05-23 23:40:19, 2022-05-11 09:31:22, 2022-05-26 18:58:18, 2022-05-10 07:38:49, 2022-05-10 1…
$ start_station_name <chr> "Wabash Ave & Grand Ave", "DuSable Lake Shore Dr & Monroe St", "Clinton St & Madison St", "Clinto…
$ start_station_id   <chr> "TA1307000117", "13300", "TA1305000032", "TA1305000032", "TA1305000032", "13196", "13290", "TA130…
$ end_station_name   <chr> "Halsted St & Roscoe St", "Field Blvd & South Water St", "Wood St & Milwaukee Ave", "Clark St & R…
$ end_station_id     <chr> "TA1309000025", "15534", "13221", "TA1305000030", "TA1306000015", "13409", "657", "TA1309000030",…
$ start_lat          <dbl> 41.89147, 41.88096, 41.88224, 41.88224, 41.88224, 41.89456, 41.90068, 41.92914, 41.88224, 41.9480…
$ start_lng          <dbl> -87.62676, -87.61674, -87.64107, -87.64107, -87.64107, -87.65345, -87.66260, -87.64908, -87.64107…
$ end_lat            <dbl> 41.94367, 41.88635, 41.90765, 41.88458, 41.88578, 41.88316, 41.89918, 41.92077, 41.90461, 41.9400…
$ end_lng            <dbl> -87.64895, -87.61752, -87.67255, -87.63189, -87.65102, -87.65110, -87.67220, -87.66371, -87.64055…
$ member_casual      <chr> "member", "member", "member", "member", "member", "member", "member", "casual", "member", "member…
> dim(all_trips)
[1] 5859061      13
> summary(all_trips)
   ride_id          rideable_type        started_at                        ended_at                      start_station_name
 Length:5859061     Length:5859061     Min.   :2022-05-01 00:00:06.00   Min.   :2022-05-01 00:05:17.00   Length:5859061    
 Class :character   Class :character   1st Qu.:2022-07-03 11:12:30.00   1st Qu.:2022-07-03 11:38:52.00   Class :character  
 Mode  :character   Mode  :character   Median :2022-08-28 12:44:57.00   Median :2022-08-28 13:07:09.00   Mode  :character  
                                       Mean   :2022-09-19 13:39:54.23   Mean   :2022-09-19 13:58:50.35                     
                                       3rd Qu.:2022-11-08 06:30:21.00   3rd Qu.:2022-11-08 06:43:39.00                     
                                       Max.   :2023-04-30 23:59:05.00   Max.   :2023-05-03 10:37:12.00                     
                                                                                                                           
 start_station_id   end_station_name   end_station_id       start_lat       start_lng         end_lat         end_lng      
 Length:5859061     Length:5859061     Length:5859061     Min.   :41.64   Min.   :-87.84   Min.   : 0.00   Min.   :-88.14  
 Class :character   Class :character   Class :character   1st Qu.:41.88   1st Qu.:-87.66   1st Qu.:41.88   1st Qu.:-87.66  
 Mode  :character   Mode  :character   Mode  :character   Median :41.90   Median :-87.64   Median :41.90   Median :-87.64  
                                                          Mean   :41.90   Mean   :-87.65   Mean   :41.90   Mean   :-87.65  
                                                          3rd Qu.:41.93   3rd Qu.:-87.63   3rd Qu.:41.93   3rd Qu.:-87.63  
                                                          Max.   :42.07   Max.   :-87.52   Max.   :42.37   Max.   :  0.00  
                                                                                           NA's   :5973    NA's   :5973    
 member_casual     
 Length:5859061    
 Class :character  
 Mode  :character  
                   
                   
                   
                   
> head(all_trips)
# A tibble: 6 × 13
  ride_id          rideable_type started_at          ended_at            start_station_name  start_station_id end_station_name
  <chr>            <chr>         <dttm>              <dttm>              <chr>               <chr>            <chr>           
1 EC2DE40644C6B0F4 classic_bike  2022-05-23 23:06:58 2022-05-23 23:40:19 Wabash Ave & Grand… TA1307000117     Halsted St & Ro…
2 1C31AD03897EE385 classic_bike  2022-05-11 08:53:28 2022-05-11 09:31:22 DuSable Lake Shore… 13300            Field Blvd & So…
3 1542FBEC830415CF classic_bike  2022-05-26 18:36:28 2022-05-26 18:58:18 Clinton St & Madis… TA1305000032     Wood St & Milwa…
4 6FF59852924528F8 classic_bike  2022-05-10 07:30:07 2022-05-10 07:38:49 Clinton St & Madis… TA1305000032     Clark St & Rand…
5 483C52CAAE12E3AC classic_bike  2022-05-10 17:31:56 2022-05-10 17:36:57 Clinton St & Madis… TA1305000032     Morgan St & Lak…
6 C0A3AA5A614DCE01 classic_bike  2022-05-04 14:48:55 2022-05-04 14:56:04 Carpenter St & Hur… 13196            Sangamon St & W…
# ℹ 6 more variables: end_station_id <chr>, start_lat <dbl>, start_lng <dbl>, end_lat <dbl>, end_lng <dbl>, member_casual <chr>









