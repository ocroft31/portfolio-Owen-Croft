---
layout: page
title: Data collection from TransferMarkt
description: Python code for a web scraper of TransferMarkt.com using BS4 and Requests 
img: assets\img\football.jpg
importance: 3
category: Academic
giscus_comments: false
---

<div class="row justify-content-center">
    <div class="col-13 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\data_collection_transfermarkt\football_cropped.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div style="border: 1px solid #ddd; border-radius: 6px; padding: 16px; margin: 16px 0; background-color: #f8f9fa;">
    <p style="font-size: 110%; text-align: center;"><strong><u>Summary</u></strong></p>
    <p style="text-align: center"> This page discusses the process of creating a webscraper to collect detailed player data from the popular football statistics site <a href="https://www.transfermarkt.com/">transfermarkt.com</a>. The scraper gives us 5,000,000+ rows and 30 columns of match level statistics for each player in the top-5 European leagues and their second division counterparts.</p>

    <p style="font-size: 110%; text-align: center;"><strong><u>Relevant Links</u></strong></p>
    <p><strong>Repository Link: </strong><a href="https://github.com/ocroft31/Webscrape-transfermarkt">Webscrape-transfermark</a></p>
    <br>

    <strong>Software Used:</strong> <span class="notion-pill pill-purple">Python</span>
</div>

The aim of this project is to collect match level data for all players listed in the squads of all teams for the top-5 European football leagues and their second division counterparts from the 2011/12 season to the 2023/24 season. This page walks through the code that was created to scrape the data from transfermarkt.com. I don't include any data cleaning processes, because of how complicated it is; however, with the data collection process, we save ourselves a lot of time that would be spent on cleaning.

<p style="font-size: 200%;"><strong>The layout of Transfermarkt</strong></p>

Transfermarkt is a widely used football statistics site where users input a range of data for footballers, football clubs, or anything else related to the sport. For our purpose, we are focused on gathering the detailed player statistics for each match they can play in. We can see an example of the page we want to collect data from below.

<div class="row justify-content-center">
    <div class="col-12 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\transfermarkt\image 1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Although the information is basic, it is very useful for a baseline analysis of each player through their minutes, goal contributions, or even rest days between games (In fact, I originally used this source as a means to collect injury data, which is captured by the position column; however, that research has been scrapped.) We will look to collect everything from this page.

As we look to collect data for every player within each squad for the ten specific leagues, we also need to make use of other information pages on the website. Firstly, there is a dedicated section for competitions on transfermarkt, if you head to one of the comptitions (here, let's use the Premier League) it gives information on all of the teams involved within a specified season, as shown below.

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\transfermarkt\image 2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

If we click on one of the teams, it gives us a table of all the listed members of the squad, with a few statistics. Then, clicking on one of the players, leads us to their profile, where we can find the detailed statistics we discussed just above.

<div class="row justify-content-center">
    <div class="col-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\transfermarkt\image 3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<br>

The website layout that is discussed above forms the basis of our webscraping strategy.

- First, we collect a dataset of all the teams that competed within our ten leagues across the time period we are studying, including links to their pages on transfermarkt.

- Second, we parse through that dataset to collect the squad lists for each team in each league.

- Finally, we go through the squad lists and collect the data for each player.

<br>
<p style="font-size: 200%;"><strong>Step 1: Collect the teams from each league</strong></p>

Fortunately, the web links for each page that we look to scrape are standardised across the leagues and players we want to collect data from, let's first look at the competition page address as an example.

<div class="row justify-content-center">
    <div class="col-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\transfermarkt\image 4.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We see from the webpage address that there are three variable parts to access the league and season we want to collect data from, those simply being the league, an associated code, and the year the season starts. As we do not need any unique id for each league and season combination, we are able to just loop through the leagues and seasons that we want data from using string manipulation. Let's review how this is done in Python.

First, we define a list of the leagues we want to collect data from for us to loop through. The list is made up of tuples with the leagues, as formatted like they are on transfermarkt, and their respective codes. 

```python
leagues = [('premier-league', 'GB1'), ('laliga', 'ES1'), ('serie-a', 'IT1'), ('bundesliga', 'L1'), ('ligue-1', 'FR1'),
           ('championship', 'GB2'), ('laliga2', 'ES2'), ('serie-b', 'IT2'), ('2-bundesliga', 'L2'), ('ligue-2', 'FR2')]
```

Once we have our list, we are then able to loop through it to access each page and scrape it, as we see below. 

```python
for league, code in leagues:
    data = [] # Creates an empty data structure for each league

    for year in range(2011, 2025): # Loops through each season within our range. Here, from 2011/12 - 2024/25
        print(f'Scraping data for {league} in {year}...')
        season, team_links = scrape_data_for_year(code, league, year) # Calls a pre-defined function to collect the season and links for each team in the league

        if season and team_links: # Checks to see if the variables are non-null
            for link in team_links:
                data.append({ # Appends the data to the empty data structure
                    'Season': season
                    'Team Link': link
                })

    df = pd.DataFrame(data) # Converts the matrix into a dataframe to be saved as a csv file
    df.to_csv(f'test/{league}_team_links.csv', index = False)
    print(f'Team links for {league} saved.')
```

The loop calls the function ```scrape_data_for_year()``` to collect the data. This function, which runs through the website code and collects the data using CSS selectors, is shown below.

```python
def scrape_data_for_year(code, league, year):
    url = f'https://www.transfermarkt.co.uk/{league}/startseite/wettbewerb/{code}/plus/?saison_id={year}' # Appends the URL with the league and year we want data for from our list
    
    ... # Some error handling that has been hidden

    soup = BeautifulSoup(response.content, 'html.parser')

    table = soup.find_all('table', class_ = 'items')[0] # Finds the first table on the page and saves it
    tbody = table.find('tbody') # Finds the table body

    team_links = [] # Creates an empty list to append with new data

    season = soup.find_all('h2', class_ = 'content-box-headline')[1].text.strip() # Finds the heading on top of the table and saves it as season

    if tbody: # Checks if tbody is non-empty
        for row in tbody.find_all('tr'): # Loops through all of the rows in the table body
            team_link = row.find('a', href = True) # On the website all rows save the links for each team under <a> and includes the href for the team. This just saves line of code

            if team_link:
                href = team_link['href'] # Collects only the href value
                team_links.append(href) # Saves it

    print(f'\n{league} and {year} - Successfully scraped\n')
    return season, team_links
```

As we saw from the 2nd code snippet, this data is then saved into a CSV file for use like we see below. Much like the first step, this gives us our strategy for step 2; we parse through the csv files and access each of the web pages for each team, saving the data to access the pages for each player into a CSV file.

<div class="row justify-content-center">
    <div class="col-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets\img\transfermarkt\image 5.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<br>
<p style="font-size: 200%;"><strong>Step 2: Collect the squad lists for each team</strong></p>

The process for collecting the squad lists for each team is almost identical, so I will not spend much time reviewing repeated code. There are two things that are interesting to touch on though. First, we look at collecting six variables - The team name, the Player's transfermarkt ID, their name, link to their page, their shirt number, and the season. Second, and much more importantly, we are scraping from a much larger number of webpages, meaning that we need to code data backups and print progress updates.

We see the first part of this code below. A thing to note is that this file can be further automated by looping through the folder with the team lists in; however, I just loaded in each file one at a time here, so the variable ```league_to_scrape``` is just allocated a string with the league that I want to get data for.

```python
ignore_backup = False # Used for testing if you want to start a fresh data frame without going and deleting the previous backup
save_every = 50 # Set how many iterations I want the code to go through to before a backup is saved. Here, there are ~300 total iterations, so 50 is likely sufficient.

backup_path = f'backup squad lists/{league_to_scrape}_squad_lists_backup.csv' # Initialise the backup and main save paths
save_path = f'squad lists/squad_lists_{league_to_scrape}.csv'

if os.path.exists(backup_path) and ignore_backup: # Checks if the backup exists but should be ignored
    print('Backup found but it is being ignored. Starting fresh data frame.')
    squad_lists = pd.DataFrame()
    iteration_count = 0
    previous_saved_iteration = 0
else: 
    if os.path.exists(backup_path): # Checks if a backup exists
        squad_lists = pd.read_csv(backup_path) # Loads in the new backup
        if 'previous_saved_iteration' in globals(): # Checks to see if the variable exists, this could be if an error led to a kernel restart
            iteration_count = previous_saved_iteration # Sets the iteration count to the no. of the previously saved iteration. This is more memory efficient than running the below calculation
        else:
            iteration_count = squad_lists.drop_duplicates(subset = ['Team Name', 'Season']).shape[0] # Sets it to the iteration the backup was saved at but through a calculation
        print(f'Loaded backup with {iteration_count} iterations.')
    else:
        squad_lists = pd.DataFrame() # Begins a fresh data frame if there isn't a backup
        print('Starting a fresh data frame.')
        iteration_count = 0
        previous_saved_iteration = 0

total_iterations = len(df) - iteration_count
```

The second part shows the loop through the team links file. There is not much more to note within this, but we can point out we use the library tqdm as it gives us a nice progress bar. Apart from that, that is all there is to step 2. We see how the substance of the code is quite similar to that of step 1 in terms of looping through a data structure and then scraping the website using CSS selectors; however, we need to be more cautious in terms of error handling and backups being saved due to the no. of iterations we have to go through. 

```python
start_time = time.time() # Saves the start time of the script running

for index, row in tqdm(df.loc[iteration_count: ].iterrows(), total = total_iterations, desc = 'Scraping Teams', dynamic_ncols = True): # Loops through the rows of the team links data frame starting at the iteration_count
    try:
        team_url = row['Team Link'] # Collects the data in the 'Team Link' row
        team_data = scrape_team_data(team_url) # Runs the scraper on the web page

        if team_data is not None:
            squad_lists = pd.concat([squad_lists, team_data], ignore_index = True) # Adds the just scraped squad list data and concatanates it to the rest of the saved data 

        iteration_count += 1 

        if (iteration_count) % save_every == 0: # Saves every time the iteration count is a multiple of the save_every variable
            squad_lists.to_csv(backup_path, index = False)
            previous_saved_iteration = iteration_count
            print(f'\nProgress saved after {iteration_count} iterations.')

            print_elapsed_time(start_time, iteration_count, total_iterations) # This is a pre defined function that just prints the avg time of a page being scraped and the estimated time left

        time.sleep(random.uniform(1, 3)) # Adds a small delay to help with limiting the number of requests sent to the website

    except Exception as e:
        print(f'\nError at iteration {index}: {e}')
        break # Stops the script if there's an error

squad_lists.to_csv(save_path)
end_time = time.time()
total_elapsed_time = end_time - start_time

print(f'\nCompleted scraping in {int(total_elapsed_time // 60)} min and {int(total_elapsed_time % 60)} secs')
```

<br>
<p style="font-size: 200%;"><strong>Step 3: Collect the Individual Player Data</strong></p>

The third step, which collects the player data at the match level just expands on step 2 with a slightly more sophisticated set of error handling; however, because of the size of the code, I'm not going to cover it here.

And that finishes the necessary code needed to web scrape player level data for every squad member for all teams in the European top-5 competitions and their second divisions, from the 2011/12 - 2023/24 seasons. It takes ages to run... but once it is complete for all leagues, it gives us a set of data sets, which combined gives us 5,154,773 player-match observations and 30 variables. 

