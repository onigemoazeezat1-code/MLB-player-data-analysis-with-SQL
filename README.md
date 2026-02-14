# MLB-player-data-analysis-with-SQL
⚾ MLB Player Data Analysis with Advanced SQL 🎯 Project Title Advanced SQL Querying for Major League Baseball (MLB) Player and Team Analysis

Project Overview I was hired as a Data Analyst Intern for Major League Baseball (MLB) to analyze a large dataset of historical player and team statistics. The primary goal was to leverage advanced SQL querying techniques—including Window Functions, CTEs, Joins, Aggregation, and Datetime functions—to track how player attributes and team spending have evolved over decades within the league.

This project is divided into four main analytical phases, each focusing on a key area of the MLB dataset: School Production, Team Salaries, Player Careers, and Player Comparisons. All queries were executed in a MySQL environment.

🔍 Data Analysis Sections I. School Analysis This section focused on answering the first project objective: "What schools do MLB players attend?"

Decadal School Production: I analyzed the data to determine the number of distinct schools that produced MLB players in each decade. This provided a temporal view of the recruitment landscape.

Top Producing Schools: I identified the top 5 schools overall that have produced the most MLB players throughout history, using a LEFT JOIN between schools and school_details to retrieve the full school names.

Decadal Top Schools: Using a Window Function (ROW_NUMBER()/DENSE_RANK()) within a Common Table Expression (CTE), I ranked schools by player count within each decade to show which institutions dominated recruitment during specific periods.

II. Salary Analysis This section tackled the second objective: "How much do teams spend on player salaries?"

Top Spending Teams: I used the NTILE(5) Window Function to partition teams into five groups (quintiles) based on their average annual spending. This effectively identified the top 20% of teams by financial commitment.

Cumulative Spending: To understand long-term financial trends, I calculated the cumulative sum of spending for each team over the years using a Rolling Calculation (SUM() OVER (PARTITION BY teamID ORDER BY yearID)).

Billion-Dollar Milestone: By applying a ROW_NUMBER() function over the cumulative sum, I determined the first year that each team's total historical spending surpassed the 1 billion dollar mark.

III. Player Career Analysis This part addressed the third objective: "What does each player's career look like?"

Career Metrics: Utilizing Datetime Functions (TIMESTAMPDIFF in MySQL), I calculated three critical career metrics for every player: age at debut game, age at final game, and the total career length in years, providing a comprehensive measure of longevity.

Starting and Ending Teams: I joined the players table with the salaries table twice—once for the starting year (YEAR(p.debut) = s.yearID) and once for the ending year (YEAR(p.finalGame) = e.yearID)—to pinpoint the teams a player began and ended their career with.

Long-Term Loyalty: Using the results from the team analysis, I filtered the dataset to identify players who demonstrated high loyalty (starting and ending on the same team) and exceptional longevity (playing for over a decade).

IV. Player Comparison Analysis The final section completed the fourth objective: "How do player attributes compare?"

Birthday Matches: I employed the GROUP_CONCAT String Function to identify and list all players who share the exact same birthdate, demonstrating a practical application of aggregating string data.

Batting Hand Preference: I created a summary table that calculates the percentage of players on each team who bat Right ('R'), Left ('L'), or Both ('B'). This was achieved using Pivoting logic (CASE WHEN...) on a de-duplicated dataset of unique player-team combinations.

Height & Weight Trends: I analyzed the longitudinal evolution of physical attributes. I first calculated the average height and weight at debut game per decade and then used the LAG Window Function to compute the decade-over-decade difference in these averages, revealing historical trends in MLB player physique.

🛠️ Key SQL Techniques Used Common Table Expressions (CTEs): Used extensively for structuring complex, multi-step queries (e.g., in tasks involving cumulative sums and ranking).

Window Functions:

Ranking: ROW_NUMBER(), DENSE_RANK() (for top schools per decade).

Analytical/Lag: LAG() (for decade-over-decade comparisons).

Distribution: NTILE(5) (for identifying top 20% spending teams).

Rolling/Cumulative: SUM() OVER (...) (for cumulative salary spending).

Joins: INNER JOIN and LEFT JOIN (for connecting player, school, and salary data).

Datetime Functions: YEAR(), TIMESTAMPDIFF(), CAST(CONCAT(...) AS DATE) (for age and career length calculations).

Aggregation & Pivoting: SUM(CASE WHEN...) / COUNT() (for calculating batting percentages).

This project demonstrates proficiency in structuring and executing complex analytical SQL queries to extract meaningful business intelligence from large datasets.
