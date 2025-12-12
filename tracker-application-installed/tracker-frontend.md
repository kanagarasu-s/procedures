## tracker-frontend:
## tracker project location

```
 /var/www/html

```

## clone git repo

```
git clone https://github.com/SQ1Security/tracker-frontend.git

```
## create .env file

```
VITE_APP_BACKEND_BASE_URL=http://beta.bellita.co.in:8085/api/
VITE_APP_BACKEND_FILES_URL=http://beta.bellita.co.in:8085/evidences/
VITE_APP_TAB_TITLE=Pro 1
VITE_APP_SECRET_KEY=541f8551773b2f6a7cd5434d9fb51ad9bbb1cca3be49df30bea6bd08a0d54729
GENERATE_SOURCEMAP=false
VITE_APP_CLIENTR=1
# VITE_APP_ANTHEM_ELEVANCE_A1=11
# VITE_APP_ANTHEM_ELEVANCE_A2=12
VITE_APP_ANTHEM_ELEVANCE=14
VITE_APP_HUMANA=13
VITE_APP_LIBERTY=18
VITE_APP_PROMINENCE=17
VITE_APP_HUMANA_WAVE_2=16

```

## Install build essentials

```
sudo apt update
sudo apt install -y build-essential

```
## Install NVM (Official Script)

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

```

## Load NVM into your shell

```
source ~/.bashrc

```

## Verify NVM installation

```
nvm -v

```
## Install Node.js with NVM

```
nvm install --lts

```
## Set the default Node version

```
nvm use 18
nvm alias default 18

```
