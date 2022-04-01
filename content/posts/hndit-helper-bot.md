---
title: "I build a Telegram Bot for HNDIT students"
date: 2022-03-27T20:59:26+05:30
draft: false
tags: ["blog", "projects"]
authors: ["Pasindu Ruwandeniya"]
---

I like to try new side projects to improve my knowledge in different languages and technologies. Recently I've been learning Python and wanted to create something useful using it. I follow my HND in SLIATE and students there have no straightforward way to get the past papers. They have to rely on their libraries, other students or some broken websites to get the materials they need. So I thought why can't I fix that issue using some familiar tools which we use daily.

I thought about making this work using a popular messaging service and I chose Telegram to do that. Telegram has a ton of cool features compared to other IM services, and it has an amazing bot eco-system, plus a lot of people use that. After some digging I found out that a lot of programming languages have libraries/wrappers (I honestly don't know the correct term for that) to easily handle the Telegram API. I had two options when it came to Python.

1. [python-telegram-bot](https://github.com/python-telegram-bot/python-telegram-bot) (I think this is the most famous one because it has the most stars in GitHub)
2. [pyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI)

I chose **pyTelegramBotAPI**. It has some amazing tutorials and lot of discussions on Stack Overflow. Then I started coding.

## Structure.

I created 4 Python files to breakdown this project into smaller pieces.

1. `main.py` - The main file which execute the bot according to the commands given.
2. `pastpapers.py` - Handles outputting past papers.
3. `notes.py` - Handles outputting notes.
4. `timetables.py` - Handles outputting exam timetables.

I created 3 objects in `main.py` for each classes and called the relevant functions under `@bot.message_handler(commands=['command_name'])`.

```python
shootPapers = pastpapers.PastPapers()
shootNotes = notes.Notes()
shootTimetables = timetables.Timetables()
```

pyTelegramBotAPI also allows to to create *ReplyKeyboardMarkup*, so it makes users to follow a command flow and makes typing optional.

```python
class PastPapers():
    def select_sem(self, message):
        markup = types.ReplyKeyboardMarkup(row_width=2)
        itembtn1 = types.KeyboardButton('/1st_sem_papers')
        itembtn2 = types.KeyboardButton('/2nd_sem_papers')
        itembtn3 = types.KeyboardButton('/3rd_sem_papers')
        itembtn4 = types.KeyboardButton('/4th_sem_papers')
        markup.add(itembtn1, itembtn2, itembtn3, itembtn4)
        bot.send_message(message.chat.id, "Choose a semester:", reply_markup=markup)
```

In each Python file I have created functions to output relevant materials. That function is called inside the `main.py` according to a command.

```python
# A function in "notes.py".
def oscs_notes(self, message):
        files = ['https://drive.google.com/uc?export=download&id=1rVW3iKtuqjvK3MpQBkYa-csIyWimnrnT',
                 'https://drive.google.com/uc?export=download&id=1lxemRO1tGVgzHNtRuscDSJaaeKQUIijl',
                 'https://drive.google.com/uc?export=download&id=1dEsAhZ-BWghAO5nRiNo_uc6t-AK-WiIM']

        bot.send_message(message.chat.id, str(len(files)) + " File/s Incoming...")

        for file in files:
            bot.send_document(message.chat.id, file)
```

```python
# "oscs_notes" function is called inside "main.py".
@bot.message_handler(commands=['OSCS_notes'])
def oscs_notes(message):
    shootNotes.oscs_notes(message)
```

## Deployment.

I have deployed the bot using [Heroku](https://heroku.com/)'s free tier. First I created the `requirements.txt` file using `pip3 freeze > requirements.txt` command. Then I created the `Procfile` to let Heroku know that I want a Worker Dyno and not a Web Dyno. I have turned on the auto deploy feature on Heroku so every time I push some changes to the GitHub repository, Heroku auto redeploys the bot to the latest version.

And that's basically it. Below I have put the links to Bot's GitHub repository and the Telegram link.

[![GitHub Repo][1]][2]

[1]: https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white
[2]: https://github.com/pasindujr/HnditHelperBot 

[![Botlink][3]][4]

[3]: https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white
[4]: https://t.me/hndithelperbot