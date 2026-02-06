# Decentralized Event Registration & Ticketing Platform (DBO Project)

**NFT Tickets • Encrypted Access • Proof of Attendance**

> Built on **Sui** • **Walrus** • **Seal** • **ZkLogin**

> Technical Proposal by **Levuka Venture Labs FZCO** | February 2026

---

## Executive Summary

This proposal outlines our approach to building a decentralized event registration and ticketing platform that reimagines how events are created, tickets are issued, and attendance is verified. Current solutions like Luma, Eventbrite, and Google Forms rely on centralized data models where users surrender control of their event data to intermediaries. Our platform returns ownership to users while providing organizers with transparent, verifiable participant data.

The platform leverages **four core Sui ecosystem technologies**:
- **Sui smart contracts** for event registration, ticketing logic, and attendance verification
- **Walrus** for decentralized storage of event metadata and hosting of event-specific content sites
- **Seal** for encrypting sensitive ticket information accessible only to rightful holders
- **ZkLogin** for frictionless user onboarding without requiring existing crypto wallets

This is a medium-to-high complexity project with consumer-facing UX requirements and real-world operational considerations (venue check-in, QR scanning, payment processing). We estimate a **14-18 week delivery timeline** with a team of **5-6 FTE**, delivering an open-source platform with full documentation and a go-to-market strategy.

---

## 1. Skill Mix Required

This project requires a balanced team with expertise in smart contract development, consumer-grade frontend engineering, and protocol integrations. The user-facing nature of the platform demands strong UX focus alongside technical depth.

| Role | Allocation | Responsibilities |
|------|------------|------------------|
| **Sui/Move Developer** | 1.5 FTE | Smart contracts for events, tickets, attendance NFTs; Seal encryption integration; payment handling; soulbound token logic; upgrade patterns |
| **Full-Stack Engineer** | 2 FTE | Organizer dashboard; attendee registration flows; Walrus Sites deployment; QR code generation and scanning; mobile-responsive UI; calendar integrations |
| **UI/UX Designer** | 0.5 FTE | Event creation UX; ticket purchase flow; check-in experience; attendee profile pages; mobile-first design; brand identity |
| **DevOps/Infrastructure** | 0.5 FTE | Walrus Sites deployment pipeline; CI/CD; monitoring; QR scanning backend; notification infrastructure |
| **Product Manager** | 0.5 FTE | Requirements refinement; feature prioritization; GTM strategy; user research; competitive analysis; documentation oversight |
| **QA Engineer** | 0.5 FTE | End-to-end testing; mobile device testing; payment flow verification; check-in scenario testing; security testing |

**Total team size: 5.5-6 FTE** across the project lifecycle. This is a mid-sized team appropriate for a consumer-facing product with complex user flows and real-world operational requirements.

---

## 2. Planned Deliverables

### Phase 1: Core Infrastructure & Identity

- Technical design and architecture document covering all system components
- Move smart contracts for event creation with configurable parameters
- ZkLogin integration for passwordless user onboarding (Google, Apple, Twitch)
- Wallet connection support for existing Sui wallet users
- Basic organizer dashboard for event creation and management
- Walrus integration for event metadata storage (title, description, images)

### Phase 2: NFT Ticketing & Registration

- Ticket NFT smart contracts with configurable tiers, pricing, and capacity limits
- Seal encryption for sensitive ticket metadata (venue address, QR codes, access links)
- Registration flow with payment integration (SUI, stablecoins, fiat via Moonpay/similar)
- Discount code and promotional pricing support
- Optional approval flow for limited-capacity or invite-only events
- ICS calendar file generation for "Add to Calendar" functionality
- Attendee ticket viewing and management interface

### Phase 3: Walrus Sites & Event Content

- Walrus Sites deployment for event-specific content portals
- Ticket-gated access to event sites (agenda, speakers, media, announcements)
- Dynamic content updates for event organizers
- Template system for quick event site creation
- Mobile-optimized event site experience

### Phase 4: Check-In & Attendance Verification

- QR code generation embedded in encrypted ticket metadata
- Organizer check-in app/interface with QR scanning capability
- Wallet-based validation as alternative to QR scanning
- Attendance NFT minting upon successful check-in (soulbound optional)
- Real-time attendance tracking dashboard for organizers
- Duplicate check-in prevention and fraud detection

### Phase 5: Communications & Notifications

- Email notification integration for confirmations and reminders
- Wallet-based notification option for crypto-native users
- Event update broadcasts to ticket holders
- Optional event chat or community features

### Phase 6: Post-Event & Analytics

- Anonymized attendance data export for organizer analytics
- Ticket sales reporting with tax-ready formats
- Attendee profile pages showcasing attendance history
- User data control: ability to delete or revoke access to Walrus-stored data
- API endpoints for third-party integrations (airdrops, loyalty programs)

### Extended Features (Stretch Goals)

- Multi-track registration for conferences with different ticket tiers and agendas
- Lead capture and networking: opt-in profile sharing, contact exchange
- Badge printing integration for in-person events
- NFC-based check-in support as alternative to QR
- Sponsor activation integrations leveraging attendance data

### Documentation & GTM Deliverables

- Technical architecture document with system diagrams
- Smart contract documentation and security considerations
- Organizer user guide for event creation and management
- Attendee user guide for registration and ticket usage
- API documentation for third-party integrations
- Open-source repository (frontend + contracts) with contribution guidelines
- Go-to-market strategy document with target segments and launch plan

---

## 3. Projected Schedule

**Total estimated duration: 14-18 weeks** from kickoff to production launch. Extended features add 3-4 weeks if pursued. Phased delivery enables early user testing and feedback incorporation.

| Phase | Duration | Key Milestones |
|-------|----------|----------------|
| **Phase 0: Discovery & Design** | 2 weeks | Requirements validation; architecture document; UX wireframes; smart contract design; competitive analysis |
| **Phase 1: Core Infrastructure** | 2-3 weeks | Event contracts; ZkLogin integration; organizer dashboard scaffold; Walrus metadata storage |
| **Phase 2: NFT Ticketing** | 3-4 weeks | Ticket NFT contracts; Seal encryption; payment integration; registration flow; calendar files |
| **Phase 3: Walrus Sites** | 2 weeks | Event site templates; ticket-gated access; content management; mobile optimization |
| **Phase 4: Check-In & Attendance** | 2-3 weeks | QR generation/scanning; check-in interface; attendance NFT minting; fraud prevention |
| **Phase 5: Communications** | 1-2 weeks | Email notifications; wallet notifications; event updates; reminder scheduling |
| **Phase 6: Post-Event & Analytics** | 1-2 weeks | Analytics export; sales reports; attendee profiles; data control features; API finalization |
| **Phase 7: Polish & Launch** | 2 weeks | End-to-end testing; documentation; open-source prep; GTM strategy; production deployment |
| **Extended Features (Optional)** | 3-4 weeks | Multi-track registration; lead capture; badge printing; NFC support; sponsor integrations |

---

## 4. Cost Estimates

This is a medium-complexity project with consumer-facing requirements. Costs reflect the need for polished UX, real-world operational flows, and multi-protocol integration.

| Component | Effort (Hours) | Cost |
|-----------|----------------|------------|
| Phase 0: Discovery & Design | 100-130 |    |
| Phase 1: Core Infrastructure | 200-280 |   |
| Phase 2: NFT Ticketing | 300-400 |    |
| Phase 3: Walrus Sites | 150-200 |    |
| Phase 4: Check-In & Attendance | 200-280 |    |
| Phase 5: Communications | 100-150 |     |
| Phase 6: Post-Event & Analytics | 100-150 |    |
| Phase 7: Polish & Launch | 150-200 |    |
| UI/UX Design (throughout) | 120-160 |    |
| QA/Testing (throughout) | 120-160 |    |
| Infrastructure & Tooling |    | Included |
| **CORE MVP SUBTOTAL** | **1,540-2,110** | **$221K** |
| Extended Features | 300-450 | $42K |
| Security Audit (recommended) |    | $25K-45K |
| **TOTAL ESTIMATED RANGE** | **1,840-2,560** | **$246-308K** |

> **Notes:** Core MVP without extended features is $246K-265K. Security audit recommended for payment handling and encryption. Fiat payment gateway fees (Moonpay, etc.) are pass-through costs not included. Walrus storage costs are usage-dependent.

---

## 5. Software Stack

### Sui Ecosystem Integrations

| Technology | Purpose |
|------------|---------|
| **Sui Blockchain** | Smart contracts for events, tickets, attendance NFTs; payment handling; soulbound token logic |
| **Walrus Storage** | Event metadata storage; encrypted ticket blobs; attendee data with user-controlled deletion |
| **Walrus Sites** | Decentralized hosting for event-specific content portals; ticket-gated access |
| **Seal** | Encryption for sensitive ticket data (venue, QR codes, access links); policy-based decryption |
| **ZkLogin** | OAuth-based authentication for easy onboarding; Google/Apple/Twitch support |
| **SuiNS (optional)** | Human-readable names for organizers and repeat attendees |

### Frontend Technologies

| Technology | Purpose |
|------------|---------|
| **Next.js 14+** | React framework for organizer dashboard and attendee interfaces; SSR for SEO |
| **TypeScript** | Type safety across complex event and ticket data models |
| **TailwindCSS** | Utility-first styling for consistent, polished UI |
| **@mysten/dapp-kit** | Wallet connection and ZkLogin flows |
| **React QR Code** | QR code generation for tickets |
| **html5-qrcode** | QR code scanning for check-in interface |
| **ics.js** | Calendar file generation for "Add to Calendar" feature |

### Backend Technologies

| Technology | Purpose |
|------------|---------|
| **Node.js / Bun** | API server for event operations, notifications, and analytics |
| **PostgreSQL** | Event metadata cache; analytics aggregation; notification queues |
| **Redis** | Session management; real-time check-in state; rate limiting |
| **Prisma** | Type-safe ORM with schema migrations |
| **BullMQ** | Job queue for notifications, analytics processing, batch operations |

### Payments & Notifications

| Technology | Purpose |
|------------|---------|
| **Native SUI/Stables** | Direct crypto payments via smart contract |
| **Moonpay / Transak** | Fiat on-ramp for credit card payments (optional) |
| **Resend / SendGrid** | Email delivery for confirmations, reminders, updates |
| **XMTP (optional)** | Wallet-to-wallet messaging for crypto-native notifications |

### Infrastructure

| Technology | Purpose |
|------------|---------|
| **Vercel / Cloudflare** | Frontend hosting with edge functions and global CDN |
| **Docker / Fly.io** | Backend API hosting with auto-scaling |
| **GitHub Actions** | CI/CD pipelines for automated testing and deployment |
| **Sentry** | Error tracking and performance monitoring |
| **PostHog (optional)** | Product analytics for user behavior insights |

---

## 6. Anticipated Risks

This project has moderate technical risk with significant operational complexity due to real-world event scenarios. Risk assessment considers both technical challenges and user experience factors.

| Risk | Impact | Description & Mitigation |
|------|--------|--------------------------|
| **Check-In Reliability** | 🔴 LARGE | Network issues or slow blockchain confirmation at venue could cause check-in failures and attendee frustration. *Mitigation:* Offline-capable check-in with sync; optimistic UI; pre-cached ticket validation; fallback to wallet verification. |
| **Payment Processing** | 🔴 LARGE | Failed payments or stuck transactions could result in unhappy users and support burden. *Mitigation:* Transaction monitoring; automatic refund flows; clear payment status UI; fiat fallback option. |
| **Seal Encryption UX** | 🟡 MEDIUM | Decryption flow may be confusing for non-crypto users; key management adds complexity. *Mitigation:* Abstract encryption behind simple UI; automatic decryption on ticket view; clear error messaging. |
| **ZkLogin Provider Dependency** | 🟡 MEDIUM | OAuth provider outages could prevent user authentication. *Mitigation:* Support multiple providers; offer wallet connection as fallback; session persistence to reduce re-auth frequency. |
| **Walrus Sites Availability** | 🟡 MEDIUM | Event site unavailability during critical moments (day-of event) would impact attendee experience. *Mitigation:* CDN caching; health monitoring; fallback content delivery; essential info in ticket itself. |
| **Ticket Scalping/Fraud** | 🟡 MEDIUM | NFT tickets could be resold at markup or used fraudulently. *Mitigation:* Optional soulbound tickets; transfer restrictions; QR codes valid only for original holder; organizer-configurable policies. |
| **Fiat On-Ramp Friction** | 🟡 MEDIUM | KYC requirements and on-ramp delays may frustrate users expecting instant checkout. *Mitigation:* Clear messaging about processing times; offer crypto payment as fast alternative; pre-fund wallet option. |
| **Mobile QR Scanning** | 🟢 SMALL | Camera permissions, lighting conditions, or old devices may cause scanning issues. *Mitigation:* Test across device range; manual entry fallback; brightness adjustment prompts. |
| **Competitive Pressure** | 🟢 SMALL | Established platforms (Luma, Eventbrite) have network effects and user familiarity. *Mitigation:* Focus on unique Web3 value props; target crypto-native events initially; emphasize data ownership. |

---

## 7. High-Level Architecture

### 7.1 Overall System Architecture

The platform follows a **hybrid architecture** optimized for real-world event operations. Trust-critical data lives onchain while performance-sensitive operations use traditional infrastructure with blockchain anchoring.

```
┌─────────────────────────────────────────────────────────────────┐
│                    SYSTEM ARCHITECTURE                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │                 Application Layer                       │    │
│  │  • Next.js frontend (organizer + attendee)              │    │
│  │  • Node.js API (caching, notifications, analytics)      │    │
│  └─────────────────────────────────────────────────────────┘    │
│                              │                                  │
│          ┌───────────────────┼───────────────────┐              │
│          ▼                   ▼                   ▼              │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────┐         │
│  │   Onchain    │   │  Encryption  │   │   Storage    │         │
│  │  Layer (Sui) │   │ Layer (Seal) │   │Layer (Walrus)│         │
│  │ ──────────── │   │ ──────────── │   │ ──────────── │         │
│  │ • Event      │   │ • Venue info │   │ • Event      │         │
│  │   records    │   │ • QR codes   │   │   metadata   │         │
│  │ • Ticket     │   │ • Access     │   │ • Encrypted  │         │
│  │   NFTs       │   │   links      │   │   ticket     │         │
│  │ • Attendance │   │ • Policy:    │   │   blobs      │         │
│  │   NFTs       │   │   holder-    │   │ • Event site │         │
│  │ • Payments   │   │   only       │   │   assets     │         │
│  └──────────────┘   └──────────────┘   └──────────────┘         │
│                                                │                │
│                                                ▼                │
│                              ┌──────────────────────────┐       │
│                              │   Sites Layer            │       │
│                              │   (Walrus Sites)         │       │
│                              │ • Ticket-gated content   │       │
│                              │ • Event portals          │       │
│                              └──────────────────────────┘       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 7.2 Smart Contract Architecture

The contract system is modular with clear separation of concerns:

| Contract | Type | Purpose |
|----------|------|---------|
| **EventRegistry** | Shared Object | Event creation; stores event_id, organizer, metadata_blob_id, config |
| **EventConfig** | Owned Object | Capacity, pricing tiers, approval requirements, dates |
| **TicketNFT** | Transferable Object | Event access; links to encrypted Walrus blob |
| **AttendanceNFT** | Minted on Check-in | Optionally soulbound; contains event_id, timestamp, metadata |
| **PaymentHandler** | Module | SUI/stablecoin acceptance; escrow and release logic; refund support |
| **DiscountCode** | Shared Object | Promotional pricing; validates code and applies discount |

### 7.3 Ticket Lifecycle Flow

The complete ticket journey from purchase to proof-of-attendance:

```
┌─────────────────────────────────────────────────────────────────┐
│                    TICKET LIFECYCLE                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. REGISTRATION                                                │
│     └── User authenticates via ZkLogin or wallet                │
│     └── Selects event and tier                                  │
│                         │                                       │
│                         ▼                                       │
│  2. PAYMENT                                                     │
│     └── User pays in SUI/stables/fiat                           │
│     └── Payment held in escrow                                  │
│                         │                                       │
│                         ▼                                       │
│  3. TICKET MINTING                                              │
│     └── TicketNFT minted to user                                │
│     └── Encrypted metadata blob created on Walrus               │
│                         │                                       │
│                         ▼                                       │
│  4. CONFIRMATION                                                │
│     └── Email/notification sent with calendar file              │
│     └── Payment released to organizer                           │
│                         │                                       │
│                         ▼                                       │
│  5. PRE-EVENT                                                   │
│     └── User decrypts ticket to view:                           │
│         • Venue details                                         │
│         • QR code                                               │
│         • Event site access                                     │
│                         │                                       │
│                         ▼                                       │
│  6. CHECK-IN                                                    │
│     └── QR scanned at venue                                     │
│     └── Onchain verification of ticket ownership                │
│                         │                                       │
│                         ▼                                       │
│  7. ATTENDANCE                                                  │
│     └── AttendanceNFT minted                                    │
│     └── Ticket marked as "used" (prevents re-entry)             │
│                         │                                       │
│                         ▼                                       │
│  8. POST-EVENT                                                  │
│     └── Attendance NFT remains as verifiable proof              │
│     └── Eligible for airdrops/rewards                           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 7.4 Encryption Strategy (Seal Integration)

Sensitive ticket information is encrypted using Seal with holder-only access:

| Aspect | Details |
|--------|---------|
| **Encrypted Fields** | Venue address, access instructions, QR code data, private event links |
| **Access Policy** | `owner == ticket_nft.owner` — only current holder can decrypt |
| **Transfer Handling** | On ticket transfer, new owner gains decryption rights automatically |
| **Dynamic Updates** | Organizers can update encrypted content (e.g., venue change) with re-encryption |

### 7.5 Walrus Sites Architecture

Each event has a dedicated Walrus Site for ticket-gated content:

- **Site Structure:** Static site with dynamic content injection based on ticket verification
- **Access Control:** Site checks for valid TicketNFT in connected wallet before revealing content
- **Content Types:** Agenda, speaker bios, venue maps, live updates, media galleries, announcements
- **Templates:** Pre-built templates for common event types (conference, meetup, concert)
- **Persistence:** Event sites remain accessible post-event for content archives and references

### 7.6 Check-In System Design

The check-in system is designed for **reliability in real-world venue conditions**:

```
┌─────────────────────────────────────────────────────────────────┐
│                    CHECK-IN FLOW                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  QR CODE CONTENTS                                               │
│  └── Signed message containing:                                 │
│      • ticket_id                                                │
│      • event_id                                                 │
│      • holder address                                           │
│                         │                                       │
│                         ▼                                       │
│  VERIFICATION FLOW                                              │
│  └── Scan QR ──► Verify signature ──► Check onchain ──► Mark    │
│                                        ownership       attended │
│                         │                                       │
│                         ▼                                       │
│  OFFLINE MODE                                                   │
│  └── Pre-cache expected attendees                               │
│  └── Sync check-ins when connectivity restored                  │
│                         │                                       │
│                         ▼                                       │
│  OPTIMISTIC UI                                                  │
│  └── Show "Checked In" immediately                              │
│  └── Handle blockchain confirmation in background               │
│                         │                                       │
│                         ▼                                       │
│  FALLBACKS                                                      │
│  └── Wallet-based verification if QR fails                      │
│  └── Manual lookup by attendee name/email                       │
│                         │                                       │
│                         ▼                                       │
│  DUPLICATE PREVENTION                                           │
│  └── Check-in state stored onchain and cached locally           │
│  └── Prevents re-entry                                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 7.7 Data Composability

Attendance data becomes composable for the broader ecosystem:

| Use Case | Description |
|----------|-------------|
| **Attendance NFTs** | Verifiable proof-of-presence usable by any dApp querying the holder's wallet |
| **Airdrop Targeting** | Projects can filter by attendance at specific events or organizers |
| **Reputation Building** | Attendees accumulate verifiable event history across the ecosystem |
| **Loyalty Programs** | Organizers can reward repeat attendees based on historical participation |
| **API Access** | RESTful endpoints for querying attendance data with appropriate permissions |

---

## 8. Go-to-Market Strategy Overview

A comprehensive GTM strategy document will be delivered as part of the project. Key elements include:

### 8.1 Target Segments

| Segment | Description |
|---------|-------------|
| **Primary** | Crypto/Web3 community events, hackathons, meetups — audiences already familiar with wallets |
| **Secondary** | NFT drops and token launches with exclusive access events |
| **Tertiary** | Tech conferences seeking verifiable attendance and reduced ticket fraud |

### 8.2 Differentiation

- **True ticket ownership:** Attendees own their tickets, not just a database entry
- **Verifiable attendance:** Proof-of-presence enables airdrops, loyalty, and reputation
- **Data sovereignty:** Users control their event data; can delete or revoke access
- **Composability:** Attendance data usable across the Sui ecosystem

### 8.3 Launch Strategy

- Pilot with 3-5 Sui ecosystem events to validate product-market fit
- Partner with Sui Foundation for visibility and credibility
- Open-source release to encourage ecosystem adoption and contributions
- Case studies from pilot events demonstrating value propositions

---

## 9. Conclusion and Next Steps

The Decentralized Event Registration & Ticketing Platform represents a compelling application of Sui ecosystem technologies to a real-world use case with clear market demand. By combining NFT ticketing, encrypted access, and verifiable attendance, we create value for organizers, attendees, and the broader ecosystem.

---

<p align="center">
  <strong>Levuka Venture Labs FZCO</strong><br>
  February 2026
</p>
