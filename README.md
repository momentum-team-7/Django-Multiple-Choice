# Multiple Choice Project

This week, you will choose one of three projects to work on.

Your creativity and common sense should be used as you work. There are common features to web applications that users expect. If they are not mentioned in the project's description, you should still do them. For example: in the code snippet application, users should have avatar images. You don't have to handle file uploads yourself -- you could use Gravatar with [django-gravatar](https://github.com/twaddington/django-gravatar) -- but you need some way of handling that.

Likewise, come up with your own features to make your project unique. You will likely use this project in your portfolio, so make it stand out!

# Rules for all projects

* Your application should be styled. It should be usable and aesthetically neutral, at a minimum.
* Your application should be able to run from scratch by downloading the repo, running `poetry install`, `poetry shell`, `python manage.py migrate`, and `python manage.py runserver`. If there are any other steps necessary, please put them in a README.md file.

# The Projects

## Project 1: Code Snippet Manager

You need a good way to manage snippets of code you reuse often. You are going to build a web application that has these goals:

- Registered users can add code snippets.
- Registered users can search their own code snippets and get results.
- Each user has a profile page that shows their public code snippets. Other users can copy a snippet with one click, adding it to their library of snippets.

### How snippets work

A snippet has code (required), a language (required), a title (optional), and whatever other fields make sense. Some ideas to consider: a description or a list of tags.

If you copy a snippet by clicking the copy button (or whatever UI element is used for this purpose), there's a link back to the original snippet. The easiest way to do this is with a foreign key. One should be able to see how many times a snippet has been copied.

The reason why we copy snippets instead of "favorite" them is that they can change. The original snippet creator can edit their snippet; the copying user can edit their copy.

### How search works

Search should look for terms in the title, in other fields like a description or tags, and in the language field. If I search for "javascript auth," I should see any snippets I have about authentication using JavaScript. See [search](https://docs.djangoproject.com/en/2.1/topics/db/search/) and [full text search](https://docs.djangoproject.com/en/2.1/ref/contrib/postgres/search/) in the Django documentation for some ideas.

### How much of this is JavaScript?

This can vary, but the two parts that _definitely_ need JavaScript are syntax highlighting and copying a code snippet to your clipboard.

For syntax highlighting, check out [Prism.js](https://prismjs.com/) or [Highlight.js](https://highlightjs.org/).

See [this article on native browser copy to clipboard](https://css-tricks.com/native-browser-copy-clipboard/) for ideas on how to copy to clipboard.

## Project 2: Habit Tracker

For this project, you will build a Django application that you can use to help track and reinforce daily habits.

- Your application should have registration and login.
- Users should be able to create a new habit tracker. Each habit should have a name and a target or goal. What is this "target"? Each habit should have a daily number of some action you want to do. Some examples:
  - I want to walk 1000 steps daily
  - I want to write 100 lines of code daily
  - I want to talk to 2 new people each day
  - I want to read 200 pages daily
  - I want to sleep 8 hours daily
- Once you have habits, you should be able to make a daily record of your activity on each habit. That record should contain a date and a number for that date.
- A user can only have one record per day per habit. You will need to use [the `unique_together` option](https://docs.djangoproject.com/en/2.2/ref/models/options/#unique-together) to enforce this.
- Optimally, users can edit/update records and add records for previous days.
- Make your interface for this feature as easy to use as possible. For example, if you can choose the date for your record, have it default to the current date.
- On the detail page for a habit, you should be able to see all the records for that habit in an HTML table. Show the user whether they met their goal for that day visually somehow -- maybe via colors. Think about accessibility here -- how would a user that can't see know whether they met their goal each day?

### Some stretch goals for this project

- Add a line chart to the detail page for a habit showing your records for the last 30 days.
- On the detail page for a habit, show the best day for that habit, and the average day for that habit.
- When you list the records for a habit, show any days that don't have a record that are between the first and last record. For example, if there's a record for June 28 and a record for June 30, show June 29 as well and highlight that it has missing data. Provide a way to fill in that data easily.
- Add the ability to have "negative habits." These habits should have a goal you want to get under. For example:
  - I want to watch less than 60 minutes of TV daily
  - I want to eat less than 15 jellybeans a day
  - I want to say less than 3 curse words a day
- If a user is missing a record for a habit for the previous day, show them a message on their dashboard that lets them know and asks them to put in the record. Make it easy to jump from that message to the form to enter the data.
- Use the [new `constraints` option for models](https://docs.djangoproject.com/en/2.2/ref/models/constraints/) with `UniqueConstraint` to make the habit records unique by user, habit, and day.

### How much of this is JavaScript?

You can make your forms a lot more usable by adding JavaScript -- to begin with, you can have a button for making a record that then shows a form without reloading the page.

If you want to add charts to your habits, you'll definitely need JavaScript.

## Project 3: Flashcards

You want to make an application to help people learn via flashcards. You are going to build a web application that has these goals:

- Registered users can create multiple decks of flashcards, each with a prompt or question and an answer.
- Registered users can quiz themselves on a deck.
- Success and failure for each card is recorded.

### How decks and cards work

A user can have multiple decks of flashcards. Each deck has a title. Each flash card has a prompt or question and an answer.

When a user is quizzing themselves on a deck, they _do not_ have to type in answers. They are shown the prompt, they click to see the answer; they then mark whether they answered it correctly or not. They should see one card at a time.

When the user marks success or failure on a card, this should be recorded.

The cards should be shown in a random order at a minimum. A preferable method would be to use something like [the Leitner system](https://www.virtualsalt.com/learn10.html) for flash cards. This system uses review times; you could use that, or just use the idea of multiple boxes, with cards in lower boxes coming up more often.

### Creating decks and running through decks

This application has two very distinct parts -- creating decks and cards and then running through those decks. This is a natural place to split work. Do not forget to make creating decks and cards an easy-to-use experience.

### How much of this is JavaScript?

"Flipping" a card (you don't have to animate a card flip, although if you do, that's very cool) will almost certainly require JavaScript.

You could have a page load in between cards and reduce your amount of JavaScript. Depending on how you do this, it could also record success or failure, eliminating most of your JavaScript.
