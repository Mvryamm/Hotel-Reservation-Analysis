# Table Of Contents

- [Project Overview](#Project-Overview)
- [Data Source](#Data-Source)
- [Data Cleaning/Preparations](#Data-Cleaning/Preparations)
- [Dataset Details](Dataset-Details)
- [Exploratory Data Analysis](Exploratory-Data-Analysis)
- [Data Analysis](Data-Analysis)
- [Result/Recommendation](Result/Recommendation)


## Project Overview
 I will be analyzing a hotel reservation dataset to uncover valuable insights that drive better decision-making in the hotel industry. By leveraging SQL, I will query and analyze data to understand guest preferences, booking trends, and key operational factors that influence hotel performance.
## Data Source
For this project, you can download the CSV file from the link [HERE](https://docs.google.com/document/d/1u2ozLXxy_TGauKCssUfbAt8WcG-upkVL3fn5MJYxoMc/edit?usp=drive_link) and load the data into your chosen database. You can use any database like MySQL Workbench, PostgreSQL, SQL Management Studio, or any other, My choice of SQL database management system (DBMS) is PostgreSQL.
## Data Cleaning/Preparations
In the initial data preparation phase, we performed the following task
1. Data Loading/inspection
2. Handling Missing Values
3. Data Cleaning and Formating
## Dataset Details
The dataset includes the following columns:

- Booking_ID: A unique identifier for each hotel reservation.
- no_of_adults: The number of adults in the reservation.
- no_of_children: The number of children in the reservation.
- no_of_weekend_nights: The number of nights in the reservation that fall on weekends.
- no_of_week_nights: The number of nights in the reservation that fall on
weekdays.
- type_of_meal_plan: The meal plan chosen by the guests.
- room_type_reserved: The type of room reserved by the guests.
- lead_time: The number of days between booking and arrival.
- arrival_date: The date of arrival.
- market_segment_type: The market segment to which the reservation
belongs.
- avg_price_per_room: The average price per room in the reservation.
- booking_status: The status of the booking.
## Exploratory Data Analysis  
  EDA involved exploring the questions for which SQL queries were written to gain insights:

1. What is the total number of reservations in the dataset?
2. Which meal plan is the most popular among guests?
3. What is the average price per room for reservations involving children?
4. How many reservations were made for the year 20XX (replace XX with the desired year)?
5. What is the most commonly booked room type?
6. How many reservations fall on a weekend (no_of_weekend_nights > 0)?
7. What is the highest and lowest lead time for reservations?
8. What is the most common market segment type for reservations?
9. How many reservations have a booking status of “Confirmed”?
10. What is the total number of adults and children across all reservations?
11. What is the average number of weekend nights for reservations involving children?
12. How many reservations were made in each month of the year?
13. What is the average number of nights (both weekend and weekday) spent by guests for each room type?
14. For reservations involving children, what is the most common room type, and what is the average price for that room type?
15. Find the market segment type that generates the highest average price per room.
## Data Analysis
 Include intresting code/features work with
 1. What is the total number of reservations in the dataset?
```sql
SELECT COUNT(*) AS total_reservations
FROM hotel_reservations;
```
2. Which meal plan is the most popular among guests?
```sql
SELECT type_of_meal_plan, COUNT(*) guest_count
FROM hotel_reservations
GROUP BY type_of_meal_plan
ORDER BY guest_count DESC
LIMIT 1;
```
3. What is the average price per room for reservations involving children?
```sql
SELECT AVG(avg_price_per_room) AS avg_price_for_children
FROM hotel_reservations
WHERE no_of_children > 0;
```
4. How many reservations were made for the year 20XX (replace XX with the desired year)?
```sql
SELECT COUNT(*) AS total_reservations_2018
FROM hotel_reservations
WHERE EXTRACT(YEAR FROM arrival_date) = 2018
```
5. What is the most commonly booked room type?
```sql
SELECT room_type_reserved, COUNT(*)AS booking_count
FROM hotel_reservations
GROUP BY room_type_reserved
ORDER BY booking_count DESC
LIMIT 1;
```
6. How many reservations fall on a weekend (no_of_weekend_nights > 0)?
```sql
SELECT COUNT(*) AS weekend_reservations
FROM hotel_reservations
WHERE no_of_weekend_nights > 0;
```
7. What is the highest and lowest lead time for reservations?
```sql
SELECT MAX(lead_time)AS highest_lead_time
from hotel_reservations;

SELECT MIN(lead_time)AS lowest_lead_time
from hotel_reservations;
```
8. What is the most common market segment type for reservations?
```sql
SELECT market_segment_type, COUNT(*)AS most_common_market_segment_count
FROM hotel_reservations
GROUP BY market_segment_type
ORDER BY most_common_market_segment_count DESC
LIMIT 1;
```
9. How many reservations have a booking status of “Confirmed”?
```sql
SELECT COUNT(*)AS confirmed_bookings_count
FROM hotel_reservations
WHERE booking_status ='Not_Canceled';
```
10. What is the total number of adults and children across all reservations?
```sql
SELECT SUM(no_of_adults)AS Total_adults, SUM(No_of_children)AS Total_children
FROM hotel_reservations;
```
11. What is the average number of weekend nights for reservations involving children?
```sql
SELECT AVG(no_of_weekend_nights) AS avg_weekend_nights_for_children
FROM hotel_reservations
WHERE no_of_children > 0;
```
12. How many reservations were made in each month of the year?
```sql
SELECT EXTRACT(MONTH FROM arrival_date)AS MONTH,COUNT(*)AS reservation_by_month
FROM hotel_reservations
GROUP BY month
ORDER BY month;
```
13. What is the average number of nights (both weekend and weekday) spent by guests for each room type?
```sql
SELECT room_type_reserved,AVG(no_of_weekend_nights + no_of_week_nights) AS avg_nights
FROM hotel_reservations
GROUP BY room_type_reserved;
```
14. For reservations involving children, what is the most common room type, and what is the average price for that room type?
```sql
SELECT room_type_reserved,COUNT(*)AS bookings_count_for_children
FROM hotel_reservations
WHERE no_of_children > 0
GROUP BY room_type_reserved
ORDER by bookings_count_for_children DESC
LIMIT 1;

SELECT AVG(avg_price_per_room) AS avg_price_for_common_room
FROM hotel_reservations
WHERE room_type_reserved = 'Room_Type 1' AND no_of_children > 0;
```
15. Find the market segment type that generates the highest average price per room.
```sql
SELECT market_segment_type,AVG(avg_price_per_room)AS Avg_price
FROM hotel_reservations
GROUP BY market_segment_type
ORDER BY Avg_price DESC
LIMIT 1;
```
## Result/Recommendation
1. Total Reservations (700): This gives us an idea of the overall volume of business for the hotel. A total of 700 reservations is a significant number, indicating a reasonably high occupancy rate.

2. Popular Meal Plan (Meal Plan 1 with 527 reservations): The hotel should ensure that it has adequate resources and supplies to cater to the demand for Meal Plan 1, as it is the most popular choice among guests.

3. Average Price per Room with Children ($144.57): This information can be used for pricing strategies and promotional offers targeting families with children.

4. Reservations in 2018 (577): The year 2018 seems to have been a busy year for the hotel, with 577 reservations made. This data can be compared with other years to identify trends and patterns.

5. Most Commonly Booked Room Type (Room Type 1 with 534 reservations): Room Type 1 is the most popular among guests. The hotel should ensure that it has an adequate inventory of this room type to meet the demand.

6. Weekend Reservations (383): A significant number of reservations (383) fall on weekends, indicating that the hotel may need to adjust staffing levels and amenities to accommodate the influx of guests during these times.

7. Lead Time (Highest: 443, Lowest: 0): The wide range of lead times suggests that the hotel caters to both last-minute bookings and reservations made well in advance. This information can help with resource planning and pricing strategies.

8. Most Common Market Segment (Online): The online market segment appears to be the most significant source of reservations for the hotel. This insight can guide the hotel’s marketing and advertising efforts, particularly in the digital space.

9. Confirmed Reservations (493): A high number of reservations (493) have a booking status of “Confirmed,” indicating a healthy demand for the hotel’s services.

10. Total Adults and Children (1316 and 69, respectively): This information can help the hotel plan its facilities and services catered to families with children, such as playgrounds, kid-friendly menus, and family-oriented activities.

11. Average Weekend Nights for Reservations with Children (1.0): Families with children tend to stay for an average of one weekend night, which could inform the hotel’s weekend programming and promotions.

12. Reservations by Month: The monthly breakdown of reservations can help the hotel identify seasonal patterns and adjust its operations accordingly. For example, months with higher reservations may require increased staffing and resource allocation.

13. Average number of nights spent by guests for each room type: Guests tend to stay longer in room_type 4 which has an average night of 3.8 nights, while room_type 5 has the shortest stay with an average night of 2.5 nights, This information helps the hotel optimize room pricing and promotional strategies based on room popularity and occupancy rate.

14. Most common room_type and an average price of the room(Room type 1,$123.1): This information will guide the hotel pricing strategy and marketing effort to cater efficiency to families with children.

Voilà!!

This concludes the Hotel Reservation Analysis Data Project. Stakeholders are now equipped to act on the insights and recommendations provided. Thank you for your time, and feel free to share any feedback or suggestions.
