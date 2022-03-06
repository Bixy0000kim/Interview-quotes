# Interview-quotes

## Procedure: 
```
•	Import selenium, Beautiful soup and Pandas packages using import
•	Now, automate a blank browser using browser = webdriver.Edge()
•	Initiate the required URL that we need to scrape using browser.get(“https://devtomanager.com/interviews”)
•	Since it is a static webpage we can get the html code of the webpage using html requests like requests.get(url).text but I’m using browser.page_source because its more functional.
•	Get the html code of the page using soup = BeautifulSoup(browser.page_source, 'html.parser')
•	Go to the required webpage  right click and select inspect and hover the mouse and select the required data to scrape to locate the division and class for that particular data.
•	Now, as we can see all the required data we need like Employee Name, Job role and company are all having same division and class div: ‘h5’ class: ‘card-title’. So, we need to use split() and indexing in order to get desired text
•	Scrape and iterate employee name using: [i.text.strip().split(', ')[0] for i in soup.find_all('h5', class_ = 'card-title')]
•	We need to use two split() functions in order to scrape and iterate Job role: [i.text.strip().split(', ')[1].split('at')[0] for i in soup.find_all('h5', class_ = 'card-title')]
•	Repeat the same for company name.
•	Interview quotes and date are in even and odd numbered lines. So, we need to use the concept of slice and skip
•	Scrape and iterate quotes using: [i.text.strip() for i in soup.find_all('p', class_ = 'card-text')[::2]]
•	Repeat the same for Date.
•	In order to get the tags, we need to use for loop and appended the data to the list comprehension in order to get tags.
•	Define a function to combine all the scrapped data and store it in a dataframe using pd.DataFrame
•	Now, we got the first page. To get the remaining pages we need to format the URL using {}: 'https://devtomanager.com/interviews/page/{}/'
•	Using for loop and range() iterate for all pages and append the data to the above function.
•	Now, lastly import the dataframe to a csv file using .to_csv(‘file name’)
```

## Challenges Faced:
```
	Got only 4 values for the company instead of 5 values. The first value on website is actually a null. So, I used (len(i.text.strip().split('at '))>1 and (i.text.strip().split('at '))[1] or 'null') in order to get the null value where ever there is a null.
	Interview quotes and date are in even and odd numbered lines. So, I used the concept of slice and skip
	Quotes: [i.text.strip() for i in soup.find_all('p', class_ = 'card-text')[::2]]
	Dates: [i.text.strip().split('\n ')[0] for i in soup.find_all('p', class_ = 'card-text')[1::2]]
	Getting tags and iterating them were a bit difficult, after iterating I had empty lists inside the list. So, to get rid of empty list I used : [x for x in data if x!= []]
```
