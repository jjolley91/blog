---
title: "Rogue Inbox"
date: 2023-10-16T13:08:05-10:01
#draft: true
tags: ['CTF','Writeups', 'Forensics', 'Medium']
---
 
# [Home](https://jjolley91.github.io/blog/) >

###  [Huntress CTF](https://jjolley91.github.io/blog/huntress_ctf_2023) >  [Medium Challenges](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/rock_paper_psychic)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/babel) 

### You've been asked to audit the Microsoft 365 activity for a recently onboarded as a customer of your MSP.

### Your new customer is afraid that Debra was compromised. We received logs exported from Purview... can you figure out what the threat actor did? It might take some clever log-fu!

For this challenge we are given 'purview.csv' to download.

We tried various methods of inspecting the file, and eventually found that the flag was being written out one cell at a time within the json data.

## Example:
```json
{"AppAccessContext":{"IssuedAtTime":"2023-09-26T01:47:34","UniqueTokenId":"3kVZRE8tFkinHtPA7_EFAA"},"CreationTime":"2023-09-26T01:56:15","Id":"85d29e27-be28-4f2c-96c8-08dbbe33c473","Operation":"New-InboxRule","OrganizationId":"df233d94-fed3-4436-bf9a-a799fb85a159","RecordType":1,"ResultStatus":"True","UserKey":"10032002F222981B","UserType":2,"Version":1,"Workload":"Exchange","ClientIP":"185.73.124.135:19823","ObjectId":"NAMPR10A011.PROD.OUTLOOK.COM\/Microsoft Exchange Hosted Organizations\/M365B132131.onmicrosoft.com\/f757cb79-dd91-4555-a45e-520c2525d932\\f","UserId":"DebraB@M365B132131.OnMicrosoft.com","AppId":"00000002-0000-0ff1-ce00-000000000000","ClientAppId":"","ExternalAccess":false,"OrganizationName":"M365B132131.onmicrosoft.com","OriginatingServer":"CH3PR10MB7864 (15.20.6813.027)","Parameters":[{"Name":"AlwaysDeleteOutlookRulesBlob","Value":"False"},{"Name":"Force","Value":"False"},{"Name":"From","Value":"flag@ctf.com"},{"Name":"MoveToFolder","Value":"Conversation History"},{"Name":"Name","Value":"f"},{"Name":"MarkAsRead","Value":"True"},{"Name":"StopProcessingRules","Value":"True"}],"SessionId":"9dfdecb6-59a0-4714-846e-86c0fc911104"}
```
```json
{"Name":"Name","Value":"f"}  

{"Name":"Name","Value":"l"}  

{"Name":"Name","Value":"a"}  
```
Following that, we were able to piece together the flag using google sheets. We first isolated the cells that contained the value '{"Name":"Name","Value":'. Then we used the extensions tab to create the following app script:
```javascript
function concatenateValuesFromColumn() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var dataRange = sheet.getRange("A:A"); // This selects the entire column A.
  var data = dataRange.getValues();
  var concatenatedValue = "";
  
  for (var i = 0; i < data.length; i++) {
    var cellData = data[i][0];
    var match = /{"Name":"Name","Value":"(.*?)"/.exec(cellData);
    if (match) {
      concatenatedValue += match[1] ;
    }
  }
  
  concatenatedValue = concatenatedValue.slice(0, -2); // Remove the trailing comma and space.
  sheet.getRange("B145").setValue(concatenatedValue); // Change to the cell where you want the concatenated value.
}
```
This caused the flag to be printed in one column!

![rogue_inbox](https://github.com/jjolley91/blog/blob/main/static/Huntress_CTF_2023/rogue_inbox.png?raw=true)

## [Back](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/rock_paper_psychic)  <> [Next](https://jjolley91.github.io/blog/huntress_ctf_2023/2.medium/babel) 
