# BGG_analysis
# Correlation analysis of the top 2000 rated  board games  on BoardGameGeeks (BGG)

## Intro 

What attributes lead to a well received board game? Is it mechanical design, the games complexity the amount of content, or something more subtle? I analysed the top 2000 rated board games on BGG with the process and the results detailed below, in order to try and address this question .

## Data - Overview, cleaning, manipulation 

### Overview 

The dataset used for this  analysis is the "Top 2000 Board Games Ratings" by Nikita Fedorov, which can be  found [here](https://www.kaggle.com/datasets/nfedorov/top-2000-board-games-ratings). No changes were made to the data set prior to loading it for analysis.

A description of all columns I used from the dataset , taken directly from the datasets page can be found below: ( an asterisk denotes its inclusion in the results ) 
boardgame_id - board game id

title - title of board game

year_published - year of publication of the board game

minplayers - minimum number of players per game

maxplayers - maximum number of players per game *

minplaytime - minimum playing time per game 

maxplaytime - maximum playing time per game *

age - lower age limit for playing *

users_rated - number of users who rated a game *

average_rating - average rating *

bayes_average_rating - bayes average rating

median - median rating

stddev - standard deviation of rating

owned - number of users who have a game *

trading - number of users who selling a game *

wishing - number of users who want to get a game *

num_of_comments - number of comments

num_of_weights - number of scores for weight

average_weight - average weight of game ( the perceived complexity of the games according to  players ) *

ranks - game ranks

main_publisher - main publisher

description - description of the game

publishers - all publishers

honors - all honors

expansions - all expansions

accessories - all accessories


mechanics - used mechanics

category - category


implementations - all implementations

suggested_numplayers - proposed number of players



In addition, there were columns I chose to remove from the dataset . These are listed below along with my reasoning for excluding them :

podcast_episodes - all podcast episodes

comments - some comments

marketplace_history - marketplace history ( listings of games, prices they were sold for )

thumbnail_link - thumbnail link

image_link - image link

I removed the image links as I did not feel there was any relevance with the analysis.

In regards to the other columns, I wanted to focus on attributes specific to the games, not to discourse surrounding them, hence why I removed the comments, marketplace history and podcast episode columns .

### Data refactoring 

Some columns, such as  honours, contained a  string with a list of  which were separated by vertical bars '|'. In order to refactor them, I turned them into columns which contained the number of awards given to a game. 

This was done by turning each string into a list of strings, with the '|' being the delimiter. Then if a value existed in the list, the length of the list would be returned . If not then 0 would be returned.
##  Criteria 


The average rating column formed  the base criteria  by which the other attributes were  represented. This was chosen as it gave the best idea of the general feeling of BGG's users on the boardgame .

The  average_rating column was  used instead of the bayes_average_rating column for the base criteria : ( the bayes_average_rating takes outside information into account to calculate the mean, used when the dataset is small. For a game to be given a displayed ranking on BGG, it has to surpassed a minimum review threshold. As this dataset was taken from the ranking list,  all games on it would have passed the threshold. Therefore it can be argued that the average_rating column is more representative of a games rating.)

In addition, average weight was used  to gauge users opinions on the complexity of the game.

Pearson  correlation was used to determine the results. It was compared against Spearman and  Kendall. While the performance of  Spearman was close, Pearson  outperformed  by a small magnitude suggesting that there were approximately linear relationships between attributes.



## Results 

 Images of the top 3 most highly correlated attributes for high average rating are shown below .. Graphs for the other attributes, including  those against the average weight of a game can be found in the attached notebook.

![Figure 1][./images/Pasted image 20260819113235.png]


Figure 1 : Scatter graph of average rating against average weight. The 1st correlation matrix used Pearson correlation. The 2nd correlation matrix used Spearman correlation. The 3rd correlation matrix used Kendall 


![Figure 2][./images/Pasted image 20260819113429.png]

Figure 2 : Scatter graph of average rating against max playtime, with  outliers of play time above 1200 minutes removed. Correlation matrix used Pearson, and was calculated after the removal of the outliers.  

![Figure 3][./images/Pasted image 20260819113500.png]

Figure 3: scatter graph of average rating against the number of 'wishes' on a games page. The correlation matrix used Pearson  
## Summary 

The average rating of a game is most closely correlated with  a high average weight(r=0.54), high number of user wishes(r=0.41), and a higher max playtime(r=0.35).Only 1 attribute has a correlation score of over  0.5 or less than -0.5. This could mean that  attributes outside the dataset more closely correlate with game ratings.

## Limitations / Next steps

While these attributes are correlated with the games rating,  this does not necessarily equate to causation. Causal inference could be used work out if any of the attributes cause the higher rating. As well as this, semantic analysis of the comments could be used in order to refactor them into a form fit for correlation.
