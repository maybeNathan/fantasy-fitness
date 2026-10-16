# Fantasy Fitness League

Treat your fitness goals like fantasy football players. Draft weekly goals, log workouts, earn points, and climb the leaderboard.

## Features

- Draft up to 8 goals per week from 12 categories (steps, runs, gym, yoga, swim, cycling, HIIT, sleep, hydration, protein, no-sugar, team sports)
- Scaled scoring — partial points at 50% completion, full at 100%, 1.3x overachievement bonus
- Effort ratings (crushed it / solid / okay) add multipliers
- Activity log for quick workout entry
- Fake league leaderboard for motivation
- Weekly streak tracker
- All data stored in localStorage

## Install & Run

### Quick start (no build)

```bash
cd fantasy-fitness
python3 -m http.server 6142
```

Then open http://localhost:6142 on any device on your Tailscale network.

### As a systemd service

```bash
sudo tee /etc/systemd/system/fantasy-fitness.service > /dev/null <<EOF
[Unit]
Description=Fantasy Fitness League
After=network.target

[Service]
Type=simple
User=nathan
WorkingDirectory=/home/nathan/fantasy-fitness
ExecStart=/usr/bin/python3 -m http.server 6142
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now fantasy-fitness
```

### Docker

```bash
docker run -d --name fantasy-fitness -p 6142:8000 -v /home/nathan/fantasy-fitness:/app --restart unless-always nginx:alpine
```

Or with Python http.server:

```bash
docker run -d --name fantasy-fitness -p 6142:8000 -v /home/nathan/fantasy-fitness:/app --restart unless-always python:3.11-alpine sh -c "cd /app && python3 -m http.server 8000"
```

## Tech

Single-file vanilla HTML/CSS/JS app. Zero dependencies. No build step.
