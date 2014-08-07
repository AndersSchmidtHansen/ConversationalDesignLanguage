CIxD Syntax
====================================

An experimental repository that acts as an online documentation for syntax that could be used in Conversational Interaction Design.


Syntax
-------------------------------------
When trying to translate a conversational design from words on a piece of paper to something actionable. I would imagine this to be even more important if using conversational design in a team setting. Here, it would be necessary for all members of the team to "speak" and understand the language fluently; hence a syntax guide might be helpful similar to those supplied for many programming languages.

In an attempt to keep "computer speak" at a minimum, I've given the UI the human name `Yui`. I have no idea if this is beneficial, but it feels much better than `Computer:` or `UI:`.


### Cheatsheet
For those in a hurry, here's a quick cheatsheet for the CIxD Syntax

 Interactions and Content                 | Marker      | Syntax Example
 ---------------------------------------- | ----------- | ------------------------
 Action (clicking buttons etc.)           | `[]`        | `[Delete this message]`
 Prompts (alert boxes)                    | `()`        | `(Are you sure?)`
 Notifications (before and after actions) | `/**/`      | `/* Message deleted. */`
 Referencing Objects and Properties       | `{{}}`      | `{{conversation.title}}`
 Input fields and Input Titles            | `__`        | `_Enter your key name_`
 List of Actions (like a menu)            | `[],[] and` | `[Applications],[Settings] and [Jazz]`
 Images and their Descriptions            | `;;`        | `;A cool picture of a cat;`
 Text and Body Copy                       | `----`      | `--This is some text--`
 Headlines                                | `##`        | `#Complete your sign up#`
 Default values                           | `/`         | `Your name / {{user.name}}`
 Tooltips                                 | `^^`        | `^Should contain 6 characters^`



### Actions
Actions could refer to any kind of active interaction that the user might take throughout the system, such as creating, deleting, editing something. This could be visualized by bracketing the text that reflects the action, which could look like this:

```
You: I want to [delete this message]. Can you do that for me?
```

Now we can skim the conversation and understand that a.) the user wants to do something that requires some sort of interaction and b.) the proposed phrasing of the interaction (the text on the actual button) would read "Delete this message".

### Prompts
As with Actions, most systems will prompt the user at some time, especially when the user is about to perform destructible actions such as deleting or removing something from the system. We might visualize such Prompts by wrapping them in `()`, like so:

```
Yui: Of course! But I need to know: (are you sure you want to delete it?)
```

By skimming this, we now know that a.) we must prompt the user before they can delete something and b.) the suggested phrasing of the prompt dialog window could read as the above example.

### Notifications
In between Actions and Prompts there is a layer of basic communication between the interface and the user. These small Notifications act as hints for the user to understand what has happened (and possibly also when). We could visualize Notifications by wrapping them in the same way we do comments in PHP or Javascript, like this `/**/`.

This could be written as below:

**Notifying the user that a conversation has been deleted**
```
You: [Yes, delete this conversation]
Yui: Alrighty, /*the conversation has been deleted*/
```

### Objects & Object References
In almost every modern web application the interface is built up by fetching objects from a database and expose either all, some or one part of them to the user for further manipulation. How may we add objects to a conversation? One way is to be inspired by the many modern web frameworks that use double curly brackets to referencing an object (or a part of one).

This could be written as below:


**Creating a new conversation**
```
You: Hey Yui, I want to [create a new conversation], can you do that for me?
Yui: Of course! It'll just take a short moment to set up.
```

**Deleting a conversation**

```
You: Hey Yui, I want to [delete this conversation], can you do that for me?
Yui: Sure thing, I just need to make sure: (are you sure that you want to delete {{conversation.name}}?)

* If you are sure *
You: [Yeah, delete it]
Yui: Alrighty, /*{{conversation.name}} has been deleted*/

* If not *
You: [No, don't!]
Yui: No problem, won't do that then.
```

It is now possible for me as a developer (or designer) to read through the "Deleting a conversation" piece and understand the following:

1. There should probably be an interaction point, a button maybe, with the text "Delete this conversation".

2. I then need to prompt the user "Are you sure you want to delete {{conversation.name}}?"

3. If they select the "Yeah, delete it" button, the system should then delete the file and then inform the user with the text "{{conversation.name}} has been deleted.

4. If they select "No, don't!", it should not delete the conversation and just go back to the previous screen.


### Input fields and Input Titles
```
You: Alright, I need to enter what kind of details?
Yui: First off, I need to you to _Enter your name here_, your _Preferred Username here_ and finally your _Email Address here_.
```

### List of Actions (like menus)

```
You: So, what can I do here?
Yui: Lots! Umm, in the top menu you can go to either [Applications],[Settings] and [Log Out] and in the bottom menu you can go to [About],[Privacy Policy] and [Terms of Use].
```
