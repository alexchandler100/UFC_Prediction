In this repository, we give all of the code necessary to scrape ufc fight data from ufcstats.com (this part is completely taken from https://github.com/swang2016/ufc_scraper so thank you to swang2016), and build a machine learning model to predict both the winner and the method (e.g. KO/TKO, SUB, U-DEC, S-DEC, etc...) of victory for any theoretical fight between any two UFC fighters. The code eventually builds a function called ufc_predict (in the file UFC_Best_ML_Model.ipynb), which takes 4 inputs (fighter1, fighter2, day1, day2). The fighter1 and fighter2 inputs are the fighters names as strings (no letter accents allowed). The last two inputs are dates, day1 being the date at which fighter1 is being considered, and day2 being the date at which fighter 2 is being considered. 
For example, we could evaluate the outcome of Petr Yan fighting Jose Aldo on July 12, 2020. The result is unsurprising.

input: ufc_predict('Petr Yan', 'Jose Aldo', 'July 12, 2020', 'July 12, 2020')

output: Petr Yan by KO/TKO

Alternatively, we could imagine what would happen if the July 12, 2020 version of Petr Yan were to fight the prime July 12, 2014 version of Jose Aldo. The result is as follows.

input: ufc_predict('Petr Yan', 'Jose Aldo', 'July 12, 2020', 'July 12, 2014')

output: Jose Aldo by U-DEC

take that Petr ;)

If you have absolutely no experience in python or using Jupyter notebooks, read this paragraph. To get started, open up your terminal (if you don't know what this is, google it) and install ipython, that is, type 'pip install ipython' and press enter. Now navigate to the directory UFC_Prediction-master by typing 'cd' followed by the path to wherever you've downloaded and unzipped this repository. For example I have the folder UFC_Prediction-master on my desktop, so I type 'cd Desktop/UFC_Prediction-master' and press enter. Now type 'jupyter notebook' and press enter. This opens a tab in your browser with a jupyter logo at the top. You will automatically be on the 'files' tab, and should see a folder 'Scripts' and the README file (this one :). Open the Scripts folder. The files ending in .ipynb can be opened as notebooks, where you can run the code provided in this repository (read on to see which ones you should run, depending on your goals). Jupyter notebooks consist of 'cells', each cell containing some number of lines of code. To evaluate a cell, click on the interior of the cell with your cursor, and press shift+enter (or shift+return on mac).

The following paragraph is only relevant to those who would like to build and update the dataset themselves (with help). If you just want to use the prediction model, skip the following paragraph.

If you would like to build the dataset yourself, you can first run the UFC_data_scraping.ipynb notebook, obtaining the files fight_hist.csv and fighter_stats.csv. Then you can go to the notebook Building_ufc_fights.ipynb to use these csv files to build the files ufc_fights_crap.csv and ufc_fights.csv (a cleaner version of ufc_fights_crap.csv but we end up needing both). To update the dataset, you must first update fight_hist.csv and fighter_stats.csv in the UFC_data_scraping.ipynb notebook, and then run the Updating_ufc_fights.ipynb notebook. The result of all of this is a fully updated version of the file ufc_fights.csv. This is the file we use to build a machine learning based prediction model in the file UFC_ML_Model_Final.ipynb. Honestly I don't know why anybody would want to build the dataset again from scratch, but one thing that would make sense is to update the files ufc_fights.csv and ufc_fights_crap.csv which are provided here since I am not sure if I will keep them updated in this repository. This can be done by first running the UFC_data_scraping.ipynb notebook and then running Updating_ufc_fights.ipynb.

To run predictions using the dataset ufc_fights.csv already included in this repository, open the notebook UFC_ML_Model_Final.ipynb. Run every cell in the notebook, the last cell being an example of how to input a prediction. Note that some fighters names naturally have accents, but for convenience we never include accents in a string. So for example, Patrick Côté would be represented as 'Patrick Cote'. Dates must be input in the form '%B %d, %y' so for example 'August 8, 2009'. 

According to my calculations using cross_val_score, predicting the winner is 71.2% accurate and predicting the method is 50% accurate, meaning 35.6% (more than a third of the time) of the time we predict both the winner and the method correctly. 

I would advise against using this predictor for any kind of betting. There certainly exist ways to improve the accuracy, and my guess is that ufc odds makers are better at forming such a model than I am.
