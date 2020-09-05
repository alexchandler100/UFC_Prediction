In this repository, we give all of the code necessary to scrape ufc fights data from ufcstats.com (this part is completely taken from https://github.com/swang2016/ufc_scraper so thank you to swang2016), and build a machine learning model to predict both the winner and the method (e.g. KO/TKO, SUB, U-DEC, S-DEC, etc...) of victory for any theoretical fight between any two UFC fighters. The code eventually builds a function called ufc_predict (in the file UFC_Best_ML_Model.ipynb), which takes 4 inputs (fighter1, fighter2, day1, day2). The fighter1 and fighter2 inputs are the fighters names as strings (no letter accents allowed). The last two inputs are dates, day1 being the date at which fighter1 is being considered, and day2 being the date at which fighter 2 is being considered. 
For example, we could evaluate the outcome of Petr Yan fighting Jose Aldo on July 12, 2020. The result is unsurprising.

input: ufc_predict('Petr Yan', 'Jose Aldo', 'July 12, 2020', 'July 12, 2020')
output: Petr Yan by KO/TKO

Alternatively, we could imagine what would happen if the July 12, 2020 version of Petr Yan were to fight the prime July 12, 2014 version of Jose Aldo. The result is as follows.

input: ufc_predict('Petr Yan', 'Jose Aldo', 'July 12, 2020', 'July 12, 2014')
output: Jose Aldo by U-DEC

take that Petr ;)

The following paragraph is only relevant to those who would like to build and update the dataset themselves (with help). If you just want to use the prediction model, skip the following paragraph.

If you would like to build the dataset yourself, you can first run the UFC_data_scraping.ipynb notebook, obtaining the files fight_hist.csv and fighter_stats.csv. Then you can go to the notebook Building_ufc_fights.ipynb to use these csv files to build the files ufc_fights_crap.csv and ufc_fights.csv (a cleaner version of ufc_fights_crap.csv but we end up needing both). To update the dataset, you must first update fight_hist.csv and fighter_stats.csv in the UFC_data_scraping.ipynb notebook, and then run the Updating_ufc_fights.ipynb notebook. The result of all of this is a fully updated version of the file ufc_fights.csv. This is the file we use to build a machine learning based prediction model in the file UFC_ML_Model_Final.ipynb.

To run predictions using the dataset ufc_fights.csv already included in this repository, open the notebook UFC_ML_Model_Final.ipynb. Run every cell in the notebook, the last cell being an example of how to input a prediction. Note that some fighters names naturally have accents, but for convenience we never include accents in a string. So for example, Patrick Côté would just be represented as 'Patrick Cote'. Dates must be input in the form ('%B %d, %y') so for example 'August 8, 2009'. 

According to my calculations using cross_val_score, predicting the winner is 71.5% accurate and predicting the method is 40% accurate, meaning 28.6% of the time we predict both the winner and the method correctly. 

I would advise against using this predictor for any kind of betting. There certainly exist ways to improve the accuracy, and my guess is that ufc odds makers are better at forming such a model than I am.
