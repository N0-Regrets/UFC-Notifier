# UFC-Notifier
This repository contains two n8n workflows that notify you via Telegram whenever there’s a UFC event happening today.
Both workflows achieve the same goal but use different data sources:

## How It Works

### API Workflow

- **Trigger the Workflow:**  
  Runs either **manually** or **automatically every weekend** (Saturday and Sunday at 7:00 AM) through a scheduled trigger.

- **Fetch Upcoming Events:**  
  Makes an **HTTP request** to the [**SportsData.io MMA API**](https://sportsdata.io/developers/api-documentation/mma#schedules) to retrieve the full UFC event schedule for 2025.

- **Filter Today’s Events:**  
  A **JavaScript node** processes the API response to **filter events happening today** based on the event date.

- **Send Notifications:**  
  If a match is scheduled for today, the workflow sends a **Telegram message** containing the event name and time.


### Scraper Workflow

- **Trigger the Workflow:**  
  Starts either **manually** or **automatically every weekend** (Saturday and Sunday at 7:00 AM) using a scheduled trigger.

- **Fetch UFC Schedule Page:**  
  Sends an **HTTP request** to the [ESPN UFC schedule page](https://www.espn.com/mma/schedule/_/league/ufc) to collect the latest fight event data.

- **Extract Webpage Content:**  
  Uses an **HTML extraction node** to capture the main page content and prepare it for processing.

- **Use LLM to Parse Event Info:**  
  A **language model (via Ollama)** analyzes the HTML and extracts details about the **closest upcoming UFC event**, returning structured data in **JSON format**.

- **Filter and Notify via Telegram:**  
  A **JavaScript node** checks if the event is happening **today**.  
  - If yes → sends a **Telegram message** with event details and time.  
  - If not → sends a “No event today” notification.


## Notes
The event time may not perfectly match between both workflows probably because the API and ESPN data may use different time zones

## Future Improvements

Include event start time and main card details.

Send reminder messages a when the main event is starting.

