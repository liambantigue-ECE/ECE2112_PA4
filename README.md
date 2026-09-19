# EXPERIMENT 4: DATA WRANGLING AND DATA VISUALIZATION
Bantigue, Liam S.<br>
Section: 2ECE-A<br>
Date Submitted: September 19, 2026
# NOTE
In problem a and b, it asked to RETAIN column "Average", but there is no "Average" column in the DataFrame assigned to df. I manually added the column "Average" in df by using the code:
```python
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)
```
Which means add a column named Average in DataFrame df and compute the mean by row using the values of Math, Electronics, GEAS, and Communication.

# A. VISAYAS COMMUNICATION DATAFRAME
The problem instructs us to create a DataFrame assigned to VisComm containing students whose Hometown is Visayas and whose Track is Communication. It must also have the specified columns in order: Name, Gender, Math, Electronics, Average. Remember we learned how to create a DataFrame in PA3 and now in PA4 we can make it more concise and optimized by using the .copy() function. This function helps by creating a standalone DataFrame with allocated memory in an optimized/fast way.
```python
.copy()
```
Note that we used boolean indexing for our filtering conditions and we stated in PA3 that using boolean indexing creates a new dataframe. I still chose to attach .copy() so that we avoid any unpredictable behaviors/error and generally to observe best practice.<br>

After creating the filtering conditions and applying the specified columns, we display the dataframe and its number of rows with the following code.
```python
VisComm = df[(df["Hometown"] == "Visayas") & (df["Track"] == "Communication")][
    ["Name", "Gender", "Math", "Electronics", "Average"]].copy()

print("VisComm")
display(VisComm)
print(f"Number of rows: {len(VisComm)}")
```
<img width="510" height="349" alt="image" src="https://github.com/user-attachments/assets/68aefbc4-91fe-4d4b-979f-957ae77ead22" />

# B. VISAYAS FEMALE DATAFRAME
Problem b is similar to problem a in terms of code used but it uses different parametes. It instructs us to create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. It must have the specified columns in order: Name, Track, GEAS, Electronics, Average. Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter. Following the code from problem a using the required parameters for problem b we get:
```python
VisFemale = df[(df["Hometown"] == "Visayas") & (df["Gender"] == "Female")][
    ["Name", "Track", "GEAS", "Electronics", "Average"]].copy()

print("VisFemale")
display(VisFemale)
```
To not overwrite VisFemale while displaying only the rows of VisFemale whose Average is at least 60, I used boolean indexing. Which is given by the code:
```python
print("\nVisFemale whose Average is at least 60")
display(VisFemale[VisFemale["Average"] >= 60])
```
<img width="601" height="646" alt="image" src="https://github.com/user-attachments/assets/fa3cce2c-475b-4a90-9df7-24e7c34dd10c" />

# C. CATEGORY-AVERAGE VISUALIZATION
Problem c instructs us to: Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown.
  ## a. For each feature, compute the mean of Average for every category using Pandas.
  ```python
track_avg = df.groupby("Track")["Average"].mean().reset_index()
gender_avg = df.groupby("Gender")["Average"].mean().reset_index()
hometown_avg = df.groupby("Hometown")["Average"].mean().reset_index()
```
Using the groupby function we group rows by their "Track" value, use the values in column "Average" to get the mean, and then reset_index() to create a new standard DataFrame.<br>

  ## b. Display the three summary tables.
  ```python
display(track_avg)
display(gender_avg)
display(hometown_avg)
```
We use the typical display() function to display the respective mean of Average of every category.
  ## c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by Hometown.
  **NOTE** I will comment on the code lines to explain each line of code to make it organized and direct.
  ```python
plt.figure(figsize=(15, 4))                         # figure() function creates a new empty figure window with size of 15in Wide by 4in Tall.

plt.subplot(1, 3, 1)                                # splits into 1 row with 3 columns situated at the left side
plt.bar(track_avg["Track"], track_avg["Average"])   # syntax: plt.bar(x, height) horizontal axis has the values of "Track" while vertical axis has values of "Average"
plt.title("Mean Average by Track")                  # Creates the title "Mean Average by Track" above the subplot

plt.subplot(1, 3, 2)                                 # splits into 1 row with 3 columns situated at the middle
plt.bar(gender_avg["Gender"], gender_avg["Average"]) # horizontal axis has the values of "Gender" while vertical axis has values of "Average"
plt.title("Mean Average by Gender")                  # Creates the title "Mean Average by Gender" above the subplot

plt.subplot(1, 3, 3)                                        # splits into 1 row with 3 columns situated at the right side
plt.bar(hometown_avg["Hometown"], hometown_avg["Average"])  # horizontal axis has the values of "Hometown" while vertical axis has values of "Average"
plt.title("Mean Average by Hometown")                       # Creates the title "Mean Average by Hometown" above the subplot

plt.tight_layout()                                   # Automatically adjusts subplot and labels to avoiding overlapping
plt.show()                                           # Displays the figure
```

  ## d. Below the figure, write three concise statements identifying the category with the highest sample mean for each feature.
The Track with the highest sample mean average is Communication, with value of 67.975.<br>
The Gender with the highest sample mean average is Male, with value of 67.183.<br>
The Hometown with the highest sample mean average is Luzon, with value of 68.083.<br>
<img width="298" height="543" alt="image" src="https://github.com/user-attachments/assets/fba605e7-69f0-4f95-ab92-823418b7ec1b" /><br>
<img width="1661" height="535" alt="image" src="https://github.com/user-attachments/assets/a1a0693a-e3db-41da-97a8-37d96f858a82" />
