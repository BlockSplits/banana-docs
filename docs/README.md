# DB Schema

## Tables

### Users

| Field Name | Type | Description |
|---|---|---|
| name | Text | User's nickname. To be used to help identify registered friends. |
| nonce | bigint | Information to be used during login. It could be cached anywhere, for now it's in the DB. |
| id | uuid | PRIMARY KEY. Uniquely identifies user across several tables. |
| address | text | User's wallet address. |
|


### groups

| Field Name | Type | Description |
|---|---|---|
| id | bigint | PRIMARY KEY. Group's identifyer. Each new group increments the identifying number. |
| name | text | Human readable group name. |
| description | text | Details about the group to give context to the user. |
|


### group_members

| Field Name | Type | Description |
|---|---|---|
| id | Text | PRIMARY KEY. Present just to function as primary key. NOTE: maybe we don't need this. |
| user_id | uuid | FOREIGN KEY from users' table. Identifies a user in the group. |
| group_id | bigint | FOREIGN KEY from groups' table. Identifies a group. |
|


### activity

| Field Name | Type | Description |
|---|---|---|
| id | bigint | PRIMARY KEY. Each new activity increments the identifying number. |
| created_at | timestamp | When was this activity created. Not necessary, also not MVP. Maybe we can add a modified_at in the future. |
| group_id | bigint | FOREIGN KEY from groups' table. Identifies a group. |
| name | text | Activity name. Helps to identify the nature of the activity/expense. |
| payer | uuid | FOREIGN KEY from users' table. Identifies the user who paid the activity. |
| creator | uuid | FOREIGN KEY from users' table. Identifies the user who created the activity. |


### splitz

| Field Name | Type | Description |
|---|---|---|
| id | bigint | PRIMARY KEY. Each new activity increments the identifying number. |
| created_at | timestamp | When was this split created. Would likely coincide with activity timestamp... Not necessary, also not MVP. Maybe we can add a modified_at in the future. |
| activity_id | bigint | FOREIGN KEY from the activity's table. Identifies the activity that to be split. |
| participant | uuid | FOREIGN KEY from the users' table. Identifies the user that has to pay this split. |
| percentage | double | percentage of the activity's cost that the participant should pay. The sum of all percentages should add to 100%. | 


## Audit