---
title: 4 tricks to be a more efficient data scientist
date: 2020-08-29
cover_image: cover_IMG_5793.jpg
slug: simple_tricks
---

Since transitioning from an academic background to doing data science in industry to leading teams of data scientists, I've learned all manner of exciting things. I've also had _many_ ☕️ chats (recently more virtual than in person)[^1] with people who want to get into data science who ask me what skills they need to join the field. There's no [dearth](https://blog.udemy.com/11-data-scientist-skills-in-demand-today/?utm_source=adwords&utm_medium=udemyads&utm_campaign=DSA_Catchall_la.EN_cc.US&utm_content=deal4584&utm_term=_._ag_95911180068_._ad_436653296108_._kw__._de_c_._dm__._pl__._ti_dsa-392284169515_._li_1016367_._pd__._&matchtype=b&gclid=EAIaIQobChMI85aFkvSL6wIVUr7ACh0UWA-0EAAYAyAAEgIvE_D_BwE) [of pages](https://blog.udacity.com/2014/11/data-science-job-skills.html), [blog](https://towardsdatascience.com/the-most-in-demand-skills-for-data-scientists-4a4a8db896db) [posts](https://towardsdatascience.com/top-10-skills-for-a-data-scientist-in-2020-2b8e6122a742), [etc.](https://www.simplilearn.com/what-skills-do-i-need-to-become-a-data-scientist-article) [about](https://www.mastersindatascience.org/data-scientist-skills/) [all](https://www.edureka.co/blog/data-scientist-skills/) [the skills](https://www.kdnuggets.com/2018/05/simplilearn-9-must-have-skills-data-scientist.html) that some people think are needed for a successful interview or career in data science. While I might quibble with some of the recommendations in those links, by and large those skills are important.

This post takes a decidedly different perspective. These are not skills that are super cutting edge machine learning or a fancy new algorithm or something that will wow people at a party. These are skills that don't (often) come up in an interview[^2]. But each and every one of these will make your job and your life **so** much easier that it's worth taking the time and learning to be comfortable with them. Depending on your workflow, you will either use them constantly so learning them well at first will pay dividends every day; or they are things that you do only so rarely that it'll feel like you need to relearn them each time. In either case, having a grasp of them will help you work faster and make you less frustrated. 

You're going to look through the headings and think to yourself "Oh, please, none of this is all that hard!" but rest assured: over the years of helping new (and even some not-so-new) data scientists, I've seen many folks struggle with each of these at one point or another. Sometimes taking hours or days to get out of a fumbled git merge or spend days going back and forth with IT about how they haven't given them access to a server when their ssh keys weren't in the right place. 

## git
Though other kinds of (distributed) version control systems exist, `git` is the one that is used most widely. `git` is massive, has a huge number of features, and can be used to do some really powerful things. Fortunately for us is that you can accomplish a lot just by knowing what it is and by mastering about five commands. Everything outside of those will (generally) come up very infrequently and you can Google for the answer.

### What it is

`git` is a distributed source control system. This sounds fancy, but in reality it is a place to store your work as well as the history of your work as you've worked on it. On top of that, `git` lets you work on multiple things at once without disrupting each other with branches and you can collaborate with others in ways that won't (usually) overwrite each other's work. [There lots of benefits to using `git` that I won't go into here.](https://happygitwithr.com/big-picture.html#why-git)

### The most important commands

You can use `git` on the command line, in which case the commands below are all preceded by `git` and (sometimes) followed by a url, file, or other argument (e.g. `git clone https://github.com/jonkeane/repo.git`). There are also a number of `git` GUI clients that can be helpful for viewing what's going on. If you're using RStudio's IDE (and you're in a project that is a `git` checkout) there's even a minimal `git` client in the Git pane[^3].

* `clone` — this is how you download the contents of a repository that already exists (e.g. on GitHub or GitLab)
* `pull` — this gets any updates that have happened on the server since the last time you `pull`ed
* `add` — this adds files that you have either created or changed in your local `git` repository  directory
* `commit` — this marks changes that you've added with `git add` for inclusion in the repository. Think of this as a save point.
* `push` — this takes all of your commits and sends them to the server (typically GitHub or GitLab)
* `checkout` — this is most useful for creating a new branch (with the `-b` flag + the branch name) to work on some code or to switch between branches (with no flag, just the branch name)

A typical workflow is something like:

* Start working by `clone`ing the repository.
* Start a branch for new work with `checkout -b`.
* Do some work, `add`, `commit`, and then `push` that work (and then repeat this step until you're happy).
* Once you're satisfied with your change, you can merge the changes you made on your branch into your main branch with an (ill-named) [pull request](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/about-pull-requests) in GitHub or a [merge request](https://docs.gitlab.com/ee/user/project/merge_requests/) in GitLab.

### Sure, but how does this help me?

It takes some getting used to, but once you begin using `git` regularly it becomes natural. If `git` is part of your workflow even occasionally, not having to think about what's going on or look up what the next command is will speed up your work. 

But wait, there's more! As you use `git` more (especially as you use branches and you commit frequently) you get the benefit of having history that you can look back through to see how things have changed: no more `script_final_final_v3_final.R`, no more giant chunks of commented code that were useful at some point (though do they work with the new data ingestion and cleaning that has changed since then? 🤷️).

Even after that, using `git` unlocks a bunch of other tools and tricks like using `git` tags to release versions, using GitHub Actions or Travis to run automated checks (or build your code, or publish your website, or almost anything else you can have a computer do).

### How to practice

Get started by putting a project (a personal project, a website with [hugo](https://gohugo.io) or [blogdown](https://bookdown.org/yihui/blogdown/)) up on GitHub or GitLab. As you work on it, practice making branches, making frequent commits, merging the branches into your main branch, etc.

### Resources
* [happygitwithr.com](https://happygitwithr.com)
* [learngitbranching.js.org](https://learngitbranching.js.org)
* [How to fix things when things have gone wrong](https://sethrobertson.github.io/GitFixUm/fixup.html)
* [Gitkraken git client](https://www.gitkraken.com)

## ssh keys

Just like keys in the physical world, ssh keys are used to unlock and gain access to systems and services. They work with [clever bits of cryptography that let you authenticate with two small files](https://en.wikipedia.org/wiki/Public-key_cryptography), your private key and your public key. The public key is something that you can send to systems and people which will let them grant you access without allowing them to be able to impersonate you. You can think of this as analogous to a lock in the key-and-lock analogy. Your private key should be kept secret and kept only on computers that you control. This is your key in the key-and-lock analogy.

ssh keys are used for a bunch of connection types (these all use `ssh` under the hood, hence why they use your ssh keys, but they all look very different at the interaction level, so I'm listing them out):

* using `ssh` to connect to a remote computer to execute commands
* using `git` to [connect to a git server (e.g. GitHub)](https://happygitwithr.com/ssh-keys.html)
* moving files to remote computers with many file transfer protocols: `scp`, `rsync`, etc.
* all kinds of other communication with remote computers (e.g. port forwarding)

[Creating ssh keys](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent), using them regularly, and feeling comfortable with where they live, what they are, and what's important about them will make it so you don't have to stumble around getting access to remote systems. And if you're using `git`, it's one of the easiest way to not have to type your password in constantly, so you'll want to set it up!

### How to practice

A good first step is to create a key for yourself and try adding it to various services (e.g. GitHub); each one is slightly different, but doing that setup process will make you familiar with your public and private keys, what kinds of things you need to do with them, and what it looks like when everything is setup correctly. You can also set up ssh access with ssh keys to a remote computer you have access to.


## SQL

SQL is not the spiffy new kid on the block—it's been around for ages. There is even a [whole group of technologies that explicitly set themselves apart from SQL](https://en.wikipedia.org/wiki/NoSQL) with the label NoSQL[^4]. But in practice, accessing data through SQL of some sort is still the most widespread way that people interact with data. 

People use SQL to refer to a bunch of different things: the query language[^5] itself, the ANSI/ISO standard(s) that define SQL, (typically traditional) databases that utilize relational models (e.g. PostgreSQL, MariaDB/MySQL, SQLite). For the purposes of this post, I will use it to refer to the general concept and shape of the query language.

SQL is a large and wide-ranging topic with many deep rabbit holes one could explore depending on the specific implementation. What's important for anyone working with data are—just like with git—the basics: how to retrieve the data you're looking for, how to filter, how to join different tables together. There's a lot more that you'll pick up over time (and then each implementation has it's own special things), but if you're confident with the basics you'll be able to do 90% of your work, and learning the more complicated aspects of SQL will be easier.

Here is all the SQL you really need to know:

* [`SELECT column1, column2 FROM table`](https://www.w3schools.com/sql/sql_select.asp) is the simplest form of a query: get columns from a table
* [`WHERE`](https://www.w3schools.com/sql/sql_where.asp) limits the rows that you get by some condition (or conditions with `AND` and `OR`). Some of the syntax for specifying conditions besides `=`, `>`, `<`, etc. can be funny and dialect-dependent, but that's what Google is for.
* [`JOIN` and `ON`](https://www.w3schools.com/sql/sql_join.asp) when the data you're after isn't all in one table, you want to join two tables together. This matches the rows from one table to the rows from another table using some common column[^6].
* [`GROUP BY`](https://www.w3schools.com/sql/sql_groupby.asp) When you want to collapse the rows from a table down to a smaller set. When you do this, for any column that is in your `SELECT` clause but not your `GROUP BY` clause, you'll need to use a function that picks a single value like `DISTINCT`, `MIN`, `MAX`, `AVG`[^7]. So say we have a table with orders, with at least one column for year and one column for order amount, if we wanted to get the total orders by year, we can `SELECT SUM(order_amount), year FROM orders GROUP BY year;`

The best part of all of this is that there are [numerous](https://prestodb.io) [applications](https://aws.amazon.com/athena/) that aren't traditional databases that expose a SQL-like syntax. With these your ability to SQL like a pro unlocks querying across massive distributed data systems or flat files as if they were a database.

Knowing SQL is a skill that will come up a lot and having a firm grasp on the basics will make your daily life easier, even if it isn't as exciting sounding as many data science tasks. Knowing it will help make it so that fetching the data doesn't get in the way of those more exciting data science tasks.

### How to practice

If you're not already working with SQL, take some time and set up some data you care about in a database (SQLite is a file-system or memory-based database that works well for learning these things). If you don't have data, and you're using R you can use [{dbplyr}'s](https://dbplyr.tidyverse.org) functions [`dbplyr::nycflights13_*()`](https://dbplyr.tidyverse.org/reference/nycflights13.html) to put the {nycflgiths13} data into a database for you.

If you're already used to using `{dplyr}` + `{dbplyr}` together, you're already using SQL under the hood. If you're more comfortable with {dplyr} syntax, try writing out some transformations and then you can use [`dbplyr::show_query()`](https://dplyr.tidyverse.org/reference/explain.html) to see what query that pipeline generated.

### Resources

* [w3schools SQL tutorial + documentation](https://www.w3schools.com/sql/default.asp)
* [SQL Fiddle for writing and testing SQL](http://sqlfiddle.com)


## Start simple, scale up

One very common mistake I see people make is that they start working with their full data set straight away[^8]. But in many circumstances starting to work on a project and using all of the data you ultimately want to use is almost surely going to slow you down. Data cleaning, transformations, and even just pulling your data can be time intensive and computationally expensive. 

If you start off with all of your data, each step you try out as you're building up your work will take more time to run. This sounds "only" inconvenient, but it's actually distracting: getting instant feedback that something worked and focusing on that task will make it quicker to solve as opposed to moving on to do something else while a step churns. Worse than that, you're susceptible to start trying to optimize each step as you write it out for the first time. And now you're in a new and different rabbit hole distracting from the main task at hand. Though this sounds efficient ("I'm writing the optimized code once, instead of slow code and then having to redo it later!"), it almost never works out like that. One obvious example is: some of the transformations you make you might be able to cut entirely (say that variable turns out to not be helpful no matter how it's transformed in your model). *No computation* is always faster than even the most optimized computation.

This is less of a skill than a way of working more efficiently. Though there are fewer technical things to practice, but a few things help to do this successfully:

* Only pull the data you need — If you're pulling from a database filter to a small subset while you're working on the code, take off that filter when you're ready to run the full analysis. (and while you're at it, only pull the columns you really care about, you don't always need to `SELECT *` on every table!)
* Use sampling if you already have your data — In R use [`sample`](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/sample)) or {dplyr}'s [`sample_n()`](https://dplyr.tidyverse.org/reference/sample.html) to make it smaller.
* Try and get a draft of code that goes from beginning to end of the model/analysis/etc. as quickly as possible — even if it's incomplete or wrong, you'll have a better understanding of the general problems to solve and you'll typically write better, more focused code at each step after seeing the whole thing in action

## Conclusion
Taking the time to learn these skills well will pay dividends in the future. They take tasks that involve them from pesky things that you kinda know what's going on to things that you can confidently do without having to think too much about it. And by removing the extra cognitive burden of thinking about these things (or effectively relearning them when they come up) means you will have more time to do things you like doing: building an amazing data visualization, fitting a new model, or exploring some new data.


[^1]: And I genuinely enjoy these: If you are looking to get in to data science send me an email or a [twitter DM](http://twitter.com/jonkeane). I can especially help people transitioning from academia (and extra especially from social science research). I would also especially like to help any folks from any kind of under-represented group in tech or data science.
[^2]: Though they aren't frequently part of formal interviews, they are some times treated as table-stakes, so if it comes up and you flub an answer it could go very negatively. For me, when I'm interviewing for roles, I will use understanding of these as a guide for how much spin up time people will need to get proficient and started with things. Sometimes a role is being filled early enough that mentally booking a few weeks at the beginning to learn these things is possible.
[^3]: Calling it a git client is a bit of a stretch, it basically only does the commands I talk about above + has some interface for seeing file differences. But in reality, this is about 90% of my git usage total. Git really is almost all these very simple interactions.
[^4]: Though this name is a bit confusing: [some "NoSQL" databases actually support SQL (or at least SQL-like) queries](https://www.couchbase.com/products/n1ql). What most of the NoSQL databases share is that they are not centered around relational connections within the data. Some even use the names non-relational or NoREL to capture this fact.
[^5]: There is a huge amount of diversity such that many of the different dialects of SQL might actually be better thought of as their own language — though even with human languages, the division between dialect and language is a fraught one.
[^6]: ...or multiple columns! Why stop at just one?
[^7]: Don't even get me started that this is (almost always) a mean, but you have to dig through the docs to figure that out. If you want a median you (usually) ~~have~~ get to implement that on your own.
[^8]: Even to this day I find myself starting off this way, until I catch myself.