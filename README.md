# Job Recommender
It is a Case-Based Approach to Job Recommendation. This application is intended to assist you on your job search by tracking your occupational interests as you bookmark and apply for jobs.

### Contribution
Mohammed Alharbi, Jonathan Velez, Yuhan Wang, Xin Zhao

### Screenshots
![Click Here](Screenshots#README)

## Introduction
Adaptive recommender systems are becoming more common-place across various domains, and they have been especially significant in e-commerce domains where a user’s preferences and feedback can be used to personalize sales support and product suggestions. Personalized recommendations are an excellent way to improve user experience regardless of the domain, but the implementation must be appropriate within the interaction context. Adaptive recommender systems essentially provide users a more intelligent approach to navigating and searching complex information spaces by reducing the search space to items that are related to the user’s profile and making the user aware of those items most likely to fit their interests (Smyth, 2007). 
The implementation of personalized recommender technologies has expanded over the last decade, and its application has become significant in industry where the technology can satisfy the needs of users in a target market. Personalized recommender systems have recently become of interest to companies providing services to job-seekers (Appan, 2016), such as Indeed, LinkedIn and CareerBuilder. Herein we analyze the significance of adaptive recommender systems within this domain while providing an example of the application of case-based recommendation as an appropriate solution to personalized job recommendation.  
Collaborative filtering and content-based techniques are two fundamental approaches to implementing adaptive recommendation. Collaborative filtering is dependent on the availability of user ratings information where this information can be used to identify similar users and offer suggestions based on item ratings rather than information about the items themselves. In opposition, case-based techniques depend on item descriptions to recommend items similar to those in which a target user has previous demonstrated interested. 
The case-based approach is a special application of the content-based technique that leverages the availability of structured information and a defined set of features. This is complemented by the availability of domain expertise and similarity knowledge about these features that allow the system to make judgements about the similarity between items based on each item’s individual features (Smyth, 2007). The domain of job recommendation is appropriately suited to the application of the case-based approach because of the structured content of each job item. Each instance of a job item can be considered as a case with a feature set that can include: job domain, job title, position, knowledge, experience, location, salary and educational qualification (Koh & Chew, 2015). The following sections provide an overview of our system, including our solution for the case-base, constructing the user-profile and resolving cold-start, as well as our solution for similarity assessment.  
## System Overview
Case-based recommender systems are established from the core concepts of case-based reasoning regarding similarity and retrieval. Items are represented as cases and the user-profile is represented as a set of cases that are of interest to a target user. Recommendations are then generated by retrieving cases that are most similar to a user’s query or profile (Smyth, 2007). Our system provides two main functionalities, recommendations of recently posted jobs based on the user profile and the re-ranking of job query results. Each instance of a job item is considered a case, and we use the following set of features to compare the similarity between cases: job domain, job title, location, job description, educational qualification, and employment type. Job items are accessed directly from CareerBuilder by delivering queries through their system’s API. 
The CareerBuilder API lets us retrieve 100 job items per request that we constrain according to a 100 mile radius of the user’s preferred location (the search radius can be updated by the user). Each request either queries for the most recent jobs within the location radius or queries the location radius for jobs that match user-submitted keywords. The set of job items are retrieved in JSON format and processed server-side using PHP. The server-side processing rates results according to their similarity to the user’s profile and re-ranks them. Each case is then delivered client-side where it is presented to the user. For each case, the user is presented with a percentage score of how relevant it is compared to the cases in their user profile, as well as a breakdown that displays a percentage score of the relevance of each case feature.

## Similarity Assessment
For each candidate job case in the return list, we present the user with a percentage score representing the relevance of that job according to their user profile. Additionally, we present the user with a breakdown displaying how each case feature actually influenced the overall relevance rating. Job domain is assigned a weight of 5, location is assigned a weight of 4, job title is assigned a weight of 3, qualification level is assigned a weight of 2, and employment type is assigned a weight of 1. Additionally, the user is presented with a toggle menu where they can prioritize a feature in order to shift its weight and re-rank the results (e.g., if the user prioritizes employment type then its weight will become 5 and the weights of all other features will shift downward). We decided upon the initial ranking of features and their weighting factors based on expert suggestions (Koh & Chew, 2015).

## Requirements
A CareerBuilder developer key is required to run this project. I do not share mine here because it is private. You can insert your developer key in "model/job-query.php".

