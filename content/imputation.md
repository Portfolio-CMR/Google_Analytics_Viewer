+++
title = 'Imputation'
date = 2024-05-22T11:52:17-07:00
draft = false
weight = 3
+++

###### Identify activity windows

```Python
# Identify all non-None indices
non_none_indices = np.where(differences != None)[0]

# Identify breaks in continuous sequences
breaks = np.where(np.diff(non_none_indices) != 1)[0] + 1

# Determine start and end indices for each window
starts = non_none_indices[np.insert(breaks, 0, 0)]
ends = non_none_indices[np.append(breaks - 1, len(non_none_indices) - 1)]

# Filter out windows where the start and end indices are the same
windows = np.column_stack((starts, ends))
windows = windows[windows[:, 0] != windows[:, 1]]
```

###### Output activity windows

| Window Start Date/Time | Window Duration (minutes) | Approximate Actions per Minute |
| -------------------------- | ------------------------- | ------------------------------ |
| 4/18/2024 22:34            | 3.9                       | 0.769                          |
| 4/18/2024 21:48            | 25.6167                   | 1.796                          |
| 4/18/2024 21:09            | 3.6167                    | 0.829                          |
