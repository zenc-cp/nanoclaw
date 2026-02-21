# Social Media Engagement Earning Skill

## Purpose
Automate social media engagement to build audience and generate indirect revenue through brand visibility, affiliate marketing, and content monetization.

## API Endpoints
- Base: `https://clawwork-cloud-api-sg.onrender.com`
- `GET /engage-cycle` - Run engagement cycle (like, reply, retweet)
- `POST /tweet` - Post original content
- `GET /tweet` - Get recent tweets
- `GET /scheduled-post` - Check scheduled posts
- `POST /reply` - Reply to tweets
- `POST /like` - Like tweets
- `POST /retweet` - Retweet content
- `GET /mentions` - Check mentions for engagement opportunities

## Engagement Strategy
1. Run `/engage-cycle` every 6 hours to maintain activity
2. Monitor `/mentions` for reply opportunities
3. Post AI security insights via `/tweet` daily
4. Engage with cybersecurity community for visibility

## Content Themes
- AI Security and threat landscape
- Cybersecurity best practices
- DeFi and crypto security
- Tech industry analysis

## n8n Integration
- Workflow: NanoClaw Earning Pipeline v4.0
- Node: Social Engage Cycle
- Schedule: Every 6 hours via Schedule Trigger

## Revenue Path
- Phase 1: Build 1K+ followers through consistent engagement
- Phase 2: Affiliate links in valuable threads
- Phase 3: Sponsored content and partnerships
- Target: $100-300/month from social monetization

## Configuration
- X automation status tracked in `/dashboard` under x_automation
- Currently: configured=false (needs X API credentials)
- Required env vars: X_API_KEY, X_API_SECRET, X_ACCESS_TOKEN
