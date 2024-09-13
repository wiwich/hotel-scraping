# Hotel Competitive Pricing Analysis
Comparing a hotel's rates with those of competitors helps strategically position the hotel, optimize revenue, and attract guests. By understanding market trends and adjusting prices accordingly, hotels can maximize occupancy, profitability, and overall market position.

This project involves developing a web scraper to extract data about hotels from online booking platforms. The collected data will be processed using ETL (Extract, Transform, Load) techniques to manage and prepare it for analysis. This will facilitate the examination of trends in hotel pricing, location, and customer ratings.

**Libraries:**
 - **BeautifulSoup:** A library for parsing HTML and extracting data in a structured way.
- **Selenium:** A web automation tool for handling dynamic content and JavaScript-loaded elements.
 - **Requests:** A library for sending HTTP requests and retrieving web pages.
 - **ChromeDriver** is used to configure the ChromeDriver service.
 - **Pandas:** for data manipulation and analysis.

## Scraping Process
**1. Setup**
- Install necessary libraries
  ```
  !pip install bs4 requests selenium
  ```
- Configure web driver for Selenium (e.g. ChromeDriver).
  ```
  # set chrome diver path
  CHROMEDRIVER_PATH = r"C:\<path>\chromedriver.exe"
  ```
**2. Data Collection**

  Set variable for specific search 
  ```
  search_city = "Cowes" # the name of the city that want to search
  nights = 2 # number of nights
  adults_no = 2 # number of adults
  children_no = 0 # number of children
  rooms_no = 1 # number of rooms
  next_days = 30 #  the period from today through the next 30 days
  currency = "AUD"
  ```

  Fetching Data 
  ```
  target_url = "https://www.booking.com/searchresults.en-gb.html?ss="+search_city+"&dest_type=city&checkin="+checkin_date+"&checkout="+checkout_date+"&group_adults="+str(adults_no)+"&group_children="+str(children_no)+"&no_rooms="+str(rooms_no)+"&selected_currency="+currency+"&order=popularity"

  response = requests.get(target_url)
  if response.status_code == 200:
      print('> Success Retrieve Data - Response: {}'.format(response.status_code))
      # Parse HTML content
      soup = BeautifulSoup(response.content, 'html.parser')
  else:
      print('> Failed Retrieve Data - Response: {}'.format(response.status_code))
  ```

  Parsing HTML
  ```
  hotel_list = []
  for i in range(len(allData)):
      tmp_info = {}
      tmp_info["arrivalDate"] = checkin_date
      tmp_info["departureDate"] = checkout_date
      try:
          tmp_info["name"] = allData[i].find('div',{'data-testid':'title'}).text
      except:
          tmp_info["name"] = None
      try:
          tmp_info["rating"] = allData[i].find('div',{'class':'d0522b0cca fd44f541d8'}).text.split(" ")[-1] # get the last index
      except:
          tmp_info["rating"] = None
      try:
          tmp_info["stars"] = allData[i].find('div',{'class':'f97c3d5c2f'}).attrs['aria-label']  # get value in aira-label
      except:
          tmp_info["stars"] = None
      try:
          tmp_info["price"] = allData[i].find('span',{'data-testid':'price-and-discounted-price'}).text.replace(u'\xa0',' ')
      except:
          tmp_info["price"] = None
      try: 
          tmp_info["location"] = allData[i].find('span',{'class':'cf35c10683 d57d1b7d64','data-testid':'address'}).text
      except:
          tmp_info["location"] = None
      hotel_list.append(tmp_info)
      try:
          tmp_info["roomType"] = allData[i].find('h4',{'class':'e8acaa0d22 e7baf22fe8'}).text
      except:
          tmp_info["roomType"] = None
  ```
  
**3. Data Processing & Transformation**

The data will be converted into a DataFrame using the pandas library, followed by cleaning and transforming the data.


