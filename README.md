### Background

[WeRateDogs](https://en.wikipedia.org/wiki/WeRateDogs) is a Twitter account that rates people's dogs with a humorous comment about the dog. These ratings almost always have a denominator of 10. The numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because ["they're good dogs Brent."](https://www.vox.com/2018/7/23/17603566/dog-rates-good-dogs-brent-brant-got-a-puppy-meme) WeRateDogs has over 8 million followers and has received international media coverage.

Please check [Dogs Are Doggos: An Internet Language Built Around Love For The Puppers](https://www.npr.org/sections/alltechconsidered/2017/04/23/524514526/dogs-are-doggos-an-internet-language-built-around-love-for-the-puppers) to familiarize yourself with formal Doggolingo as you will see much use of it in this analysis

For more on dog breeds, please check [DogTime](https://dogtime.com/). Also, all breed info were collected and stored in a separate CSV file for your convenience.

### Scope

The dataset featured is the tweet archive of Twitter user [@dog_rates](https://twitter.com/dog_rates), scope of this analysis covers the period starting Nov'15 till July'17 with a total of 1467 tweets. Only tweets with dog images and original ratings were considered (no replies or retweets) with the aim of concluding on two main things:

- Why is this account successful.
- Key drivers of higher follower engagement. 

### Code

Python 3 with Pandas, Numpy being main libraries

### Data source

- Twitter archive for the period mentioned earlier.
- Image prediction results, these predictions are outputs of a neural network that can classify breeds of dogs based on their images. Results are based on three tests for each picture along with their relative confidence level of the true dog's breed.
- Twitter API, to query any missing data from the archive.
- Dog breeds info scraped from [DogTime](https://dogtime.com/)

### Challenges

Biggest challenge was cleaning image prediction results for the following reasons:
  - Some results were so confusing. Several false predictions, which means that images are not for an actual dogs, were in fact for an actual dogs!. [Lusy Imbergerova & Deril](https://www.youtube.com/watch?v=GL3DXJE9UJk) were referenced as 'Home Theater' in image prediction results :(
  - Very close confidence levels for true prediction results, while highest prediction not always correct. Example: one image had first breed prediction result being a Lakeland terrier at 19% confidence and second prediction result being a Labrador retriever at 16% confidence, the actual image was for a Labrador retriever!
  - I have very limited knowledge of dog breeds, so to decide on what picture is for which breed was like 'IS THIS FOR REAL??'

To overcome these challenges I designed a systematic cleaning process as follows:
  - Built a dataset of all breed info scraped from [DogTime](https://dogtime.com/) in order to make an informed decision cleaning these pictures and producing accurate analysis
  - Incorporated engagement metrics to filter prediction results of false predictions that are for actual dogs. Most likely, higher engagement signals that this tweet is for an actual dog.
  - Assessed accuracy of true prediction by identifying which test result groups (1st/2nd/3rd) had most correct predictions, discarded groups with lowest correct counts and manually verified the results of tweets with high engagement metrics based on visual inspection of the image.

### Approach

Systematic steps in assessing and cleaning data were taken. First thing was to spot all issues that I could possible identify in the context of clean and tidy data both visually and programmatically. Then came the actual cleaning of these issues in a logical order to save time.

### Assessment outcome

- A-Quality Issues
  - A.1-Twitter Archive Dataframe:
    - A.1.1-Variables does not conform to our defined schema
    - A.1.2-Time stamp dtype not properly identified
    - A.1.3-Some tweets have misleading rating
    - A.1.4-Dog name column has several wrong input ('a','the','this','an'), missing names are misrepresented and sometimes not properly extracted from tweet text
    - A.1.5-Multiple dog stage occurrences for a single tweet
    - A.1.6-Dog stage not properly extracted and missing values are misrepresented
  - A.2-Image predictions Dataframe:
    - A.2.1-Duplicated records, mainly related to retweets and replies
    - A.2.2-Image prediction results are somewhat misleading
    - A.2.3-Some breed names are incorrect and sometimes misleading
  - A.3-Breed Dataframe:
    - A.3.1-Breed column's naming convention is not unified
  - A.4-Breed Info Dataframe:
    - A.4.1-Breed column's naming convention is not unified
- B-Tidiness Issues
  - B.1-Twitter Archive Dataframe:
    - B.1.1-Tweet text column include both tweet text and links
    - B.1.2-One variable in four columns. I.e: 'doggo', 'floofer' are different representations of a single variable 'Dog Stage'
    - B.1.3-Total entries does not match that in Image predictions Dataframe
  - B.2-Image predictions Dataframe:
    - B.2.1-All breed information should be included in the Dataframe

### Conclusion

- Account management is successful in studying followers behavior and adjusting accordingly, this is evidenced through a rigorous content filtering process that drive higher user engagement

- Both content and context influence user engagement. Tweets composed of a good mixture of both are most likely to receive higher user engagement. If you are a dog owner seeking to celebritize your doggo then take this into consideration in your next photo session.

__*I really enjoyed this project from start to end, it was challenging but was very rewarding. I aim that readers of this analysis with limited knowledge of dog breeds become more enlightened after going through it and that breed CSV proves useful to someone analyzing breeds for some reason.*__

__*Hopefully you will enjoy reading through it.*__

<img src="https://pbs.twimg.com/media/C2tugXLXgAArJO4.jpg" width="1000">
This is the image that was first identified as Lakeland terrier at 19% confidence :)
