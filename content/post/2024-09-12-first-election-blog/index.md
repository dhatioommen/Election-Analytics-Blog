---
title: First Election Blog
author: Dhati Oommen
date: '2024-09-12'
slug: first-election-blog
categories: []
tags: []
---



# R Markdown


```r

library(ggplot2)

df <- read.csv("popvote_1948-2020.csv")

# line plot
ggplot(df, aes(x = year, y = pv2p, color = party, group = party)) +
  geom_line(size = 1) +
  geom_point() +
  labs(title = "Two-Party Vote Share Over Time",
       x = "Year",
       y = "Two-Party Vote Share (%)") +
  scale_color_manual(values = c("democrat" = "blue", "republican" = "red")) +
  theme_minimal() +
  theme(legend.title = element_blank())
## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
## ℹ Please use `linewidth` instead.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

<!-- ```{r} -->

<!-- library(ggplot2) -->
<!-- library(dplyr) -->
<!-- library(usmap) -->


<!-- df <- read.csv("C:/Users/dhati/Downloads/clean_wide_state_2pv_1948_2020.csv") -->

<!-- # Calculate the forecast for 2024 using the electoral cycle model -->
<!-- df <- df %>% -->
<!--   mutate(D_Y2024 = (3/4 * D_pv2p) + (1/4 * D_pv2p_lag1), -->
<!--          R_Y2024 = (3/4 * R_pv2p) + (1/4 * R_pv2p_lag1)) -->

<!-- # Determine the party with the higher forecasted vote share for each state -->
<!-- df <- df %>% -->
<!--   mutate(winning_party_2024 = ifelse(D_Y2024 > R_Y2024, "Democrat", "Republican")) -->

<!-- # Plot the forecast on a state map -->
<!-- plot_usmap(data = df, values = "winning_party_2024", color = "black") + -->
<!--   scale_fill_manual(name = "2024 Winning Party", values = c("Democrat" = "blue", "Republican" = "red")) + -->
<!--   theme_minimal() + -->
<!--   labs(title = "2024 Election Forecast based on Electoral Cycle Model", -->
<!--        subtitle = "Forecast: 3/4 * 2020 vote + 1/4 * 2016 vote") -->


<!-- ``` -->
<!-- ```{r} -->

<!-- library(ggplot2) -->
<!-- library(dplyr) -->
<!-- library(usmap) -->


<!-- df <- read.csv("C:/Users/dhati/Downloads/clean_wide_state_2pv_1948_2020.csv") -->

<!-- # Calculate the forecast for 2024 using the electoral cycle model -->
<!-- df <- df %>% -->
<!--   mutate(D_Y2024 = (3/4 * D_pv2p) + (1/4 * D_pv2p_lag1), -->
<!--          R_Y2024 = (3/4 * R_pv2p) + (1/4 * R_pv2p_lag1)) -->

<!-- # Calculate the margin for 2024 (Democratic margin is positive, Republican margin is negative) -->
<!-- df <- df %>% -->
<!--   mutate(pv2p_margin_2024 = D_Y2024 - R_Y2024) -->

<!-- # Plot the two-party vote margin for 2024 on a state map -->
<!-- plot_usmap(data = df, values = "pv2p_margin_2024", color = "black") + -->
<!--   scale_fill_gradient2(name = "2024 Vote Margin", low = "red", mid = "white", high = "blue", midpoint = 0) + -->
<!--   theme_minimal() + -->
<!--   labs(title = "2024 Election Forecast: Two-Party Vote Margin", -->
<!--        subtitle = "Positive = Democratic advantage, Negative = Republican advantage") -->

<!-- ``` -->
<!-- ```{r} -->

<!-- install.packages("ggthemes") -->
<!-- install.packages("maps") -->

<!-- library(ggplot2) -->
<!-- library(ggthemes) -->
<!-- library(maps) -->
<!-- library(tidyverse) -->
<!-- library(usmap)  -->
<!-- library(readr) -->



<!-- # Read presidential popular vote -->
<!-- d_popvote <- read_csv("C:\\Users\\dhati\\Downloads\\popvote_1948-2020 (1).csv") -->


<!-- # Subset data to most recent past election year -->
<!-- d_popvote |> colnames() -->
<!-- d_popvote |>  -->
<!--   filter(year == 2020) |>  -->
<!--   select(party, candidate, pv2p) -->

<!-- # Pivot data to wide format with party names as columns and two-party vote share as values -->
<!-- (d_popvote_wide <- d_popvote |> -->
<!--     select(year, party, pv2p) |> -->
<!--     pivot_wider(names_from = party, values_from = pv2p)) -->

<!-- # Modify winner column to show "D" if Democrats win and "R" if Republicans win -->
<!-- (d_popvote_wide <- d_popvote_wide |>  -->
<!--     mutate(winner = case_when(democrat > republican ~ "D", -->
<!--                               TRUE ~ "R"))) -->

<!-- # Summarize data with respect to winners -->
<!-- d_popvote_wide |>  -->
<!--   group_by(winner) |> -->
<!--   summarise(races = n()) -->



<!-- # Visualize the two-party presidential popular vote over time -->
<!-- d_popvote |>  -->
<!--   ggplot(aes(x = year, y = pv2p, color = party)) +  -->
<!--   geom_line() +  -->
<!--   scale_color_manual(values = c("dodgerblue4", "firebrick1")) +  -->
<!--   theme_stata() -->

<!-- my_custom_theme <- theme_bw() +  -->
<!--   theme(panel.border = element_blank(), -->
<!--         plot.title = element_text(size = 15, hjust = 0.5),  -->
<!--         axis.text.x = element_text(angle = 45, hjust = 1), -->
<!--         axis.text = element_text(size = 12), -->
<!--         strip.text = element_text(size = 18), -->
<!--         axis.line = element_line(colour = "black"), -->
<!--         legend.position = "top", -->
<!--         legend.text = element_text(size = 12)) -->

<!-- d_popvote |>  -->
<!--   ggplot(aes(x = year, y = pv2p, color = party)) +  -->
<!--   geom_line() +  -->
<!--   scale_color_manual(values = c("dodgerblue4", "firebrick1")) +  -->
<!--   my_custom_theme -->

<!-- states_map <- map_data("state") -->


<!-- d_pvstate_wide <- read_csv("C:\\Users\\dhati\\Downloads\\clean_wide_state_2pv_1948_2020.csv") -->



<!-- d_pvstate_wide$region <- tolower(d_pvstate_wide$state) -->

<!-- pv_map <- d_pvstate_wide |> -->
<!--   filter(year == 2020) |> -->
<!--   left_join(states_map, by = "region") -->

<!-- pv_win_map <- d_pvstate_wide |>  -->
<!--   filter(year == 2020) |>  -->
<!--   left_join(states_map, by = "region") |>  -->
<!--   mutate(winner = ifelse(R_pv > D_pv, "republican", "democrat")) -->

<!-- pv_win_map |>  -->
<!--   ggplot(aes(long, lat, group = group)) +  -->
<!--   geom_polygon(aes(fill = winner), color = "black") +  -->
<!--   scale_fill_manual(values = c("dodgerblue4", "firebrick1")) -->

<!-- d_pvstate_wide |>  -->
<!--   filter(year >= 1980) |>  -->
<!--   left_join(states_map, by = "region") |>  -->
<!--   mutate(winner = ifelse(R_pv > D_pv, "republican", "democrat")) |>  -->
<!--   ggplot(aes(long, lat, group = group)) +  -->
<!--   facet_wrap(facets = year ~.) +  -->
<!--   geom_polygon(aes(fill = winner), color = "white") +  -->
<!--   scale_fill_manual(values = c("dodgerblue4", "firebrick1")) +  -->
<!--   theme_void() +  -->
<!--   ggtitle("Presidential Vote Share by State (1980-2020)") +  -->
<!--   theme(strip.text = element_text(size = 12),  -->
<!--         aspect.ratio = 1) -->



<!-- # Create prediction (pv2p and margin) based on simplified electoral cycle model:  -->
<!-- # vote_2024 = 3/4*vote_2020 + 1/4*vote_2016 (lag1, lag2, respectively) -->
<!-- d_pvstate_wide |> colnames() -->

<!-- pv2p_2024_states <- d_pvstate_wide |>  -->
<!--   filter(year == 2020) |>  -->
<!--   group_by(state) |>  -->
<!--   summarize(D_pv2p_2024 = 0.75*D_pv2p + 0.25*D_pv2p_lag1,  -->
<!--             R_pv2p_2024 = 0.75*R_pv2p + 0.25*R_pv2p_lag1) |>  -->
<!--   mutate(pv2p_2024_margin = R_pv2p_2024 - D_pv2p_2024,  -->
<!--          region = tolower(state)) -->

<!-- pv2p_2024_states |>  -->
<!--   left_join(states_map, by = "region") |>  -->
<!--   ggplot(aes(long, lat, group = group)) +  -->
<!--   geom_polygon(aes(fill = pv2p_2024_margin), color = "black") +  -->
<!--   scale_fill_gradient2(high = "firebrick1",  -->
<!--                        mid = "white",  -->
<!--                        low = "dodgerblue4",  -->
<!--                        breaks = c(-50, -25, 0, 25, 50),  -->
<!--                        limits = c(-50, 50)) +  -->
<!--   theme_void() -->


<!-- # Read electoral vote data -->


<!-- # Merge with electoral votes and summarize results -->
<!-- pv2p_2024_states <- pv2p_2024_states |>  -->
<!--   mutate(year = 2024,  -->
<!--          winner = ifelse(R_pv2p_2024 > D_pv2p_2024, "R", "D")) |>  -->
<!--   left_join(ec, by = c("state", "year")) -->

<!-- # Summarize electoral votes by winner -->
<!-- pv2p_2024_states |>  -->
<!--   group_by(winner) |>  -->
<!--   summarize(electoral_votes = sum(electors)) -->

<!-- # Visualize the electoral vote distribution -->
<!-- pv2p_2024_states |>  -->
<!--   ggplot(aes(long, lat, group = group)) +  -->
<!--   geom_polygon(aes(fill = winner), color = "black") +  -->
<!--   scale_fill_manual(values = c("dodgerblue4", "firebrick1")) +  -->
<!--   labs(title = "2024 Presidential Election: Predicted Winners and Electoral Votes") -->

<!-- ``` -->
<!-- Predicting the 2024 U.S. Presidential Election: Competitiveness and State Voting Patterns -->
<!-- How Competitive Are U.S. Presidential Elections? -->
<!-- Presidential elections in the United States are notoriously competitive, with both major political parties—Democratic and Republican—alternating periods of dominance. Political polarization and socioeconomic factors play a crucial role in driving this competition, especially in recent decades. As Fiorina (2017) argues, the U.S. electorate has become increasingly polarized, contributing to the unpredictability of many elections. -->

<!-- From 1948 to 2020, the two-party popular vote share has oscillated significantly, as shown in Figure 1. The 1964 and 1972 elections stand out as landslide victories for Democrats and Republicans, respectively, while elections in 2000 and 2016 were decided by very narrow margins. These trends underscore the competitiveness and volatility of U.S. presidential elections, particularly in more recent cycles. -->

<!-- Figure 1: The graph displays the percentage of the two-party vote share for Democrats and Republicans over time, showing clear swings in party dominance. -->

<!-- This volatility highlights why forecasting elections, especially in battleground states, is a complex and uncertain process. Demographic shifts, changes in voter turnout, and emerging political issues can all play significant roles in influencing election outcomes. -->

<!-- Which States Vote Blue or Red, and How Consistently? -->
<!-- States generally fall into one of three categories in modern elections: "solid blue," "solid red," or "swing." Solid blue states, such as California and New York, reliably vote Democratic, while solid red states like Texas and Alabama lean Republican. Swing states—Florida, Pennsylvania, and Ohio—are more unpredictable and play a crucial role in determining the outcome of elections. -->

<!-- The maps in Figure 2 display state-by-state winners for presidential elections from 1980 to 2020. Notably, the "Rust Belt" states (e.g., Michigan, Wisconsin) flipped from Democratic in 2012 to Republican in 2016, a critical factor in Donald Trump’s victory. These states are projected to remain key battlegrounds in 2024. -->

<!-- Figure 2: Maps show the winning party (Democratic or Republican) in each state for U.S. presidential elections between 1980 and 2020. -->

<!-- Voting patterns are often influenced by economic factors. Bartels (2006) highlights the impact of economic inequality on voter preferences, particularly in swing states. This is evident in the changing allegiances of states like Michigan and Wisconsin, which have seen significant economic shifts over recent decades. -->

<!-- 2024 Election Prediction: First Visualizations and Forecast -->
<!-- To predict the 2024 election, we used a simplified electoral cycle model, which averages 75% of the 2020 vote share and 25% of the 2016 vote share. This model provides a baseline forecast by accounting for recent voting trends while incorporating past election results. -->

<!-- Figure 3 shows the forecasted vote margins for 2024, where red represents a Republican advantage and blue represents a Democratic advantage. Our projections suggest that Republicans will likely dominate in states such as Alabama and Wyoming, while Democrats are expected to hold firm in states like California and New York. However, several key swing states—such as Georgia, Arizona, and Pennsylvania—are expected to remain highly competitive, making them critical targets for both parties. -->

<!-- Figure 3: Map shows the projected two-party vote margin for 2024, with red indicating a Republican advantage and blue indicating a Democratic advantage. -->

<!-- This model aligns with contemporary political analyses that emphasize the growing urban-rural divide. Rural areas have increasingly shifted toward the Republican Party, while urban centers have consolidated Democratic support. This divide is expected to further intensify competition in swing states, where rural and urban votes are more evenly balanced. -->

<!-- 2024 Electoral College Projection -->
<!-- The Electoral College is the determining factor in U.S. presidential elections. Each state is allocated a set number of electoral votes based on population, and candidates must secure at least 270 out of 538 electoral votes to win the presidency. Using our projected vote margins, we estimate the Electoral College outcome for 2024. -->

<!-- According to our model, Democrats are likely to win around 270 electoral votes, while Republicans are projected to win 268—a razor-thin margin. The final outcome will hinge on key swing states, particularly Pennsylvania and Wisconsin, which could easily swing the election in either direction. -->

<!-- Figure 4: The projected Electoral College outcome for 2024, based on the predicted two-party vote margins. -->

<!-- Political scientists like Edwards (2011) have long argued that the Electoral College system disproportionately favors smaller, more rural states, giving Republicans a structural advantage. While Democrats tend to win the popular vote more frequently, they often struggle to secure enough electoral votes due to the distribution of voters in key swing states. This dynamic played a significant role in the 2000 and 2016 elections, and it is likely to be a factor in 2024 as well. -->

<!-- Conclusion -->
<!-- In summary, U.S. presidential elections remain highly competitive, particularly in swing states, where small shifts in voter behavior can have significant impacts on the final outcome. Our simplified electoral cycle model provides an initial forecast for the 2024 election, but many factors—such as campaign strategies, voter turnout, and economic conditions—will influence the final result. As things stand, the 2024 election is poised to be one of the closest and most contested elections in recent history. -->

<!-- Sources: -->
<!-- Fiorina, M. P. (2017). Unstable Majorities: Polarization, Party Sorting, and Political Stalemate. Hoover Institution Press. -->
<!-- Bartels, L. M. (2006). Unequal Democracy: The Political Economy of the New Gilded Age. Princeton University Press. -->
<!-- Edwards, G. C. (2011). Why the Electoral College is Bad for America. Yale University Press. -->
<!-- Abramowitz, A. I. (2018). The Great Alignment: Race, Party Transformation, and the Rise of Donald Trump. Yale University Press. -->
<!-- Hetherington, M. J., & Weiler, J. D. (2018). Prius or Pickup? How the Answers to Four Simple Questions Explain America’s Great Divide. Houghton Mifflin Harcourt. -->
<!-- Wasserman, D. (2020). “The Swing States of 2020.” The Cook Political Report. -->
