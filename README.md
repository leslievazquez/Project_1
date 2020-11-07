# Analysis of Global Countries' Covid-19 Pandemic Responses
By Leslie Vazquez, Steven Pennington, Wolphy, Joseph, Rejane Beringer, and Brian Roberts

#### Motivation: 	      
The motivation for our project stemmed from a desire to investigate a current, real-world circumstance or situation that impacts our everyday lives. So obviously, the Covid-19 pandemic stuck out like a sore thumb. And the last thing any of us wanted to place more focus on was the upcoming election (lol). The pandemic has been at the forefront of the entire globe’s mind and efforts since the year 2020 began, dramatically altering the way we all function in today’s world, and endlessly stocking media timeslots on every network.  If asked how you believe the United States has handled the Covid-19 Pandemic, I have a feeling the general consensus would be “not very well at all”.  The media constantly shows the rates of infection and deaths, and the impact on economies both here and abroad.  The lack of action by our government increases our frustration and time spent away from our friends and loved ones while some countries seem to have actually already “rounded-the-corner” and returned to some essence of normalcy. These circumstances led our group to ponder what other governments have done to curb the spread of the virus, protect their citizens, and weather this storm of uncertainty that has loomed over humanity for over 10 months now.

#### Hypothesis & Q’s:        
The main hypothesis that led our research and analyses was “Countries with stricter mandates would be more successful in limiting both the spread and lethality of Covid-19”.  To accompany this core message, we developed a set of questions to explore throughout our data cleaning and analysis, in the hopes of unearthing more intimate relationships within our data. The first being “How did countries spending impact the spread of Covid-19?”. This question is impactful for the study because Covid-19 has also presented a great economic burden on many nations. We looked to identify if countries’ investment into their own nations well-being curbed the rate of infection.  Our next question took into consideration the role information spread played in lowering the rate of infection and mortality. This was a particularly interesting question to consider given the difficult nature of how to quantify such a variable.  Also, in the social media age how would one account for spread of disinformation as well?   

--------

### Questions & Data

#### Finding Data:      
For our main hypothesis and all of our supplemental questions we needed data that reflected, both, information on each countries’ mandates, and the impact Covid-19 had on their respective populations.  Thankfully, a simple google search yielded a dataset from the University of Oxford on GitHub that has tracked global covid-19 policy implementation as well as confirmed cases and deaths since as early the end of December 2019.  

#### Sample:      	
When determining sample we wanted to reflect a wide variety of countries, not only geographically, but also with how they had handled Covid-19. Background research paired with some prior knowledge of countries who had success or trouble based on their own measures led us to select the following; Brazil, China, UK, Italy, Japan, New Zealand, Sweden, and the United States.  In hindsight, if we had known the statistical analysis was going to be introduced halfway through the project, we would have expanded our study to more broadly encompass the whole dataset, as a hand-picked sample size of 8, which would later become two groups of four, was destined to yield insignificant results.  These countries were selected because of their availability of data, geographic spread, varying population sizes, and their know differences of covid-19 mandates.  For those who have followed global media coverage, these countries all had varying success with handling covid-19. From varying successful strategies like Sweden’s lack of any forced mandates and New Zealand’s largely successful country lockdown to nations and Japan’s data-based approach to those who were hit hardest by Covid-19 such as Brazil, the UK, Italy, and the US. We also felt the need to include China because they were not only the country of origin, but they also were incredibly efficient in curbing spread while being a very large country. So although the small sample and it experiencing selection bias, we were excited to see what relationships we could unearth from our data.  

--------

### Data Cleanup & Exploration

#### Exploring/Cleaning:
Our first issue when cleaning came up as soon as we tried to read in the csv.  Pandas was attempting to read and guess data types for each column, which can be very memory demanding for the code to run. Inserting the low_memory=False ensures that the dataframe generates the same datatype for each column.  Then, Null values were dropped and the columns containing Date, each of the mandates available, and the confirmed cases and deaths were added into our final cleaned dataframe.  Additionally, it was important for us to look into how the dataset had quantified something so open to change as “strictness of a mandate”. The mandates were ranked on a scale of 0-4 No Measures, Recommended, Required on some levels, and closing required on all levels. Some varied though as Income support was 0-2 being no support, and either less or greater than 50% income lost being supplied to its citizens.  

Then, placing a loc on the dataframe to find country was initiated to groupby mandate scores across all mandates. Once this was done, the average mandate score from throughout the pandemic timeline was taken for each mandate, summed together, and divided once more to yield the average strictness measure for all mandates for each of our countries. 

Finally, the mandates dataframe was run thorugh the describe function to find our overall mandate strictness across all countries, which was 1.4. From this, our groupings were defined as being “strict” or “relaxed” based one their position relative to this summary value. 

--------

### Data Analysis
The data analysis pertaining to our primary hypothesis was fairly straightforward. After reading in the cleaned dataframe, pandas’ .loc property was used to extract information for confirmed Cases and Deaths for both the groupings, being “Strict” and “Relaxed” countries defined during the Data Cleanup process.  Line plots were developed to assess for unexpected trends from this data. It is important to note that although these types of visualizations have the potential to show interesting phenomena, they can also be misleading due to scale. Without a reference to the total population of each country, it is hard to get an understanding of how the values compare to one another.  To account for this, the most recent date with records for all countries of interest was converted into its own dataframe, and a new column was appended with the total populations of each country.  The Confirmed Cases and Deaths per capita were found by dividing Confirmed values by populations and stored into a new dataframe. From here, bar charts can yield a more comprehensive picture of how Covid-19 spread, and the toll it had on each country, comparatively.  Between the two, scale should still be taken into account.  One interesting thing to investigate further would be to determine why these two graphs have discrepancies such as the UK. Possible explanations to investigate are comorbidities and the average level of health between each countries’ citizens. To statistically test our hypothesis, 2-Sample T-tests were run between the means of each groups Infection rates, and then between mortality rates. Before delving into the results of the T-tests, it was interesting to see that for our countries of interest the more relaxed countries had lower rates of infection and mortality. The resulting p-value for Infection Rate was 0.58 and the p-value for Mortality Rate was 0.60.  Immediately it was prevalent that the small sample sizes resulted in such large p-values. Obviously, the result being a failure to reject the null Hypothesis.  We can reflect on changes that could be made to this study to improve the accuracy of the statistical results in the Post-Mortem.   

--------

### Supplemental Questions:

###### Q1: 
Comparing the spending of each country in relation to the spread of the virus was a very daunting task.  A great deal of time was spent examining how different pairs of countries of interest had spent portions of GDP towards curbing the virus, whether that be acquiring PPE for healthcare workers, or providing economic aid to its citizens in response to the closure of so many businesses.  The dataframe was exported to Excel to evaluate for further insights. Ultimately, linear regression and a Pearson’s R Coefficient to numerically evaluate for a relationship. The difficulties with answering this question were not in the technical details. Sub data frames comparing countries spending and increasing cases were straightforward, and the same went for the correlation and regression. The largest problem here was staying specific to the question. While exploring the data, it was noticeable that a great deal of the countries that had spent little money, also had a smaller proportion of the cases.  

###### Q2: 
The process for exploring the relationship between government information dissemination and Covid-19 case and mortality rate was performed by grouping the data on government  information output in the original dataframe by country and date aligned with spread of cases and deaths later, to evaluate at eye-glance for any possible trends that jumped out.  Because of the format of this information, graphing, and especially graphing all of the countries of interest together to observe differences and possible nuances, was exceedingly difficult. A linear regression was ultimately run but did not yield what we expected. The expectation was that more intensive campaigns would result in lower case rates. Empirical findings showed the New Zealand, Japan and Sweden, the countries with the lower average confirmed cases, had information campaigns starting with officials urging caution, then one month into the campaign, jumping to a maximum value for information output. 

###### Q3:  
The final question we considered was the impact of geographic spread and population density. This was used as a metric of counter to our original hypothesis. We wanted to determine if population density served as a limiting factor to how well a government’s mandates could impact covid-19 spread.  A second dataset from the website Our World in Data needed to be cleaned to allow for investigation. This was completed by selecting the relevant columns that pertained to the question, aided by a specific delimiter join function denoted as ‘magic’ and then locating the countries of interest. It was surprising to see the UK at such a high rate of transmission given the countries standing amongst the others in terms of density.         

--------

### Post-mortem

###### Difficulties:  
The most major problem we dealt with throughout this project was defining, and redefining, our scope. The original idea of comparing the effectiveness of global countries’ Covid-19 government responses was incredibly exciting and the variety of factors we could delve into grew organically during our first group meeting. Over time however, and with the addition of the necessity for statistical testing, the end-goal of the project and what could be accomplished in the two-week period immediately narrowed.  To deal with this we decided to make our primary hypothesis focus directly on the relation between mandate strictness and the effect Covid-19 has had on their respective populations.  But we did not want to limit the degree to which we explored our supplementary questions and data, so we looked to uncover progressive insights, even if not statistically significant at present. 
	
Another issue to take into consideration from this project stems from the original issue of scope. When trying to look deeper into how each countries’ mandates changed Covid-19 impact, a new variety of variables need to be considered when trying to determine causation, even if a correlation was found. Things such as population density, geography, the level of development in each country, and even the relationship and trust between central governments and their citizens can all influence how well a mandate works, no matter how strict it is.  As considerable variables grow, finding suitable and preferable ways to quantify and assess all of these variables can become overwhelming.   

--------

### Further Research:
Given more time we would need to rerun the mandate aggregation and averages for all of the countries present in the original dataframe. This would allow us to rerun the t-tests with much larger sample sizes for both the “Strict” and “Relaxed” groupings.  Additionally, it would have been very interesting to have developed a way to determine how impactful certain countries’ mandates resulted in preservation of life and limiting spread of the virus.  We were caught between opening our main analyses run to the entire dataset and trying to find specifically which countries’ mandates had the greatest impact on success. For most of our supplemental questions, more in-depth datasets relating to those variables would be ideal but we could not find readily available data for each of the questions we considered for all of the countries we investigated, although we had tried to select ones with high media coverage and are fully developed economically. 














