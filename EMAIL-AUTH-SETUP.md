# Activate Archon email/password authentication

The email login/signup/password-reset pages are implemented. They remain disabled by the API until a Supabase Auth project is configured. Existing ChatGPT sign-in continues to work.

1. Create a Supabase project and enable the email/password provider with email confirmation.
2. In Auth URL configuration, set Site URL to the Archon origin and add `https://rehearse-building-twin.divyanshu21522.chatgpt.site/signin.html` to allowed redirect URLs.
3. Configure an email sender (SMTP) and check the provider's sending limits before inviting external users.
4. Set hosted runtime values `SUPABASE_URL` (the project's HTTPS *.supabase.co URL) and `SUPABASE_PUBLISHABLE_KEY` (publishable key; legacy anon key can also work). Never use a service-role or secret key here. Redeploy to apply the values.
5. Test signup, confirmation email, sign-in, reset email, password change, logout, and cross-account building access with two real email accounts.

Email accounts use separate owner IDs (`email:<provider-user-id>`) from existing ChatGPT accounts. Matching email strings do not merge accounts or grant access to existing buildings. The app validates identity with the provider before accessing private data. Session tokens are in Secure, HttpOnly, SameSite=Lax cookies. Passwords are sent to the provider via the server and are not stored in Archon's database.

Production email delivery has not been verified without a configured project and sender. The confirmation/reset callback uses the provider's implicit email flow; token fragments are removed from the browser address bar before processing. Provider email templates must retain the supported confirmation link and redirect.
