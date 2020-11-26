# learning-web-scraping
Learning Web Scraping with FreeCodeCamp.org

Reference:https://www.youtube.com/watch?v=XVv6mJpFOb0&t=1949s 

### How to Install BeautifulSoup4
Type in Command Prompt

    pip install beautifulsoup4
    
### Installing lxml

    pip install lxml
    
    
### Importing BeautifulSoup into .py file
    from bs4 import BeautifulSoup

### Final Code
    from bs4 import BeautifulSoup
    import requests

    # Web Scraping Real Website
    print('Put some skill that your are not familiar with')
    unfamiliar_skill = input('>')
    print(f'Filtering out {unfamiliar_skill}')
    html_text = requests.get('https://www.timesjobs.com/candidate/job-search.html?searchType=personalizedSearch&from=submit&txtKeywords=python&txtLocation=').text
    #print(html_text)
    soup = BeautifulSoup(html_text, 'lxml')
    jobs = soup.find_all('li', class_ = 'clearfix job-bx wht-shd-bx')
    for job in jobs:
        published_date = job.find('span', class_ = 'sim-posted').span.text
        if 'few' in published_date:
            company_name = job.find('h3', class_ = 'joblist-comp-name').text.replace(' ', '')
            skills = job.find('span', class_ = 'srp-skills').text.replace(' ','')
            more_info = job.header.h2.a['href']
            if unfamiliar_skill not in skills:
                print(f"More Info: {more_info}")
                print(f"Company Name: {company_name.strip()}")
                print(f"Required Skills: {skills.strip()}")

                print('')


### How to scrape for every ten minutes
    if __name == '__main__':
        while True: 
            find_jobs()
            time_wait = 10
            print(f'Waiting {time_wait} seconds...')
            time.sleep(time_wait * 60)

### How to run the program in cmd
1. Go to Command Prompt
2. Search the file path
Then write: python web_scrap.py
python + your file name.py

Example:

![](images/web_scrap_tutor.png)

### How to store the output in separated file format
    if unfamiliar_skill not in skills:
            with open(f'posts/{index}.txt', 'w') as f:
                f.write(f"More Info: {more_info}")
                f.write(f"Company Name: {company_name.strip()}")
                f.write(f"Required Skills: {skills.strip()}")
