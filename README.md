# Recommender System Analysis of Movie Rating Data
Connor Ranson
500941791
CKME-136

## Introduction 

The use of recommender systems in technology spaces had done wonders for companies like Amazon, Netflix, Instagram, and many more in the ability for them to increase the ease for current and potential customers to find products or entertainment they might personally enjoy. This has been show to increase both purchase amounts and frequency, entertainment viewing time on a platform, and customer satisfaction of the service offering the tailored recommendation. 

With all that being said, one can see how important accurately recommending options that the customer would actually be interested in to that specific customers would be.  There are quite a few approaches that companies use to provide accurate recommendations to customers.

The first method is popularity-based recommendation system. When a company has little amounts of time, money, or data to build a more complex recommendation system, they might turn to a popularity-based system where they recommend all customers what the most popular items are to all customers over a designated amount of time. This is used well in Netflix’s “Top 10” feature that it has added as a component of their overall recommendation platform, to show users what are the most streamed shows or movies that month while also having their more tailored recommendations as well. It is also used a lot when a new user signs up and a company has little to know information on that person, but would like to recommend products the customer might be most likely to enjoy. 

When a new user signs up with a platform and provides introductory information like Age, Gender or Search History (i.e. product type, average item cost) a different recommendation system can be used called a Content Based Recommender System. This system takes that information and produce a binary value of if that customer will like a product or not. As the customer used the platform more the purchase history can add to the accuracy of a classification system. 

Another form of recommending can be done on the belief that you will like something that other people with similar reviews of products or similar tastes like. This is called Collaborative Filtering. This can be done using multiple methods including nearest neighbour user and item based filtering as well as matrix factorization. This will be explored more during the execution of the analysis.

With the many methods of recommending products to customers the goal of this paper is “to find the method that will most accurately and precisely recommend movie options to a person, based on the data collected from the MovieLens dataset  including users and their ratings of particular movies from January 1995 to September 2018.” Multiple methods will be tried using popularity, content-based, collaborative, and a hybrid filtering method to see which elicits the highest precision, highest recall, and lowest absolute mean error.

## Literature Review

Popularity Based Recommender System
Jonnalagedda, Nirmal & Gauch, Susan, Personalized News Recommendation Using Twitter

Recommendation Systems have grown a lot since the birth of the idea of recommending stories based on view count. This article explains how the popularity based systems on twitter of ranking the popularity of articles from Twitter’s public timeline is combined with information users personally construct to better outline their preferences and interests to provide popular stories that match their interests [2]. 

Content-based Recommender Systems
Alspector, J., Koicz, A. & Karunanithi, N. Feature-based and Clique-based User Models for Movie Selection: A Comparative Study. User Modeling and User-Adapted Interaction 

The authors discuss the ability to apply a feature-based approach to movie recommendations. The results showed that the feature based models was equally as effective as movie rating experts. The feature based approach was also compared to a clique-based approach (collaborative filtering) which saw advantages when other users were available and viewed the same movies as the end-user [3].

Collaborative Filtering
Kanagal, B., Ahmed, A., Pandey, S., Josifovski, V., Garcia-Pueyo, L., & Yuan, J, Focused matrix factorization for audience selection in display advertising

Although this paper was in relation to ad campaigns, it came across a similar issue that is this Movie Data recommender system is trying to solve. When using matrix factorization most users will not have purchased from all campaign in the same way that the viewers have not seen all movies. The authors suggest a more focused matrix factorization that borrows information from related campaigns while ignoring information from unrelated ones. They saw the focused model outperform consistently [4].

Bartłomiej Twardowski, Modelling Contextual Information in Session-Aware Recommender Systems with Neural Networks

Twardowski explains the situation where recommendations are needed for a user with little to no background information on the user. With this case recommendations need to be made based on their current session. They explain the use of Recurrent Neural Networks (RNN) to better mimic the sequential behavior of this case and train the model to have more accurate results [5]

Hybrid Recommender Systems
J. Salter and N. Antonopoulos, CinemaScreen recommender agent: combining collaborative and content-based filtering

This article spoke to a similar issue this paper is trying to face: How to get the most accurate movie recommendations to the end-user. It tackles the difficult of using the content-based recommendation system and not being sure if the recommendations are highly rated by viewers and collaborative recommendation systems and recommending a movie outside of the preferred genre or directorial style. This article proposes a hybrid method to better represent the data presented [6].

## Dataset
This analysis uses data from the MovieLens small dataset and contains ratings on a 5 star scale and free-text tagging. 9742 unique movies were reviewed by 610 randomly selected users (who had rated at least 20 movies) between March 29, 1996 and September 24, 2018. No information other than User ID was provided to distinguish the different users. Those users left 100836 ratings along with 3683 text tags. Each review will include a User Id, Movie Id, Rating, Title, IMDb Id, IMDb Rating, Genre, and Tag (if available). Recommendations will be evaluated on Precision, Recall, and Root Standard Mean Error. Timestamp of rating and tag has been removed. This dataset can be found at: https://grouplens.org/datasets/movielens/latest/

## Approach
Step 1: Merge datasets and scrape IMDb Ratings
This set will include cleaning and merging the datasets provided. I am looking to scrape IMDb for ratings to add to the analysis but that has not been accomplished yet. Data cleaning can be found here: https://github.com/ConnorRansonRyerson/CKME-136/blob/master/CKME136%20%20Initial%20Data%20Description.ipynb
Step 2: Build Basic Popularity Recommender
This step is to find a basic starting ground for the analysis. The goal is to count the number of ratings a movie has received and provide the end-user with that list. The assumption is that the most popular movies will have the highest chance of being liked by anyone in the audience. There is no tailored recommendations. These recommendations will be tailored to their specific genre.
Step 3: Build Item-based Content Filtered Recommender
Since we have Tags, Movie Name, and Genre we can use those to build a Content-Based Recommender System. Each movie will be given a list of words coming from the Genre, and tags with the index becoming the Movie Title. When modeling, I will use a TF-IDF Vectorizer to build a cosine similarity matrix. This will be used to supply the recommendations.
Step 4: Build Collaborative Filter Recommender
I will then build a Collaborative Filter Recommender System to allow for recommendations of movies outside of the same genre. The method used will be Singular Value Decomposition (SVD) Matrix Factorization on measures like Root Square Mean Error and Mean Absolute Error. 
Step 5: Build Hybrid Recommender
I will then build a Hybrid model taking the best performing Content-Based Recommender and the best performing Collaborative Filter Recommender.

## Results

### Content-Based Recommender Systems

Two content-based Recommender Systems were built. The first recommender built was built using the ‘Overview’ column provided by the Movie Database. A TF-IDF was built using the following formula. 
 
Cosine Similarity was used and ranked to provide a top 10 list for the movie provided to the recommender system as shown here.
 
As seen the overview does not do a great job at recommending similar movies. There are some similarities in the type of movies and general theme. It can be shown that movies with more common names (ex The Lion King) that have a more general overview do a better job at recommending similar movies.

The next content-based recommender was more Metadata-Based Recommender System. A metadata ‘Soup’ was created using the tags left by user reviews and the genre of the movie. The methods were the same as an IF-IDF and Cosine Similarity were used. An example of this recommender is shown here.
 

This recommender seems to recommend similar movies a lot better. It does a good job at recommending young adult fantasy adventure movies. It is also a lot more consistent in it’s recommending ability.

The evaluation metric of Root Mean Square Error (RMSE) was used to evaluate the predicted rating of a user created in this format against the provided user rating of a film. The RMSE is 0.991. Ways in which this could possibly be reduced would be creating a feature to classify a more specific sub-genre category, include more metadata from the larger dataset, or include a popularity filter to allow for more popular movies to be recommender more frequently.

### Collaborative Filter Recommender System

Two approaches of Collaborative Filtering was used in this analysis. The fist method is User-based Recommender Systems. A ratings matrix is used to create a mean rating function with a RMSE of 0.98.

Two Model-Based Systems were built. The first one was built using K-Nearest Neighbors algorithm on 5 splits. This method computes the Euclidean distance of all points in the training set from the chosen movie and selects the closest ones to that movie as recommendations. This method found a mean RMSE of 0.94 as shown below.

The second was a Single Value Decomposition (SVD) method which is a matrix analysis technique that allows a higher dimensional matrix to be represented in a lower dimension. It identifies and removes less important parts and produces an approximation in the desired amount of dimensions .  The result of this was a mean RMSE of 0.87 as shown below.

### Hybrid Recommender System

The final recommender system that was built was a Hybrid Recommender System. This method is used to try and help with some of the shortcomings of the two other methods. It includes user-data and ratings to find the best recommendations. This method allows for users to have tailored results even if the inputted movie is the same. This is shown below.
As shown, the user preferences come into account and can even impact the recommendation of one movie over another regardless of the vote average. 


## Conclusion

Multiple methods for finding recommendations were tested and evaluated on the MovieLens Small Dataset. The Content-Based Recommendation System found that the metadata approach saw the best results as it provided insight into the genre and keywords the audience thought of when rating the movie. This could be improved in the future buy using even more metadata to recommend movies with a similar cast or director. The Collaborative Filtering Recommendation System found that the SVD approach had a better result than the KNN approach and it was able to find the most important factors and recommended based on that. This was improved by a Hybrid Model which combined the metadata approach with the SVD approach to create a more user-tailored recommender engine.
 
## Bibliography
[1] F. Maxwell Harper and Joseph A. Konstan. 2015. The MovieLens Datasets: History and Context. ACM Transactions on Interactive Intelligent Systems (TiiS) 5, 4: 19:1–19:19. https://doi.org/10.1145/2827872

[2] Jonnalagedda, Nirmal & Gauch, Susan. 2013. Personalized News Recommendation Using Twitter. 21-25. 10.1109/WI-IAT.2013.144.

[3] Alspector, J., Koicz, A. & Karunanithi, N. Feature-based and Clique-based User Models for Movie Selection: A Comparative Study. User Modeling and User-Adapted Interaction 7, 279–304 1997. https://doi.org/10.1023/A:1008286413827

[4] Kanagal, B., Ahmed, A., Pandey, S., Josifovski, V., Garcia-Pueyo, L., & Yuan, J. 2013, April. Focused matrix factorization for audience selection in display advertising. In 2013 IEEE 29th International Conference on Data Engineering (ICDE) (pp. 386-397). IEEE.

[5] Bartłomiej Twardowski. 2016. Modelling Contextual Information in Session-Aware Recommender Systems with Neural Networks. In Proceedings of the 10th ACM Conference on Recommender Systems (RecSys ’16). Association for Computing Machinery, New York, NY, USA, 273–276. DOI:https://doi.org/10.1145/2959100.2959162

[6] J. Salter and N. Antonopoulos, "CinemaScreen recommender agent: combining collaborative and content-based filtering," in IEEE Intelligent Systems, vol. 21, no. 1, pp. 35-41, Jan.-Feb. 2006. doi: 10.1109/MIS.2006.4

[7] Banik, Rounak. 2018. Hands-On Recommendation Systems with Python: Start building powerful and personalized, recommendation engines with Python. Packt Publishing.




