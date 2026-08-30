---
date: '2026-07-03T00:00:00Z'
draft: false
title: 'Skid Detector — Privacy Policy'
toc: false
---

---

**Effective date:** 3 July 2026

**Applies to:** the "Skid Detector" Discord application operated by the Hard Way Hacking and Coding (HWHC) moderation team, within the HWHC Discord community.

Skid Detector is a **self-hosted moderation assistant**. It helps human moderators find low-effort, malicious, or rule-breaking ("skid") messages by running message text through a locally-hosted AI model and flagging likely matches for a moderator to review and act on. This policy explains exactly what data it touches, what it keeps, why, and how you can opt out.

## 1. Scope

- Skid Detector runs in **one Discord guild** (the HWHC community) that it is explicitly configured for. It ignores messages from every other server.
- It **does not read direct messages (DMs)**.
- It only processes messages in the specific channels its moderators have chosen to watch, and it **skips messages from trusted/exempt members** (see §6).

## 2. What the bot accesses

To do its job the bot receives, from Discord's API:

- **Message content** — the text of messages in watched channels, from non-exempt members. Used to classify whether a message is likely a "skid" message.
- **Author identity** — the message author's Discord user ID and username, so a flagged message can be attributed and moderators can act on the right account.
- **Server membership and roles** — a member's roles and top-role position, used only to decide whether that member is exempt from scanning **before** their message is classified.

## 3. What is stored, where, and for how long

Skid Detector is **self-hosted on the HWHC team's own server**. There is no third-party analytics, advertising, or data-broker involvement.

**Processed in memory only and NOT stored:**

- Ambient message content that is scanned and scored. To classify a message, its text is passed to the locally-hosted AI model **in memory**; if the message is not flagged and not acted on, it is discarded — **not written to disk or logged, and not sent to any external service**.
- Membership and role data used for exemption checks.

**Stored off-platform (on the operator's server):**

- **Moderator-labeled messages.** When a moderator explicitly labels a message as "skid" or "clean" (via the message context menu or a flag button), the message text (truncated to 4,000 characters), the numeric Discord ID of the moderator who applied the label, a timestamp, and the label are stored. This is used to improve the classifier (see §4).
- **Messages that trigger a moderation action.** When a moderator takes an action on a flagged message, the flagged text is stored as a labeled training example in the same way.
- **Moderation action records** (e.g. temporary-ban expiry timers) needed to carry out and reverse actions.

Stored labeled messages are retained for as long as they are useful for maintaining the classifier. You may request deletion of data associated with your account at any time (see §7).

## 4. Use of message content for AI classification

Detection is powered by a **locally-hosted AI model** — a large language model that runs entirely on the HWHC team's own server through a local runtime (ollama). To classify a message, its text is sent **only to this on-server model**, processed in memory, and — unless the message is flagged and acted on, or explicitly labeled by a moderator — discarded.

- Message content is **never sent to any external or third-party AI provider** (such as OpenAI, Anthropic, or Google). The model runs on-premises; nothing leaves the operator's server in order to classify a message.
- **Stored, moderator-labeled message content may be used to improve detection** — for example, to refine the model's instructions and worked examples, or to train and evaluate classifier models. All such work happens on the operator's own infrastructure.
- The model, the prompts, and the underlying data are used **solely for moderation triage inside the HWHC community**, and are **never sold, shared, published, or used for any purpose outside this community's moderation.**

## 5. How data is shared

Skid Detector does **not** share your data with third parties. It is self-hosted and does not send message content to any external service. The only "processor" involved is the platform itself, Discord, whose handling of your data is governed by [Discord's Privacy Policy](https://discord.com/privacy).

## 6. Opting out

You can opt out of being scanned and stored:

- Members with a **trusted/exempt role** are never scanned and never have their content stored. Ask the HWHC moderation team for the exempt role, or use the `/skidoptout` command where available, to receive it.
- Once you hold an exempt role, Skid Detector ignores your messages entirely.

## 7. Accessing or deleting your data

To request a copy or deletion of any stored data associated with your Discord account, contact the HWHC moderation team (see §9). Because storage is limited to moderator-labeled messages and action records, most members have **no stored data at all.**

## 8. Security

Data is held on infrastructure controlled by the HWHC moderation team, with access limited to server operators and moderators. No credentials, payment data, or contact details are collected.

## 9. Contact

Questions, data-access, or deletion requests: contact the Hard Way Hacking and Coding moderation team in the [HWHC Discord server](https://discord.gg/MwVE6KffFK) (open a ModMail / ticket, or contact a moderator directly).

## 10. Changes to this policy

Material changes will be posted to this document. The "Effective date" at the top reflects the most recent revision. Continued participation in channels watched by Skid Detector after a change constitutes acceptance of the updated policy.
