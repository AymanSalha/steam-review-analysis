# What Makes a Steam Game Well Reviewed?

A statistical analysis of **27,075 Steam games** in R, asking how price, indie status,
genre, player tags and release year relate to a game's share of positive reviews.

**Full report:** [steam_project.pdf](steam_project.pdf) · **Source:** [steam_project.Rmd](steam_project.Rmd)

## Questions
1. Are indie games reviewed better than games from larger studios?
2. Is there a price "sweet spot"?
3. Which genres and player tags are well or poorly reviewed?
4. Did the flood of releases after Steam Greenlight (2012) and Steam Direct (2017) lower review scores?

## Methods
- **Wrangling:** derived review score, release year, owner-range bounds, indie / Early Access / free flags,
  price groups, and a games-vs-software filter; kept English-language games with at least 50 reviews
  (11,560 games) after showing that scores are unreliable below that.
- **Join:** reshaped a 371-column player-tag table to long form and joined it to the cleaned games.
- **Tests:** Welch two-sample t-test (indie vs. not indie), one-way ANOVA with Tukey HSD (price groups).
- **Model:** multiple linear regression of review score on indie status, price group,
  log(number of reviews), release year and Early Access.

## Key findings
- Indie games score about **2.6 points** higher on average (Welch t-test, p ≈ 2.6 × 10⁻¹⁴); the gap holds after controlling for other factors.
- Games priced **£10–20** are reviewed best; free and under-£5 games worst. Games over £20 score lower than £10–20 games.
- **Early Access** games score about **4.1 points** lower, holding other factors fixed.
- Average scores hit their low in **2014**, the first big year of the release flood, then recovered — partly a **survivorship-bias** artifact of the review filter.
- The model explains only **R² ≈ 0.09** of the variation: with 11,000+ games, effects are statistically clear but small.

## Reproduce
1. Download the data (see [data/README.md](data/README.md)).
2. Install `dplyr`, `tidyr`, `ggplot2`, `scales`, `knitr`.
3. Knit `steam_project.Rmd` to PDF in RStudio.

## Related
Interactive two-sample t-test app built in R Shiny: <https://aymansalha.shinyapps.io/lab3/>

*Ayman Salha · Arizona State University, Fall 2026*
