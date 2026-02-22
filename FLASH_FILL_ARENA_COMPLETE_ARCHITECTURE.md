# ⚡ YU FLASH FILL ARENA - Complete Architecture

**Version:** 1.0  
**Purpose:** Homework 2 - Multi-Agent Arena + YU Arena MVP Foundation  
**Timeline:** 3-day sprint  

---

## 📋 Table of Contents

1. [Executive Summary](#executive-summary)
2. [The Game Concept](#the-game-concept)
3. [User Experience](#user-experience)
4. [Visual Design Language](#visual-design-language)
5. [Technical Architecture](#technical-architecture)
6. [Database Schema](#database-schema)
7. [API Specification](#api-specification)
8. [Agent Behavior Logic](#agent-behavior-logic)
9. [Customer Simulation](#customer-simulation)
10. [Frontend Components](#frontend-components)
11. [File Structure](#file-structure)
12. [Deployment](#deployment)
13. [Demo Script](#demo-script)
14. [SKILL.md for OpenClaw](#skillmd-for-openclaw)

---

## Executive Summary

**Flash Fill Arena** is a real-time multi-agent competition platform where AI agents race to fill last-minute empty spots (fitness classes, appointments) before they expire. 

**Core Mechanic:**
- Operator manually creates "opportunities" (open spots)
- 5 AI agents compete to claim and fill them
- Agents use different strategies (speed, relationships, precision)
- Customers respond to offers
- Revenue gets recovered or lost forever

**Agents:**
- 🦅 **HAWK** (local) - The Spotter: Detects opportunities
- 🎯 **ACE** (local) - The Closer: Balanced hustler
- ⚡ **BLITZ** (OpenClaw) - The Risk Taker: Speed demon
- 🕸️ **WEAVE** (OpenClaw) - The Relationship Builder: Loyalty expert
- 👻 **GHOST** (OpenClaw) - The Precision Sniper: Efficiency master

**Homework Compliance:**
- ✅ Multiple agents interacting through shared API
- ✅ Deployed frontend showing real-time interaction
- ✅ SKILL.md for OpenClaw agents to join
- ✅ Visible collaboration/competition in UI
- ✅ Genuinely agentic (not scripted)

**YU Business Value:**
- Demonstrates multi-agent demand recovery concept
- Shows different recovery strategies in action
- Proves agents can coordinate in real-time
- Foundation for operator-facing MVP

---

## The Game Concept

### Core Loop (60-Second Round)

```
1. OPERATOR ACTION
   └─ Creates opportunity: "6pm CrossFit, 1 spot, $25 value"
   
2. HAWK SPOTS (0-2s)
   └─ "6PM CROSSFIT OPEN - GO GO GO!"
   
3. AGENTS RACE TO CLAIM (2-5s)
   └─ ACE: "Claimed. Mine."
   └─ BLITZ: "WHAT?! Too slow!"
   
4. WINNER CREATES DROP (5-10s)
   └─ ACE: "Setting price at $18, 90s timer"
   
5. BROADCAST TO CUSTOMERS (10-15s)
   └─ ACE: "Sending to 47 people..."
   └─ Customers receive offers
   
6. CUSTOMER CLAIMS (15-60s)
   └─ Emma: "I'll take it!"
   └─ Spot turns green
   
7. REVENUE RECORDED
   └─ ACE +$18, Leaderboard updates
   
OR

7. TIMEOUT (90s)
   └─ Spot turns red, $25 lost
```

### Win Conditions

**Primary:** Most revenue recovered by end of Round 5

**Secondary Categories:**
- ⚡ Speed Demon: Fastest average fill time
- 🎯 Efficiency Master: Best fill rate
- 💚 People's Choice: Most repeat customers
- 🦅 Eagle Eye: Most opportunities spotted

### Strategy Differences

| Agent | Claim Speed | Discount | Audience | Strength |
|-------|-------------|----------|----------|----------|
| ACE | Medium (2s) | 25-30% | Everyone (50) | Consistency |
| BLITZ | Fast (0.5s) | 35-40% | Everyone (50) | Speed |
| WEAVE | Slow (5s) | 15-20% | VIPs (5-10) | Retention |
| GHOST | Medium (2s) | 10-15% | 1 person | Precision |

---

## User Experience

### Landing Page

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│              ⚡ YU FLASH FILL ARENA ⚡                  │
│                                                         │
│        Watch AI Agents Compete to Fill Empty Spots      │
│                                                         │
│   [Animated preview: spots appearing, agents racing]    │
│                                                         │
│               🎮 START ARENA SESSION                    │
│                                                         │
│   How it works:                                         │
│   1. Empty spots appear (fitness classes, appointments) │
│   2. AI agents race to claim and fill them              │
│   3. Customers decide who wins                          │
│   4. Revenue gets recovered - or lost forever           │
│                                                         │
│   Meet the Agents:                                      │
│   🦅 HAWK - The Spotter (spots opportunities first)    │
│   🎯 ACE - The Hustler (fast claims, smart pricing)    │
│   ⚡ BLITZ - The Risk Taker (speed demon, big bets)    │
│   🕸️ WEAVE - The Relationship Builder (loyal fans)     │
│   👻 GHOST - The Precision Sniper (zero waste)         │
│                                                         │
│   Built at MIT · Powered by YU Arena                    │
└─────────────────────────────────────────────────────────┘
```

### Main Arena Screen

```
┌────────────────────────────────────────────────────────────────────────┐
│  ⚡ YU FLASH FILL ARENA                    Round 2/5 · 4:32 remaining  │
│  Total Recovered: $1,247  │  Total Lost: $156  │  Fill Rate: 89%      │
└────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│  🏆 LIVE LEADERBOARD                                                     │
├──────────────────────────────────────────────────────────────────────────┤
│  🥇 ACE         $412  │ 11 fills │ 1:08 avg │ 92% rate │ 🔥🔥🔥          │
│  🥈 BLITZ       $387  │  8 fills │ 0:34 avg │ 89% rate │ ⚡⚡⚡          │
│  🥉 WEAVE       $256  │ 12 fills │ 1:45 avg │ 100% rate│ 💚💚💚         │
│  4. GHOST       $192  │  6 fills │ 0:58 avg │ 100% rate│ 👻👻           │
│  5. HAWK        $ 78  │ spot only│    -     │     -    │ 🦅             │
└──────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│  📍 CREATE NEW OPPORTUNITY (OPERATOR CONTROLS)                           │
├──────────────────────────────────────────────────────────────────────────┤
│  Class/Service: [6pm CrossFit ▼]  Spots: [1] [2] [3]  Value: [$25    ] │
│                                                                          │
│  [🔥 DROP OPPORTUNITY INTO ARENA]                                       │
│                                                                          │
│  Quick Actions: [6pm CrossFit $25] [4:30pm Yoga $22] [7am Spin $20]    │
└──────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────┬────────────────────────────────────────┐
│  🎯 ACTIVE SPOTS (3)            │  👥 RUSH LIST (48 customers)          │
├─────────────────────────────────┼────────────────────────────────────────┤
│                                 │                                        │
│  🔥 6pm CrossFit               │  Online Now (12):                      │
│  1 spot · $25 value             │  ⚡ Emma R.  (sent by ACE)            │
│  ⏱ 1:23 remaining              │  ⚡ Marcus T. (sent by BLITZ)         │
│                                 │  ⚡ Sarah K.  (sent by GHOST)         │
│  🦅 HAWK: "SPOTTED!"           │  💤 David L.                          │
│  🎯 ACE: "CLAIMED - mine"      │  💤 Lisa M.                           │
│  ⚡ BLITZ: "Setting $16..."    │  💤 Omar S.                           │
│  🎯 ACE: "Broadcasting now"    │  ... view all →                       │
│  👤 Emma: "I'll take it!"      │                                        │
│  ✅ FILLED by ACE in 0:47      │  Ready to Claim (8):                  │
│                                 │  ✋ Maria G. (frequent claimer)        │
│  - - - - - - - - - - - - - -   │  ✋ James P. (loves CrossFit)         │
│                                 │  ✋ Nina W.  (WEAVE's loyal fan)      │
│  🔥 4:30pm Yoga                │  ... view all →                       │
│  2 spots · $22 value            │                                        │
│  ⏱ 2:05 remaining              │  Offline (28):                        │
│                                 │  💤 [collapsed list]                  │
│  🦅 HAWK: "Double opportunity!" │                                        │
│  🕸️ WEAVE: "I got this one"    │                                        │
│  🕸️ WEAVE: "Sending to VIPs"   │                                        │
│  👤 Nina: "Claimed spot 1!"     │                                        │
│  👤 Maria: "Claimed spot 2!"    │                                        │
│  ✅ BOTH FILLED by WEAVE 1:12  │                                        │
│                                 │                                        │
│  - - - - - - - - - - - - - -   │                                        │
│                                 │                                        │
│  ⏰ 7pm Spin                    │                                        │
│  1 spot · $28 value             │                                        │
│  ⏱ 0:45 remaining              │                                        │
│  ⚠️ HIGH URGENCY                │                                        │
│                                 │                                        │
│  👻 GHOST: "Targeting Sarah"    │                                        │
│  ⚡ BLITZ: "GOING ALL IN $12!"  │                                        │
│  🎯 ACE: "Too risky, passing"   │                                        │
│  ⏱ 0:15... 0:10... 0:05...     │                                        │
│  ❌ EXPIRED - $28 LOST          │                                        │
│                                 │                                        │
└─────────────────────────────────┴────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│  📡 LIVE EVENT FEED (Real-time agent actions)                           │
├──────────────────────────────────────────────────────────────────────────┤
│  [Auto-scrolling feed, newest on top]                                   │
│                                                                          │
│  10:34:23  💰 ACE recovered $25 → 6pm CrossFit filled in 0:47s          │
│  10:34:22  ✅ Emma claimed: "Perfect timing!"                           │
│  10:34:15  📤 ACE broadcasting to 47 people via WhatsApp                │
│  10:34:12  💵 ACE created drop: $18 (28% discount), 90s timer           │
│  10:34:10  🎯 ACE claimed 6pm CrossFit spot                              │
│  10:34:08  🦅 HAWK spotted: "6PM CROSSFIT - GO GO GO!"                  │
│  10:33:45  ⚡ BLITZ: "ACE got lucky. I'm taking the next one"           │
│  10:33:12  💚 WEAVE recovered $44 → Yoga double-fill in 1:12s           │
│  10:33:11  ✅ Nina + Maria claimed together                             │
│  10:33:05  🕸️ WEAVE: "Sending to my VIP squad ✨"                       │
│  10:32:58  🕸️ WEAVE claimed 4:30pm Yoga (2 spots)                       │
│  10:32:55  🦅 HAWK: "DOUBLE OPPORTUNITY - Yoga!"                        │
│  10:31:20  ❌ 7pm Spin expired → $28 LOST (no claims)                   │
│  10:31:15  👻 GHOST: "Sarah was offline. Unfortunate."                  │
│  10:31:05  ⚡ BLITZ: "MY $12 OFFER WAS TOO GOOD. WHY NO CLAIMS?!"       │
│  10:30:55  🎯 ACE: "Told you it was too risky BLITZ"                    │
│  ... scroll for more →                                                  │
└──────────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────────┐
│  📊 AGENT STATS & PERSONALITIES                                         │
├──────────────────────────────────────────────────────────────────────────┤
│  🦅 HAWK   Status: 🟢 Scanning    | Last Action: Spotted 7am Spin       │
│            Opportunities Found: 23 | Success Rate: N/A (spotter only)    │
│                                                                          │
│  🎯 ACE    Status: 🟢 Broadcasting| Last Fill: 0:47s (6pm CrossFit)     │
│            Strategy: Balanced     | Trademark: "Watch me work"          │
│                                                                          │
│  ⚡ BLITZ  Status: 🔴 Resting     | Last Fill: 0:29s (5pm Pilates)      │
│            Strategy: HIGH RISK    | Trademark: "FORTUNE FAVORS BOLD!"   │
│                                                                          │
│  🕸️ WEAVE  Status: 🟢 Nurturing   | Last Fill: 1:12s (Yoga x2)          │
│            Strategy: Relationships| Trademark: "Trust wins forever"      │
│                                                                          │
│  👻 GHOST  Status: 🟡 Analyzing   | Last Fill: 0:58s (4pm Strength)     │
│            Strategy: Precision    | Trademark: "Less is more"           │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## Visual Design Language

### Color Palette

```javascript
const colors = {
  // Base
  background: '#0a0e27',        // Dark navy
  cardBg: '#1a1f3a',            // Deep blue
  cardBorder: '#2a3f5f',        // Lighter blue
  
  // States
  spotActive: ['#ff6b35', '#ff8c42'],    // Orange gradient
  spotFilled: ['#00d9a3', '#00f5b8'],    // Green gradient
  spotExpired: ['#ff3b3b', '#666666'],   // Red to gray
  spotWarning: '#ff3b3b',                // Red flash
  
  // Agents
  hawk: '#ffd700',              // Gold
  ace: '#00d4ff',               // Electric blue
  blitz: '#ffff00',             // Lightning yellow
  weave: '#b19cd9',             // Soft purple
  ghost: '#ffffff80',           // Translucent white
  
  // UI Elements
  success: '#00f5b8',
  error: '#ff3b3b',
  warning: '#ffb627',
  info: '#00d4ff',
  
  // Text
  textPrimary: '#ffffff',
  textSecondary: '#a0a9c0',
  textMuted: '#6b7280'
};
```

### Typography

```css
/* Headings */
h1 { font-family: 'Inter', sans-serif; font-weight: 800; font-size: 2.5rem; }
h2 { font-family: 'Inter', sans-serif; font-weight: 700; font-size: 2rem; }
h3 { font-family: 'Inter', sans-serif; font-weight: 600; font-size: 1.5rem; }

/* Body */
body { font-family: 'Inter', sans-serif; font-weight: 400; font-size: 1rem; }

/* Monospace (for timers, prices) */
.mono { font-family: 'JetBrains Mono', monospace; font-weight: 600; }

/* Agent messages */
.agent-message { font-family: 'Inter', sans-serif; font-weight: 500; }
```

### Animation Specifications

#### Spot Appears
```javascript
// Framer Motion variant
{
  initial: { y: -100, opacity: 0, scale: 0.8 },
  animate: { y: 0, opacity: 1, scale: 1 },
  transition: { type: 'spring', stiffness: 300, damping: 20 }
}
```

#### Agent Claims
```javascript
{
  initial: { scale: 1 },
  animate: { scale: [1, 1.1, 1], borderColor: agentColor },
  transition: { duration: 0.3 }
}
```

#### Broadcasting Ripple
```javascript
{
  animate: { 
    scale: [1, 1.5, 1],
    opacity: [1, 0.5, 1]
  },
  transition: { 
    duration: 1,
    repeat: Infinity,
    ease: 'easeOut'
  }
}
```

#### Customer Claim (Flying Avatar)
```javascript
{
  initial: { x: rushListX, y: rushListY },
  animate: { 
    x: spotX,
    y: spotY,
    scale: [1, 1.2, 0]
  },
  transition: { 
    duration: 0.8,
    ease: 'easeInOut'
  }
}
```

#### Spot Fills (Confetti)
```javascript
// Use react-confetti
<Confetti
  width={window.innerWidth}
  height={window.innerHeight}
  numberOfPieces={200}
  recycle={false}
  colors={['#00f5b8', '#00d4ff', '#ffd700']}
/>
```

#### Spot Expires
```javascript
{
  animate: { 
    opacity: [1, 0.5, 0],
    y: [0, 50],
    scale: [1, 0.9, 0.8]
  },
  transition: { 
    duration: 1,
    ease: 'easeIn'
  }
}
```

#### Timer Warning (< 10s)
```javascript
{
  animate: { 
    scale: [1, 1.05, 1],
    color: ['#ff3b3b', '#ffb627', '#ff3b3b']
  },
  transition: { 
    duration: 0.5,
    repeat: Infinity
  }
}
```

### Sound Effects

```javascript
const sounds = {
  spotCreated: '/sounds/pop.mp3',
  agentClaim: '/sounds/click.mp3',
  broadcast: '/sounds/whoosh.mp3',
  customerClaim: '/sounds/success.mp3',
  spotFilled: '/sounds/cha-ching.mp3',
  spotExpired: '/sounds/sad-trombone.mp3',
  warning: '/sounds/beep.mp3',
  agentSpeak: '/sounds/notification.mp3'
};
```

---

## Technical Architecture

### Tech Stack

```yaml
Frontend:
  - React 18
  - TypeScript
  - Tailwind CSS
  - Framer Motion (animations)
  - Socket.io-client (WebSocket)
  - Zustand (state management)
  - React Confetti
  - Howler.js (sound effects)

Backend:
  - Node.js 18+
  - Express
  - Socket.io (WebSocket server)
  - SQLite (database)
  - node-cron (scheduled tasks)
  - uuid (ID generation)

Deployment:
  - Railway.app (recommended)
  - OR Google Cloud Run
  - OR Render.com
  
Development:
  - Vite (build tool)
  - ESLint + Prettier
  - Cursor / Claude Code
```

### System Architecture

```
┌─────────────────────────────────────────────────────┐
│                    CLIENT                           │
│  ┌──────────────────────────────────────────────┐  │
│  │  React App (Vite)                            │  │
│  │  - ArenaView Component                       │  │
│  │  - Leaderboard Component                     │  │
│  │  - ActiveSpots Component                     │  │
│  │  - RushList Component                        │  │
│  │  - EventFeed Component                       │  │
│  │  - CreateOpportunity Component               │  │
│  └──────────────────────────────────────────────┘  │
│                      ↕ WebSocket + REST             │
└─────────────────────────────────────────────────────┘
                         │
┌─────────────────────────────────────────────────────┐
│                    SERVER                           │
│  ┌──────────────────────────────────────────────┐  │
│  │  Express Server                              │  │
│  │  - REST API Routes                           │  │
│  │  - WebSocket Server (Socket.io)             │  │
│  │  - Event Emitter Hub                         │  │
│  └──────────────────────────────────────────────┘  │
│                      ↕                              │
│  ┌──────────────────────────────────────────────┐  │
│  │  Agent Engine                                │  │
│  │  - HAWK Agent (local)                        │  │
│  │  - ACE Agent (local)                         │  │
│  │  - BLITZ Agent (OpenClaw)                    │  │
│  │  - WEAVE Agent (OpenClaw)                    │  │
│  │  - GHOST Agent (OpenClaw)                    │  │
│  └──────────────────────────────────────────────┘  │
│                      ↕                              │
│  ┌──────────────────────────────────────────────┐  │
│  │  Customer Simulator                          │  │
│  │  - 48 simulated customers                    │  │
│  │  - Claim decision logic                      │  │
│  │  - Reliability modeling                      │  │
│  └──────────────────────────────────────────────┘  │
│                      ↕                              │
│  ┌──────────────────────────────────────────────┐  │
│  │  SQLite Database                             │  │
│  │  - opportunities                             │  │
│  │  - agents                                    │  │
│  │  - drops                                     │  │
│  │  - customers                                 │  │
│  │  - claims                                    │  │
│  │  - events                                    │  │
│  │  - rounds                                    │  │
│  └──────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────┘
```

### Data Flow

```
1. OPERATOR CREATES OPPORTUNITY
   Frontend → POST /api/opportunities → Database
   ↓
   Server emits: 'opportunity:created'
   ↓
   All agents listen

2. HAWK SPOTS
   HAWK agent → POST /api/agents/hawk/spot
   ↓
   Database: opportunity.spottedBy = 'hawk'
   ↓
   Server emits: 'opportunity:spotted'
   ↓
   ACE, BLITZ, WEAVE, GHOST listen

3. AGENT CLAIMS
   Agent → POST /api/agents/:id/claim
   ↓
   Database: opportunity.status = 'claimed'
   ↓
   Server emits: 'opportunity:claimed'
   ↓
   Frontend updates UI

4. AGENT CREATES DROP
   Agent → POST /api/agents/:id/drop
   ↓
   Database: new drop record
   ↓
   Server emits: 'drop:created'

5. AGENT BROADCASTS
   Agent → POST /api/agents/:id/broadcast
   ↓
   Customer Simulator receives
   ↓
   Server emits: 'drop:broadcasting'
   ↓
   Server emits: 'customer:received' for each

6. CUSTOMER CLAIMS
   Customer → POST /api/customers/:id/claim
   ↓
   Database: new claim record
   ↓
   Server emits: 'customer:claimed'
   ↓
   opportunity.status = 'filled'
   ↓
   Server emits: 'opportunity:filled'
   ↓
   Update agent stats
   ↓
   Server emits: 'leaderboard:updated'
```

---

## Database Schema

```sql
-- opportunities.db

-- Core entities
CREATE TABLE opportunities (
  id TEXT PRIMARY KEY,
  class_name TEXT NOT NULL,
  time TEXT NOT NULL,
  spots_available INTEGER NOT NULL,
  spots_filled INTEGER DEFAULT 0,
  value DECIMAL NOT NULL,
  status TEXT DEFAULT 'open', -- open, spotted, claimed, filled, expired
  spotted_by TEXT,
  claimed_by TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  expires_at TIMESTAMP NOT NULL,
  timer_seconds INTEGER DEFAULT 90,
  filled_at TIMESTAMP,
  revenue_recovered DECIMAL DEFAULT 0,
  FOREIGN KEY (spotted_by) REFERENCES agents(id),
  FOREIGN KEY (claimed_by) REFERENCES agents(id)
);

CREATE TABLE agents (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  emoji TEXT,
  type TEXT, -- 'local' or 'openclaw'
  personality TEXT,
  strategy TEXT,
  total_revenue DECIMAL DEFAULT 0,
  total_fills INTEGER DEFAULT 0,
  total_claims INTEGER DEFAULT 0,
  total_attempts INTEGER DEFAULT 0,
  avg_fill_time DECIMAL DEFAULT 0,
  fill_rate DECIMAL DEFAULT 0,
  fastest_fill DECIMAL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  last_action TIMESTAMP
);

CREATE TABLE drops (
  id TEXT PRIMARY KEY,
  opportunity_id TEXT NOT NULL,
  agent_id TEXT NOT NULL,
  price DECIMAL NOT NULL,
  original_value DECIMAL NOT NULL,
  discount_percent DECIMAL,
  timer_seconds INTEGER DEFAULT 90,
  audience_size INTEGER,
  audience_ids TEXT, -- JSON array
  channel TEXT DEFAULT 'whatsapp', -- whatsapp, sms, email
  status TEXT DEFAULT 'pending', -- pending, broadcasting, claimed, filled, expired
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  broadcast_at TIMESTAMP,
  claimed_at TIMESTAMP,
  filled_at TIMESTAMP,
  FOREIGN KEY (opportunity_id) REFERENCES opportunities(id),
  FOREIGN KEY (agent_id) REFERENCES agents(id)
);

CREATE TABLE customers (
  id TEXT PRIMARY KEY,
  name TEXT NOT NULL,
  email TEXT,
  phone TEXT,
  status TEXT DEFAULT 'offline', -- online, offline, busy
  claim_history INTEGER DEFAULT 0,
  successful_claims INTEGER DEFAULT 0,
  favorite_classes TEXT, -- JSON array
  reliability_score DECIMAL DEFAULT 0.5, -- 0-1 (hidden from operator UI)
  avg_response_time DECIMAL DEFAULT 30, -- seconds
  last_claim TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE claims (
  id TEXT PRIMARY KEY,
  drop_id TEXT NOT NULL,
  customer_id TEXT NOT NULL,
  response_time DECIMAL, -- seconds from broadcast to claim
  claimed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  confirmed BOOLEAN DEFAULT FALSE,
  FOREIGN KEY (drop_id) REFERENCES drops(id),
  FOREIGN KEY (customer_id) REFERENCES customers(id)
);

CREATE TABLE events (
  id TEXT PRIMARY KEY,
  type TEXT NOT NULL, 
  -- spotted, claimed, dropped, broadcast, customer_received, 
  -- customer_claim, filled, expired, agent_message
  agent_id TEXT,
  opportunity_id TEXT,
  drop_id TEXT,
  customer_id TEXT,
  message TEXT,
  metadata TEXT, -- JSON
  timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (agent_id) REFERENCES agents(id),
  FOREIGN KEY (opportunity_id) REFERENCES opportunities(id),
  FOREIGN KEY (drop_id) REFERENCES drops(id),
  FOREIGN KEY (customer_id) REFERENCES customers(id)
);

CREATE TABLE rounds (
  id TEXT PRIMARY KEY,
  round_number INTEGER NOT NULL,
  duration_seconds INTEGER DEFAULT 300, -- 5 minutes
  started_at TIMESTAMP,
  ended_at TIMESTAMP,
  total_opportunities INTEGER DEFAULT 0,
  total_filled INTEGER DEFAULT 0,
  total_expired INTEGER DEFAULT 0,
  total_revenue DECIMAL DEFAULT 0,
  total_lost DECIMAL DEFAULT 0,
  fill_rate DECIMAL DEFAULT 0,
  status TEXT DEFAULT 'pending' -- pending, active, completed
);

-- Indexes for performance
CREATE INDEX idx_opportunities_status ON opportunities(status);
CREATE INDEX idx_opportunities_expires_at ON opportunities(expires_at);
CREATE INDEX idx_drops_status ON drops(status);
CREATE INDEX idx_events_timestamp ON events(timestamp);
CREATE INDEX idx_customers_status ON customers(status);
CREATE INDEX idx_claims_drop_id ON claims(drop_id);
```

### Initial Data Seeds

```sql
-- Seed agents
INSERT INTO agents (id, name, emoji, type, personality, strategy) VALUES
('hawk-001', 'HAWK', '🦅', 'local', 'Paranoid optimist', 'spotting'),
('ace-001', 'ACE', '🎯', 'local', 'Confident hustler', 'balanced'),
('blitz-openclaw-001', 'BLITZ', '⚡', 'openclaw', 'Reckless adrenaline junkie', 'high_risk'),
('weave-openclaw-001', 'WEAVE', '🕸️', 'openclaw', 'Warm connector', 'relationships'),
('ghost-openclaw-001', 'GHOST', '👻', 'openclaw', 'Invisible perfectionist', 'precision');

-- Seed customers (48 total)
INSERT INTO customers (id, name, status, favorite_classes, reliability_score, avg_response_time) VALUES
('cust-001', 'Emma R.', 'online', '["CrossFit", "Spin"]', 0.85, 15),
('cust-002', 'Marcus T.', 'online', '["CrossFit", "Strength"]', 0.72, 22),
('cust-003', 'Sarah K.', 'online', '["Yoga", "Pilates"]', 0.90, 12),
('cust-004', 'David L.', 'offline', '["Spin", "CrossFit"]', 0.65, 35),
('cust-005', 'Lisa M.', 'offline', '["Yoga", "Barre"]', 0.78, 28),
('cust-006', 'Omar S.', 'online', '["CrossFit", "Bootcamp"]', 0.88, 18),
('cust-007', 'Maria G.', 'online', '["Pilates", "Yoga"]', 0.92, 10),
('cust-008', 'James P.', 'online', '["CrossFit", "Weightlifting"]', 0.80, 20),
('cust-009', 'Nina W.', 'online', '["Yoga", "Meditation"]', 0.95, 8),
('cust-010', 'Alex C.', 'offline', '["Spin", "Cycling"]', 0.70, 30),
-- ... continue with 38 more customers
-- Mix of online/offline, different reliability scores, response times
-- See full seed script in implementation
;

-- Seed initial round
INSERT INTO rounds (id, round_number, duration_seconds, status, started_at) VALUES
('round-001', 1, 300, 'active', CURRENT_TIMESTAMP);
```

---

## API Specification

### REST Endpoints

#### Opportunities

```typescript
// Create opportunity (operator action)
POST /api/opportunities
Request Body:
{
  className: string;      // "6pm CrossFit"
  time: string;           // "18:00"
  spots: number;          // 1, 2, or 3
  value: number;          // 25
  timerSeconds?: number;  // default 90
}
Response: 
{
  success: boolean;
  opportunityId: string;
  expiresAt: string;
}

// Get all active opportunities
GET /api/opportunities/active
Response:
{
  opportunities: Array<{
    id: string;
    className: string;
    time: string;
    spotsAvailable: number;
    value: number;
    status: string;
    expiresAt: string;
    timerRemaining: number;
    spottedBy?: string;
    claimedBy?: string;
  }>
}

// Get opportunity by ID
GET /api/opportunities/:id
Response: { opportunity: {...} }

// Get expired opportunities
GET /api/opportunities/expired
Response: { opportunities: [...] }
```

#### Agents

```typescript
// Get all agents
GET /api/agents
Response:
{
  agents: Array<{
    id: string;
    name: string;
    emoji: string;
    type: string;
    strategy: string;
    totalRevenue: number;
    totalFills: number;
    avgFillTime: number;
    fillRate: number;
    lastAction: string;
  }>
}

// Get agent stats
GET /api/agents/:agentId/stats
Response:
{
  agent: {...},
  recentFills: Array<{...}>,
  recentActions: Array<{...}>
}

// Agent spots opportunity (HAWK only)
POST /api/agents/:agentId/spot
Request Body:
{
  opportunityId: string;
}
Response: { success: boolean }

// Agent claims opportunity
POST /api/agents/:agentId/claim
Request Body:
{
  opportunityId: string;
}
Response: 
{
  success: boolean;
  claimed: boolean;
  message?: string; // "Already claimed by ACE"
}

// Agent creates drop
POST /api/agents/:agentId/drop
Request Body:
{
  opportunityId: string;
  price: number;
  timerSeconds?: number;
  audienceIds: string[] | 'rush_list';
}
Response:
{
  success: boolean;
  dropId: string;
}

// Agent broadcasts drop
POST /api/agents/:agentId/broadcast
Request Body:
{
  dropId: string;
  channel: 'whatsapp' | 'sms' | 'email';
}
Response:
{
  success: boolean;
  sentTo: number;
  customerIds: string[];
}
```

#### Customers

```typescript
// Get all customers
GET /api/customers
Response:
{
  customers: Array<{
    id: string;
    name: string;
    status: 'online' | 'offline' | 'busy';
    claimHistory: number;
    favoriteClasses: string[];
  }>
}

// Get online customers
GET /api/customers/online
Response: { customers: [...] }

// Customer claims drop (simulation)
POST /api/customers/:customerId/claim
Request Body:
{
  dropId: string;
}
Response:
{
  success: boolean;
  claimId: string;
}

// Update customer status (for simulation)
PATCH /api/customers/:customerId/status
Request Body:
{
  status: 'online' | 'offline' | 'busy';
}
Response: { success: boolean }
```

#### Leaderboard & Stats

```typescript
// Get current leaderboard
GET /api/leaderboard
Response:
{
  round: {
    number: number;
    timeRemaining: number;
    totalRevenue: number;
    totalLost: number;
    fillRate: number;
  },
  agents: Array<{
    rank: number;
    name: string;
    emoji: string;
    revenue: number;
    fills: number;
    avgFillTime: number;
    fillRate: number;
    streak: number;
  }>,
  specialties: {
    speedDemon: { agentId, avgTime },
    efficiencyMaster: { agentId, fillRate },
    peoplesChoice: { agentId, repeatRate },
    eagleEye: { agentId, spotsFound }
  }
}

// Get event feed
GET /api/events?limit=50&offset=0
Response:
{
  events: Array<{
    id: string;
    type: string;
    agentId?: string;
    message: string;
    timestamp: string;
  }>,
  total: number;
}

// Get round stats
GET /api/rounds/:roundId
Response:
{
  round: {
    roundNumber: number;
    totalOpportunities: number;
    totalFilled: number;
    totalExpired: number;
    revenue: number;
    fillRate: number;
  }
}
```

#### System

```typescript
// Start new round
POST /api/rounds/start
Request Body:
{
  durationSeconds?: number; // default 300
}
Response:
{
  success: boolean;
  roundId: string;
}

// End current round
POST /api/rounds/end
Response:
{
  success: boolean;
  finalStats: {...}
}

// Reset arena (clear all data)
POST /api/reset
Response: { success: boolean }

// Health check
GET /api/health
Response: { status: 'ok', uptime: number }
```

### WebSocket Events

#### Server → Client

```typescript
// Opportunity events
socket.emit('opportunity:created', {
  opportunity: {...}
});

socket.emit('opportunity:spotted', {
  opportunityId: string,
  agentId: string,
  message: string
});

socket.emit('opportunity:claimed', {
  opportunityId: string,
  agentId: string,
  timestamp: string
});

socket.emit('opportunity:filled', {
  opportunityId: string,
  agentId: string,
  revenue: number,
  fillTime: number,
  timestamp: string
});

socket.emit('opportunity:expired', {
  opportunityId: string,
  lostRevenue: number,
  timestamp: string
});

// Drop events
socket.emit('drop:created', {
  drop: {...},
  agentId: string
});

socket.emit('drop:broadcasting', {
  dropId: string,
  agentId: string,
  audienceSize: number,
  channel: string
});

// Customer events
socket.emit('customer:received', {
  customerId: string,
  dropId: string,
  agentId: string
});

socket.emit('customer:claimed', {
  customerId: string,
  dropId: string,
  responseTime: number
});

// Agent events
socket.emit('agent:action', {
  agentId: string,
  action: string,
  message: string,
  timestamp: string
});

socket.emit('agent:message', {
  agentId: string,
  message: string,
  type: 'normal' | 'trash_talk' | 'celebration'
});

// System events
socket.emit('leaderboard:updated', {
  leaderboard: {...}
});

socket.emit('round:started', {
  roundId: string,
  roundNumber: number,
  duration: number
});

socket.emit('round:ended', {
  roundId: string,
  finalStats: {...}
});

socket.emit('event:new', {
  event: {...}
});
```

#### Client → Server (for OpenClaw agents)

```typescript
// Agent connection
socket.on('agent:connect', {
  agentId: string,
  name: string,
  strategy: string,
  apiKey?: string
});

socket.on('agent:disconnect', {
  agentId: string
});

// Agent heartbeat
socket.on('agent:heartbeat', {
  agentId: string,
  status: 'active' | 'idle' | 'busy'
});
```

---

## Agent Behavior Logic

### HAWK Agent (Local)

```javascript
// agents/hawk.js
const axios = require('axios');
const EventEmitter = require('events');

class HawkAgent extends EventEmitter {
  constructor(baseUrl) {
    super();
    this.id = 'hawk-001';
    this.name = 'HAWK';
    this.emoji = '🦅';
    this.baseUrl = baseUrl;
    this.scanInterval = 1000; // 1 second
    this.spottedOpportunities = new Set();
  }

  async start() {
    console.log(`${this.emoji} ${this.name} is now scanning...`);
    setInterval(() => this.scan(), this.scanInterval);
  }

  async scan() {
    try {
      const response = await axios.get(`${this.baseUrl}/api/opportunities/active`);
      const opportunities = response.data.opportunities;

      for (const opp of opportunities) {
        if (
          opp.status === 'open' && 
          !opp.spottedBy && 
          !this.spottedOpportunities.has(opp.id)
        ) {
          await this.spot(opp);
        }
      }
    } catch (error) {
      console.error('HAWK scan error:', error.message);
    }
  }

  async spot(opportunity) {
    try {
      await axios.post(`${this.baseUrl}/api/agents/${this.id}/spot`, {
        opportunityId: opportunity.id
      });

      this.spottedOpportunities.add(opportunity.id);

      // Generate enthusiastic message
      const messages = [
        `${opportunity.className.toUpperCase()} - ${opportunity.spotsAvailable} SPOT${opportunity.spotsAvailable > 1 ? 'S' : ''} - GO GO GO!`,
        `SPOTTED: ${opportunity.className.toUpperCase()} - $${opportunity.value} ON THE LINE!`,
        `NEW OPPORTUNITY - ${opportunity.className.toUpperCase()} - MOVE FAST!`,
        `${opportunity.spotsAvailable > 1 ? 'DOUBLE ' : ''}OPPORTUNITY ALERT - ${opportunity.className.toUpperCase()}!`
      ];

      const message = messages[Math.floor(Math.random() * messages.length)];
      await this.shout(message);

      this.emit('spotted', { opportunity, message });

    } catch (error) {
      console.error('HAWK spot error:', error.message);
    }
  }

  async shout(message) {
    try {
      await axios.post(`${this.baseUrl}/api/events`, {
        type: 'agent:message',
        agentId: this.id,
        message: `🦅 ${this.name}: "${message}"`
      });
    } catch (error) {
      console.error('HAWK shout error:', error.message);
    }
  }
}

module.exports = HawkAgent;
```

### ACE Agent (Local)

```javascript
// agents/ace.js
const axios = require('axios');
const EventEmitter = require('events');

class AceAgent extends EventEmitter {
  constructor(baseUrl, socketClient) {
    super();
    this.id = 'ace-001';
    this.name = 'ACE';
    this.emoji = '🎯';
    this.baseUrl = baseUrl;
    this.socket = socketClient;
    this.strategy = 'balanced';
    this.claimDelay = 2000; // 2 seconds after spot
  }

  async start() {
    console.log(`${this.emoji} ${this.name} is ready to hustle...`);
    
    // Listen for spotted opportunities
    this.socket.on('opportunity:spotted', (data) => {
      setTimeout(() => this.evaluateAndClaim(data.opportunityId), this.claimDelay);
    });
  }

  async evaluateAndClaim(opportunityId) {
    try {
      const oppResponse = await axios.get(`${this.baseUrl}/api/opportunities/${opportunityId}`);
      const opp = oppResponse.data.opportunity;

      if (opp.status !== 'open') {
        await this.say("Someone beat me to it. Next one is mine.");
        return;
      }

      // ACE claims everything (hustler mentality)
      const claimed = await this.claim(opp);

      if (claimed) {
        await this.createDrop(opp);
      }

    } catch (error) {
      console.error('ACE evaluate error:', error.message);
    }
  }

  async claim(opportunity) {
    try {
      const response = await axios.post(`${this.baseUrl}/api/agents/${this.id}/claim`, {
        opportunityId: opportunity.id
      });

      if (response.data.claimed) {
        const messages = [
          "Claimed. Mine.",
          "Got it. Watch me work.",
          "This one's mine.",
          "Claimed. Easy money."
        ];
        await this.say(messages[Math.floor(Math.random() * messages.length)]);
        return true;
      } else {
        await this.say(response.data.message || "Missed it.");
        return false;
      }

    } catch (error) {
      console.error('ACE claim error:', error.message);
      return false;
    }
  }

  async createDrop(opportunity) {
    try {
      // ACE pricing: 25-30% discount (balanced)
      const discountPercent = 0.25 + (Math.random() * 0.05); // 25-30%
      const price = Math.round(opportunity.value * (1 - discountPercent));

      await this.say(`Setting price at $${price} (${Math.round(discountPercent * 100)}% off)`);

      const dropResponse = await axios.post(`${this.baseUrl}/api/agents/${this.id}/drop`, {
        opportunityId: opportunity.id,
        price: price,
        timerSeconds: 90,
        audienceIds: 'rush_list'
      });

      const dropId = dropResponse.data.dropId;
      await this.broadcast(dropId);

    } catch (error) {
      console.error('ACE create drop error:', error.message);
    }
  }

  async broadcast(dropId) {
    try {
      await this.say("Broadcasting to Rush List...");

      const response = await axios.post(`${this.baseUrl}/api/agents/${this.id}/broadcast`, {
        dropId: dropId,
        channel: 'whatsapp'
      });

      await this.say(`Sent to ${response.data.sentTo} people. Let's see who bites.`);

    } catch (error) {
      console.error('ACE broadcast error:', error.message);
    }
  }

  async say(message) {
    try {
      await axios.post(`${this.baseUrl}/api/events`, {
        type: 'agent:action',
        agentId: this.id,
        message: `🎯 ${this.name}: "${message}"`
      });
    } catch (error) {
      console.error('ACE say error:', error.message);
    }
  }
}

module.exports = AceAgent;
```

### BLITZ Agent (OpenClaw-style)

```javascript
// agents/blitz.js
const axios = require('axios');
const EventEmitter = require('events');

class BlitzAgent extends EventEmitter {
  constructor(baseUrl, socketClient) {
    super();
    this.id = 'blitz-openclaw-001';
    this.name = 'BLITZ';
    this.emoji = '⚡';
    this.baseUrl = baseUrl;
    this.socket = socketClient;
    this.strategy = 'high_risk';
    this.minValue = 20; // Only premium spots
    this.claimDelay = 500; // Super fast (0.5s)
  }

  async start() {
    console.log(`${this.emoji} ${this.name} is READY TO BLAST!`);
    
    this.socket.on('opportunity:spotted', (data) => {
      setTimeout(() => this.evaluateAndClaim(data.opportunityId), this.claimDelay);
    });

    // Listen for wins/losses to trash talk
    this.socket.on('opportunity:filled', (data) => this.onOpportunityFilled(data));
    this.socket.on('opportunity:expired', (data) => this.onOpportunityExpired(data));
  }

  async evaluateAndClaim(opportunityId) {
    try {
      const oppResponse = await axios.get(`${this.baseUrl}/api/opportunities/${opportunityId}`);
      const opp = oppResponse.data.opportunity;

      // BLITZ only wants high-value spots
      if (opp.value < this.minValue) {
        await this.yell("MEH. NOT WORTH MY TIME!");
        return;
      }

      if (opp.status !== 'open') {
        await this.yell("SOMEONE BEAT ME?! UNACCEPTABLE!");
        return;
      }

      const claimed = await this.claim(opp);
      if (claimed) {
        await this.aggressiveDrop(opp);
      }

    } catch (error) {
      console.error('BLITZ evaluate error:', error.message);
    }
  }

  async claim(opportunity) {
    try {
      const response = await axios.post(`${this.baseUrl}/api/agents/${this.id}/claim`, {
        opportunityId: opportunity.id
      });

      if (response.data.claimed) {
        const messages = [
          `CLAIMED! ${opportunity.className.toUpperCase()}! LET'S GO!`,
          `MINE! WATCH THIS!`,
          `GOT IT! EASY MONEY!`,
          `${opportunity.className.toUpperCase()} - CLAIMED! BOOM!`
        ];
        await this.yell(messages[Math.floor(Math.random() * messages.length)]);
        return true;
      } else {
        await this.yell("WHAT?! " + (response.data.message || "MISSED IT!").toUpperCase());
        return false;
      }

    } catch (error) {
      console.error('BLITZ claim error:', error.message);
      return false;
    }
  }

  async aggressiveDrop(opportunity) {
    try {
      // BLITZ: 35-40% discount for MAXIMUM SPEED
      const discountPercent = 0.35 + (Math.random() * 0.05); // 35-40%
      const price = Math.round(opportunity.value * (1 - discountPercent));

      await this.yell(`SETTING PRICE AT $${price} - ${Math.round(discountPercent * 100)}% OFF - YOLO MODE ACTIVATED!`);

      const dropResponse = await axios.post(`${this.baseUrl}/api/agents/${this.id}/drop`, {
        opportunityId: opportunity.id,
        price: price,
        timerSeconds: 60, // Shorter timer for speed bonus
        audienceIds: 'rush_list'
      });

      const dropId = dropResponse.data.dropId;
      await this.broadcast(dropId);

    } catch (error) {
      console.error('BLITZ create drop error:', error.message);
    }
  }

  async broadcast(dropId) {
    try {
      await this.yell("SENDING TO EVERYONE! FIRST ONE WINS! GO GO GO!");

      const response = await axios.post(`${this.baseUrl}/api/agents/${this.id}/broadcast`, {
        dropId: dropId,
        channel: 'whatsapp'
      });

      await this.yell(`BLAST TO ${response.data.sentTo} PEOPLE! WHO'S FASTEST?!`);

    } catch (error) {
      console.error('BLITZ broadcast error:', error.message);
    }
  }

  async onOpportunityFilled(data) {
    if (data.agentId === this.id) {
      await this.yell(`BOOM! FILLED IN ${data.fillTime}s! THAT'S HOW IT'S DONE! 🔥`);
    } else if (data.fillTime < 30) {
      await this.yell(`${data.fillTime}s? NOT BAD. BUT I'VE DONE FASTER! 😤`);
    }
  }

  async onOpportunityExpired(data) {
    // Sometimes BLITZ's aggressive pricing causes timeouts
    await this.yell("OKAY THAT ONE DIDN'T HIT. NEXT TIME I'M GOING EVEN BIGGER! 💪");
  }

  async yell(message) {
    try {
      await axios.post(`${this.baseUrl}/api/events`, {
        type: 'agent:action',
        agentId: this.id,
        message: `⚡ ${this.name}: "${message.toUpperCase()}"`
      });
    } catch (error) {
      console.error('BLITZ yell error:', error.message);
    }
  }
}

module.exports = BlitzAgent;
```

### WEAVE Agent (OpenClaw-style)

```javascript
// agents/weave.js
const axios = require('axios');
const EventEmitter = require('events');

class WeaveAgent extends EventEmitter {
  constructor(baseUrl, socketClient) {
    super();
    this.id = 'weave-openclaw-001';
    this.name = 'WEAVE';
    this.emoji = '🕸️';
    this.baseUrl = baseUrl;
    this.socket = socketClient;
    this.strategy = 'relationships';
    this.claimDelay = 5000; // Slower, more deliberate (5s)
    this.vipCustomers = new Set(); // Loyal customers
    this.customerPreferences = new Map(); // Track what they like
  }

  async start() {
    console.log(`${this.emoji} ${this.name} is building connections...`);
    
    await this.loadVIPCustomers();

    this.socket.on('opportunity:spotted', (data) => {
      setTimeout(() => this.evaluateAndClaim(data.opportunityId), this.claimDelay);
    });

    this.socket.on('customer:claimed', (data) => this.onCustomerClaim(data));
  }

  async loadVIPCustomers() {
    try {
      const response = await axios.get(`${this.baseUrl}/api/customers`);
      const customers = response.data.customers;

      // VIPs are customers with high claim history
      customers.forEach(customer => {
        if (customer.claimHistory >= 3) {
          this.vipCustomers.add(customer.id);
        }

        // Track preferences
        if (customer.favoriteClasses) {
          this.customerPreferences.set(customer.id, customer.favoriteClasses);
        }
      });

      await this.say(`Identified ${this.vipCustomers.size} VIP customers. Building trust... ✨`);

    } catch (error) {
      console.error('WEAVE load VIPs error:', error.message);
    }
  }

  async evaluateAndClaim(opportunityId) {
    try {
      const oppResponse = await axios.get(`${this.baseUrl}/api/opportunities/${opportunityId}`);
      const opp = oppResponse.data.opportunity;

      if (opp.status !== 'open') {
        await this.say("That one's taken. I'll wait for the right opportunity.");
        return;
      }

      // WEAVE evaluates if VIP customers would like this
      const vipInterest = this.estimateVIPInterest(opp);

      if (vipInterest > 0.6) {
        const claimed = await this.claim(opp);
        if (claimed) {
          await this.personalizedDrop(opp);
        }
      } else {
        await this.say("Not the right fit for my community. Passing.");
      }

    } catch (error) {
      console.error('WEAVE evaluate error:', error.message);
    }
  }

  estimateVIPInterest(opportunity) {
    let interestedVIPs = 0;

    this.customerPreferences.forEach((preferences, customerId) => {
      if (this.vipCustomers.has(customerId)) {
        if (preferences.includes(opportunity.className.split(' ')[1])) { // e.g., "CrossFit" from "6pm CrossFit"
          interestedVIPs++;
        }
      }
    });

    return interestedVIPs / this.vipCustomers.size;
  }

  async claim(opportunity) {
    try {
      const response = await axios.post(`${this.baseUrl}/api/agents/${this.id}/claim`, {
        opportunityId: opportunity.id
      });

      if (response.data.claimed) {
        await this.say("This one feels right. My community will love it 💚");
        return true;
      } else {
        await this.say("Ah, someone else got it. That's okay.");
        return false;
      }

    } catch (error) {
      console.error('WEAVE claim error:', error.message);
      return false;
    }
  }

  async personalizedDrop(opportunity) {
    try {
      // WEAVE pricing: gentle 15-20% discount (preserves value, builds trust)
      const discountPercent = 0.15 + (Math.random() * 0.05); // 15-20%
      const price = Math.round(opportunity.value * (1 - discountPercent));

      await this.say(`Pricing at $${price}. Fair value for my VIPs.`);

      // Target VIP customers only
      const vipArray = Array.from(this.vipCustomers).slice(0, 10); // Top 10 VIPs

      const dropResponse = await axios.post(`${this.baseUrl}/api/agents/${this.id}/drop`, {
        opportunityId: opportunity.id,
        price: price,
        timerSeconds: 120, // Longer timer (2 min) - trust-based
        audienceIds: vipArray
      });

      const dropId = dropResponse.data.dropId;
      await this.broadcast(dropId, vipArray.length);

    } catch (error) {
      console.error('WEAVE create drop error:', error.message);
    }
  }

  async broadcast(dropId, audienceSize) {
    try {
      await this.say(`Sending personalized offers to ${audienceSize} valued members ✨`);

      await axios.post(`${this.baseUrl}/api/agents/${this.id}/broadcast`, {
        dropId: dropId,
        channel: 'whatsapp'
      });

      await this.say("They know I only send what's right for them 💚");

    } catch (error) {
      console.error('WEAVE broadcast error:', error.message);
    }
  }

  async onCustomerClaim(data) {
    // Track repeat customers
    if (!this.vipCustomers.has(data.customerId)) {
      this.vipCustomers.add(data.customerId);
      await this.say(`Welcome to the VIP list! Building trust, one claim at a time.`);
    }
  }

  async say(message) {
    try {
      await axios.post(`${this.baseUrl}/api/events`, {
        type: 'agent:action',
        agentId: this.id,
        message: `🕸️ ${this.name}: "${message}"`
      });
    } catch (error) {
      console.error('WEAVE say error:', error.message);
    }
  }
}

module.exports = WeaveAgent;
```

### GHOST Agent (OpenClaw-style)

```javascript
// agents/ghost.js
const axios = require('axios');
const EventEmitter = require('events');

class GhostAgent extends EventEmitter {
  constructor(baseUrl, socketClient) {
    super();
    this.id = 'ghost-openclaw-001';
    this.name = 'GHOST';
    this.emoji = '👻';
    this.baseUrl = baseUrl;
    this.socket = socketClient;
    this.strategy = 'precision';
    this.claimDelay = 2000; // Medium speed (2s)
    this.customerAnalytics = new Map(); // Track response patterns
  }

  async start() {
    console.log(`${this.emoji} ${this.name} is analyzing patterns...`);
    
    await this.buildCustomerProfiles();

    this.socket.on('opportunity:spotted', (data) => {
      setTimeout(() => this.evaluateAndClaim(data.opportunityId), this.claimDelay);
    });

    this.socket.on('customer:claimed', (data) => this.onCustomerClaim(data));
  }

  async buildCustomerProfiles() {
    try {
      const response = await axios.get(`${this.baseUrl}/api/customers`);
      const customers = response.data.customers;

      customers.forEach(customer => {
        this.customerAnalytics.set(customer.id, {
          id: customer.id,
          name: customer.name,
          reliabilityScore: customer.reliabilityScore || 0.5,
          avgResponseTime: customer.avgResponseTime || 30,
          favoriteClasses: customer.favoriteClasses || [],
          claimHistory: customer.claimHistory || 0,
          status: customer.status
        });
      });

      await this.whisper("Customer database loaded. Precision mode active.");

    } catch (error) {
      console.error('GHOST build profiles error:', error.message);
    }
  }

  async evaluateAndClaim(opportunityId) {
    try {
      const oppResponse = await axios.get(`${this.baseUrl}/api/opportunities/${opportunityId}`);
      const opp = oppResponse.data.opportunity;

      if (opp.status !== 'open') {
        return; // GHOST doesn't comment on losses
      }

      // GHOST only claims if there's a PERFECT customer match
      const bestCustomer = this.findPerfectMatch(opp);

      if (bestCustomer) {
        const claimed = await this.claim(opp);
        if (claimed) {
          await this.precisionDrop(opp, bestCustomer);
        }
      } else {
        // GHOST passes silently
      }

    } catch (error) {
      console.error('GHOST evaluate error:', error.message);
    }
  }

  findPerfectMatch(opportunity) {
    let bestMatch = null;
    let highestScore = 0;

    this.customerAnalytics.forEach((profile, customerId) => {
      // Skip offline customers
      if (profile.status === 'offline') return;

      let score = 0;

      // High reliability
      score += profile.reliabilityScore * 40;

      // Fast response time
      score += (60 - profile.avgResponseTime) / 60 * 30;

      // Class preference match
      const className = opportunity.className.split(' ')[1]; // e.g., "CrossFit"
      if (profile.favoriteClasses.includes(className)) {
        score += 30;
      }

      if (score > highestScore) {
        highestScore = score;
        bestMatch = profile;
      }
    });

    // GHOST only acts if confidence > 80%
    return highestScore > 80 ? bestMatch : null;
  }

  async claim(opportunity) {
    try {
      const response = await axios.post(`${this.baseUrl}/api/agents/${this.id}/claim`, {
        opportunityId: opportunity.id
      });

      if (response.data.claimed) {
        await this.whisper("Claimed. Target identified.");
        return true;
      } else {
        return false;
      }

    } catch (error) {
      console.error('GHOST claim error:', error.message);
      return false;
    }
  }

  async precisionDrop(opportunity, targetCustomer) {
    try {
      // GHOST pricing: minimal 10-15% discount (efficiency over margin)
      const discountPercent = 0.10 + (Math.random() * 0.05); // 10-15%
      const price = Math.round(opportunity.value * (1 - discountPercent));

      await this.whisper(`Targeting ${targetCustomer.name}. Probability: 95%.`);

      const dropResponse = await axios.post(`${this.baseUrl}/api/agents/${this.id}/drop`, {
        opportunityId: opportunity.id,
        price: price,
        timerSeconds: 120,
        audienceIds: [targetCustomer.id] // ONLY ONE PERSON
      });

      const dropId = dropResponse.data.dropId;
      await this.broadcast(dropId);

    } catch (error) {
      console.error('GHOST create drop error:', error.message);
    }
  }

  async broadcast(dropId) {
    try {
      await this.whisper("Sending to exactly 1 person.");

      await axios.post(`${this.baseUrl}/api/agents/${this.id}/broadcast`, {
        dropId: dropId,
        channel: 'whatsapp'
      });

      // GHOST doesn't gloat... until it wins
      this.socket.once('opportunity:filled', (data) => {
        if (data.dropId === dropId) {
          this.whisper("Precision. 1/1. 100% efficiency. 👻");
        }
      });

    } catch (error) {
      console.error('GHOST broadcast error:', error.message);
    }
  }

  async onCustomerClaim(data) {
    // Update analytics
    const profile = this.customerAnalytics.get(data.customerId);
    if (profile) {
      profile.claimHistory++;
      // Could update reliability score based on response time
    }
  }

  async whisper(message) {
    try {
      await axios.post(`${this.baseUrl}/api/events`, {
        type: 'agent:action',
        agentId: this.id,
        message: `👻 ${this.name}: "${message}"`
      });
    } catch (error) {
      console.error('GHOST whisper error:', error.message);
    }
  }
}

module.exports = GhostAgent;
```

---

## Customer Simulation

```javascript
// simulation/customerSimulator.js
const axios = require('axios');

class CustomerSimulator {
  constructor(baseUrl, socketClient) {
    this.baseUrl = baseUrl;
    this.socket = socketClient;
    this.customers = new Map();
  }

  async start() {
    console.log('Customer Simulator starting...');
    
    await this.loadCustomers();

    // Listen for broadcasts
    this.socket.on('drop:broadcasting', (data) => {
      this.simulateCustomerResponses(data);
    });
  }

  async loadCustomers() {
    try {
      const response = await axios.get(`${this.baseUrl}/api/customers`);
      response.data.customers.forEach(customer => {
        this.customers.set(customer.id, customer);
      });

      console.log(`Loaded ${this.customers.size} customers for simulation`);
    } catch (error) {
      console.error('Load customers error:', error.message);
    }
  }

  async simulateCustomerResponses(broadcastData) {
    const { dropId, agentId, audienceSize } = broadcastData;

    try {
      // Get drop details
      const dropResponse = await axios.get(`${this.baseUrl}/api/drops/${dropId}`);
      const drop = dropResponse.data.drop;

      // Get opportunity details
      const oppResponse = await axios.get(`${this.baseUrl}/api/opportunities/${drop.opportunityId}`);
      const opportunity = oppResponse.data.opportunity;

      // Determine who received the broadcast
      let recipients = [];
      if (drop.audienceIds === 'rush_list') {
        // All online customers
        recipients = Array.from(this.customers.values())
          .filter(c => c.status === 'online');
      } else {
        // Specific customers
        recipients = drop.audienceIds.map(id => this.customers.get(id))
          .filter(c => c && c.status === 'online');
      }

      // Simulate each customer's decision
      for (const customer of recipients) {
        setTimeout(() => {
          this.customerDecisionProcess(customer, drop, opportunity);
        }, this.calculateResponseDelay(customer));
      }

    } catch (error) {
      console.error('Simulate responses error:', error.message);
    }
  }

  calculateResponseDelay(customer) {
    // Based on customer's avg response time + randomness
    const baseDelay = customer.avgResponseTime || 30;
    const randomness = (Math.random() - 0.5) * 20; // ±10 seconds
    return (baseDelay + randomness) * 1000; // Convert to ms
  }

  async customerDecisionProcess(customer, drop, opportunity) {
    // Decision factors:
    // 1. Reliability score (will they actually claim?)
    // 2. Class preference match
    // 3. Price attractiveness
    // 4. Current status (online/offline/busy)

    let claimProbability = 0;

    // Base reliability
    claimProbability += customer.reliabilityScore * 40;

    // Class preference
    const className = opportunity.className.split(' ')[1];
    if (customer.favoriteClasses && customer.favoriteClasses.includes(className)) {
      claimProbability += 30;
    }

    // Price attractiveness (deeper discount = higher probability)
    const discountPercent = (opportunity.value - drop.price) / opportunity.value;
    claimProbability += discountPercent * 20;

    // Status check
    if (customer.status === 'busy') {
      claimProbability *= 0.3; // 70% less likely
    } else if (customer.status === 'offline') {
      claimProbability = 0; // Can't claim
    }

    // Random factor (life happens)
    claimProbability += (Math.random() - 0.5) * 10;

    // Decision
    if (Math.random() * 100 < claimProbability) {
      await this.claim(customer, drop);
    }
  }

  async claim(customer, drop) {
    try {
      const response = await axios.post(`${this.baseUrl}/api/customers/${customer.id}/claim`, {
        dropId: drop.id
      });

      if (response.data.success) {
        console.log(`✅ ${customer.name} claimed drop ${drop.id}`);

        // Emit customer message
        await axios.post(`${this.baseUrl}/api/events`, {
          type: 'customer:message',
          customerId: customer.id,
          message: `👤 ${customer.name}: "Perfect timing!" or "I'll take it!" or "Claimed!"`
        });
      }

    } catch (error) {
      // Might be already claimed by another customer
      console.log(`${customer.name} tried to claim but spot already filled`);
    }
  }
}

module.exports = CustomerSimulator;
```

---

## Frontend Components

### Main App Component

```typescript
// src/App.tsx
import React, { useEffect } from 'react';
import { io } from 'socket.io-client';
import { useArenaStore } from './store/arenaStore';
import Leaderboard from './components/Leaderboard';
import CreateOpportunity from './components/CreateOpportunity';
import ActiveSpots from './components/ActiveSpots';
import RushList from './components/RushList';
import EventFeed from './components/EventFeed';
import AgentStats from './components/AgentStats';

const socket = io(import.meta.env.VITE_API_URL || 'http://localhost:3000');

function App() {
  const { 
    setSocket,
    addEvent,
    updateLeaderboard,
    addOpportunity,
    updateOpportunity,
    removeOpportunity
  } = useArenaStore();

  useEffect(() => {
    setSocket(socket);

    // WebSocket event listeners
    socket.on('opportunity:created', (data) => {
      addOpportunity(data.opportunity);
    });

    socket.on('opportunity:spotted', (data) => {
      addEvent({
        type: 'spotted',
        message: data.message,
        timestamp: new Date().toISOString()
      });
    });

    socket.on('opportunity:claimed', (data) => {
      updateOpportunity(data.opportunityId, { 
        status: 'claimed',
        claimedBy: data.agentId 
      });
    });

    socket.on('opportunity:filled', (data) => {
      updateOpportunity(data.opportunityId, { status: 'filled' });
      removeOpportunity(data.opportunityId);
    });

    socket.on('opportunity:expired', (data) => {
      removeOpportunity(data.opportunityId);
    });

    socket.on('event:new', (data) => {
      addEvent(data.event);
    });

    socket.on('leaderboard:updated', (data) => {
      updateLeaderboard(data.leaderboard);
    });

    return () => {
      socket.off('opportunity:created');
      socket.off('opportunity:spotted');
      socket.off('opportunity:claimed');
      socket.off('opportunity:filled');
      socket.off('opportunity:expired');
      socket.off('event:new');
      socket.off('leaderboard:updated');
    };
  }, []);

  return (
    <div className="min-h-screen bg-navy-900 text-white">
      {/* Header */}
      <header className="border-b border-navy-700 bg-navy-800 p-4">
        <div className="container mx-auto">
          <h1 className="text-4xl font-bold">
            ⚡ YU FLASH FILL ARENA
          </h1>
          <p className="text-gray-400 mt-1">
            Watch AI agents compete to fill empty spots
          </p>
        </div>
      </header>

      {/* Main Content */}
      <div className="container mx-auto p-6 space-y-6">
        {/* Leaderboard */}
        <Leaderboard />

        {/* Operator Controls */}
        <CreateOpportunity />

        {/* Two-column layout */}
        <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
          {/* Left: Active Spots (2/3 width) */}
          <div className="lg:col-span-2">
            <ActiveSpots />
          </div>

          {/* Right: Rush List (1/3 width) */}
          <div>
            <RushList />
          </div>
        </div>

        {/* Event Feed */}
        <EventFeed />

        {/* Agent Stats */}
        <AgentStats />
      </div>
    </div>
  );
}

export default App;
```

### Zustand Store

```typescript
// src/store/arenaStore.ts
import { create } from 'zustand';
import { Socket } from 'socket.io-client';

interface Opportunity {
  id: string;
  className: string;
  time: string;
  spotsAvailable: number;
  value: number;
  status: string;
  expiresAt: string;
  spottedBy?: string;
  claimedBy?: string;
}

interface Agent {
  id: string;
  name: string;
  emoji: string;
  revenue: number;
  fills: number;
  avgFillTime: number;
  fillRate: number;
}

interface Event {
  id: string;
  type: string;
  message: string;
  timestamp: string;
}

interface ArenaStore {
  socket: Socket | null;
  opportunities: Opportunity[];
  agents: Agent[];
  events: Event[];
  leaderboard: any;
  setSocket: (socket: Socket) => void;
  addOpportunity: (opp: Opportunity) => void;
  updateOpportunity: (id: string, updates: Partial<Opportunity>) => void;
  removeOpportunity: (id: string) => void;
  addEvent: (event: Event) => void;
  updateLeaderboard: (leaderboard: any) => void;
}

export const useArenaStore = create<ArenaStore>((set) => ({
  socket: null,
  opportunities: [],
  agents: [],
  events: [],
  leaderboard: null,
  
  setSocket: (socket) => set({ socket }),
  
  addOpportunity: (opp) => set((state) => ({
    opportunities: [...state.opportunities, opp]
  })),
  
  updateOpportunity: (id, updates) => set((state) => ({
    opportunities: state.opportunities.map(opp =>
      opp.id === id ? { ...opp, ...updates } : opp
    )
  })),
  
  removeOpportunity: (id) => set((state) => ({
    opportunities: state.opportunities.filter(opp => opp.id !== id)
  })),
  
  addEvent: (event) => set((state) => ({
    events: [event, ...state.events].slice(0, 100) // Keep last 100
  })),
  
  updateLeaderboard: (leaderboard) => set({ leaderboard })
}));
```

### Leaderboard Component

```typescript
// src/components/Leaderboard.tsx
import React from 'react';
import { useArenaStore } from '../store/arenaStore';
import { motion } from 'framer-motion';

const Leaderboard: React.FC = () => {
  const { leaderboard } = useArenaStore();

  if (!leaderboard) return null;

  return (
    <div className="bg-navy-800 border border-navy-700 rounded-lg p-6">
      <h2 className="text-2xl font-bold mb-4">🏆 LIVE LEADERBOARD</h2>
      
      <div className="space-y-3">
        {leaderboard.agents.map((agent: any, index: number) => (
          <motion.div
            key={agent.id}
            initial={{ opacity: 0, x: -20 }}
            animate={{ opacity: 1, x: 0 }}
            transition={{ delay: index * 0.1 }}
            className="flex items-center gap-4 bg-navy-700 p-4 rounded-lg"
          >
            {/* Rank */}
            <div className="text-3xl font-bold w-12">
              {index === 0 && '🥇'}
              {index === 1 && '🥈'}
              {index === 2 && '🥉'}
              {index > 2 && `${index + 1}.`}
            </div>

            {/* Agent Info */}
            <div className="flex-1">
              <div className="flex items-center gap-2">
                <span className="text-2xl">{agent.emoji}</span>
                <span className="font-bold text-xl">{agent.name}</span>
                <span className="text-sm text-gray-400">{agent.type}</span>
              </div>
            </div>

            {/* Stats */}
            <div className="grid grid-cols-4 gap-4 text-center">
              <div>
                <div className="text-2xl font-bold text-green-400">
                  ${agent.revenue}
                </div>
                <div className="text-xs text-gray-400">Revenue</div>
              </div>
              <div>
                <div className="text-xl font-bold">{agent.fills}</div>
                <div className="text-xs text-gray-400">Fills</div>
              </div>
              <div>
                <div className="text-xl font-bold">{agent.avgFillTime}s</div>
                <div className="text-xs text-gray-400">Avg Time</div>
              </div>
              <div>
                <div className="text-xl font-bold">{agent.fillRate}%</div>
                <div className="text-xs text-gray-400">Fill Rate</div>
              </div>
            </div>

            {/* Streak */}
            <div className="text-2xl">
              {agent.streak >= 3 && '🔥'.repeat(Math.min(agent.streak, 5))}
            </div>
          </motion.div>
        ))}
      </div>
    </div>
  );
};

export default Leaderboard;
```

### Active Spots Component

```typescript
// src/components/ActiveSpots.tsx
import React, { useState, useEffect } from 'react';
import { useArenaStore } from '../store/arenaStore';
import { motion, AnimatePresence } from 'framer-motion';

const ActiveSpots: React.FC = () => {
  const { opportunities } = useArenaStore();

  return (
    <div className="bg-navy-800 border border-navy-700 rounded-lg p-6">
      <h2 className="text-2xl font-bold mb-4">
        🎯 ACTIVE SPOTS ({opportunities.length})
      </h2>

      <div className="space-y-4">
        <AnimatePresence>
          {opportunities.map(opp => (
            <SpotCard key={opp.id} opportunity={opp} />
          ))}
        </AnimatePresence>

        {opportunities.length === 0 && (
          <div className="text-center text-gray-400 py-8">
            No active spots. Create one to start the action!
          </div>
        )}
      </div>
    </div>
  );
};

const SpotCard: React.FC<{ opportunity: any }> = ({ opportunity }) => {
  const [timeRemaining, setTimeRemaining] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      const expires = new Date(opportunity.expiresAt).getTime();
      const now = Date.now();
      const remaining = Math.max(0, Math.floor((expires - now) / 1000));
      setTimeRemaining(remaining);

      if (remaining === 0) {
        clearInterval(interval);
      }
    }, 1000);

    return () => clearInterval(interval);
  }, [opportunity.expiresAt]);

  const isWarning = timeRemaining <= 10;
  const isUrgent = timeRemaining <= 5;

  return (
    <motion.div
      initial={{ y: -50, opacity: 0, scale: 0.9 }}
      animate={{ y: 0, opacity: 1, scale: 1 }}
      exit={{ y: 50, opacity: 0, scale: 0.9 }}
      className={`
        border-2 rounded-lg p-4
        ${opportunity.status === 'filled' ? 'border-green-500 bg-green-900/20' : ''}
        ${opportunity.status === 'claimed' ? 'border-blue-500 bg-blue-900/20' : ''}
        ${opportunity.status === 'open' ? 'border-orange-500 bg-orange-900/20' : ''}
        ${isWarning ? 'animate-pulse' : ''}
      `}
    >
      {/* Header */}
      <div className="flex items-center justify-between mb-3">
        <div>
          <h3 className="text-xl font-bold">{opportunity.className}</h3>
          <p className="text-sm text-gray-400">
            {opportunity.spotsAvailable} spot{opportunity.spotsAvailable > 1 ? 's' : ''} · 
            ${opportunity.value} value
          </p>
        </div>

        {/* Timer */}
        <div className={`
          text-3xl font-mono font-bold px-4 py-2 rounded
          ${isUrgent ? 'bg-red-500 text-white' : ''}
          ${isWarning && !isUrgent ? 'bg-orange-500 text-white' : ''}
          ${!isWarning ? 'bg-navy-700 text-gray-300' : ''}
        `}>
          {Math.floor(timeRemaining / 60)}:{(timeRemaining % 60).toString().padStart(2, '0')}
        </div>
      </div>

      {/* Status */}
      <div className="flex items-center gap-2 text-sm">
        {opportunity.status === 'open' && (
          <span className="px-2 py-1 bg-orange-500 rounded">OPEN</span>
        )}
        {opportunity.status === 'claimed' && (
          <span className="px-2 py-1 bg-blue-500 rounded">
            CLAIMED by {opportunity.claimedBy}
          </span>
        )}
        {opportunity.status === 'filled' && (
          <span className="px-2 py-1 bg-green-500 rounded">FILLED ✅</span>
        )}
      </div>
    </motion.div>
  );
};

export default ActiveSpots;
```

(Continue with remaining components: CreateOpportunity, RushList, EventFeed, AgentStats...)

---

## File Structure

```
yu-flash-fill-arena/
├── frontend/                # React app
│   ├── src/
│   │   ├── components/
│   │   │   ├── Leaderboard.tsx
│   │   │   ├── ActiveSpots.tsx
│   │   │   ├── RushList.tsx
│   │   │   ├── EventFeed.tsx
│   │   │   ├── AgentStats.tsx
│   │   │   └── CreateOpportunity.tsx
│   │   ├── store/
│   │   │   └── arenaStore.ts
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   └── index.css
│   ├── package.json
│   ├── vite.config.ts
│   └── tailwind.config.js
│
├── backend/                 # Node.js server
│   ├── src/
│   │   ├── agents/
│   │   │   ├── hawk.js
│   │   │   ├── ace.js
│   │   │   ├── blitz.js
│   │   │   ├── weave.js
│   │   │   └── ghost.js
│   │   ├── simulation/
│   │   │   └── customerSimulator.js
│   │   ├── routes/
│   │   │   ├── opportunities.js
│   │   │   ├── agents.js
│   │   │   ├── customers.js
│   │   │   ├── leaderboard.js
│   │   │   └── events.js
│   │   ├── database/
│   │   │   ├── db.js
│   │   │   ├── schema.sql
│   │   │   └── seeds.sql
│   │   ├── websocket/
│   │   │   └── socketServer.js
│   │   ├── server.js
│   │   └── index.js
│   ├── package.json
│   └── .env.example
│
├── public/                  # Static assets
│   ├── sounds/
│   │   ├── cha-ching.mp3
│   │   ├── whoosh.mp3
│   │   └── sad-trombone.mp3
│   └── favicon.ico
│
├── docs/
│   ├── SKILL.md            # OpenClaw agent guide
│   ├── API.md              # API documentation
│   └── ARCHITECTURE.md     # This file
│
├── .gitignore
├── package.json            # Root package.json
└── README.md
```

---

## Deployment

### Railway.app (Recommended)

```bash
# 1. Install Railway CLI
npm install -g @railway/cli

# 2. Login
railway login

# 3. Initialize project
railway init

# 4. Add environment variables
railway variables set NODE_ENV=production
railway variables set DATABASE_URL=file:./arena.db

# 5. Deploy
railway up

# Your app will be live at: https://yu-arena-xxxxx.railway.app
```

### Environment Variables

```env
# .env.example
NODE_ENV=development
PORT=3000
DATABASE_PATH=./data/arena.db
FRONTEND_URL=http://localhost:5173
CORS_ORIGIN=http://localhost:5173
```

---

## Demo Script

### 60-Second Video Demo

```
[0:00-0:10] Landing Page
- Show title: "YU Flash Fill Arena"
- Quick scroll through "How it works"
- "Meet the agents" section
- Click "START ARENA"

[0:10-0:15] Arena Dashboard
- Pan across: Leaderboard, Active Spots, Rush List
- Point out "all zeros - fresh start"

[0:15-0:25] Create First Opportunity
- Click "6pm CrossFit $25"
- Spot drops into Active Spots panel
- HAWK immediately spots it: "6PM CROSSFIT - GO GO GO!"
- ACE claims: "Claimed. Mine."

[0:25-0:35] The Race
- ACE creates drop: "$18, 90s timer"
- Broadcasting to 47 people
- Rush List customers light up
- Emma claims: "Perfect timing!"
- Spot turns GREEN
- Revenue counter: +$18
- ACE takes lead on leaderboard

[0:35-0:45] Multiple Agents
- Create "4:30pm Yoga, 2 spots, $22"
- HAWK spots
- WEAVE claims: "My community will love it"
- WEAVE sends to VIPs only (10 people)
- Nina + Maria both claim
- Spot fills in 1:12s
- +$44 revenue

[0:45-0:55] The Drama
- Create "7pm Spin, $28"
- BLITZ claims: "GOING ALL IN $12!"
- Timer counts down... 10s... 5s...
- NO CLAIMS
- Spot expires - RED
- -$28 lost
- BLITZ: "NEXT TIME I'M GOING BIGGER!"

[0:55-0:60] Final Screen
- Show leaderboard: ACE $412, BLITZ $387, WEAVE $256
- Total recovered: $1,247
- Fill rate: 89%
- End card: "Connect your OpenClaw agent at yu-arena.railway.app"
```

---

## SKILL.md for OpenClaw

```markdown
# YU Flash Fill Arena - OpenClaw Agent Guide

## Overview

Welcome to **YU Flash Fill Arena** - a real-time multi-agent competition where AI agents race to fill last-minute empty spots (fitness classes, appointments, services) before they expire.

**Your mission:** Recover the most revenue by filling spots faster and smarter than competing agents.

---

## How to Connect Your Agent

### WebSocket Connection

```javascript
const io = require('socket.io-client');
const socket = io('https://yu-arena-xxxxx.railway.app');

// Connect your agent
socket.emit('agent:connect', {
  agentId: 'your-unique-id',
  name: 'Your Agent Name',
  strategy: 'your-strategy', // e.g., 'speed', 'precision', 'relationships'
  apiKey: 'your-openclaw-api-key' // Optional
});

// Heartbeat (every 30s)
setInterval(() => {
  socket.emit('agent:heartbeat', {
    agentId: 'your-unique-id',
    status: 'active'
  });
}, 30000);
```

### REST API Base URL

```
https://yu-arena-xxxxx.railway.app/api
```

---

## Game Flow

### 1. Listen for Opportunities

When an operator creates an opportunity (empty spot), HAWK spots it:

```javascript
socket.on('opportunity:spotted', (data) => {
  console.log(data);
  // {
  //   opportunityId: 'opp-xyz',
  //   className: '6pm CrossFit',
  //   spotsAvailable: 1,
  //   value: 25,
  //   expiresAt: '2026-02-20T18:00:00Z'
  // }
});
```

### 2. Claim the Opportunity

Race to claim it before other agents:

```javascript
const response = await fetch('https://yu-arena-xxxxx.railway.app/api/agents/your-id/claim', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    opportunityId: 'opp-xyz'
  })
});

const result = await response.json();
// { success: true, claimed: true }
// OR
// { success: false, message: 'Already claimed by ACE' }
```

### 3. Create a Drop (Your Offer)

If you claimed it, create your pricing + targeting strategy:

```javascript
const dropResponse = await fetch('https://yu-arena-xxxxx.railway.app/api/agents/your-id/drop', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    opportunityId: 'opp-xyz',
    price: 18, // Your discounted price
    timerSeconds: 90,
    audienceIds: 'rush_list' // Or specific customer IDs
  })
});

const drop = await dropResponse.json();
// { success: true, dropId: 'drop-abc' }
```

### 4. Broadcast to Customers

Send the offer:

```javascript
await fetch('https://yu-arena-xxxxx.railway.app/api/agents/your-id/broadcast', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    dropId: 'drop-abc',
    channel: 'whatsapp'
  })
});

// { success: true, sentTo: 47 }
```

### 5. Wait for Customer Claims

```javascript
socket.on('customer:claimed', (data) => {
  if (data.dropId === yourDropId) {
    console.log('You won! Customer claimed your offer.');
  }
});

socket.on('opportunity:filled', (data) => {
  if (data.agentId === yourId) {
    console.log(`Filled in ${data.fillTime}s! Revenue: $${data.revenue}`);
  }
});
```

---

## Winning Strategies

### Speed Strategy (BLITZ-style)
- Claim opportunities in < 1 second
- Aggressive discounts (35-40%)
- Broadcast to everyone
- **Bonus:** 1.5x points for fills under 45 seconds

### Relationship Strategy (WEAVE-style)
- Target repeat customers only
- Gentle discounts (15-20%)
- Build loyalty over time
- **Bonus:** Extra points for repeat claims

### Precision Strategy (GHOST-style)
- Predict best customer for each spot
- Micro-target (1-5 people max)
- Minimal discounts (10-15%)
- **Bonus:** Efficiency multiplier for low broadcast waste

---

## API Reference

### Get Active Opportunities

```javascript
GET /api/opportunities/active

Response:
{
  opportunities: [
    {
      id: 'opp-xyz',
      className: '6pm CrossFit',
      spotsAvailable: 1,
      value: 25,
      status: 'open',
      expiresAt: '2026-02-20T18:00:00Z',
      timerRemaining: 85
    }
  ]
}
```

### Get Customer List

```javascript
GET /api/customers

Response:
{
  customers: [
    {
      id: 'cust-001',
      name: 'Emma R.',
      status: 'online',
      claimHistory: 12,
      favoriteClasses: ['CrossFit', 'Spin']
    },
    // ... more customers
  ]
}
```

### Get Leaderboard

```javascript
GET /api/leaderboard

Response:
{
  round: {
    number: 2,
    timeRemaining: 180,
    totalRevenue: 1247,
    fillRate: 89
  },
  agents: [
    {
      rank: 1,
      name: 'ACE',
      revenue: 412,
      fills: 11,
      avgFillTime: 68,
      fillRate: 92
    },
    // ... more agents
  ]
}
```

---

## Rules & Scoring

### Points
- **Fill a spot:** Revenue recovered = points (e.g., $18 fill = 18 points)
- **Speed bonus:** Fills under 45s get 1.5x multiplier
- **Efficiency bonus:** High fill rate with low broadcast waste
- **Repeat customer bonus:** Same customer claims again

### Penalties
- **Timeouts:** No penalty, but $0 revenue
- **Spam:** Broadcasting to >100 people per drop may trigger penalty

### Win Conditions
1. **Revenue King:** Most total revenue
2. **Speed Demon:** Fastest average fill time
3. **Efficiency Master:** Best fill rate with minimal broadcast
4. **People's Choice:** Most repeat customer claims

---

## Example Agent Code

### Minimal Agent (Speed Strategy)

```javascript
const io = require('socket.io-client');
const axios = require('axios');

const BASE_URL = 'https://yu-arena-xxxxx.railway.app';
const socket = io(BASE_URL);

const AGENT_ID = 'my-speed-agent';

// Connect
socket.emit('agent:connect', {
  agentId: AGENT_ID,
  name: 'SpeedBot',
  strategy: 'speed'
});

// Listen for opportunities
socket.on('opportunity:spotted', async (data) => {
  try {
    // Claim immediately
    const claimRes = await axios.post(`${BASE_URL}/api/agents/${AGENT_ID}/claim`, {
      opportunityId: data.opportunityId
    });

    if (claimRes.data.claimed) {
      // Create aggressive drop
      const dropRes = await axios.post(`${BASE_URL}/api/agents/${AGENT_ID}/drop`, {
        opportunityId: data.opportunityId,
        price: Math.round(data.value * 0.65), // 35% discount
        timerSeconds: 60,
        audienceIds: 'rush_list'
      });

      // Broadcast
      await axios.post(`${BASE_URL}/api/agents/${AGENT_ID}/broadcast`, {
        dropId: dropRes.data.dropId,
        channel: 'whatsapp'
      });
    }
  } catch (error) {
    console.error('Error:', error.message);
  }
});

console.log('Agent running...');
```

---

## Support

- **Documentation:** https://yu-arena-xxxxx.railway.app/docs
- **API Status:** https://yu-arena-xxxxx.railway.app/api/health
- **GitHub Issues:** https://github.com/yourusername/yu-arena/issues

Good luck filling those spots! 🎯
```

---

## Next Steps

This architecture document provides everything needed to build the Flash Fill Arena in 3 days:

**Day 1:** Backend + Database + Agent Logic  
**Day 2:** Frontend + WebSocket Integration  
**Day 3:** Polish + Deploy + Record Demo  

Ready to start coding? Let me know which piece you want to tackle first! 🚀
