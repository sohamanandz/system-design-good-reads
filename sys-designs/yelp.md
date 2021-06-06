# Assumption / Clarification
- Total places in system
500M
growth rate - 20%
- Queries per second
100K
growth rate - 20%
- Write to Read Ratio
1:10
- Reviews per place ?
1000 review per place
- Photos per place ?
10 photos per place
- Photos per review ?
10 photos per review
- Char length of review ?
500 chars

# Functional Requirements
- Users should be able to add/update/delete places
- Users should be able to add/update/delete feedback/review about a place
- Users feedback/review can have pictures, text and ratings
- Users should be able to search nearby places within a given radius of thier location (latitude, longitude) 

# Non-Functional Requirements
- minimum latency
- read heavy
- read requests > write requests


# System Design
## Entities
### Places
### Reviews
- Ratings
- Photos
- Text
## Storage Estimation
- Place Photos
= # places * 10 * 2(assuming 20% growth per year; places will double in 5 years)
= 500M * 10 * 2 
= 10 B Photos

- Review Photos
= # places * # reviews per place * # of photos per review * 2(assuming 20% growth per year; places will double in 5 years)
= 500M * 1000 * 10 * 2
= 5000 B * 2
= 10000 B Photos

Total = 10010 B Photos

## Database
- No SQL Database as there is no inherent concurrency requierment.
- Places Table
= # places * 2(assuming 20% growth per year; places will double in 5 years) Records
= 500M * 2
= 1B Records
  - Record Size = 2000 Bytes
  - Table Size = 2,000,000,000,000 Byes = 2 TB
- Places_Photo
= 10B Records
  - Record Size = 100 Bytes
  - Table Size = 1000,000,000,000,000 Byes = 1 TB

- Review Table
= # places * 2(assuming 20% growth per year; places will double in 5 years) Records * # of Reviews per place
= 500M * 2 * 1000
= 1000 B Records
  - Record Size = 2000 Bytes
  - Table Size = 2,000,000,000,000,000 Byes = 2000 TB


- Review_Photo
= 10000B Records
  - Record Size = 100 Bytes
  - Table Size = 1,000,000,000,000,000 Byes = 1000 TB

Total db size:
3.1 PB

## APIs
- /places/search (api_key, user_location, search_radius, search_category, search_text, page, pagesize)
- /places/add(api_key, user_location, place_category, place_name, place_description)
- /places/delete(api_key, place_id)
- /places/update(api_key, place_id, place_category, place_name, place_description)

- /reviews/add (api_key, place_id, user_id, review_description, review_rating)
- /reviews/update (api_key, place_id)
- /reviews/delete (api_key, place_id)
- /reviews/list (api_key, place_id, user_id, page, pagesize)

## Databases
