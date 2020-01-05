# Firebase Authentication Architecture

## Swimlane diagram

Throttling and robots checks that Google provide on their side
The client credentials can't be abused
Don't share your admin credentials on the client side
Check tokens
Don't store tokens in your server side database, let firebase deal with it.
Key your user database by the firebase user id
Anonymous users are great, you are allowed up to 1,000,000 and might need to clean them up progressively. You can merge anonymous users into full users.