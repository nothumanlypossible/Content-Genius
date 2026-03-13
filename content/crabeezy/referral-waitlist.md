# Crabeezy — Referral Waitlist Program

**Goal:** Turn each waitlist signup into a source of 2–3 additional signups through a structured referral mechanic
**Type:** Pre-launch waitlist referral (position-based incentive)
**Compatible with:** Supabase (no external referral platform required for MVP)

---

## Why a Referral Waitlist Works for Crabeezy

Crabeezy is a hyper-local product. The best marketing is a friend in Maryland telling another Maryland friend that fresh crabs are available direct from a waterman nearby. A referral mechanic channels that natural word of mouth into a measurable loop.

The Chesapeake Bay community has strong local pride and food culture. "Jump the line" and "early access" mechanics work especially well when the product is place-specific — people feel like they're getting in on something local before the crowds arrive.

---

## Incentive Design

### Mechanic: Position-Based "Move Up the List"

**How it works:**
- Every waitlist member gets a unique referral link
- For each person they refer who signs up, they move up X spots on the waitlist
- The earlier they get access, the fresher the catch they can pick from on launch day

**Why this works over cash/credit:**
- Pre-launch: You have no revenue to give credits against
- Position-based rewards cost you nothing and create urgency
- The waitlist position itself becomes a status symbol ("I'm #47")
- Natural FOMO: "I need to move up before launch so I get the best selection"

### Reward Tiers

| Referrals | Reward |
|-----------|--------|
| 1 referral | Move up 10 spots + "Founding Buyer" badge in app |
| 3 referrals | Move up 25 spots + First Month Free Delivery (if delivery is offered) |
| 5 referrals | Move up 50 spots + Invited to a private "first catch" event at a waterman's dock |
| 10+ referrals | Top of list + named recognition in the app ("Crabeezy Pioneer") |

**Adjust tiers based on your waitlist size.** If you have 200 people, 10-spot jumps feel meaningful. If you have 2,000, scale proportionally.

---

## Implementation Plan (Supabase + No External Tool)

This is an MVP referral system you can build without a dedicated referral platform. It uses Supabase, your existing landing page, and a short Supabase Edge Function.

### Database Schema

```sql
-- Add to your existing waitlist table, or create:

CREATE TABLE waitlist (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  email TEXT UNIQUE NOT NULL,
  first_name TEXT,
  referral_code TEXT UNIQUE NOT NULL,  -- unique 8-char code per user
  referred_by TEXT,                    -- referral_code of who referred them
  referral_count INTEGER DEFAULT 0,    -- how many they've referred
  position INTEGER,                    -- waitlist position (lower = earlier access)
  signed_up_at TIMESTAMPTZ DEFAULT NOW()
);

-- Index for fast referral code lookups
CREATE INDEX idx_referral_code ON waitlist(referral_code);
```

### Referral Code Generation (Edge Function)

```javascript
// Supabase Edge Function: generate-referral-code.js
// Called when user signs up for the waitlist

function generateCode(email) {
  // Simple deterministic code from email — swap for crypto.randomUUID() slice if preferred
  return btoa(email).replace(/[^a-zA-Z0-9]/g, '').substring(0, 8).toUpperCase();
}

// On signup: INSERT into waitlist with referral_code = generateCode(email)
// If ?ref=CODE in URL, set referred_by = CODE, then increment referral_count on the referrer
```

### Referral Link Format

```
https://crabeezy.com/waitlist?ref=YOURCODE
```

When someone visits this URL and signs up:
1. Their `referred_by` field is set to `YOURCODE`
2. The referrer's `referral_count` is incremented by 1
3. The referrer's `position` is updated (moved up by your tier amount)

### Position Assignment

```sql
-- Assign position on signup (simple sequential):
INSERT INTO waitlist (email, first_name, referral_code, position)
VALUES ($1, $2, $3, (SELECT COALESCE(MAX(position), 0) + 1 FROM waitlist));

-- Move up on referral:
UPDATE waitlist
SET position = GREATEST(1, position - 10)  -- move up 10 spots, floor at 1
WHERE referral_code = $referred_by_code;
```

---

## If You Don't Want to Build It Yourself

Use **dub.co** for link tracking (free tier available) paired with a simple Google Sheet or Airtable to track referral counts manually. Not as automated, but zero engineering time.

The integration guide for dub.co is at `tools/integrations/dub-co.md` in this repo.

---

## Share Copy

Write these into your waitlist confirmation email (Email 1 of the waitlist sequence) and embed them directly in the referral widget.

### Share Copy — Email

> Subject: Get crabs before everyone else — share this
>
> Hey [Name],
>
> You're on the Crabeezy waitlist. Fresh crabs, direct from Maryland watermen, coming soon to an app near you.
>
> Want to move up the list? Every person you refer jumps you 10 spots closer to day-one access.
>
> Your personal link: [referral_link]
>
> The higher your spot, the more watermen you'll have to choose from on launch day.

---

### Share Copy — Text Message

> "I'm on the waitlist for Crabeezy — fresh Maryland crabs direct from the waterman, no middleman. You should get on it. Use my link and we both move up: [link]"

---

### Share Copy — Facebook (for sharing in groups or on timeline)

> Just got on the waitlist for Crabeezy — a new app that lets you buy fresh crabs directly from Maryland watermen. No wholesaler, live map of what's available near you. If you want crabs that were actually pulled this morning, this is it. Get on the list: [link]

---

## Referral Program Landing Page Copy

Add this block to your existing waitlist/landing page after the signup form.

---

**Tell a friend. Move up the line.**

Every person you refer moves you 10 spots closer to the front.

The early spots get first pick of watermen on launch day. The best catch sells fast.

Your referral link: `[unique link]` ← [Copy]

[Share via Text] [Share on Facebook] [Share via Email]

---

## Announcement Email to Existing Waitlist

Send this to everyone already on the list to launch the referral mechanic.

```
Subject: New: move up the Crabeezy waitlist
Preview: Every person you refer bumps you 10 spots.

Hey [First Name],

Quick update:

You're on the Crabeezy waitlist. We appreciate that.

We just added a referral mechanic — for every person you bring in, you move up 10 spots on the list. The earlier your spot, the more watermen you'll have available on day one.

Your personal link: [referral_link]

Refer 1 person → +10 spots
Refer 3 people → +25 spots + Founding Buyer badge
Refer 5 people → +50 spots + invite to a private dock event

The list is first come, first served on launch day. Make your move.

— The Crabeezy Team
```

```
CTA: [Copy my referral link] → [copies link to clipboard]
```

---

## Success Metrics

| Metric | Target |
|--------|--------|
| % of waitlist who share at least once | 15–25% |
| Average referrals per active sharer | 2–4 |
| Waitlist growth from referrals vs. organic | 30–50% from referral |
| Conversion: referral signup → app download | Should be higher than organic (referred users are warmer) |

---

## Fraud Prevention (Simple)

For a pre-launch waitlist with no money changing hands, fraud risk is low. Basic guards:
- One signup per email address (enforce at database level with UNIQUE constraint)
- Rate limit the referral endpoint (max 100 signups via one code without manual review)
- Optional: Add email verification step before referral credit is applied
