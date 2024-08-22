   

Introduction to Python 3

Two ways to execute Python Scripts

1. running the code from a .py file  
    - Handy for developing an actual script  
    - Process is create a txt document and put in the code and save it as a .py file  
    ![3671c8e91aa0b769f0c5947da9a79e7a.png](9422f35bf225432fa00acaf1ab4adafa.png)
2. Running it directly inside the Python IDLE  
    - Useful to quickly test something small  
    - ![18da55f56511fe781198d72f94f1d466.png](a96e7eee17cc4b7f996fd65fc67a5e98.png)  
    - To exit type exit(0)
3. Running the code via a shebang (#!/usr/bin/env python3)  
    - Put the shebang in the first line in a Python script  
    ![c91390af18188aa9f040493785661fc9.png](8aed0b81c1b544408ec22b01140782fa.png)  
    - Give the .py file execution privilege to execute

While-Loop  
![ec2a9f9832fed9f294ddf7be5071e901.png](a090e70092b84cf39c60c61ba129927f.png)

For-Loop  
![fafe25af48515495b1f6c18513fcccfd.png](4040e7591f384174a514b4c798b88949.png)

Function  
![88fc20934fd9476f91337a48ab69a79b.png](fc5a4a9bca2e4a7087c26f206b47f272.png)

- Within def you define the function and everything within that function can be called upon when you call it
- print(sample_text) // is a placeholder. Once you call the function you will replace the "sample_text" with the parameters

Classes  
![f2b7ae5403db18b470ab4feb399b3199.png](2de22d2208614655957141ab45a25def.png)  
![d590aacc8507a3a9f138876b0cb39fa8.png](adda79eaf1b047fdbb8891197d85c49b.png)

- class keyword uses the CapWord naming convention. ex. CapWordsArePrettyCool
- The variables within can change if needed and are called Attributes within classes
- In this particular case the **init** function is allowing flexibility in changing the topping and garnish by locally redefining the attributes to no toppings/garnish
- We can do this with all attributes listed however all cakes have set ingredients and only the toppings and garnish change hence why they are redefine as a function to allow modular changes with each cake  
    ![fb38b54bedcd6f30135ae36de37846ac.png](53090a803d8a4f819daf6f714efdb903.png)
- In the above example we redefine the toppings and garnish since they are named parameters  
    ![95db1a44bf48644979a9676d671f1e23.png](dc88de7bf99c495583bfada88370b3d3.png)

Magic Methods  
**str**  
**enter**  
**exit**

Uses  
![6d2c7e3f51f2f1b9eab4f80eba31a6d4.png](f125177c49bf43faa9bef78b3c5e1a3f.png)

- allows for the execution of opening and closing of code
- the with keyword allows for the code to be initiated around the function
- the with Foo() as foo allow the same, but in addition stores the information within the variable foo

Introduction to Libraries:  
![fd86e1921d68d26508f3230b7f2cba77.png](502ff001ae9d4b538b2c59ebfadce5bf.png)

PIP Commands  
install (package) // installs the package directly  
--upgrade // flag to upgrade the installation to the latest version  
uninstall  
freeze // print a list of all installled packages and their dependencies  
![294d7d27f2f1a0fce79e98b257464a99.png](6d5a68dc3dbc45198e4f4f9fda71df70.png)  
![76b70eeee21d944e2e64a2cd20ce67c6.png](51ad7ffadb4a4a53b9ed6d7c73ebc111.png)  
![ec278407ec6c8023c0a6d7b1cfc6743e.png](d14a3af5d371421ea49171cde7f5093c.png)

import requests # Importing the requests module for making HTTP request  
import re # Importing the re module for regular expressions  
from bs4 import BeautifulSoup #Importing BeautifulSoup for parsing HTTP requests

**#Url of the web page to fetch HTML content from. Replace with our target url**  
PAGE_URL = '[http://target](http://target "http://target"):port'

**#Function to fetch HTML content from a url**  
def get_html_of(url):  
resp = requests.get(url) **#Sends an HTTP GET request to the URL**

**#Checks if the response status code is not 200 (OK)**  
if resp.status_code != 200:

**#prints an error message and exit the program**  
print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')  
exit(1)

**#Returns the decoded HTML content of the response**  
return resp.content.decode()

**#Get the HTML content of the webpage**  
html = get_html_of(PAGE_URL)

**#Create a beautifulSoup object from the HTML content**  
soup = BeautifulSoup(html, 'html.parser')

**#Extract the text content from the BeautifulSoup object**  
raw_text = soup.get_text()

**#Tokenize the text into words using a regular expression**  
all_words = re.findall(r'\w+', raw_text)  
![7b6e3e0f0104e96bbfc47a766ea4ca83.png](d3c1293b53f24c74a5be61893f6beaf3.png)

**#Previous code omitted**

**#Initialize an empty dictionary to store word counts**  
word_count = {}

**#Loop through each word in the list of all words**  
for word in all_words:

**#If the word is not already in the word_count dictionary, add it with a count of 1**  
if word not in word_count:  
word_count[word] = 1  
else:

**#If the word is already in the dictionary, retrieve its current count**  
current_count = word_count.get(word)

**#Increment the count by 1 and update the dictionary with the new count**  
word_count[word] = current_count + 1