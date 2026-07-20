from telegram import Update, ReplyKeyboardMarkup
from telegram.ext import Application, CommandHandler, MessageHandler, ContextTypes, filters


TOKEN = "8883253659:AAHE_EpXz_GC8gUUsLKXZR15b1BcEx8pnJ8"

CARD = "6062561024304431"

ADMIN = "@velorixtem"

CHANNEL = "https://t.me/+V7-EcY6c3YQxNjM8"


async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):

    keyboard = [
        ["🛒 خرید اشتراک", "💎 قیمت‌ها"],
        ["💳 پرداخت", "👤 پشتیبانی"],
        ["📢 کانال ما"]
    ]

    await update.message.reply_text(
        "🔥 Velorix VPN 🔥\n\n"
        "⚡️ فروش اشتراک VPN پرسرعت\n"
        "🔐 اتصال امن و پایدار\n\n"
        "یکی از گزینه‌ها را انتخاب کنید 👇",
        reply_markup=ReplyKeyboardMarkup(
            keyboard,
            resize_keyboard=True
        )
    )


async def buttons(update: Update, context: ContextTypes.DEFAULT_TYPE):

    text = update.message.text


    if text == "💎 قیمت‌ها":

        await update.message.reply_text(
            "💎 قیمت Velorix VPN\n\n"
            "🟢 تک کاربر ماهیانه\n"
            "💰 165,000 تومان\n\n"
            "🔵 دو کاربر ماهیانه\n"
            "💰 250,000 تومان"
        )


    elif text == "🛒 خرید اشتراک":

        keyboard = [
            ["🟢 تک کاربر ماهیانه"],
            ["🔵 دو کاربر ماهیانه"]
        ]

        await update.message.reply_text(
            "🛒 پلن خود را انتخاب کنید:",
            reply_markup=ReplyKeyboardMarkup(
                keyboard,
                resize_keyboard=True
            )
        )


    elif text == "🟢 تک کاربر ماهیانه":

        await update.message.reply_text(
            "🟢 پلن تک کاربر انتخاب شد\n\n"
            "💰 مبلغ: 165,000 تومان\n\n"
            "💳 شماره کارت:\n"
            f"{CARD}\n\n"
            "بعد از پرداخت عکس رسید را ارسال کنید ✅"
        )


    elif text == "🔵 دو کاربر ماهیانه":

        await update.message.reply_text(
            "🔵 پلن دو کاربر انتخاب شد\n\n"
            "💰 مبلغ: 250,000 تومان\n\n"
            "💳 شماره کارت:\n"
            f"{CARD}\n\n"
            "بعد از پرداخت عکس رسید را ارسال کنید ✅"
        )


    elif text == "💳 پرداخت":

        await update.message.reply_text(
            "💳 شماره کارت:\n\n"
            f"{CARD}\n\n"
            "بعد از پرداخت رسید را ارسال کنید."
        )


    elif text == "👤 پشتیبانی":

        await update.message.reply_text(
            f"👤 پشتیبانی:\n{ADMIN}"
        )


    elif text == "📢 کانال ما":

        await update.message.reply_text(
            f"📢 کانال رسمی:\n{CHANNEL}"
        )



async def receipt(update: Update, context: ContextTypes.DEFAULT_TYPE):

    await update.message.reply_text(
        "✅ رسید شما دریافت شد.\n\n"
        "⏳ پس از بررسی پرداخت، اشتراک شما فعال می‌شود.\n\n"
        "👤 برای دریافت کانفیگ بعد از تایید پرداخت به پشتیبانی پیام دهید:\n"
        f"{ADMIN}"
    )



app = Application.builder().token(TOKEN).build()


app.add_handler(CommandHandler("start", start))

app.add_handler(
    MessageHandler(filters.TEXT, buttons)
)

app.add_handler(
    MessageHandler(filters.PHOTO, receipt)
)


print("🔥 Velorix VPN Bot Running...")

app.run_polling()
