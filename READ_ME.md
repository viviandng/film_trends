# Film Industry Trends

Team: Joseph McHugh & Vivian Dang


![Marvel.webp](./zippedData/Marvel%20Image.webp)

### Prompt:
In recent years, the executives at Microsoft have noticed many large tech firms have begun creating original video content. Not wanting to miss out on a lucrative business opportunity, they have decided to get in on the action. They plan to create a new movie studio, but unfortunately don’t know anything about making movies. 

To rectify this deficiency, they have hired a crack data-science duo to help them better understand the movie industry. The team has conducted a thorough data analysis and created a presentation highlighting the types of films that are most likely to be successful at the box office. The team has translated their findings into actionable insights that Microsoft can use when deciding what type of film they should be creating. 


### Three Questions We Want to Answer:

1.	What movie genre produces the most profit?
2.	In this genre, what is the best runtime?
3.	How much should we spend on budget production?


### Data Collection

Here are the two sets of data files that were used: https://github.com/viviandng/flatiron-project-1/tree/master/zippedData


#### Data description:
    File one: movie_budget = ‘tn.movie_budgets.csv.gz’ 
        Shape:
            6 columns
                1. id: index id
                2. release date: when the movie was released to the public
                3. movie: name of the movie
                4. production_budget: cost in U.S dollars to create the movie 
                5. domestic_gross: movie earnings in the U.S
                6. worldwide_gross: movie earnings worldwide
            5782 rows
 
     File two: title_basics = 'imdb.title.basics.csv.gz'
         Shape:
            6 columns
                1. tconst: movie id
                2. primary title: movie title
                3. original title: movie title 
                4. start_year: the year the was released
                5. runtime_minutes: the length of the movie in minutes
                6. genres: the style of the movie
            6144 rows
 


### Data Processing
To answer our business questions about the film industry, we wanted to create a dataframe that includes columns: Movie Title, Production Budget, Domestic Gross, Worldwide Gross, Runtime (in minutes) and Genres for further analysis
 
Tool: pandas
1. Create the main dataframe
    main_df = pd.DataFrame(movie_budgets['movie']
 
2. Populate the main dataframe from “movie_buddgets’ dataset with relevant columns like: production budget, domestic gross, worldwide gross
 
3. Rename dataframe columns for main_df and title_basics so we could merge on “Title”
 
4. Merge title_basics with main_df using pandas merge function
    main_df = pd.merge(main_df, title_basics, how='outer', on='Title')
 
5. Trim size of dataframe to first 5782 rows (number of rows with financial data)
 
6. Decrease noise by dropping columns like tconst, original title, start year
 
7. Drop duplicate  rows and rows with null values and they will offset our data
 
8. Create a profit column where profit = worldwide gross – budget production

9. Create a new dataframe, group by genre and its average values
    genres_profit = main_df_genres.groupby(main_df['genres']).mean()

10. Sort profit by descending mean profit values. We found that action, adventure, sci-fi generated the most mean profit.

11. Create a new dataframe with just movies in the action, adventure, sci-fi genre. 

12. Create scatter plots and regression lines for runtime vs profit, production and production budget vs profit. Analyze for correlations.

13. Create a whisker plot to analyze runtime distribution

14. Create a whisker plot to analyze production budget distribution

15. Create a new dataframe with movie title and profit percentage then select for movies with over 100% profit for further research


### Data Visualization & Analysis : 
We created 5 figures to show our findings.
 
Tool: NumPy, Matplotlib (pyplot), Statistic (mean)

Figure 1: We created a bar graph to show the different movie genres and their mean profit. Mean profit is the profit of all the movies in that genre divided by the number of movies in that genre. From the graph, we can see that the highest bar belongs to action, adventure, sci-fi. This tells us that on average, movies that belong in the genre (action, adventure, sci-fi) generate more profit than movies in the other genres. 
![Bar_Chart.png](./zippedData/Bar_Chart.png)

Figure 2: We created a scatter plot for runtime in minutes vs. profits. We wanted to see if there was a relation between a movie’s length and its profit. Our plot shows that there is a moderate positive correlation between the two variables. As we can see below, as runtime increases, profit also increases. However, this is not a strong correlation with an r value of 0.57. More data and further research is needed to see if the rising trend will continue or if profit will decrease when runtime becomes too long. We also want to see a stronger correlation (r >0.7) before suggesting that increasing a movie’s runtime will also increase the profit it produces. The top 10 profit points are between runtime 120 and 160 minutes. 
![Run_Time.png](./zippedData/Runtime_vs_Profit.png)

Figure 3: We created a whisker plot to show the distribution of runtime. The plot suggested that 50% of movies have a runtime between 122 - 140 minutes. 
![Whisker_Runtime.png](./zippedData/Box_Whisker_Runtime.png)

Figure 4: We created a scatter plot for production budget and profit. We wanted to see if there was a relation between spending more money producing a movie and its profit. Our plot shows that there is a moderate positive correlation between the two variables with r = 0.4. Similar to our runtime vs profit scatter plot, we will need more data and further research to establish the relationship between production budget and profit. The two outliers on the right show that a high production budget may generate a very high profit or cause a huge loss. Ignoring the outliers on the right, we see that the top 10 highest profit producing movies have a production budget between 140 - 200 hundreds of million USD.
![Budget_Profit.png](./zippedData/Budget_vs_Profit.png)

Figure 5: We created a whisker plot to show the distribution of production budget. The plot suggested that 50% of movies have a budget distribution between 140 - 200 hundreds of millions USD. 
![Whisker_Budget_Profit.png](./zippedData/Box_Whisker.png)


### Business Insight
From our data analysis, we would like to suggest to the CEO of Microsoft to produce an action, adventure, sci-fi film and be prepared for a production budget between 140 - 200 hundreds of millions USD. In addition, to aim for a high profit, the CEO of Microsoft should try to make the runtime of this movie between 120 to 160 minutes. 


### Limitations & Further Research
We had three days to clean and analyze the data so due to the lack of time, we were not able to explore how other factors may affect the profit of these films. For example, we were not able to explore how picking a producer, writer, or actor may impact the revenue of a film. Moreover, we noticed that some of our data had duplicates with the same movie title but different genre and runtime values. With more time, we would research the integrity of our dataset and try to obtain a dataset that is higher in quantity and quality and explore other variables.

