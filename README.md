# Dear Future Recovery Reader

A standalone page that helps you recover a Dear Future preserved message using your **Recovery Kit** and **recovery key**.

It runs locally in your browser. It does not contact Dear Future, Supabase, Vercel, Stripe, Next.js, React, Node, or any other backend.

## What it is for

Dear Future gives you a Recovery Kit so your preserved message is not only tied to your account.

This reader lets you:

1. Open the Recovery Reader.
2. Choose or paste your Recovery Kit.
3. Enter your recovery key if needed.
4. Recover your message.
5. Check whether the recovered message matches the saved proof code.

## What you need

You need the Recovery Kit you downloaded from your private Dear Future receipt page.

The Recovery Kit may include:

- your recovery key
- your preserved record
- your message proof code
- your message id
- your preservation references

The Recovery Kit is private. Keep it somewhere safe and do not share it unless you want someone else to be able to recover the message.

## How to use it

1. Open `index.html` in a modern browser such as Chrome, Edge, Firefox, or Safari.
2. Choose your Dear Future Recovery Kit `.txt` file.
3. If the fields are not filled automatically, open the Recovery Kit and paste the preserved record into the page manually.
4. Check that your recovery key is filled in.
5. Click **Recover message**.
6. Look for **Match confirmed**.

If the reader says **Match confirmed**, it means the recovered message matches the saved proof code from the kit.

If the match is not confirmed, check that you used the correct Recovery Kit and recovery key together.

## Does it send my key anywhere?

No.

This reader is designed to run locally in your browser. Your recovery key and recovered message are not sent to Dear Future or any server.

You should still only use the reader on a device you trust.

## What the match result means

The Recovery Reader checks the recovered message against the saved message proof code.

If it says:

```txt
Match confirmed