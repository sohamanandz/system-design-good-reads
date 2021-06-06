# Assumptions / Clarification
- Total # of users
1.5 B 
- # of Daily Active Users 
800 M
- Total # of video uploads in a day
upload:view ratio 1200

- Total # of video views in a day by user
5 videos per day per user

- Avg. # of comments per video
5 comments per day per user

- Avg. # of likes/dislikes per video
5 likes/dislikes per day per user

- Avg. Duration of videos
500 hours worth videos are uploaded to youtube every min

- Avg. Size of Videos
50 MB for 1 minute


# Functional Requirements
- Users should be able to
  - upload video
  - view video
  - add/view comment
  - add/view like / dislike
  - add/update/view video metadata
   

# Non-Functional Requirements
- highly reliable
- highly available. consistency can take hit
- real-time experience while watching video and should not feel any lag


# System Design
## Capacity Estimation
### 
- # of view requests per sec
= 800M * 5 / (24*60*60)
= 0.046 * 1,000,000
= 46,000 per sec

- # of upload requests per sec
upload to view ratio 1:200
= 46,000 / 200
= 230 per sec

- Video Content size per min
= 500*60 mins of view is uploaded every min
* 50 (MB per minute of video)
= 1,500,000 MB per min
= 1,500 GB per min

- Bandwidth Estimation per sec
incoming bandwith
= upload bandwith
= 500 * 60 * 10 / 60 MB/sec 
= 5000 MB / sec
= 5 GB / sec


outgoing bandwith
= 200 * 5 GB / sec
= 1000 TB / sec



![image](https://user-images.githubusercontent.com/81834364/120912290-e4548500-c65b-11eb-8e26-d701d68b93d9.png)
