# Tour Event Notifier with Web Scraping, SQLite & Email Alerts

This Python project scrapes a web page for upcoming tour events, stores unique events in a local SQLite database, and sends an email notification if a new event is found. It continuously monitors the website in a loop, making it ideal for real-time tracking.

---

## Project Structure
```bash
├── main.py # Main application logic
├── extract.yaml # SelectorLib YAML file for data extraction
├── data.txt # Sample data entries
├── headers.txt # Optional: User-Agent headers
├── data.db # SQLite database (auto-created)
```

---

## Features

- Scrapes tour data from a public website.
- Extracts event information (band, city, date) using [SelectorLib](https://selectorlib.io/).
- Stores events in an SQLite database to avoid duplicates.
- Sends email alerts for newly found events.
- Runs continuously in a loop for automated monitoring.

---

## Requirements

- Python 3.x
- Libraries:
  - `requests`
  - `selectorlib`
  - `sqlite3`
  - `smtplib`, `ssl`
  - `time`, `os`

### Install required packages using:

```bash
pip install requests selectorlib
```
##  Getting Started
### 1. Clone the repository
```bash
git clone https://github.com/your-username/tour-event-notifier.git
cd tour-event-notifier
```
### 2. Create extract.yaml
Create a file named extract.yaml with the correct CSS selector to target the tour data:

```yaml
tours:
    css: "div.card-content"
    type: Text
```
### 3. Setup SMTP Email
- In main.py, update:
- username: your Gmail address
- password: app-specific password (not your Gmail password)
- receiver: recipient email address
- Don't expose your email credentials in production. Use environment variables or a .env file with python-dotenv.

### 4. Run the Application
```bash
python main.py
```
## You will see:
- Repeated scraping attempts.
- Newly found tours stored in data.db.
- Email notifications for new events.

## Database Schema
The SQLite table Events should be created with:

```sql
CREATE TABLE Events (
    band TEXT,
    city TEXT,
    date TEXT
);
```
This table avoids duplicate notifications by checking if the event already exists.

## Email Format
Email subject and content can be customized. Currently:

```vbnet
Subject: Hey, new event was found!
```
## Stopping the Script
To stop the infinite loop, press CTRL+C.

## Notes
- Be respectful when scraping external websites. Ensure your script does not overload servers.
- Consider adding error handling and logging for robustness.
- You may add headers (e.g., from headers.txt) to your requests.get() for better reliability.
