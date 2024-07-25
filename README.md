# chasm_node_ColonyAirdrops   
---
Use these commands one by one
```bash
sudo apt update && sudo apt upgrade -y
```
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```bash
sudo apt install screen -y
```
```bash
 curl -s https://ngrok-agent.s3.amazonaws.com/ngrok.asc | sudo tee /etc/apt/trusted.gpg.d/ngrok.asc >/dev/null && echo "deb https://ngrok-agent.s3.amazonaws.com buster main" | sudo tee /etc/apt/sources.list.d/ngrok.list && sudo apt update && sudo apt install ngrok
```
- Now paste the command, you copied earlier from ngrok website (example : `ngrok config add-authtoken yourauthtoken`)
```bash
screen ngrok http 3001
```
- Go to forwarding section and copy the first URL and save it somewhere (It will look like `https://1bXX.XX.XXX.XXX.ngrok-free.app`)
- Press `Ctrl + A + D` to detach from screen session
```bash
nano .env
```
- Copy this format and paste the required value there, you copied earlier from different websites
```bash
PORT=3001
LOGGER_LEVEL=debug

ORCHESTRATOR_URL=https://orchestrator.chasm.net
SCOUT_NAME=YOUR NAME
SCOUT_UID=PASTE UID
WEBHOOK_API_KEY=PASTE API KEY
WEBHOOK_URL=PASTE NGROK FREE APP URL LINK HERE
PROVIDERS=groq
MODEL=gemma2-9b-it
GROQ_API_KEY=PASTE GROK API KEY HERE
```
- Save this file using `Ctrl + X` then `Y` and then press `Enter`
```bash
docker pull chasmtech/chasm-scout:latest
```
```bash
docker run -d --restart=always --env-file ./.env -p 3001:3001 --name scout chasmtech/chasm-scout
```
```bash
docker logs scout
```
```bash
curl localhost:3001
```
```bash
source ./.env
curl -X POST \
     -H "Content-Type: application/json" \
     -H "Authorization: Bearer $WEBHOOK_API_KEY" \
     -d '{"body":"{\"model\":\"gemma2-9b-it\",\"messages\":[{\"role\":\"system\",\"content\":\"You are a helpful assistant.\"}]}"}' \
     $WEBHOOK_URL
```
- Done !!
- Telegram - https://t.me/colonyairdrops

- Credits - @EBA
