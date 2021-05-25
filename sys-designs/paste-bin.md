# Design Paste Bin
Pastebin like services enable users to store plain text or images over the network (typically the Internet) and generate unique URLs to access the uploaded data. Such services are also used to share data over the network quickly, as users would just need to pass the URL to let other users see it.
If you haven’t used pastebin.com before, please try creating a new ‘Paste’ there and spend some time going through the different options their service offers. This will help you a lot in understanding this chapter.

## Functional Requirements
### User should be able to create/update/delete new pastebin with plain text or images
### User should be able to share pastebin url
### User should be able to access pastebin url
### Authentication ?

## Non-Functional Requirements
### Read-Heavy Application
Ratio of Read:Write 100:1
### Request Volume
#### Request volume
- 1 Year -> 50 Million paste bins
- count of paste bin in year = 50,000,000
- count of paste bin in a day = 50,000,000 /(365) ~ 150,000

- Write Requests per day ~               150,000
- Read Requests per day ~             15,000,000
- Write Requests per hour ~                6,250
- Read Requests per hour ~               625,000
#### User volume

#### Storage Requirement
- Total number of paste bins =  50,000,000 * 2 Years (retention period)
                             = 100,000,000    
                       
- DB Storage Sizing = 100,000,000 (Total number of paste bins) * 1 KB
          = 100,000,000 KB
          =     100,000 MB
          =         100 GB
          
- File Storage  =   100,000,000 (Total number of paste bins) * 10 MB 
              = 1,000,000,000 MB
              =     1,000,000 GB
              =         1,000 TB
              =             1 PB



## Assumption
### How many pastebins can be created by user ? unlimited
### What is the max size of paste bin plain text ? 10 MB
### what is the max size of paste bin image ? 10 MB
### Paste Bin will be active for how long ? 1 Year
### Only authenticated users should be allowed to create paste bin ? or unauthenticated user can create paste bin
### image and text will be stored as file on filestorage

## Entities
### Users
|fields               |
|---------------------|
|id                   |
|name                 |
|email                |
|created_by           |
|created_on           |
|modified_by          |
|modified_on          |
|active               |

### pastebin
|fields               |
|---------------------|
|id                   |
|content_location     |
|user_id              |
|created_by           |
|created_on           |
|modified_by          |
|modified_on          |
|active               |

### hashkey (unique identifier for each pastebin)
#### We will need 100,000,000 identifiers (Total number of paste bins)
#### hashkey can include a-z(26), A-Z(26), 0-9(10), .~(2) = 64 characters
#### using 64 characers and key length of 5 letters (2^6)^5 = (2)^30 = 1,000,000,000 hashkeys
#### We will be using hashkey of 5 characters

### hashkey
hashkey
active
cached


## api
### users
|api                               | type    |
|----------------------------------|---------|
|/users/create                     |  Write  |
|/users/user-id/update             |  Write  |
|/users/user-id/delete             |  Write  |
|/users/user-id                    |  Read   |
|/pastebin/create                  |  Write  |
|/pastebin/pastebin-id/update      |  Write  |
|/pastebin/pastebin-id/delete      |  Write  |
|/pastebin/pastebin-id             |  Read   |

