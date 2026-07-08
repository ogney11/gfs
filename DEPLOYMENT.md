# Discord Bot Deployment on Fly.io

This guide explains how to deploy your Discord bot to Fly.io.

## Prerequisites

- [Fly.io account](https://fly.io/app/sign-up)
- [flyctl CLI installed](https://fly.io/docs/hands-on/install-flyctl/)
- Discord bot token stored in your `config.py`

## Deployment Steps

### 1. Install flyctl

If you haven't already, install the Fly.io CLI:

```bash
curl -L https://fly.io/install.sh | sh
```

### 2. Authenticate with Fly.io

Log in to your Fly.io account:

```bash
flyctl auth login
```

### 3. Launch the App (First Time Only)

Initialize and create your app on Fly.io:

```bash
flyctl launch
```

During the launch process:
- Confirm the app name: `my-strike-bot`
- Confirm the region: `waw`
- Choose **No** when asked to set up a database
- Choose **No** when asked to set up Redis

This creates the app and generates the initial configuration.

### 4. Set Environment Variables

If your bot uses environment variables (e.g., Discord token), set them:

```bash
flyctl secrets set DISCORD_TOKEN=your_token_here
```

Or if using multiple secrets:

```bash
flyctl secrets set VAR1=value1 VAR2=value2
```

View all secrets:

```bash
flyctl secrets list
```

### 5. Deploy the App

Deploy your bot using:

```bash
flyctl deploy
```

This will:
- Build the Docker image
- Deploy it to the specified region (waw)
- Start the bot

### 6. Monitor the Bot

View live logs:

```bash
flyctl logs
```

Check app status:

```bash
flyctl status
```

View detailed information:

```bash
flyctl info
```

## Updating the Bot

After making changes to your code:

```bash
flyctl deploy
```

The bot will be updated with your latest changes.

## Troubleshooting

### Bot crashes or won't start
Check the logs:
```bash
flyctl logs -a my-strike-bot
```

### Need to restart the bot
```bash
flyctl restart
```

### SSH into the running instance
```bash
flyctl ssh console
```

### Remove the app
```bash
flyctl apps destroy my-strike-bot
```

## Configuration Notes

- **App Name**: `my-strike-bot` – Change this in `fly.toml` if desired
- **Region**: `waw` – Europe (Warsaw). Change in `fly.toml` if you prefer another region
- **Internal Port**: `8080` – Set for Fly.io requirements (not used by Discord bot)
- **Dockerfile**: Uses Python 3.11 slim for minimal image size

For more information, visit: https://fly.io/docs/
