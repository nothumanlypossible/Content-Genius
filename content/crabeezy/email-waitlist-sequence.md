# Crabeezy — Waitlist Email Sequence

**Sequence type:** Pre-launch lead nurture
**Trigger:** User signs up for the Crabeezy waitlist
**Goal:** Keep waitlist warm and primed to download and buy on launch day
**Length:** 5 emails over ~3 weeks
**Platform:** Any email tool (Mailchimp, Kit, Resend, etc.)

---

```
Sequence Name: Crabeezy Pre-Launch Waitlist
Trigger: Waitlist form submission
Goal: Activate buyer on launch day (app download + first order)
Length: 5 emails
Timing: Immediate, +3 days, +7 days, +12 days, T-2 days before launch
Exit Condition: User downloads app OR launch day passes
```

---

## Email 1 — Welcome + What You're Getting Into

```
Send: Immediately after signup
Subject: You're on the Crabeezy list. Here's what that means.
Preview: Fresh crabs, direct from the waterman who pulled them this morning.
```

Hey [First Name],

You just joined the Crabeezy waitlist.

Here's what that actually means:

When we launch, you'll be among the first people who can open an app, see a live map of Maryland watermen selling fresh catch near you, and buy direct — straight from the person who pulled the trap.

No wholesaler. No warehouse. No guessing if it's actually fresh.

Every seller on Crabeezy is verified through their DNR commercial fishing license. So when you buy, you know it's legal, local, and caught by someone who's been working these waters for years.

We're bringing a handful of watermen on first, then opening the map to buyers like you.

Stay tuned — we'll let you know the moment you can order.

— The Crabeezy Team

P.S. Know someone else who'd want early access? Forward this to them. The more buyers on the list, the more watermen we can bring on.

```
CTA: [Share with a friend] → [referral link or mailto]
```

---

## Email 2 — The Story

```
Send: 3 days after Email 1
Subject: He's been doing this for 30 years. Now he keeps more of what he earns.
Preview: Meet the kind of waterman you're buying from on Crabeezy.
```

Hey [First Name],

I want to tell you about the kind of person you're buying from when you use Crabeezy.

His name is [Name]. He's been working the Chesapeake Bay out of [Location] for over 30 years — same as his father before him.

Every morning he's up before 4am. On the water by dawn. Pulling traps by sunrise.

Then he sells his catch to a wholesaler for whatever price they're offering that day.

He doesn't set the price. He doesn't know the buyer. He doesn't know if what he caught will be on a table in Maryland or sitting in a warehouse in another state.

He gets a check — eventually — and moves on.

That's how it's worked his entire life.

Crabeezy is different. When [Name] lists a haul on the app, he sets the price. Buyers near him see his name, his location, his catch. They order. He gets paid the same day.

He's not a supplier anymore. He's a business owner with direct customers.

That's what you're supporting when you buy through Crabeezy. A real person. A real tradition. A fair deal for the person who did the work.

— The Crabeezy Team

```
CTA: None (story email — no sell)
```

---

## Email 3 — How It Works

```
Send: 7 days after Email 1
Subject: Here's exactly how ordering on Crabeezy works
Preview: Open app → find fresh catch near you → order in 60 seconds.
```

Hey [First Name],

A few people have asked how Crabeezy works. Here's the simple version:

**Open the app.**
You'll see a live map of Maryland watermen who have fresh catch available near you — right now, today.

**Tap a listing.**
You'll see the waterman's name, location, what they've got, how much, and the price. Every seller has been verified through their DNR commercial license, so you know it's the real thing.

**Order in about 60 seconds.**
Pay securely through the app. Arrange pickup at the dock or ask about delivery — that's between you and the waterman.

**Get the freshest crabs you've had.**
Because the person who listed that catch pulled it this morning.

That's it.

No calls. No driving around hoping someone's open. No wondering if it's actually fresh.

We're getting the last few watermen set up and then we're opening it up to the list.

You'll be notified the day it's live.

— The Crabeezy Team

```
CTA: [Forward to a friend who loves crabs] → [share link]
```

---

## Email 4 — Momentum + Social Proof

```
Send: 12 days after Email 1
Subject: [X] watermen are ready. Are you?
Preview: The map is filling up. Here's where things stand.
```

Hey [First Name],

Quick update before we flip the switch:

We now have **[X] verified Maryland watermen** on Crabeezy — from [County] to [County], Chesapeake Bay to the tidal rivers.

They're ready to list. Some already have their first hauls queued up.

We're [holding back launch / opening the list in batches] to make sure the first buyers have a great experience — not a half-empty map.

Here's what early waitlist members are saying:

> "Finally. I've been trying to find a good local source for years. This is exactly what I needed." — [Name, location]

> "I can't wait to buy direct from a waterman. I had no idea this was even possible." — [Name, location]

We're getting close.

When we open, it'll be waitlist-first. You're already on it.

— The Crabeezy Team

```
CTA: [Share with someone who wants in] → [referral link]
```

---

## Email 5 — Launch Countdown

```
Send: 2 days before launch date
Subject: You're getting access in 48 hours.
Preview: The map goes live [Day]. Here's what to do first.
```

Hey [First Name],

This is it.

Crabeezy opens to waitlist members in **48 hours** — [Launch Day], [Date].

Here's what to do the moment the app is live:

1. **Download Crabeezy** from the App Store or Google Play
2. **Open the map** — you'll see fresh hauls available near you
3. **Tap a listing and place your first order**

The first people to order will be buying from watermen who've been on the water since before sunrise.

That's dock-to-dish. That's what you signed up for.

We'll send you the download link the moment the app goes live.

See you on launch day.

— The Crabeezy Team

P.S. Know someone who missed the waitlist? Forward this to them — we'll let as many people in as we can on day one.

```
CTA: [Add to calendar: Crabeezy launches [Date]] → [calendar link]
```

---

## Metrics to Track

| Metric | Benchmark to aim for |
|--------|---------------------|
| Email 1 open rate | 50–60% (welcome emails are highest) |
| Email 1 share rate | 5–10% forward/share |
| Email 2 open rate | 35–45% |
| Email 3 open rate | 30–40% |
| Email 4 open rate | 30–40% |
| Email 5 open rate | 50–60% (launch anticipation) |
| Launch day app download rate from list | Target: 20–30% of waitlist |

---

## Implementation Notes

**Platform recommendations (compatible with your Supabase stack):**
- **Resend** — developer-friendly, works well with Supabase edge functions, easy API integration
- **Kit (ConvertKit)** — strong for creator/waitlist sequences, easy automation without code
- **Mailchimp** — familiar, drag-and-drop, works for a first launch without complex automation

**Personalization fields needed:**
- `[First Name]` — required on signup form
- `[X]` in Email 4 — pull from your Supabase waterman count at send time, or hardcode to the current number

**Trigger setup:**
- Email 1: Send immediately on form submission
- Emails 2–4: Time delays (set in your email tool as days after Email 1)
- Email 5: Send manually OR set to trigger on a specific date (your launch date minus 2 days)
