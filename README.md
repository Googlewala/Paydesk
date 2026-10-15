# Pay Desk

Calm personal payment and expense tracker. No ads, no trackers. Installable PWA.

## Deploy (about 15 minutes, free)
1. Create a free account at https://app.netlify.com and a free GitHub account.
2. Create a new GitHub repository and upload every file in this folder (keep the `netlify` folder).
3. In Netlify: Add new site > Import an existing project > pick the repository. Leave build command empty, publish directory `.`. Deploy.
4. Open the site on your phone. In Chrome choose Add to Home screen.

The app already works fully for free (tracking, history, UPI pay links). Razorpay is only needed when you start charging.

## Turn on paid plan (later)
1. Create a Razorpay account, finish KYC, and copy Test keys first.
2. In Netlify > Site configuration > Environment variables add RZP_KEY_ID, RZP_KEY_SECRET, RZP_WEBHOOK_SECRET, PLAN_PRICE_RUPEES (see .env.example). Redeploy.
3. In Razorpay Dashboard > Webhooks add `https://YOUR-SITE.netlify.app/.netlify/functions/webhook`, events payment.captured and payment.failed, using the same RZP_WEBHOOK_SECRET.
4. In index.html change `PRICING_ON:false` to `true`. Test with Razorpay test UPI, then switch to Live keys.

## Known limits
- Data is stored in the browser on each device (no login or sync yet). Next step: Supabase Auth + Postgres.
- The paid plan flag is stored on the device; move it to a database before relying on it for revenue.
- Daily reminders need push notifications and a server; not included yet.
- Razorpay Checkout collects money into your account. Paying friends and billers uses UPI links with manual confirmation.
