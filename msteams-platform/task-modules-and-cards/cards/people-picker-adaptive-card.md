---
title: People Picker in Adaptive Cards
description: Describes how to use the People Picker control in Adaptive Cards
localization_priority: Normal
keywords: Adaptive Cards People Picker
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
---

# People Picker in Adaptive Cards

> [!NOTE]
> This feature is available in [public developer preview](~/resources/dev-preview/developer-preview-intro.md) only.

People Picker helps users to search and select users in Adaptive Card. You can add People Picker as input control to Adaptive Card, which works across chats, channels, task modules, and tabs. People Picker supports the following features:        

* Searches single or multiple users.
* Selects single or multiple users. 
* Reassigns to single or multiple users. 
* Prepopulates the name of selected users.

## Popular scenarios 

The following table provides popular scenarios for People Picker in Adaptive Cards and the corresponding actions:

|Scenarios|Actions|
|----------|-------------------------|
|Approval-based scenarios| To request, assign, and reassign the approval to the intended user based on the requirement.|
|Incident management| To track incidents and notify, assign, and reassign to the intended user for immediate action.| 
|Project management| To assign tickets or bugs to particular users.|
|User lookup| To search for users across the organization.|

# [Desktop](#tab/desktop)

The web and desktop client support People Picker in Adaptive Card. While searching on the web, People Picker involves an inline typing experience.

### Reassignment scenario example

User A (Robert) receives a ticket for a task in a channel and realizes incorrect assignee. User A reassigns the task that sends the information back to the bot. 

**To reassign any task**

1. Select **Reassign** where the people picker field is prepopulated with name to reassign the task to the intended user.
1. Remove the incorrect user's name. 
1. Select intended users as per the image scenario, user B (Mona), and user C (Robin) for the task. 
1. Select **Assign**. After assigning, the information is sent to the bot. 
   The bot updates Adaptive Card and notifies the intended users. 
 
The following image shows the reassignment scenario:    

![People Picker on Desktop](../../assets/images/cards/desktoppp.gif)

# [Mobile](#tab/mobile)

Android and iOS mobile clients support People Picker in Adaptive Cards. You can use People Picker in mobile to search and select user to enhance user experience. The search experience is similar to any other user selection experience in mobile.

### Reassignment scenario example

User A (Robert) receives a ticket for a task in a channel and realizes incorrect assignee. User A reassigns the task that sends the information back to the bot. 

**To reassign any task**

1. Select **Reassign** where the people picker field is prepopulated with name to reassign the task to the intended user.
1. Remove the incorrect user's name.
1. Select intended users as per the image scenario, user B (Mona), and user C (Robin) for the task.
1. Select **Done**.
1. Select **Assign**. After assigning, the information is sent to the bot. 
   The bot updates Adaptive Card and notifies the intended users. 

The following image shows the reassignment scenario: 

![People Picker on Mobile](../../assets/images/cards/mobilepp.gif)

---

## Implement People Picker

People Picker is implemented as an extension of the [Input.ChoiceSet](https://adaptivecards.io/explorer/Input.ChoiceSet.html) control. The input control includes the following selections:   

* Dropdown, such as an expanded selection.
* Radio button, such as a single selection.
* Check boxes, such as multiple selections.  

> [!NOTE]
> The `Input.ChoiceSet` control is based on the `style` and `isMultiSelect` properties.  

### Update schema

The following properties are the new additions to the `Input.ChoiceSet` schema to enable People Picker experience on the card:  

#### Input.ChoiceSet control

|Property |Type |Required |Description |
|----|----|----|----|
|**choices.data** |**Data.Query** |No |Enables dynamic auto complete for different user types, by fetching results from the dataset specified. |

#### Data.Query

|Property |Type |Required |Description |
|--|--|--|--|
|**dataset** |String |Yes |The type of data that must be fetched dynamically.|   

#### dataset
The following table provides predefined values as **dataset** for people picker:   

|dataset|Search Scope
|--|--|
|**graph.microsoft.com/users** |Search all members across the organization.|
|**graph.microsoft.com/users?scope=currentContext** |Search within the members of the current conversation, such as chat or channel in which the particular card is sent.|      

> [!NOTE]
> Currently, the search functionality for all the members across the organization is supported in 1:1 chats with bots, Adaptive Card task modules and tabs only. It is not supported in other 1:1 chats, group chats or channels.  

### Example
The code example for creating People Picker with organization search is as follows:

```json 
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        },
        {
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "size": "Medium",
      "weight": "Bolder",
      "text": "People Picker with Org search enabled"
    },
    {
      "type": "Input.ChoiceSet",
      "choices": [],
      "choices.data": {
        "type": "Data.Query",
        "dataset": "graph.microsoft.com/users"
      },
      "id": "people-picker",
      "isMultiSelect": true
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```  

The following image illustrates People Picker in Adaptive Cards with organization search:

![People Picker Org Search](../../assets/images/cards/peoplepicker-org-search.png)

To enable search within a list of conversation members, use the appropriate dataset defined in the [dataset](#dataset) table. `isMultiSelect` property is used to enable the selection of multiple users  in the control. It's set to false by default and this setting allows you to select single user only.

### Data Submission

You can use `Action.Submit` or `Action.Execute` to submit selected data to your bot. The `invoke` payload received on your bot is a list of AAD IDs or the IDs provided in static list.
In People Picker, when a user is selected in the control, the `AAD ID` of the user is the value sent back. The `AAD ID` is a string and uniquely identifies a user in the directory.

The format of the value submitted to the bot depends on the value of the `isMultiSelect` property:

|value of `isMultiSelect`|Format|
|--|--|
|false _(single select)_|<selected_AAD_ID>.|
|true _(multi select)_|<selected_AAD_ID_1>,<selected_AAD_ID_2>,<selected_AAD_ID_3>.|  

With the `AAD ID`, People Picker preselects the corresponding user. 

## Preselection of user

People Picker supports preselection of user in the control, when creating and sending an Adaptive Card. `Input.ChoiceSet` supports the `value` property that is used to preselect a user. The format of this `value` property is the same as the submitted value format in [data submission](#data-submission).  
The following list provides the information to preselect users:

* For single user in the control, specify the `AAD ID` of the user as the `value`. 
* For multiple users, such as `isMultiSelect` is `true`, specify a comma-separated string of `AAD ID`s.  

The following example describes preselection of a single user:

```json
{ "type": "Input.ChoiceSet", 
"choices": [],
 "choices.data":
 { 
   "type": "Data.Query", 
 "dataset": "graph.microsoft.com/users"
  }, 
 "id": "people-picker",
  "value": "<AAD ID 1>"
   }
```  

The following example describes preselection of multiple users:

```json
{ 
  "type": "Input.ChoiceSet",
"choices": [], 
 "choices.data":
   { 
    "type": "Data.Query",
     "dataset": "graph.microsoft.com/users" 
    }, 
  "id": "people-picker",
  "isMultiSelect": true, 
  "value": "<AAD ID 1>,<AAD ID 2>,<AAD ID 3>" 
      }
```
 
## Static choices

The static choices support scenarios where custom profiles must be inserted into the predefined datasets. `Input.ChoiceSet` supports specifying `choices` statically in the json. The static choice is used to create the choices from which the user can select.

> [!NOTE]
> Static `choices` are used with dynamic datasets. 

The choice consists of `title` and `value`. When used along with People Picker, these choices are translated to user profiles that have the `title` as the name and the `value` as the identifier. These custom profiles are also part of the search results when the search query matches the given `title`.    
The following example describes static choices: 

```json
{
	"type": "Input.ChoiceSet",
	"choices": [
		{
			"title": "Result 1",
			"value": "1000"
		},
		{
			"title": "Result 2",
			"value": "2000"
		}
	],
	"choices.data": {
		"type": "Data.Query",
		"dataset": "graph.microsoft.com/users"
	},
	"id": "people-picker",
	"isMultiSelect": true
}
```
 
You can implement People Picker for efficient task management in different scenarios.  

## See also

[Cards Reference](cards-reference.md)
