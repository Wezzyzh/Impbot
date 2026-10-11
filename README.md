# IMP — Root Community App

IMP is a custom app built for my community on [Root](https://www.rootapp.com/). It brings welcome messages, member statistics, and a join history into one community app channel.

This repository contains **Stage 1**. Chat moderation and support are planned features; their tabs currently show placeholders.

## Features

- **Welcome messages:** Personalized text using the member and community names.
- **Member statistics:** Total members and online/offline counts when Root makes status information available.
- **Join history:** Recorded joins with a member name, profile picture, time, and welcome text, with more entries loaded as you scroll.
- **Staff recognition:** The community owner and configured staff roles or members can see the moderation tab.
- **Persistent storage:** Join history is stored in the app's SQLite database.

Welcome messages are displayed inside the app. This version does not post welcome messages to chat, moderate messages, or handle support tickets.

## Requirements

- Node.js 22 or newer and npm.
- A Root account and an app registered in the [Root Developer Portal](https://dev.rootapp.com/).
- The **Manage Apps** permission in the community where the app will be installed.

## Setup

Run the following commands from the app folder containing `package.json`. If you downloaded the Stage 1 ZIP, this is the `imp-app` folder.

1. Register an app in the Root Developer Portal.
2. Replace `your-app-id` in `root-manifest.json` with your app ID.
3. Create a developer token and set it in `server/.env`:

   ```dotenv
   DEV_TOKEN=your-developer-token
   ```

4. Install dependencies, prepare the networking packages, and build:

   ```sh
   npm run setup
   ```

Keep developer tokens private. Do not commit your populated `.env` file or put tokens in client code.

For subsequent builds:

```sh
npm run build
```

## Local development

Start the Root development host in one terminal:

```sh
cd server
npm run server
```

Start the client in a second terminal:

```sh
cd client
npm run client
```

The project also includes a standalone preview using mock data:

```sh
cd client
npm run preview:build
```

The preview build is written to `client/dist-preview`. Demo data does not reflect a live Root community.

## Customize and install

Edit `server/src/welcome.config.json` to change the welcome template. Supported placeholders are `{member}` and `{community}`. Rebuild and upload a new package after changing it.

To create a Root package, run this from the app folder:

```sh
npx rootsdk build package
```

Upload the generated `.pkg` file through Root's developer workflow and install the app in your community. Configure **Staff-Rollen** in the app settings to select staff roles or individual members. The community owner is always treated as staff.

Root hosts the published app's server and datastore, with a separate instance for each installing community.

## Tests

From the app folder:

```sh
npm test
```

The supplied tests cover staff access decisions, welcome text rendering, and join storage with pagination.

## Privacy and current limitations

The app stores Root user IDs, display names, profile-picture references, recorded join times, and welcome text. The join history is visible to members who can access the app, rather than being restricted to staff.

Stage 1 has no automatic retention period or built-in deletion interface. Leaving the community does not automatically remove a member's join records. Deletion handling needs to be addressed before relying on the app to fulfil deletion requests.

Online status depends on what Root exposes to the viewing member. Counts may be unavailable or incomplete; they should not be treated as a full activity log.

This version contains no AI, advertising, or analytics integration. Although AI assisted development, the supplied app does not send member data to an AI service.

Read the [Privacy Policy](PRIVACY.md) for details. Root's hosting does not remove the app operator's responsibilities under Root's terms or applicable law.

## Contact

Questions or privacy requests: **herzog.luca@hotmail.com**.
