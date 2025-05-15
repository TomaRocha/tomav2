# PRD: Ask-Me-Anything (AMA) SMS Bot – Reactive Prototype

**Product Owner:** Dave Rocha
**Prototype Goal:** Clickable demo that lets a dealer sign up, send live-like SMS, and preview ticket workflows—all in < 5 minutes.

---

## Project Overview

**Project Name:** Ask-Me-Anything (AMA) SMS Bot – Reactive Prototype
**Target Audience:** Dealership service managers, BDC representatives, parts and service advisors at automotive dealerships seeking low-risk AI adoption.
**Core Features:**

* Self-serve signup wizard with pretend CDK integration
* AI-driven SMS “Ask Me Anything” bot (parts, warranty, status, DIY guidance)
* Dual-tab ticket UI (AI Chat + Internal staff pings)
* NPS survey & heat-case/promoter tracking
* Instant ROI dashboard (calls deflected, \$ saved, consents)
* Locked-upgrade path for full customer communications suite

**Tech Stack for Lovable:**

* **Frontend:** React + Tailwind CSS
* **State Management:** localStorage + in-memory mocks
* **Edge Functions:** AI Edge Function (for future BDC supercharge & GPT API integration)
* **API Stubs:** Mocked Twilio SMS endpoint, DMS/CDK stub, VIN lookup stub
* **Hosting:** Vercel / Lovable serverless
* **Demo Data:** JSON file (`demoTickets.json`) driving seeded tickets and responses

---

## 1 · Executive Summary

• **Problem:** Dealers drown in 5 % of inbound inquiries (parts, warranty, status). Toma’s AMA SMS Bot deflects these via AI text, fetching staff answers without calls.
• **Goal:** Prototype a no-login, SMS-first experience that:

1. Signs up in < 2 min, fakes DMS connect, sends first SMS.
2. Handles 5–10 demo inquiries via dual-tab threads (AI Chat + Internal pings).
3. Captures explicit opt-in & consent metrics.
4. Ends with ROI dashboard (calls deflected, \$ saved, NPS).
   • **Upgrade Path:** Greyed “Customer Comms” tab + upgrade CTA dead until full suite launch.

---

## 2 · Customer & Dealer Journeys

### 2.1 Dealer Onboarding (5 min value path)

1. **Landing Page:** “Kill 5 % of inquiry calls with AI SMS in 5 min.” Click **Try Demo**.
2. **Signup Wizard:** Enter dealership name, hours, contacts, CDK key (optional → Skip).
3. **Pretend DMS Connect:** “Connecting to CDK…” spinner → “Connected.”
4. **Launch:** “Your AMA Bot is live. Send first SMS to your phone” → triggers welcome SMS.
5. **Ticket UI:** Opens demo queue with seeded tickets; dealer sees AI Chat & Internal tabs.
6. **Upgrade CTA:** Greyed “Customer Comms” tab hints at full suite purchase.

### 2.2 Customer Conversation Flow (SMS only)

* **Bot Intro:** “Hi Alex, it’s Dublin Toyota AMA Bot. Ask me anything about your Camry!” (includes opt-out/STOP)
* **Inbound Questions:** Bot interprets intent, pings staff when needed, and replies with staff-supplied or GPT-canned answers.
* **Consent Tracking:** Customer replies YES to call or marketing prompts; bot logs consent for future features.

### 2.3 Post-RO & NPS Loop

* **RO Close Event:** Demo host clicks **Close RO** → triggers NPS SMS: “0–10 likely to recommend?”
* **Promoter Path (9–10):** Bot texts “Would you share a short comment?” → survey reply appears in dashboard testimonials.
* **Detractor Path (0–6):** Bot pings manager’s cell + marks heat case in dashboard.

---

## 3 · Prototype Scenes & Interactions

| Scene  | Trigger                       | UI Element                         | SMS Demo Phone             | Notes                          |
| ------ | ----------------------------- | ---------------------------------- | -------------------------- | ------------------------------ |
| **0**  | Load `/`                      | Landing page + **Try Demo**        | —                          | Hero text + video placeholder. |
| **1**  | Click Try Demo                | 3-step wizard                      | —                          | CDK stub connect.              |
| **2**  | Click **Launch Bot**          | Toast “RO #123 created”            | —                          | Seeds `roOpen`.                |
| **3**  | Auto-send welcome SMS         | —                                  | “Ask me anything…”         | Twilio stub.                   |
| **4**  | “Send parts question”         | Ticket #101                        | “Do you have brake pads?”  | Seeds ticket.                  |
| **5**  | Internal Tab                  | “Checking parts…”                  | —                          | Flags `awaitingReply`.         |
| **6**  | Staff types “Yes, 4 in stock” | Internal tab updates               | —                          | Sets `staffReply`.             |
| **7**  | Bot answer                    | AI Chat tab shows reply            | “Pads in stock…”           | Clears `staffReply`.           |
| **8**  | “Send status ask”             | New ticket #105                    | “Status on my Civic?”      | Bot asks for ping/call.        |
| **9**  | Tap **Ping advisor**          | Internal ping & staff reply        | —                          | Bot relays update.             |
| **10** | Click **Close RO**            | Dashboard “NPS survey sent”        | “How likely to recommend?” | Stores NPS=10.                 |
| **11** | Reply **10**                  | Dashboard “Promoter” + testimonial | —                          | Shows green badge.             |
| **12** | Bot texts marketing ask       | —                                  | “Want oil-change deals?”   | Logs consent.                  |
| **13** | **Fast-forward 90 days**      | Ticket #109                        | “How replace filter?”      | Bot DIY + YouTube.             |
| **14** | Hover **Customer Comms**      | Greyed + tooltip “Upgrade soon”    | —                          | Dead link.                     |

---

## 4 · Seed Data & Mock Stubs

1. **demoTickets.json:** defines #101–#109, intents, pings, staffReply placeholders, bot replies.
2. **DMS Stub:** `/api/connectCDK` → `{connected:true}` after 1.2 s.
3. **VIN Stub:** `/api/vinLookup/:vin` → canned recall/warranty.
4. **SMS Layer:** Twilio sandbox for texts.
5. **State Machine:** flags `awaitingStaff`, `awaitingCust`, `npsSent`, `demoMode` via `?demo=true`.

---

## 5 · UI Components

* **LandingPage**, **SignupWizard**, **Toast**
* **DashboardNav** (metrics tiles + icons)
* **TicketList** (real-time highlights)
* **TicketDetail** with tabs: *AI Chat* + *Internal* (plus greyed *Customer Comms*)
* **MiniPhoneSim** – parallel SMS thread
* **Quick-Actions:** WARRANTY, RECALL, UPSELL buttons
* **Consent Icons:** Blue SMS check, Grey phone, Red heat-case, Green promoter.

---

## 6 · Success Criteria

1. **Flow Completion:** Scenes 2–10 < 4 min.
2. **Perceived Value:** ≥ 80 % cite “saves time.”
3. **Upgrade Hooks:** ≥ 2 clicks on greyed CTA.
4. **Realism:** SMS sim + typing dots feel credible.

---

## 7 · Tech & Scaling Notes

* **Edge Function for BDC Supercharge & Future GPT Integration:** Lovable AI Edge Function will host GPT API key and power advanced ticketing in later phases.
* **Infrastructure:** React/Tailwind front-end, Lovable serverless for mocks, localStorage for state.
* **Prototype Only:** No real data retention, SLAs, or security beyond demo.

---

## 8 · Next Steps

* Provide `demoTickets.json` & component list to dev.
* Record landing video.
* Dry-run with sales team; refine timing/messaging.

*This PRD is ready for upload to Lovable to drive the reactive prototype build.*
