+++
title = 'Data Cleaning'
date = 2024-05-22T11:52:09-07:00
draft = false
weight = 2
+++

###### Convert date format and remove mangled date entries

```Python
parsed_dates = [None] * len(date_array)  # Pre-allocate list for parsed dates
bad_indices = []  # List to store indices of unparseable dates

for i, date_str in enumerate(date_array):
    if not date_str:
        bad_indices.append(i)
    try:
        full_date = parse_iso_datetime(date_str)
        local_date = get_local_naive_datetime_from_utc(full_date)

        parsed_dates[i] = local_date  # Store the adjusted datetime object
    except (ValueError, TypeError):
        bad_indices.append(i)  # Record the index of any unparseable date string
```

###### Cleaned data table (head 3)

| Date            | Video_Title                                                                                       | Channel_Title        | Video_URL                                   |
| --------------- | ------------------------------------------------------------------------------------------------- | -------------------- | ------------------------------------------- |
| 4/19/2024 20:25 | Watched Nvidia Revolutionizes AI: 4X Efficiency Boost & 25X Cost Reduction with Ultimate AI Chip! | The AI Entrepreneurs | https://www.youtube.com/watch?v=pcvVpuDSOP4 |
| 4/19/2024 20:23 | Watched How bikes \*actually\* work                                                               | Veritasium           | https://www.youtube.com/watch?v=scliyWrN7mk |
| 4/13/2024 17:29 | Watched MOD Function to calculate the working hours in Excel #excelformula                        | PK: An Excel Expert  | https://www.youtube.com/watch?v=Uz5w4VlG4Aw |