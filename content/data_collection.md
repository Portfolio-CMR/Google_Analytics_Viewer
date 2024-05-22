+++
title = 'Data Collection'
date = 2024-05-22T11:52:01-07:00
draft = false
weight = 1
+++

###### Raw files from Google Takeout are in JSON format

```JSON
{
  "header": "YouTube",
  "title": "Watched ChatGPT for Data Analytics: Full Course",
  "titleUrl": "https://www.youtube.com/watch?v\u003duhyMqbZI6rM",
  "subtitles": [{
    "name": "Luke Barousse",
    "url": "https://www.youtube.com/channel/UCLLw7jmFsvfIVaUFsLs8mlQ"
  }],
  "time": "2024-04-14T18:09:56.549Z",
  "products": ["YouTube"],
  "activityControls": ["YouTube watch history"]
}
```

###### Extract features from JSON file

```Python
extracted_data = []

for entry in json_data:
    title = clean_string(entry.get('title', None))
    time = clean_string(entry.get('time', None))
    titleUrl = clean_string(entry.get('titleUrl', None))
    channel_info = entry.get('subtitles', [])
    if channel_info:
        channel_name = clean_string(channel_info[0].get('name', None))

    extracted_data.append({
        'Date': time,
        'Video_Title': title,
        'Channel_Title': channel_name,
        'Video_URL': titleUrl
    })
```

###### For security reasons, we generate a random sampling of fake data using our personal data as a template

```Python
from faker import Faker

# Replace 'Video Title' with random text while retaining the prefix
def modify_title(title):
    if title.startswith('\"Watched '):
        return '\"Watched ' + fake.sentence()
    elif title.startswith('Watched '):
        return 'Watched ' + fake.sentence()
    else:
        return title  # or return fake.sentence() if every title should be modified

df['Video_Title'] = df['Video_Title'].apply(modify_title)

# Replace 'Channel Title' with random text
df['Channel_Title'] = [fake.company() for _ in range(len(df))]

# Replace 'Video URL' with a random URL
df['Video_URL'] = [fake.url() for _ in range(len(df))]
```

