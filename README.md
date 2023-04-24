
# KeyBox
A Microsoft Dataverse solution to govern credentials.

## Features
 - Lets you store keys directly inside Dataverse, directly beside the customers they belong to
 - Lets you generate new passwords, based on the rules of your organization
 - Reminds you to renew the secret when a valid until or reminder date is set

## Requirements
- None, excepts of a Dataverse

## Security
 - As the data is stored in Dataverse, it is as safe as Dataverse itself
 - The security inside Dataverse can be defined with the Dataverse security model to control the access to records
 - All automations are build without any compiled code, so that you can review and trust it 

## Screenshots
A KeyBox record
![KeyBox Record](https://benjaminjohn.de/wp-content/uploads/2023/04/image-2.png)

The KeyBox configuration
![KeayBox Config](https://benjaminjohn.de/wp-content/uploads/2023/04/image-3.png)
 
## Datamodel
### Table: bj_key
User owned table
| Name | Type | Description
|--|--|--|
| bj_keyid | Unique Identifier | The primary key of the table |
| bj_name | Single line of text | A free text where you can give the record a name |
| bj_description | Multiple lines of text | More space for notes | 
| bj_keytypecode | Choice (local) | Lets you choose between 'Username & Password' and 'App ID & Client Secret'|
| bj_keyidentifier | Single line of text | The space for the username or App ID |
| bj_keysecret | Single line of text | The space for the password or client Secret |
| bj_validuntil | Date | Note here the end of life of the secret |
| bj_remindmeon | Date | Set a date for reminder that pop up before the 'Valid until' date is reached |
| bj_customerid | Customer | A reference to the contact or account that belongs to the key |
| bj_url | Single line of text  | A place for the URL where the key is used for |
| bj_ismfarequired | Boolean | Lets you mark that the key needs a second authentication factor |
| bj_mfanote | Single line of text | Here you can write down notes about the second factor, like the used phone number. |

### Relations
```mermaid
erDiagram
account  {  }
contact  {  }
bj_key  {  }
activities { }
account  ||--o{  bj_key  :has
contact  ||--o{  bj_key  :has
bj_key  ||--o{  activities  :has
```
