## Data 512A Au 20: Human-Centered Data Science Assignment 2 - Bias in Data

## Objective:

The goal of this assignment is to identify potential sources of bias (if any) that may exist in a corpus of human-annotated datasets, and to describe the implications of how these biases might impact the behavior of machine learning models trained on the data or used for research purposes or to power data-driven applications. Additionally, demonstrate that we are able to perform a self-directed exploratory data analysis and think critically about the implications of our findings on how the data is collected and processed and how reliabile our findings are based on that data. To successfully complete this assignment we will need to follow the below steps:

- Identify potential sources of bias in at least two of the three datasets.
- Describe implications of how the dataset bias could lead to potential unintended negative consequences of using machine learning models trained on these datasets in scientific research and/or data-driven software applications.
- Suggest how these sources of bias could be corrected or otherwise accounted for in order to avoid these unintended consequences.
- Demonstrate the ability to use literate programming capabilities of Jupyter Notebooks in order to document the analysis (in programming cells, tables, and graphs) and insights, questions, and explanations (in markdown cells) within the same document.


## Dataset Details:

The corpus used in this assignment is called the Wikipedia Talk corpus which consists of three datasets. Each dataset contains thousands of online discussion posts made by Wikipedia editors who were discussing how to write and edit Wikipedia articles. Crowdworkers labelled these posts for three kinds of hostile speech: “toxicity”, “aggression”, and “personal attacks”. Many posts in each dataset were labelled by multiple crowdworkers for each type of hostile speech, to improve accuracy. 

Each of these 3 datasets contain 3 `.tsv` files per dataset for which the link is provided below -

 - Toxicity : [https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973)
 - Aggression : [https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Aggression/4267550](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Aggression/4267550)
- Personal Attack : [https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Personal_Attacks/4054689](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Personal_Attacks/4054689)


## Dataset Description: 

Detailed schema for each of these dataset can be found [here](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release).


## Input Files used:

For this analysis I have used 2 out of the 3 datasets which can be found in the [Input Data Files](https://github.com/sandhyatharanian/data-512/tree/main/data-512-a2/Input%20Data%20Files) folder. These files are `.zip` files with toxcity split as `Toxicity_1.zip` and `Toxicity_2.zip` due to GIT's size constraint.

Dataset Used for this analysis are listed below. Please note that I have used all the 3 files for each of the 2 datasets.

1. Toxicity
   - toxicity_annotated_comments.tsv
   - toxicity_annotations.tsv
   - toxicity_worker_demographics.tsv
2. Personal Attack
   - attack_annotated_comments.tsv
   - attack_annotations.tsv
   - attack_worker_demographics.tsv
   
   
**Note-** 

 - Download the `.zip` files, extract them and upload them to the jupyter environment before proceeding to use the `.py` notebook.
 - As the `Toxicity` dataset is split into 2 files, please make sure to combine them in case using the dataset from `.zip` files. In order to skip this step, the user can directly download the datasets from [here](https://figshare.com/projects/Wikipedia_Talk/16731).
 - Duplicate columns created during the join was dropped inorder to have a clean dataset.
 - The dataset was checked for blank/null values. 
 
 
**Analysis 1 -** Uses the toxicity dataset with all three `.tsv` files comibined. Given below is the description of the columns along with the user generated calculated field available in the final dataset used for this analysis. 


| Column | Dataset | Value |
| ------ | ----- | ----- |
| rev_id | toxicity_annotations.tsv | MediaWiki revision id of the edit that added the comment to a talk page |
| worker_id | toxicity_annotations.tsv | Anonymized crowd-worker id |
| toxicity | toxicity_annotations.tsv | Indicator variable for whether the worker thought the comment is toxic (1) or non-toxic (0) |
| toxicity_score | toxicity_annotations.tsv | Categorical variable ranging from very toxic (-2), to neutral (0), to very healthy (2) |
| comment | toxicity_annotated_comments.tsv | Comment text |
| year | toxicity_annotated_comments.tsv | The year the comment was posted in |
| logged_in | toxicity_annotated_comments.tsv | Indicator for whether the user who made the comment was logged in. Takes on values in {0, 1} |
| ns | toxicity_annotated_comments.tsv |  Namespace of the discussion page the comment was made in. Takes on values in {user, article} |
| sample | toxicity_annotated_comments.tsv | Indicates whether the comment came via random sampling or blocked {random, blocked} |
| split | toxicity_annotated_comments.tsv | Describes if the comments where split into train, dev and test sets for the model. Takes on values in {train, dev, test} |
| gender | toxicity_worker_demographics.tsv | The gender of the crowd-worker. Takes a value in {'male', 'female', and 'other'} |
| english_first_language | toxicity_worker_demographics.tsv | Does the crowd-worker describe English as their first language. Takes a value in {0, 1} |
| age_group | toxicity_worker_demographics.tsv | The age group of the crowd-worker. Takes on values in {'Under 18', '18-30', '30-45', '45-60', 'Over 60'} |
| education | toxicity_worker_demographics.tsv | The highest education level obtained by the crowd-worker |
| comment_length | User devrived | character count of the comments |
| total_words | User devrived | word count of the comments |
| binned_wordcount | User devrived | user generated bins to group the word count of the comments |



**Analysis 2 -** Uses the personal attack and toxicity dataset with all six `.tsv` files comibined. Given below is the description of the columns along with the user generated calculated field available in the final dataset used for this analysis. 
 

| Column | Dataset | Value |
| ------ | ----- | ----- |
| rev_id | attack_annotations.tsv | MediaWiki revision id of the edit that added the comment to a talk page |
| worker_id | attack_annotations.tsv | Anonymized crowd-worker id |
| quoting_attack | attack_annotations.tsv | Indicator for whether the worker thought the comment is quoting or reporting a personal attack that originated in a different comment |
| recipient_attack | attack_annotations.tsv | Indicator for whether the worker thought the comment contains a personal attack directed at the recipient of the comment |
| third_party_attack | attack_annotations.tsv | Indicator for whether the worker thought the comment contains a personal attack directed at a third party |
| other_attack | attack_annotations.tsv | Indicator for whether the worker thought the comment contains a personal attack but is not quoting attack, a recipient attack or third party attack |
| attack | attack_annotations.tsv | Indicator for whether the worker thought the comment contains any form of personal attack |
| comment | attack_annotated_comments.tsv | Comment text |
| year | attack_annotated_comments.tsv | The year the comment was posted in |
| logged_in | attack_annotated_comments.tsv | Indicator for whether the user who made the comment was logged in. Takes on values in {0, 1} |
| ns | attack_annotated_comments.tsv |  Namespace of the discussion page the comment was made in. Takes on values in {user, article} |
| sample | attack_annotated_comments.tsv | Indicates whether the comment came via random sampling or blocked {random, blocked} |
| split | attack_annotated_comments.tsv | Describes if the comments where split into train, dev and test sets for the model. Takes on values in {train, dev, test} |
| gender | attack_worker_demographics.tsv | The gender of the crowd-worker. Takes a value in {'male', 'female', and 'other'} |
| english_first_language | attack_worker_demographics.tsv | Does the crowd-worker describe English as their first language. Takes a value in {0, 1} |
| age_group | attack_worker_demographics.tsv | The age group of the crowd-worker. Takes on values in {'Under 18', '18-30', '30-45', '45-60', 'Over 60'} |
| education | attack_worker_demographics.tsv | The highest education level obtained by the crowd-worker |
| toxicity | toxicity_annotations.tsv | Indicator variable for whether the worker thought the comment is toxic (1) or non-toxic (0) |
| toxicity_score | toxicity_annotations.tsv | Categorical variable ranging from very toxic (-2), to neutral (0), to very healthy (2) |

Code is available in - **[Bias in data.ipynb]**(https://github.com/sandhyatharanian/data-512/tree/main/data-512-a2/Input%20Data%20Files) file. 

## Python packages used

- pandas version 1.0.3
- numpy  version 1.18.1
- seaborn  version 0.10.0
- matplotlib version 3.1.3
- tabulate version 0.8.7

Note - Packages used along with its version can be found using **pip list** command.

## Required resources

- Overview of the research project that : [https://meta.wikimedia.org/wiki/Research:Detox](https://meta.wikimedia.org/wiki/Research:Detox)
- Dataset description and schemas: [https://meta.wikimedia.org/wiki/Research:Detox/Data_Release](https://meta.wikimedia.org/wiki/Research:Detox/Data_Release)
- Overview of Google’s Conversation AI project: [https://conversationai.github.io/](https://conversationai.github.io/)


## Additional resources:

- Fancy landing page for Perspective API: [https://www.perspectiveapi.com/#/](https://www.perspectiveapi.com/#/)
- Research paper that describes the corpus: [https://arxiv.org/abs/1610.08914](https://arxiv.org/abs/1610.08914)
- Sample notebook for exploratory analysis: [https://github.com/ewulczyn/wiki-detox/blob/master/src/figshare/Wikipedia%20Talk%20Data%20-%20Getting%20Started.ipynb](https://github.com/ewulczyn/wiki-detox/blob/master/src/figshare/Wikipedia%20Talk%20Data%20-%20Getting%20Started.ipynb)
- Perspective API docs on GitHub: [https://github.com/conversationai/perspectiveapi/blob/master/2-api/methods.md](https://github.com/conversationai/perspectiveapi/blob/master/2-api/methods.md)
- Wired article about Perspective API: [https://www.wired.com/2017/08/internet-troll-map/](https://www.wired.com/2017/08/internet-troll-map/) 
- Engadget article about Perspective API: [https://www.engadget.com/2017-09-01-google-perspective-comment-ranking-system.html](https://www.engadget.com/2017-09-01-google-perspective-comment-ranking-system.html)


## License Information:

License and copy right information for all of the 3 datasets can be found [here](https://creativecommons.org/publicdomain/zero/1.0/).


## Citation

The dataset can be cited as:
     Wulczyn, Ellery; Thain, Nithum; Dixon, Lucas (2016): Wikipedia Detox. Figshare[https://figshare.com/projects/Wikipedia_Talk/16731]
