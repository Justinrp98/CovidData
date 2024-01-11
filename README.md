-- FULL TABLE (BATTING) (2,477 rows)
SELECT *
FROM atlanta-braves-project.atlanta_braves_statistics.atl_batting
ORDER BY Year desc, On_Base_Percentage desc

-- FULL TABLE (PITCHING) (1,228 rows)
SELECT *
FROM atlanta-braves-project.atlanta_braves_statistics.atl_pitching

-- Who had the most extra base hits in 2023? (includes extra base hits as a percentage of plate appearances)
SELECT Name, Position, Plate_Appearances, (Home_Runs + Triples + Doubles) as extra_base_hits, Home_Runs, ((Home_Runs + Triples + Doubles)/Plate_Appearances)*100 as xb_percent
FROM atlanta-braves-project.atlanta_braves_statistics.atl_batting
WHERE Year = 2023 AND Plate_Appearances > 0
ORDER BY extra_base_hits desc

-- Career batting averages of all players (all-time, only includes players with 100 or more at-bats)
SELECT Name, sum(At_Bats) as total_at_bats, sum(Hits) as total_hits, round(avg(Batting_Average),3) as total_batting_avg
FROM atlanta-braves-project.atlanta_braves_statistics.atl_batting
GROUP BY Name
HAVING sum(At_Bats) > 100
ORDER BY total_batting_avg desc, total_at_bats desc

-- Who has the highest OBP since 2020?
SELECT Name, Year, Plate_Appearances, On_Base_Percentage
FROM atlanta-braves-project.atlanta_braves_statistics.atl_batting
WHERE Year >= 2020 AND Plate_Appearances > 100
ORDER BY On_Base_Percentage desc

-- Team OBP since 2020
SELECT Year, ROUND(AVG(On_Base_Percentage),3) AS atl_obp
FROM atlanta-braves-project.atlanta_braves_statistics.atl_batting
WHERE Year >= 2020 AND Plate_Appearances >= 100
GROUP BY Year
ORDER BY Year desc
