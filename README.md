# IPL Analysis Dashboard using PowerBI
Requirement:- Develop a IPL Dashboard for season 2008 to 2022 to have a detailed insight on below 
problem statements
* Find the Title Winner, Orange Cap Winner, Purple Cap Winner, Tournament 6's and 4's
  for the respective seasons on IPL 
* Develop IPL Batting and Bowling stats and add a filter where user can select the bowler
  and batsman to see these stats 
* Winning percentage based on the toss decision 
* Matches win by venue 
* Total wins by team in a season 
* Matches won based on the result type

# Stakeholders 
* BCCI 
* Franchise/Team Owners 
* Team Management 
* Coaches
* Players
* Media
* Public 

# I worked on this project 
* Data Collecting
* Data Importing
* Data Cleaning
* Data Processing
* Data Modeling
* Data Analysis & Visualization
* Conclusion

# Data Importing
The data was present in ipl_database and loaded into powerbi by fetching required rows and columns 
through postgre sql.

# Data Cleaning 
After importing data into PowerBI performed various activities in Power Query Editor like, removing duplicates, removing missing values, rectified spelling mistakes and transforming the data into a format that can be easily analyzed.

# Data Processing 
* A new table called calendar table is created using Dax query and year is fetched from there for the convenience of understanding which   match was played in which year. 
  Formula : Calender Table = CALENDAR(MIN(ipl_matches_2008_2022[match_date]),MAX(ipl_matches_2008_2022[match_date]))
            Year = YEAR('Calender Table'[Date])
* Created Batter Runs column in ipl_ball_by_ball_2008_2022 table for to see total runs of every batsman in every season. 
  Formula : Batter Runs = CONCATENATE(sum(ipl_ball_by_ball_2008_2022[batsman_run])," Runs")
* Created Bowler Wickets column in ipl_ball_by_ball_2008_2022 table for to see total wickets of every bowler in every season. 
  Formula : Bowler Wickets = CONCATENATE(sum(ipl_ball_by_ball_2008_2022[iswicket_delivery])," Wickets")
* Created Matches won on toss decision column in ipl_ball_by_ball_2008_2022 table for to see if winning the toss has any correlation 
  with winning the match. 
  Formula : Matches won on toss decision = CALCULATE(COUNTROWS(ipl_matches_2008_2022)) 
* Created Strike Rate for Batsman column in ipl_ball_by_ball_2008_2022 table for to see every batsman's strike rate in every year. 
  Formula : Strike Rate for Batsman = (sum(ipl_ball_by_ball_2008_2022[batsman_run])/COUNT(ipl_ball_by_ball_2008_2022[ball_number]))*100
* Created Average by Bowler column in ipl_matches_2008_2022 table for to see the number of runs allowed per wicket for every bowlers
  in every year.
  Formula : Average by Bowler = DIVIDE(
                SUMX(
                FILTER(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[extra_type]<>"legbyes" &&      ipl_ball_by_ball_2008_2022[extra_type]<> "byes"), ipl_ball_by_ball_2008_2022[total_run]),  sum(ipl_ball_by_ball_2008_2022[iswicket_delivery])) 
* Created Bowling SR column in ipl_matches_2008_2022 table for to see the number of balls bowled per wicket for every bowlers in every   year.
 Formula : Bowling SR = COUNT(ipl_ball_by_ball_2008_2022[bowler])/SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery])
* Created Economy column in ipl_matches_2008_2022 table for used to measure a bowler's efficiency in terms of conceding runs for every 
  bowler's in every season. 
  Formula : Economy = DIVIDE(
                SUMX(
                FILTER(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[extra_type]<>"legbyes" && ipl_ball_by_ball_2008_2022[extra_type]<> "byes"), ipl_ball_by_ball_2008_2022[total_run]), (COUNT(ipl_ball_by_ball_2008_2022[overs])/6))
* Created Title winner column for to see which team won the title in which year.
  Formula : Title winner = VAR max_date = CALCULATE(max('Calender Table'[Date]), ALLSELECTED(ipl_matches_2008_2022),VALUES(ipl_matches_2008_2022)) 
var title_winner = CALCULATE(SELECTEDVALUE(ipl_matches_2008_2022[winning_team]), 'Calender Table'[Date] = max_date)
return title_winner 

# Data Modeling 
Created a relationship between three tables (ipl_matches_2008_2022, ipl_ball_by_ball_2008_2022 and Calender Table) 
which makes the data useful for analysis.

# Data Analysis & Visualization 
* Created KPI for to show Title winner team, Orange & Purple Cap holder player and Tournament 6's and 4's in every year.
* Created Slicer for to change every year and Batting and Bowling stats for every bowlers and batsman. 
* Created two Horizontal bar charts for to analysis Matches win by venue and Total wins by a team for a season.   
* Created two Donut charts for to analysis Matches Win based on toss decision and Matches win by Result Type. 

# Conclusion 
This dashboard has intended on analyzing and visualizing the results of the Indian Premier League matches during the year 2008-2022, 
also on the basis of the data we were successful in showing that IPL as a tournament is quite interesting from user point of view, as most of the matches that have a result are quite nail-biting.
   




  
 
  

