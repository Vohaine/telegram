from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes
import requests
from bs4 import BeautifulSoup
def get_news():
    list_news = []
    r = requests.get("https://news.mail.ru/")
    soup = BeautifulSoup(r.text, 'html.parser')
    mydivs = soup.find_all("a", {"class": "newsitem__title link-holder"})
    for news in mydivs :
        newdict = {}
        newdict["link"] = news.get("href")
        newdict["title"] = news.get("title")
        list_news.append(newdict)
    return list_news
async def hello(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text(f'Hello {update.effective_user.first_name}')

async def news(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    data = get_news()
    for item in data:
        await update.message.reply_text(f'{item["link"]}')

async def help(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text(f'Write /news to see the latest news')
    await update.message.reply_text(f'Write /politics to see the latest on politics')
    await update.message.reply_text(f'Write /economics to see the latest economic news')
    await update.message.reply_text(f'Write /society to see the latest news about todays society')
    await update.message.reply_text(f'Write /incident to see the latest updates on todays incident')
    await update.message.reply_text(f'Write /sport to see the latest sports news today')
def get_news1():
    list_news1 = []
    r1 = requests.get("https://news.mail.ru/politics/")
    soup1 = BeautifulSoup(r1.text, 'html.parser')
    mydivs1 = soup1.find_all("a", {"class": "newsitem__title link-holder"})
    for news in mydivs1 :
        newdict1 = {}
        newdict1["link"] = news.get("href")
        newdict1["title1"] = news.get("title")
        list_news1.append(newdict1)
    return list_news1
async def politics(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    data1 = get_news1()
    for item1 in data1:
        await update.message.reply_text(f'{item1["link"]}')
def get_news2():
    list_news2 = []
    r2 = requests.get("https://news.mail.ru/economics/")
    soup2 = BeautifulSoup(r2.text, 'html.parser')
    mydivs2 = soup2.find_all("a", {"class": "newsitem__title link-holder"})
    for news2 in mydivs2 :
        newdict2 = {}
        newdict2["link"] = news2.get("href")
        newdict2["title2"] = news2.get("title")
        list_news2.append(newdict2)
    return list_news2
async def economics(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    data2 = get_news2()
    for item2 in data2:
        await update.message.reply_text(f'{item2["link"]}')
def get_news3():
    list_news3 = []
    r3 = requests.get("https://news.mail.ru/society/")
    soup3 = BeautifulSoup(r3.text, 'html.parser')
    mydivs3 = soup3.find_all("a", {"class": "newsitem__title link-holder"})
    for news3 in mydivs3 :
        newdict3 = {}
        newdict3["link"] = news3.get("href")
        newdict3["title3"] = news3.get("title")
        list_news3.append(newdict3)
    return list_news3
async def society(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    data3 = get_news3()
    for item3 in data3:
        await update.message.reply_text(f'{item3["link"]}')

def get_news4():
    list_news4 = []
    r4 = requests.get("https://news.mail.ru/incident/")
    soup4 = BeautifulSoup(r4.text, 'html.parser')
    mydivs4 = soup4.find_all("a", {"class": "newsitem__title link-holder"})
    for news4 in mydivs4 :
        newdict4 = {}
        newdict4["link"] = news4.get("href")
        newdict4["title2"] = news4.get("title")
        list_news4.append(newdict4)
    return list_news4
async def incident(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    data4 = get_news4()
    for item4 in data4:
        await update.message.reply_text(f'{item4["link"]}')

def get_news5():
    list_news5 = []
    r5 = requests.get("https://www.sports.ru/")
    soup5 = BeautifulSoup(r5.text, 'html.parser')
    mydivs5 = soup5.find_all("a", {"class": "h2"})
    for news5 in mydivs5 :
        newdict5 = {}
        newdict5["link"] = news5.get("href")
        newdict5["title2"] = news5.get("title")
        list_news5.append(newdict5)
    return list_news5
async def sport(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    data5 = get_news5()
    for item5 in data5:
        await update.message.reply_text(f'{item5["link"]}')

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    await update.message.reply_text(f'Hello. Nice to have you visit. Write /help to see whats new today?')

app = ApplicationBuilder().token("5794874228:AAHkQYeFjrnpC53cM9l_ncX8-xKpJNioWPs").build()

app.add_handler(CommandHandler("hello", hello))
app.add_handler(CommandHandler("news", news))
app.add_handler(CommandHandler("help", help))
app.add_handler(CommandHandler("politics", politics))
app.add_handler(CommandHandler("economics", economics))
app.add_handler(CommandHandler("society", society))
app.add_handler(CommandHandler("incident", incident))
app.add_handler(CommandHandler("sport", sport))
app.add_handler(CommandHandler("start", start))

app.run_polling()
