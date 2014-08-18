Conversational Design Syntax
====================================

An experimental repository that acts as an online documentation for a syntax or that could be used in Conversational Design.

What is Conversational Design?
----------------------------------------------------------
Conversational Design is a "working title" I use for the method described by [Luca Leone in this great article](http://www.smashingmagazine.com/2014/07/21/how-do-you-design-interaction/) which is featured at Smashing Magazine. It is an approach to designing interfaces and interaction by writing out an everyday conversation, as if you were talking to a friend or employee in a store.

So, what is so special about this method? It activates your awesome, designer empathy superpowers very early on, way before you crank out sketches, prototypes and so on. Furthermore, Conversational Design is **ridiculously cost-effective** because, at its core, you only need yourself, a pen and paper.


So, why do you need a Syntax?
----------------------------------------------------------
A very good question with a simple answer: applicability with the real, scary world. Very often, there are many others working together to ship a digital product. Being an app, a website or something else that is interactive in some way. And it is in this situation (well also in solo-projects too) that Conversational Design falls a bit short, especially in the proces of transfering a conversational design script from simple text to actual code and design.

That's where the Syntax comes in. And it is quite simple to understand and use, with a little practice.

By wrapping parts of a conversational design script in different symbols that hold some specific meaning, we can begin to scan a script and quickly understand what we should actually make. What buttons do what, how many input fields, what phrasing we should use and so on. All before even opening a code editor or Photoshop!

Combine this with iterating the scripts until you and / or your team feels satisfied and you can save yourself a bunch of future headaches. Heck, throw in some user feedback and get real people to review your scripts before potentially wasting your time on unnecessary or confusing features. If you're courageous, I dare you to try some [Method Acting](http://www.rawnet.com/latest-news/empathetic-design-what-can-the-web-learn-from-the-method-acting-technique) with said real people to really get an idea of things.

Now, without any further ado, let's introduce the Syntax.

Syntax
-------------------------------------
When trying to translate a conversational design from words on a piece of paper to something actionable. I would imagine this to be even more important if using conversational design in a team setting. Here, it would be necessary for all members of the team to "speak" and understand the language fluently; hence a syntax guide might be helpful similar to those supplied for many programming languages.

In an attempt to keep "computer speak" at a minimum, I've given the UI the human name `Yui`. I have no idea if this is beneficial, but it feels much better than `Computer:` or `UI:`.


## Examples of Use

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

### Images and their Descriptions
```
You: I'd love to [see an example] of the product, is that possible?
Yui: Of course! Here's ;An example of the product;
```
Here I would know that the user will be clicking a button with the text "See an example", which in return should display an image with the `title` and `alt` tag containing the text "An example of the product". A coded result could look like
`<img src="/example.png" title="An example of the product" alt="An example of the product" />`

### Headlines and Text Paragraphs
Almost every interface contains some mix of Headlines and Text Paragraphs, whether for marketing purposes, descriptive purposes and so on. To write this in CD syntax, you wrap headlines in two `#` characters and paragraphs in two `--` characters. Like so:

```
Yui: #Thanks for signing up as a customer!#
Yui: --As a welcome gift, we've added 20 free credits to your account. Spend it wisely!--
```
Here I would know that the page should contain a headline, e.g. a `<h1>` tag with the text `Thanks for signing up as a customer!`. The same being true for the following text paragraph, which would probably be displayed with a `<p>` or `<span>` tag.

### Default Values
What do we do if we need to display some default text like "Your Company Name" when the user has not yet told us what it is? In CD syntax we could solve it with the `/` character, stating an "or". Like this:
```
Yui: #{{company.name}} / Your Company Name#
```
In this more complex example, I would know that here is a Headline that contains the text "Your Company Name" IF no value for `{{company.name}}` has been given. For PHP developers who use the Laravel framework this could be coded like this:
`{{{ $company_name or 'Your Company Name' }}}`

### Tooltips & Titles
Most form fields display some kind of tooltips or titles that aid the user when entering their data. How may we write this in CD? By using the caret character `^^` we can indicate something "above" another thing, like an input field. Like so:
```
You: So, what information do you need from me?
Yui: Not much, just your _Password_, which ^Must contain at least 6 characters^
```
This could translate directly into the following code:
```
<label for="input_password">Password</label>
<input type="password" id="input_password" name="input_password" title="Must contain at least 6 characters" />
```


## Cheatsheet
For those in a hurry, here's a quick cheatsheet for the CD Syntax

 Interactions and Content                 | Marker      | Syntax Example
 ---------------------------------------- | ----------- | ------------------------
 Action (clicking buttons etc.)           | `[]`        | `[Delete this message]`
 Prompts (alert boxes)                    | `()`        | `(Are you sure?)`
 Notifications (before and after actions) | `/**/`      | `/* Message deleted. */`
 Referencing Objects and Properties       | `{{}}`      | `{{conversation.title}}`
 Input fields and Input Titles            | `__`        | `_Enter your key name_`
 List of Actions (like a menu)            | `[],[] and` | `[Applications],[Settings] and [Jazz]`
 Images and their Descriptions            | `;;`        | `;A cool picture of a cat;`
 Text Paragraphs                          | `----`      | `--This is some text--`
 Headlines                                | `##`        | `#Complete your sign up#`
 Default values                           | `/`         | `{{user.name}} / Your name`
 Tooltips                                 | `^^`        | `^Should contain at least 6 characters^`



## Complementary Design Methods
To make the most out of CD and the CD Syntax, I'd definitely recommend trying the scripts you produce in combination with classic design methods and evaluate how this affects the iteration of your scripts. Methods I could definitely see as very applicable are:

- **Method Acting**
  Taking one or more of your scripts, find a friend or a potential user and act out the script with them. It might become painfully clear that your design or interaction flow is asking too much of the user, seems rude or confusing. Many e-commerce checkout processes could benefit from this approach. Just think of how strange it would be if shopping in the offline world would be if it mirrored the flow many webshops force customers through.