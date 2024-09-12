# Hotel Competitive Pricing Analysis
Comparing a hotel's rates with those of competitors helps strategically position the hotel, optimize revenue, and attract guests. By understanding market trends and adjusting prices accordingly, hotels can maximize occupancy, profitability, and overall market position.

This project involves developing a web scraper to extract data about hotels from online booking platforms, such as Booking.com, for the next 30 days in Cowes, VIC 3922. The collected data will be used to analyze trends in hotel pricing, location, and customer ratings.

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
**2. Fetching Data**
**3. Parsing HTML**

