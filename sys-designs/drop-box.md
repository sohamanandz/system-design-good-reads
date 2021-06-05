
# Assumption / Clarification
- What type of documents are processed by this system ?
- How many versions are we allowing ?
- Is there any storage limit for the user ?
- Do we teirs of the user ?
  - Free
  - Paid
- Different Type of sharing
  - Read-Only
  - Read-Write


# Functional Requirements
- User should be able to login / logout
- User should be able to upload / download documents [image, pdf, doc etc.]
- User should be able to edit / update / delete documents
- User should be able to version documents
- User should be able to share documents
- Content should be synchronized on all devices after update
- File operations should be ACID
- User should be able to edit documents offline and when they come online, all their changes will be synced

# Non-Functional Requirements
- Availability of the system
  - 90.00 (36.5 days downtime)
  - 99.00 (3.65 days downtime)
  - 99.90 (7.31 hours downtime)
  - 99.99 (52.1 minutes downtime)
  - 99.999 (5.21 minuets downtime)

- How many concurrent users will be using the system at any given point in time ?
100M daily active users (DAU)

- How many total users will be using the system in a month / year ?
500M total users

- Document Archival ?

- Document count per user
200 files per user

- Total Storage Size for Files
= total users * files per user * max size of a file
= 500,000,000 * 200 * 1 GB
= 1,000,000,000 GB
= 1000 PB

- DB Size
Total Files / Documents
= total users * files per user * db record size
= 500,000,000 * 200 * 500 Bytes
= 250,000,000,000 Bytes
= 250 GB
  - Sharding by Location

- Cache Size
20% (DB Size)
50 GB

- Can we get Write-Read Ratio ?
1:1
- Max. document size allowed for upload ?
1 GB 
- User to Device Ratio
1:3


# System Design
## APIs
### Public
- /users/login
- /users/logout
- /users/signup
- /users/id

- /documents/syncup


- /documents/folders/list
- /documents/folders/create
- /documents/folders/id/update
- /documents/folders/id/share

- /documents/files/list
- /documents/files/upload
- /documents/files/download
- /documents/files/id/update
- /documents/files/id/delete

### Private
## Entities
### Folders
|Field          |Data Type        |Constraints / Remarks      |
|---------------|-----------------|---------------------------|
|id             |Integer          |PK                         |
|folder_name    |Text             |                           |
|folder_location|Text             |                           |
|is_active      |Boolean          |                           |
|user_id        |Integer          |FK                         |
|created_at     |Timestamp        |Metadata fields            |
|created_by     |Text             |Metadata fields            |
|modified_at    |Timestamp        |Metadata fields            |
|modified_by    |Text             |Metadata fields            |

### Files
|Field          |Data Type        |Constraints / Remarks      |
|---------------|-----------------|---------------------------|
|id             |Integer          |PK                         |
|file_name      |Text             |                           |
|folder_id      |Integer          |FK                         |
|file_location  |Text             |                           |
|is_active      |Boolean          |                           |
|user_id        |Integer          |FK                         |
|created_at     |Timestamp        |Metadata fields            |
|created_by     |Text             |Metadata fields            |
|modified_at    |Timestamp        |Metadata fields            |
|modified_by    |Text             |Metadata fields            |


### Users
|Field          |Data Type        |Constraints / Remarks      |
|---------------|-----------------|---------------------------|
|id             |Integer          |PK                         |
|first_name     |Text             |                           |
|last_name      |Text             |                           |
|is_active      |Boolean          |                           |
|user_type_id   |Integer          |FK                         |
|auth_engine    |Enum             |                           |
|created_at     |Timestamp        |Metadata fields            |
|created_by     |Text             |Metadata fields            |
|modified_at    |Timestamp        |Metadata fields            |
|modified_by    |Text             |Metadata fields            |

### UserTypes
|Field          |Data Type        |Constraints / Remarks      |
|---------------|-----------------|---------------------------|
|id             |Integer          |PK                         |
|user_type_name |Text             |                           |
|is_active      |Boolean          |                           |
|created_at     |Timestamp        |Metadata fields            |
|created_by     |Text             |Metadata fields            |
|modified_at    |Timestamp        |Metadata fields            |
|modified_by    |Text             |Metadata fields            |

### Shares
|Field          |Data Type        |Constraints / Remarks      |
|---------------|-----------------|---------------------------|
|id             |Integer          |PK                         |
|folder_id      |Integer          |FK                         |
|share_type     |Text / Enum      | (read,write)              |
|email_address  |Text             |                           | 
|is_active      |Boolean          |                           |
|user_id        |Integer          |FK                         |
|created_at     |Timestamp        |Metadata fields            |
|created_by     |Text             |Metadata fields            |
|modified_at    |Timestamp        |Metadata fields            |
|modified_by    |Text             |Metadata fields            |




- Partitioning
- Caching
- LB
- Security, Permissions, File Sharing


![image](https://user-images.githubusercontent.com/81834364/120908177-ca07b080-c635-11eb-8073-2496fb094874.png)

