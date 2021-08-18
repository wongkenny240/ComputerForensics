# Browser

## Browser Artifacts

* C:\Users\USERNAME\AppData\Local\Google\Chrome\User Data\Default\
* C:\Users\USERNAME\AppData\Local\Microsoft\Edge\User Data\Default\
* C:\Users\USERNAME\AppData\Microsoft\Windows\INetCache\IE
* C:\Users\USERNAME\AppData\Microsoft\Windows\WebCache\

### Chrome

syncdata.sqlite3

![](../.gitbook/assets/image%20%2876%29.png)

Use the SQLite Database Browser to view SQLite database

![](../.gitbook/assets/image%20%2881%29.png)

#### Last Visited

```
SELECT urls.id, urls.url, urls.title, urls.visit_count, urls.typed_count, urls.last_visit_time, urls.hidden, visits.visit_time, visits.from_visit, visits.transition, visits.id AS visit_id FROM urls, visits WHERE urls.id = visits.url ORDER BY visits.visit_time
```

#### Download

```
SELECT downloads.id AS id, downloads.start_time,downloads.target_path, downloads_url_chains.url, downloads.received_bytes, downloads.total_bytes FROM downloads, downloads_url_chains WHERE downloads.id = downloads_url_chains.id
```

Note: Start time is recorded when the Save As Windows is triggered

### Edge

### Firefox

### BrowsingHistoryView

* Select load history form the specified history files

![](../.gitbook/assets/image%20%2884%29.png)

* Copy the file location of the WebCacheV01.dat in Internet Explorer \(Version 10.0/11.0\) history files\(WebCacheV01.dat\) and click OK to proceed

![](../.gitbook/assets/image%20%2883%29.png)

* Click Ok again to start loading the Web browsing history

![](../.gitbook/assets/image%20%2885%29.png)

* Browsing history will be shown after loading the history file

![](../.gitbook/assets/image%20%2882%29.png)

