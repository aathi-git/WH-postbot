import telegram
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

TELEGRAM_TOKEN = '5998394878:AAGHcuuSteT4lqyZhZOxy7j56zxYqAEn1Ss'
TELEGRAM_CHANNEL_ID = '-1001815444289'

def start(update, context):
    context.bot.send_message(chat_id=update.effective_chat.id, text="Welcome to the Amazon Product Poster Bot!")

def post_product(update, context):
    context.bot.send_message(chat_id=update.effective_chat.id, text="Please enter the Amazon product URL:")
    context.bot.send_message(chat_id=update.effective_chat.id, text="Please enter the product name:")
    context.bot.send_message(chat_id=update.effective_chat.id, text="Please enter the product price:")

def handle_user_input(update, context):
    user_input = update.message.text
    context.user_data[update.message.chat_id] = context.user_data.get(update.message.chat_id, {})
    context.user_data[update.message.chat_id]['input'] = context.user_data[update.message.chat_id].get('input', {})

    if 'product_url' not in context.user_data[update.message.chat_id]['input']:
        context.user_data[update.message.chat_id]['input']['product_url'] = user_input
        context.bot.send_message(chat_id=update.effective_chat.id, text="Please enter the product name:")
    elif 'product_name' not in context.user_data[update.message.chat_id]['input']:
        context.user_data[update.message.chat_id]['input']['product_name'] = user_input
        context.bot.send_message(chat_id=update.effective_chat.id, text="Please enter the product price:")
    elif 'product_price' not in context.user_data[update.message.chat_id]['input']:
        context.user_data[update.message.chat_id]['input']['product_price'] = user_input

        # Post the product details on the channel
        product_url = context.user_data[update.message.chat_id]['input']['product_url']
        product_name = context.user_data[update.message.chat_id]['input']['product_name']
        product_price = context.user_data[update.message.chat_id]['input']['product_price']

        message = f"Product: {product_name}\nPrice: {product_price}\n\n{product_url}"
        context.bot.send_message(chat_id=TELEGRAM_CHANNEL_ID, text=message)

        # Reset the user input data
        del context.user_data[update.message.chat_id]['input']

def main():
    updater = Updater(TELEGRAM_TOKEN, use_context=True)
    dispatcher = updater.dispatcher

    dispatcher.add_handler(CommandHandler('start', start))
    dispatcher.add_handler(CommandHandler('post', post_product))
    dispatcher.add_handler(MessageHandler(Filters.text, handle_user_input))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
