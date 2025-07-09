# ngrok

## Install
[official website of ngrok](https://dashboard.ngrok.com/get-started/setup/linux)

```
curl -sSL https://ngrok-agent.s3.amazonaws.com/ngrok.asc \
  | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null \
  && echo "deb https://ngrok-agent.s3.amazonaws.com buster main" \
  | sudo tee /etc/apt/sources.list.d/ngrok.list \
  && sudo apt update \
  && sudo apt install ngrok
```

```
ngrok config add-authtoken 2tA89LzU3gZxKudtb5Acljij6WD_7NLdKZ2soDpVqhpUzQdcT
```
You may need to add your credit card for verification. 
