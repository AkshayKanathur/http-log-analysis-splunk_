# http-log-analysis-splunk_
This project simulates analyzing a sample HTTP log to identify anomalies, web traffic patterns, etc...

## Tools Used
- Splunk enterprise
- Kali linux

## Steps Performed
- Imported http log file to splunk
- Analysed fields
- Used SPL (Search Processing Language) to perform tasks like
  - Search for HTTP Events
    - SPL query used:
    ```bash
    source="http_logs.json" host="kali" sourcetype="_json"
    ```
  - Determine the distribution of request methods (GET, POST, etc.) to understand web traffic patterns.
    - SPL query used:
    ```bash
    index=_* OR index=* sourcetype=access_combined | stats count by method
    ```

  - Identify top URLs or endpoints accessed by users.
    - SPL query used:
    ```bash
    index=_* OR index=* sourcetype=access_combined | top limit=10 url
    ```
  - Analyze response codes to identify errors or successful requests.
    - SPL query used:
    ```bash
    index=_* OR index=* sourcetype=access_combined | stats count by status_code
    ```
  - Look for unusual patterns in file transfer activity.
    - SPL query used:
    ```bash
    index=_* OR index=* sourcetype=http_log | timechart span=1h count by time
    ```
  - Analyzed high volumes of error responses.
    - SPL query used:
    ```bash
    index=_* OR index=* sourcetype=http_log | stats count by status_code | sort -status_code
    ```
  - Investigate file transfers to or from suspicious IP addresses.
    - SPL query used:
    ```bash
    index=_* OR index=* sourcetype=http_log | search src_ip="192.168.202.118"
    ```

## Screenshots
<img width="1920" height="1020" alt="Screenshot 2025-10-30 130340" src="https://github.com/user-attachments/assets/3b9b258c-5b9f-4774-9d40-a3b3b604261d" />
<img width="1920" height="1020" alt="Screenshot 2025-10-30 131122" src="https://github.com/user-attachments/assets/4625b7e2-450f-4d6e-96ec-fa0b4b6d73fc" />
<img width="1920" height="1020" alt="Screenshot 2025-10-30 131525" src="https://github.com/user-attachments/assets/c4bea4ba-13fc-4e0f-9c60-e8fffdd4c977" />
<img width="1920" height="1020" alt="Screenshot 2025-10-30 131649" src="https://github.com/user-attachments/assets/d3af94e4-880c-474b-98c3-d7ef87239711" />
<img width="1920" height="1020" alt="Screenshot 2025-10-30 135058" src="https://github.com/user-attachments/assets/f6b93059-57d1-4e5a-97fa-20ade9999d10" />
<img width="1920" height="1020" alt="Screenshot 2025-10-30 135348" src="https://github.com/user-attachments/assets/977eece3-9642-4b84-a07b-371bc60b7c7e" />
<img width="1920" height="1020" alt="Screenshot 2025-10-30 135558" src="https://github.com/user-attachments/assets/e5dc4727-b882-4130-a005-7f6c127469a6" />

## Outcome
Successfully analysed http log file using SPL.

## Note
This was a self-simulated lab exercise for learning and practicing.
