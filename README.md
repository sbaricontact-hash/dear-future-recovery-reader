# Recovery Reader (Dear Future v2)

A **standalone static page** that decrypts **Dear Future** preserved messages **only in your browser**, using the Web Crypto API. It does not talk to Dear Future, Supabase, Vercel, Stripe, Next.js, React, Node, or any other backend.

## What it does

`index.html` is a single file containing HTML, CSS, and JavaScript. You paste:

1. **Preserved payload JSON** — usually copied from your **Dear Future Recovery Kit** `.txt` file (the JSON between `START_PRESERVED_PAYLOAD_JSON` and `END_PRESERVED_PAYLOAD_JSON`), i.e. the object that includes `encryptedPayload`, `messageId`, `contentHash`, etc.
2. **Recovery key** — in the form `dfk_v1_<base64url-32-byte-key>` (also provided in the recovery kit file).

When you click **Decrypt locally**, the page:

- Parses the JSON and the `dfenc_v2:<iv>:<tag>:<ciphertext>` string
- Derives an AES-GCM key from the recovery key material
- Decrypts with AES-GCM (ciphertext and auth tag concatenated for `crypto.subtle.decrypt`, as required by the Web Crypto API)
- Decodes plaintext as UTF-8
- Computes **SHA-256** of the plaintext and compares it to `contentHash` from the payload (with sensible normalization for hex; other encodings may show “No” until aligned with the app’s exact format)

All processing stays on your machine in the browser tab.

## How to use it

1. Save or clone this folder and open `index.html` in a modern browser (Chrome, Firefox, Edge, Safari). You can open it **directly from disk** (`file://`) or host it as a static file; no build step or server is required for decryption logic.
2. Open your **Dear Future Recovery Kit** `.txt` file.
3. Copy the JSON block between `START_PRESERVED_PAYLOAD_JSON` and `END_PRESERVED_PAYLOAD_JSON`.
4. Paste it into the **Preserved payload JSON** box.
5. Copy the `dfk_v1_…` **recovery key** from the kit file into the **Recovery key** box.
6. Click **Decrypt locally**.

If something is wrong (bad JSON, wrong key, wrong payload format), an error message is shown at the top of the form. Recovery keys are **not** written to the console.

## What data you need

1. **Preserved payload JSON** — typically what you received or exported from Code-In / your preservation flow, shaped like:

```json
{
  "app": "dear-future",
  "protocolVersion": 1,
  "messageId": "…",
  "contentHash": "…",
  "encryptedPayload": "dfenc_v2:…",
  "visibility": "…",
  "revealAtIso": null,
  "pricingTier": "…",
  "receiptMetadata": {},
  "createdAtIso": "…"
}
```

2. **Recovery key** — the `dfk_v1_…` string that was generated for that message.

The recovery kit file itself is sensitive because it contains both the recovery key and the encrypted payload.

This first version requires the preserved payload JSON. A transaction hash alone is not enough unless a future lookup feature or gateway fetch is added.

## First version: manual paste only

This version **does not** fetch payloads by transaction hash, order id, or URL. You must paste the JSON yourself.

**Possible later enhancement:** resolve a payload (or ciphertext bundle) via an **IQ / Code-In gateway** using a transaction hash or similar identifier, then feed the same decrypt path. That would add a deliberate network step and should be optional and clearly labeled when added.

## Security notes

- Use a **trusted device**.
- Anyone with **both** the preserved payload and the **recovery key** can decrypt the message offline.
- This README and `index.html` describe a tool that **does not contact Dear Future or any server** in this first version.
