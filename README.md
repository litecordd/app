# Nexus

Nexus is a Discord-inspired chat app with registration/login, profiles, selectable/uploadable avatars, custom profile frames, badges, channels, server boosts, and a five-guess Nitro number game.

## Run locally
1. Install Node.js 18 or newer.
2. Open a terminal in this folder and run `npm install`.
3. Run `npm start`.
4. Visit http://localhost:3000.

## Developer access
Set `DEV_USERNAMES` before starting the server to allow named accounts to receive the developer badge on registration. Example (PowerShell):
`$env:DEV_USERNAMES="yourusername"; npm start`
Linux/macOS:
`DEV_USERNAMES=yourusername npm start`

Developers can create custom badges with a symbol, color, name, and optional description through the `/api/dev/badges` API. The `⛊` developer badge is displayed next to the name. Do not expose the development API to untrusted users.

## Notes
- Data is stored in `nexus-data.json` beside the server.
- This is a starter project, not a production-hardened public service. Before internet deployment, add rate limiting, CSRF protection, persistent sessions, moderation/reporting, backups, and stronger operational controls.
- The server includes private-message API routes (`/api/dms/users`, `/api/dms/:userId`) ready for a DM interface.
- Nitro is a free guessing game: five guesses, 1–10,000, warmer/colder feedback. Boosting is restricted to Nitro users.


## Servers and developer badge tools

- Use the **+** button in the left server rail to create a separate server. Each server has its own channels, messages, boost count and channel limit.
- Select a server using its icon in the left rail.
- To enable the Developer role for a new account, set `DEV_USERNAMES` before starting the server. Example:
  - Windows PowerShell: `$env:DEV_USERNAMES="rainga"; npm start`
  - macOS/Linux: `DEV_USERNAMES=rainga npm start`
- The developer role is assigned when the listed username registers. Existing accounts do not automatically gain the role; for a local test, use a fresh database/account or migrate the account's `badges` array to include `dev` in `nexus-data.json` while the server is stopped.
- Only accounts with the server-side `dev` badge can see **Settings → Developer Tools** and create custom badges/grant them to registered usernames. The server also enforces the role on the badge API, so hiding the UI is not the only protection.

## Channel badges and roles
- In **Settings → Developer Tools**, you can grant an existing badge to a username, create a new badge for a channel, or add an existing badge to a channel.
- When creating a channel, choose which server roles are allowed to type. Leaving every role unchecked allows all members to type.
- Server owners and developers can open **Settings → Server Roles** to create roles and assign roles to a member by username.
- New servers start with Member, Moderator, and Admin roles. The server owner is assigned Admin automatically.
- Channels are stored per server and should remain listed when switching between channels or servers.
