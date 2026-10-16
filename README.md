# Archon — latest complete source

Green Building Digital Twin hackathon prototype. This export includes the latest published source: Home-page rotating building and green spiral, account building builder, multiple saved buildings, deletion, interactive 3D models, shared live-room demo, local person detection, calibrated fan/light checks, estimated energy, and notification code.

## Local setup
1. Install Node.js 22.13 or newer and pnpm 10.
2. In this folder run `pnpm install`.
3. Run `pnpm build`.
4. Apply each SQL file under `drizzle/` in numeric order to the local database. Example (repeat for every migration):
   `node --import ./scripts/sites-env.mjs ./node_modules/wrangler/bin/wrangler.js d1 execute DB --local --config dist/server/wrangler.json --persist-to .wrangler/state --file drizzle/0000_exotic_venom.sql`
5. Run `pnpm dev`, then open the loopback URL printed in the terminal and `/archon.html`.

Use HTTPS or localhost for camera permission. Portable development provides a mock ChatGPT sign-in; see README-Framework.md. Production ChatGPT sign-in depends on the Sites hosting dispatcher. Email/password sign-in uses Supabase Auth; see EMAIL-AUTH-SETUP.md for environment values and redirect configuration. Runtime secrets and provider settings are not included in this export. Deploying to another host requires compatible Worker/D1 bindings and authentication configuration; this is not a static-only application.

## Included and excluded
All application source, bundled Three.js/TensorFlow libraries, person-model weights, database migrations, lockfile, and tests are included. Dependencies, generated builds, Git history, database contents, deployment archives, and runtime secrets are excluded. Existing users/buildings/session records are not exported.

Push notifications require a separately configured VAPID key pair in the deployment environment: VAPID_PRIVATE_JWK (secret) and VAPID_PUBLIC_KEY. Hosted secret values are not in this ZIP. See app/api/notifications/route.ts.

## Important behavior
Fan/light vision checks require a fixed camera and calibration; AC state remains manual. Equipment switches in 3D are virtual. Energy is estimated from configured watts and runtime, not a meter reading. Camera images stay on the presenting computer. Browser, camera, and phone delivery should be tested on the devices used for judging. Notification text currently uses a generic review/test message.

## Checks
Run `node tests/buildings-api.cjs`, `node tests/building-config.cjs`, `node tests/building-collection.cjs`, `node tests/demo-api.cjs`, `node tests/live-rooms.cjs`, and `node tests/building-energy.cjs` after installing dependencies.

Source commit: 395390fadc78715f695649f6de77b34880afd685

Latest export includes the circular profile menu, simplified Home navigation, email sign-in/signup/reset integration, building selection, and deletion. Authentication provider connectivity was verified, but end-to-end email confirmation/reset and phone push delivery still require real-device testing.
