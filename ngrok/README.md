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

Then, authenticate ngrok with your account token:
```
ngrok config add-authtoken <your_ngrok_auth_token>
```
E.g.: 
```
ngrok config add-authtoken 2tA89LzU3gZxKudtb5Acljij6WD_7NLdKZ2soDpVqhpUzQdcT
```
You may also need to add your **credit card** for verification. 

## Setup
Create a .sh file:
```
nano ngrok.sh
```

Write the following:
```
cd /usr/local/bin
./ngrok tcp 22 # for ssh purpose
```
Save and close the file. Then, add execute permission:

```
chmod +x ngrok.sh
```

## Run ngrok
```
./ngrok.sh
```
The terminal will show ngrok information:\
Next to `Forwarding`, you should see something like: *tcp://x.tcp.yyy.ngrok.io:zzzzz -> localhost:22*.\
where:\
- `x` is a single-digit number
- `yyy` is the region
- `zzzzz` is a 5-digit port number

On your remote machine (i.e. the computer you want to use to control the above computer), open a terminal and run:
```
ssh <your_username>@x.tcp.yyy.ngrok.io -pzzzzz
```
E.g.
```
ssh athena@6.us-cal-0.ngrok.io -p18893
```
where:\
- `athena`: username
- `6`: the single-digit number
- `us-cal-0`: the region
- `18893`: the 5-digit port number
