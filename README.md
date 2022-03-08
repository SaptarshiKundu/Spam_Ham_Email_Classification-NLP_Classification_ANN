# Spam Email Classifier

## Project Goal
This is an overview of the project, more in-depth details including code and the final report can be found in this repo. To use traditional machine learning algorithms to correctly identify Spam or Ham emails based on both Subject and Messages of emails. A basic artificial neural network (ANN) was also built to compare to traditional ML algorithms.
## Dataset
The dataset is: [Enron Spam dataset](http://nlp.cs.aueb.gr/software_and_datasets/Enron-Spam/index.html). This processed dataset can be found as enron_spam_ham_email_processed_v2.csv in the repository. This is a real-life dataset consistent of both sent and received emails. It was put together by former employees of Enron, who went through and labelled their work emails as “Ham” or “Spam.” The dataset contains 33665 emails in total.
## Approach
1)	Label Encoding
    - The first step was to label encode the ‘Spam/Ham’ column with ‘Spam’ values mapped to 0 and ‘Ham’ mapped to 1, followed by renaming the column to ‘label’.
2)	Cleaning
    - In the cleaning step, we encountered three distinct cases: first, only the ‘Subject’ field was empty; second, only the ‘Message’ field was empty; and third where both ‘Subject’ and ‘Message’ was empty.
    - The following table summarizes the actions we took against each scenario.

| Subject | Message | Action | #Rows (% of Dataset) |
| :--- | :--- | :--- | :--- |
| EMPTY | EMPTY | DROPPED | 51 (0.15%) |
| EMPTY | DATA AVAILABLE | REPLACED EMPTY SUBJECT WITH “(NO_SUBJECT)” | 238 (0.7%) |
| DATA AVAILABLE | EMPTY | REPLACED EMPTY MESSAGE WITH “(NO_MESSAGE_TEXT)” | 320 (0.95%) |

3) RegEx Expressions – Applied independently on ‘Subject’ and ‘Message’ columns
    - To reduce the complexity and mismatching of regex expressions employed in the following steps, all texts were lowercased.
    - Then we matched and removed all characters except for alphabets (a-z) and full stop (.). This was done to get rid of special characters that we otherwise presumed might interfere during tokenization.
    - This step was followed by removal of extra white spaces and multiple occurrences of full stop (.).
4) Dropping Sentences – Applied independently on ‘Subject’ and ‘Message’ columns
    - The first task was to sentence tokenize each text.
    - Any sentence that contained less than 2 words were dropped and the remaining sentences were joined and replaced the original text.
    - However, if dropping such sentences resulted in an empty text, then original text was retained as such.
5) Lemmatization – Applied independently on ‘Subject’ and ‘Message’ columns
    - Primarily, each text was sentence tokenized.
    -	Then, we realized that lemmatizer output accuracy is improved when, along with the word, its pos-tag is also passed as an additional parameter.
    -	Hence, each sentence was then word tokenized and in turn each word was pos-tagged (part-of-speech).
## Conclusion
All traditional machine learning models were run with 100% of the data using a 66/33 train-test split. After tuning, SVM was the best model for ‘Subject’ while the artificial neural network was the best for ‘Messages’ scoring 93.8% and 98.3% respectively. Due to RAM limitations, the neural network (NN) model was run at 60% of the total data with the same 66/33 train-test split being applied on that 60% of the total dataset. For this reason, after finding that SVM was the best traditional machine learning model it was run again with 60% of the data for true comparison purposes.
