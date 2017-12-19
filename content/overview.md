+++
title = "Overview"
date = 2017-12-19T14:05:02+01:00
draft = false
[menu.main]
	name = "Overview"
	parent = "About"
	weight = 1
+++

## History
I started managing my finances using a spread sheet, but soon wanted something more.
Since I was a student I started using [YNAB](https://www.youneedabudget.com/) because they offered a free year.
After the year had passed, I wanted to continue using such a service,
but didn't see why I should pay so that someone else gets all my financial information.

After some searching I found a great open-source project called [Firefly-III](https://firefly-iii.org/) which I used for some time.
It was quite happy with it. Of course there were a couple of things I would have done differently,
but overall I was satisfied so I used it.

As the number of small things that annoyed be started to grow
I decided I have to take matters into my own hands. Since Firefly is built using PHP,
which I don't really want to use, I decided to built something from scratch using Django which is written in Python.


## Relationship to Firefly
If you compare Firefly-III to SilverStrike you will find things in common. This starts with the [design](https://html5up.net/editorial) of this site and the used [UI framework](https://adminlte.io/) for the app itself. This is not at all intended to be a rip-off.
It should rather be considered the result of a search for options with the outcome that the people behind Firefly decided to use awesome stuff, for which I didn't find any similar/superior alternatives. Since I wanted to jumpstart everything I started with things I knew others are using.

Don't be mistaken by the looks, there are a couple of smaller and bigger differences...

If you are happy with Firefly-III there really is no reason to switch. It is a very nice project with a very active developer backing it. If you feel the same about the things mentioned below, I welcome you to try SilverStrike and see if it's a better fit for you or not.


## Differences to Firefly
Things that I consider better in SilverStrike:

* SilverStrike is built on **Python and Django**, which I consider to be more userfriendly and easy to develop in. (This is a totaly personal opinion, and doesn't affect end users at all)
* By using Django, a **rest API** is easily integrated using the [django-rest-framework](http://www.django-rest-framework.org/). This enabled others to write applications that can interact with SilverStrike easily.
Things that I plan to implement in the future are:
	* A **generic client** that can be used to easily import transactions from banks without having to provide any private information to a server
	* A **mobile application** so I can manage everything from a native application on my phone. The primary target is Android, but this is still something in the future.
* Better support for **sharing access**. I am married and thus my wife should also have access to all the stored information.
Firefly does support multiple users, but each user gets their own data. Sharing can only be done by sharing credentials. The goal behind SilverStrike is to enable better sharing of the data. Currently all users have access to all the data, but proper multi-user support is on the roadmap, so one instance can serve multiple households where multiple persons can be part in multiple/different households.
* Proper support for **recurring transactions**. Firefly only has a notion of bills, that are used to match against created transactions. I prefer having support for all kinds of transactions (Deposits, Withdrawls, Transfers) so I can have a better overview of what is expected to happen in the future.

Things that you can consider Firefly to be (currently) superior at:

* Firefly has **categories, budgets and tags**. I don't need all that. I'm not convinced all of this distinction is needed,
SilverStrike only supports one kind, which is a category which can then also be used as a budget. A notion of tags might be added in the future, but I currently don't see how I would use it.
* Firefly has a much more advanced **import functionality**. Currently SilverStrike only has a method to import data from Firefly, because I used it to transfer all my data. More is to be supported but currently isn't, mainly because I don't need it.
* Firefly allows you to create a vast number of **reports**. SilverStrike doesn't support any reports at the moment.
Such a functionality will be implemented in the future, but since I currently don't need it, it's not on top of the list.
* Firefly has the notion of **piggy-banks**. I like that, and want to implement it in SilverStrike as well. I'm not yet entirely sure how I want to model and display it...
* Firefly has **multi-currency support**. I currently don't need it, and probably won't need it in the near future. I'm not opposed to it, but I'm not sure how this is best implemented, so I didn't tackle it yet (maybe never will...)
* Firefly supports **cryptocurrencies**. Currently SilverStrike doesn't because amounts are limited to two decimal places.
I'm not inclined to change that until they really become widespread.
* Firefly has an advanced **search funtionality**. I don't need it, the builtin django-admin allows it, so I didn't implement it in the user frontend yet. Probably will come sometime in the future, it just isn't a priority yet.
* Firefly **encrypts some information**. SilverStrike doesn't. Passwords are of course stored encrypted, but all other data you enter, is stored as is in the database. I don't see the necessity of it for primarily self hosted software. If someone really wants it, and can show me how to do that in a transparent and secure way using Django I might consider adding that.