# Web Scraping task: Anakin Tech

This repository contains a solution to the task provided by Anakin.



## Installation

You can clone this repo by running
```bash
git clone https://github.com/felirox/web-scraping-anakin
```

The program was written using Python3. The code is available in a Python Notebook (.ipynb) file. 

No additional application is necessary if you have Jupyter installed.
(VPN might be required to run the scraping at certain locations)


To download Anaconda/Jupyter, [click here](https://www.anaconda.com/)

## Requirements

To install the requirements, open your terminal and head over to the directory where this cloned code is present. 

Run the following command to install all the necessary libraries:

```bash
pip install -r requirements.txt
```
## Thought Process and General Approach

- Connecting to the website - Since this company is based in Singapore, it was necessary to use a VPN as mentioned. However, in certain instances, this was not necessary. 
### Task 1
- Once the website loaded, I laid out a rough sketch of the flow I would need to follow. This helped me in developing the task flow on selenium.
- Once the base URL was loaded, it was necessary to enter the search term, this was possible by automating the submission of the search query using its class name and the search button was initiated to be clicked once the query as entered
- Since there were plenty of "Load More" and the number of tries required to completely load the page would vary based on the location - this is because the number of restaurants would differ based on the location it is searched for.
- For this reason, a dynamic approach is taken and the search continues to occur until the specific class cannot be found at all. Once the exception for not finding the same is raised, the program is let to continue for the rest of the program.
- Once the page loads completely, the Name of the Restaurant and its URL are recorded. We are noting these as they are key parameters. In the code, you can see that the URL and Name are narrowed down by exacting the class attributes
- The location parameters of every restaurant are in its URL. Given that the assignment prevents us from using any third-party applications and usage of explicit selenium traversal, we can use the approach to get the raw HTML response and work on it.
- Each URL is looped and a GET request is sent to fetch the data of that URL. This does NOT involve the usage of selenium and get requests are comparatively faster and less intrusive
- We send some header parameters along with the request to prevent ending up with a 403 request
- A tricky code to then get the body parameters is carefully written. This code extracts the inner value of the __NEXT_DATA__ class and then it is parsed as a JSON object. 
- The JSON dump is taken and then again traversed to find the path to the place where the Location is present.
- The output is then appended to a Pandas data frame and the program is terminated once the CSV is extracted.

### Task 2
- Task two requires us to get the location fields of all the restaurants in Singapore. Given the fact that no information about the restaurants is provided manually, we will have to go based on the menu choices on the main page. 
- The main page has a section under promotions named - "There's something for everyone!"
- This section contains a range of food varieties. On further exploring these pages, we can view the restaurants that are serving that specific cuisine. 
- In other words, if we scrape through all these URLs by tweaking the program written for Task 1, we can get the data for all restaurants in Singapore!

## Limitations

- Task 2 takes a lot of time to run. At the time of writing this readme, the program has run for more than an hour. This is because of the time delay implemented. This delay is very necessary as repeated requests with no time delay on my local network will block my IP for a certain cooldown time. 
- The code relies on the structure of the JSON and HTML classes. If any of those names were to be changed, the code will fail.
- The code relies on a safely caught exception to understand when the "Load More" option isn't present
- Unstable VPN and frequent running will lead to a 402 or 403 error

## References
- JSON Documentation for Python
- Selenium Documentation for Python
- Requests Documentation for Python
- https://pypi.org/ for all the pip-based downloads
- https://www.makeareadme.com/ to make this readme
- https://jsonpathfinder.com/ to find the JSON path amidst the mountain of parsed data
- https://stackoverflow.com/ for the countless doubts and silly errors that popped up

## License
None