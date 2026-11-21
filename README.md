# API Keys: How to Store Them Safely

A beginner's guide to keeping your API keys secret.

## What is an API key?

An API key is like a password that tells a service (weather, maps, AI) who is sending a request. If someone steals your key, they can use your account, and you may get charged or blocked.

## Rule 1: Never hardcode keys in your code

Bad:

```python
API_KEY = "sk_live_abc123"
```

Anyone who sees your code sees your key.

## Rule 2: Store keys in a .env file

Create a file named `.env` in your project folder:

```
API_KEY=your_key_here
```

Read it in Python using `python-dotenv`:

```bash
pip install python-dotenv
```

```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("API_KEY")
```

## Rule 3: Never commit secrets to GitHub

1. Create a file named `.gitignore` and add this line:

```
.env
```

2. Check before every commit:

```bash
git status
```

If `.env` appears in the list, stop and fix `.gitignore`.

3. Share a `.env.example` file instead, with fake values:

```
API_KEY=your_key_here
```

Others copy it to `.env` and add their own key.

## Rule 4: Use limited keys

Give each key only the permissions it needs, and use separate keys for testing and real use.

## What to do if a key leaks

1. **Revoke or regenerate** the key immediately in the provider's dashboard. This is called key rotation.
2. Put the new key in your `.env` file.
3. Check usage logs for activity you did not make.
4. Remove the secret from your code. Deleting it in a new commit is not enough, because git history still contains it. Rotating the key is what makes the old one useless.
5. Update your code and push again.

GitHub may also email you a secret-scanning alert if it detects a key. Treat that alert as a real leak.

## Quick checklist

- [ ] Key is in `.env`, not in code
- [ ] `.env` is listed in `.gitignore`
- [ ] `.env.example` has fake values only
- [ ] I know how to rotate my key
- [ ] I never share keys in screenshots, chats or videos
