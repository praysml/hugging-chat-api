# hugging-chat-api

English | [简体中文](README_cn.md)

HuggingChat Python API

[![PyPi](https://img.shields.io/pypi/v/hugchat.svg)](https://pypi.python.org/pypi/hugchat)
[![Support_Platform](https://img.shields.io/pypi/pyversions/hugchat)](https://pypi.python.org/pypi/hugchat)
[![Downloads](https://static.pepy.tech/badge/hugchat)](https://pypi.python.org/pypi/hugchat)

Leave a star :)

Recently new updates:
- Change LLMs supported. See more at https://github.com/Soulter/hugging-chat-api/issues/56 (v0.0.9)

> When you use this project, it means that you have agreed to the following two requirements of the HuggingChat:
>
> 1. AI is an area of active research with known problems such as biased generation and misinformation. Do not use this application for high-stakes decisions or advice.
> 2. Your conversations will be shared with model authors.

**Server resources are precious, it is not recommended to request this API in a high frequency.**

(`Hugging Face's CTO🤗` just liked the suggestion)

<div align="center"><img width=500 src="https://github.com/Soulter/hugging-chat-api/assets/37870767/06e64501-02fb-4d4a-ab6f-cf18d8638ace"></img></div>

## Authentication (Required Now)

### Get Cookies

```python
from hugchat.login import Login

# login
sign = Login(email, passwd)
cookies = sign.login()
sign.saveCookiesToDir(cookie_path_dir)

# load cookies from usercookies/<email>.json
sign = login(email, None)
cookies = sign.loadCookiesFromDir(cookie_path_dir) # This will detect if the JSON file exists, return cookies if it does and raise an Exception if it's not.
```

## Usage

### Basic mode

```bash
pip install hugchat
```

```py
from hugchat import hugchat
from hugchat.login import Login

# Log in to huggingface and grant authorization to huggingchat
sign = Login(email, passwd)
cookies = sign.login()

# Save cookies to the local directory
cookie_path_dir = "./cookies_snapshot"
sign.saveCookiesToDir(cookie_path_dir)

# Create a ChatBot
chatbot = hugchat.ChatBot(cookies=cookies.get_dict())  # or cookie_path="usercookies/<email>.json"
print(chatbot.chat("HI"))

# Create a new conversation
id = chatbot.new_conversation()
chatbot.change_conversation(id)

# Get conversation list
conversation_list = chatbot.get_conversation_list()
```

The `chat()` function receives these parameters:

- `text`: Required[str].
- `temperature`: Optional[float]. Default is 0.9
- `top_p`: Optional[float]. Default is 0.95
- `repetition_penalty`: Optional[float]. Default is 1.2
- `top_k`: Optional[int]. Default is 50
- `truncate`: Optional[int]. Default is 1024
- `watermark`: Optional[bool]. Default is False
- `max_new_tokens`: Optional[int]. Default is 1024
- `stop`: Optional[list]. Default is ["`</s>`"]
- `return_full_text`: Optional[bool]. Default is False
- `stream`: Optional[bool]. Default is True
- `use_cache`: Optional[bool]. Default is False
- `is_retry`: Optional[bool]. Default is False
- `retry_count`: Optional[int]. Number of retries for requesting huggingchat. Default is 5

### CLI mode

> `version 0.0.5.2` or newer

Simply run the following command in your terminal to start the CLI mode

```bash
python -m hugchat.cli
```

Commands in cli mode:

- `/new` : Create and switch to a new conversation.
- `/ids` : Shows a list of all ID numbers and ID strings in current session.
- `/switch <id>` : Switches to the ID number passed.
- `/exit` : Closes CLI environment.
- `/llm`: get available models you can switch to
- `/llm [index]` switch model to given models

## Disclaimers

This is not an official [Hugging Face](https://huggingface.co/) product. This is a **personal project** and is not affiliated with [Hugging Face](https://huggingface.co/) in any way. Don't sue us.
