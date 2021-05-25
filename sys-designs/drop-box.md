# Design file hosting service
Let's design a file hosting service like Dropbox or Google Drive. Cloud file storage enables users to store their data on remote servers. Usually, these servers are maintained by cloud storage providers and made available to users over a network (typically through the Internet). Users pay for their cloud data storage on a monthly basis.

Similar Services: OneDrive, Google Drive

# Functional Requirement
User should be able to 
- login to the file hosting service from multiple devices.
- logout from the file hosting service from multiple devices.
- upload documents to the file hosting service from multiple devices.
- download documents from the file hosting service from multiple devices.
- update documents
- version documents
- highly available
- highly reliable
- increase / decrease storage quota / plan per his/her storage needs
- share url for the document

Document contents should be synchronized across multiple devices
Document can be edited offline. 

# Non functional requirements
- total number of users
- max. file size allowed: 1 GB
- max. file versions allowed: 100
- total number of documents uploaded in year: 1,000,000,000 
- read / write ratio for uploaded documents: 10:1


- total number of documents uploaded per minute: 1,000,000,000 / (365*24*60) = ~2000 


- total number of write requests per minute: 2000 * 100 (max. versions) = 200,000
- total number of read requests per minute: (write request * 10) = 2,000,000
- total write bandwidth required per minute = 200,000 * 1 GB = 2,000,000 GB = 2 PB
- total read bandwidth required per minute = 2,000,000 * 1 GB = 20,000,000 GB = 20 PB

File Storage for documents
- per min : (total docs uploaded per min) * 1 GB = 20,000 GB
























1. Users should be able to upload and download their files/photos from any device.
2. Users should be able to share files or folders with other users.
3. Our service should support automatic synchronization between devices, i.e., after updating a file on one device, it should get synchronized on all devices.
4. The system should support storing large files up to a GB.
5. ACID-ity is required. Atomicity, Consistency, Isolation and Durability of all file operations should be guaranteed.
6. Our system should support offline editing. Users should be able to add/delete/modify files while offline, and as soon as they come online, all their changes should be synced to the remote servers and other online devices.
# Non-Functional Requirements

# Assumption
