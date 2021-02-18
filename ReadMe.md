TOP 100 MOVIES OF ALL TIME – ROTTEN TOMATOES 


MAIN CONTENT
•	SUMMARY
•	PYTHON IMPORT MODULE
•	CODE EXPLANATION
•	OUTPUT


SUMMARY
This task consists of extracting data from a website, restructure the format, clean the HTML tags and convert it into a csv. file. This can be known as web scrapping.
The website to do web scrapping for this task is: https://www.rottentomatoes.com/top/bestofrt/
What I do is write down the code that search the contents from a table in a webpage, and storing that contents by appending in a csv file. It’s also removed the \n character while copying contents. It also searches for tr and td tags, that means searching an HTML document.


PYTHON IMPORT MODULE
1.	import requests
Requests module allows you to send HTTP requests using Python. The HTTP request returns a Response Object with all the response data (content, encoding, status, etc).
2.	import pandas as pd
Pandas presents a diverse range of utilities, ranging from parsing multiple file formats to converting an entire data table into a NumPy matrix array
3.	from bs4 import BeautifulSoup
Beautiful Soup is a Python library for pulling data out of HTML and XML files. It works with your favorite parser to provide idiomatic ways of navigating, searching, and modifying the parse tree.
 

CODE EXPLANATION
url = requests.get('https://www.rottentomatoes.com/top/bestofrt/')                      
- Grab the contents of the URL

soup = BeautifulSoup(url.text, 'lxml')                                                  
- Lxml allows for easy handling of XML and HTML files, and can also be used for web scraping

table = soup.find('table',{'class':'table'})                                            
- The soup.find extracts all the data that have a class attribute of table

new_columns = 4	                                                                        
- Declare a variable new_columns and set it to 4 to create 4 columns

new_rows = 100	                                                                        
- Declare a variable new_rows and set it to 4 to create 100 rows

new_table = pd.DataFrame(columns = range(0, new_columns), index = range(0, new_rows))	
- Creating a new dataframe with new_rows,new_columns as shape of dataframe

rows_data = 0	                                                                        
- Where the data will be place in rows

for row in table.find_all('tr'):	                                                    
- Searching for 'tr' gives rows present in that html code

columns_data = 0	                                                                    
- Where the data will be place in columns

columns = row.find_all('td')	                                                        
- Searching for 'td' in that specific 'tr' gives columns present

for column in columns:	                                                                
- Create a for loop

new_table.iat[rows_data,columns_data] = str(column.get_text().replace('\n',''))	        
- Take contents of that cell, remove \n from that text and put that in new_table dataframe

columns_data += 1	                                                                    
- Increasing columns_data for next entry

if len(columns) > 0:	                                                                
- If contents are still left

rows_data += 1	                                                                       
- Increase rows_data

new_table                                                                              
- Print the table containing the data

with open('Rotten Tomatoes Top 100 Movies of All Time.csv', 'a') as file:               
new_table.to_csv(file, header=['Rank', 'Rating', 'Title', 'No_of_Reviews'], index = False, line_terminator = '\n')
- Append new table to Rotten Tomatoes Top 100 Movies of All Time.csv with columns as 'Rank', 'Rating', 'Title', 'No_of_reviews'


OUTPUT
    0	1	2	                                        3
0	1.	96%	Black Panther (2018)	                    518
1	2.	98%	Parasite (Gisaengchung) (2019)	            457
2	3.	94%	Avengers: Endgame (2019)	                537
3	4.	97%	Knives Out (2019)	                        460
4	5.	93%	Us (2019)	                                542
...	...	...	...	... ... ... ... ... ... ... ... ... ... ...
95	96.	98%	Jaws (1975)	                                90
96	97.	98%	Up (2009)	                                298
97	98.	98%	The Bride of Frankenstein (1935)	        47
98	99.	98%	The Godfather, Part II (1974)	            85
99	100. 97% Won't You Be My Neighbor? (2018)	        252