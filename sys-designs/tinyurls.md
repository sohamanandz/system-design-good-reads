# Design TinyUrl System

## Requirements
system should be able to 
- generate tinyurl for a given long url
- redirect request to given url when accessed via tinyurl
- generate dashboard with url usage details (regions, browsers, network providers, date, time, hits per day etc.
- delete tinyurl after expiry period
- bill users
- login/logout users
- allow login using google account, facebook accounts, linkedin accounts

## Assumption
- how mnay users per day ?
- how many tinyurls will be created per day ?
- how many tinyurl access requests per day ?
- what will be the expiry duration of tinyurl ?
- user interface ? app / website ?
- type of users ? admin / consumer
- journal data requirrements ?

## Constraints

## Design

## Entities

### Users
### AuthProviders
### UserTypes

### TinyURLs

### Requests
