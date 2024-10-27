
# Distributed File Sharing System

I build a group based file sharing system where users can share, download files from the group they belong to. Download should be parallel with multiple pieces from multiple peers, parallel downloading and custom piece selection algorithm.

## Architecture Overview

#### Tracker

- Maintain information of clients with their files to assist them for the communication between peers

#### Client

- User should create an account and register with the Tracker

- Login using user credentials

- The client which create the group, by default should become owner of that group.

- If owner leaves the group, the member which joined the group just after admin will be a new admin of a group

- Fetch list of all groups in server

- Request to join a group

- Leave group

- List/Accept group join requests (If owner)

- Share file across group: Share the filename and SHA1 hash of the completefile as well as piecewise SHA1 with the tracker

- fetch list of all shareble files in a group

- Download File \[Core Part\]

    - Retrieve peer information from tracker for the file

    - Download file from multiple peers (different pieces of file from different peers - piece selection algorithm) simultaneously and all the files which client downloads will be shareable to other users in the same group

    - Your algorithm should ensure that pieces are downloaded from more than 1 peers (if available)

    - Ensure file integrity from SHA1 comparison

    - Users should be able to download files concurrently in their respective sessions.

- Show downloads

- Stop sharing file

- Stop sharing all files temporarily (Logout)

- Whenever client logins, all previously shared files before logout should automatically be on sharing mode





**Software Requirement**

1 OpenSSL library

   - **To install OpenSSL library :** `sudo apt-get install openssl`


## How to Run

```
1 cd client
2 make
3 cd ../tracker
4 make
```

### Tracker

1 Run Tracker:

```
cd tracker
./tracker​ <TRACKER INFO FILE> <TRACKER NUMBER>
ex: ./tracker tracker_info.txt 1
```

`<TRACKER INFO FILE>` contains the IP, Port details of all the trackers.

```
Ex:
127.0.0.1
5000
127.0.0.1
6000
```

2 Close Tracker:

```
quit
```

### Client:

1 Run Client:

```
cd client
./client​ <IP>:<PORT> <TRACKER INFO FILE>
ex: ./client 127.0.0.1:18000 trackerInfo.txt
```

2 Create user account:

```
create_user​ <user_id> <password>
```

3 Login:

```
login​ <user_id> <password>
```

4 Create Group:

```
create_group​ <group_id>
```

5 Join Group:

```
join_group​ <group_id>
```

6 Leave Group:

```
leave_group​ <group_id>
```

7 List pending requests:

```
list_requests ​<group_id>
```

8 Accept Group Joining Request:

```
accept_request​ <group_id> <user_id>
```

9 List All Group In Network:

```
list_groups
```

10 List All sharable Files In Group:

```
list_files​ <group_id>
```

11 Upload File:

```
​upload_file​ <file_path> <group_id​>
```

12 Download File:​

```
download_file​ <group_id> <file_name> <destination_path>
```

13 Logout:​

```
logout
```


