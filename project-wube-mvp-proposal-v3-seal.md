# Project Wube: Short-Form Video Infrastructure MVP

**Upload • Store • Encrypt • Stream**

> Built on **Walrus** • **Sui** • **Seal**

> Technical Proposal by **Levuka Venture Labs FZCO** | February 2026

---

## Executive Summary

This proposal presents **Project Wube**, a deliberately constrained minimum viable product for decentralized video infrastructure on the Sui/Walrus ecosystem. Rather than competing head-to-head with full-featured platforms like Mux or Cloudflare Stream, Wube targets a specific, underserved niche: **short-form video content (≤5 minutes)** with policy-based access control powered by Seal encryption.

**Wube takes a unique approach:** deliver a focused, production-ready tool that handles the most common Web3 video use cases exceptionally well, with **native encryption and access controls** as a core differentiator from centralized alternatives.

### MVP Constraints (By Design)

| Constraint | Limit | Rationale |
|------------|-------|-----------|
| **Maximum Duration** | 5 minutes | Covers 80%+ of Web3 video use cases; simplifies playback |
| **Maximum File Size** | 8 GB | Supports all consumer 4K formats including H.264 at 60fps |
| **Supported Inputs** | MP4, MOV, WebM | Covers iPhone, Android, and web-native recordings |
| **Delivery Format** | MP4 (H.264/AAC) | Universal browser playback; no client-side codec issues |
| **Access Control** | Public, Owner-only, Shared List, NFT-gated | Seal encryption with policy-based decryption |
| **Analytics** | Basic metrics only | View counts, bandwidth; defer advanced analytics |

### File Size Reality Check

We sized the 8 GB limit based on actual device output:

| Source | Bitrate | Per Minute | 5 Minutes | Supported? |
|--------|---------|------------|-----------|------------|
| iPhone 4K HEVC 30fps | ~54 Mbps | ~400 MB | **~2 GB** | ✅ Yes |
| iPhone 4K HEVC 60fps | ~100 Mbps | ~750 MB | **~3.75 GB** | ✅ Yes |
| iPhone 1080p 60fps HEVC | ~28 Mbps | ~210 MB | **~1.05 GB** | ✅ Yes |
| GoPro 4K 60fps (100Mbps) | 100 Mbps | ~750 MB | **~3.75 GB** | ✅ Yes |
| Android 4K HEVC | ~54 Mbps | ~400 MB | **~2 GB** | ✅ Yes |
| iPhone 4K H.264 30fps | ~135 Mbps | ~1 GB | **~5 GB** | ✅ Yes |
| iPhone 4K H.264 60fps | ~200 Mbps | ~1.5 GB | **~7.5 GB** | ⚠️ Borderline |
| iPhone ProRes 4K 30fps | ~1000 Mbps | ~6 GB | **~30 GB** | ❌ No |

**ProRes and RAW formats are explicitly out of scope**—these are professional production formats that require transcoding before distribution regardless of platform.

### What This Enables

With Seal encryption, Wube enables **premium Web3 video use cases**:

- **Token-gated content:** NFT holders can view exclusive videos
- **Private DAO communications:** Encrypted proposal videos visible only to members
- **Premium creator content:** Subscription or one-time payment for access
- **Confidential business videos:** Share with specific wallet addresses only
- **Time-limited access:** Unlock videos for specific time windows

Plus standard use cases:
- DAO proposal explainer videos (typically 2-3 minutes)
- NFT reveal/preview videos (typically 30-60 seconds)
- Protocol tutorial clips (typically 3-5 minutes)
- Creator teaser content (typically 1-2 minutes)

**Estimated cost: $197.5K over 14-16 weeks (price does not include audit costs)** 

---

## 1. Scope Definition: What's In, What's Out

### 1.1 In Scope (MVP)

```
┌─────────────────────────────────────────────────────────────────┐
│                    WUBE MVP SCOPE                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  UPLOAD                                                         │
│  ✓ Chunked upload (required for files up to 5 GB)               │
│  ✓ Resumable uploads (survive network interruption)             │
│  ✓ Parallel chunk upload (performance optimization)             │
│  ✓ Client-side chunking via SDK                                 │
│  ✓ Format validation (MP4, MOV, WebM containers)                │
│  ✓ Codec validation (H.264, H.265/HEVC, VP8, VP9)               │
│  ✓ Duration validation (reject >5 minutes)                      │
│  ✓ Metadata extraction (duration, resolution, bitrate, codec)   │
│  ✓ Progress indication with chunk-level granularity             │
│  ✓ Walrus blob storage (one blob per chunk)                     │
│  ✓ Manifest generation linking chunks                           │
│                                                                 │
│  ENCRYPTION (Seal Integration)                                  │
│  ✓ Chunk-level encryption before Walrus storage                 │
│  ✓ Policy-based access control                                  │
│  ✓ Access policies: public, owner-only, shared list, NFT-gated  │
│  ✓ On-chain policy storage and verification                     │
│  ✓ Decryption key retrieval for authorized viewers              │
│  ✓ Policy updates without re-upload                             │
│                                                                 │
│  PLAYBACK                                                       │
│  ✓ Policy verification before playback                          │
│  ✓ Transparent chunk decryption for authorized viewers          │
│  ✓ Byte-range request support (seeking)                         │
│  ✓ Browser-native playback (MP4 delivery)                       │
│  ✓ Lightweight aggregation service (decrypt + stitch)           │
│  ✓ Embeddable player component with auth flow                   │
│                                                                 │
│  OWNERSHIP & CONTROL                                            │
│  ✓ On-chain video asset registration (Sui object)               │
│  ✓ Ownership transfer capability                                │
│  ✓ Access policy management                                     │
│  ✓ Delete capability (Walrus blobs + on-chain record)           │
│                                                                 │
│  DEVELOPER EXPERIENCE                                           │
│  ✓ REST API for all operations                                  │
│  ✓ TypeScript SDK with chunked upload + encryption              │
│  ✓ API key authentication                                       │
│  ✓ Webhook on upload complete                                   │
│  ✓ Documentation site                                           │
│                                                                 │
│  BASIC ANALYTICS                                                │
│  ✓ View count per video (authorized views only)                 │
│  ✓ Total bandwidth consumed                                     │
│  ✓ Storage usage per account                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 1.2 Explicitly Out of Scope (Deferred to v2+)

| Feature | Complexity | Deferral Rationale |
|---------|------------|-------------------|
| **Transcoding pipeline** | Very High | Accept web-compatible formats only; no server-side conversion |
| **Adaptive bitrate (HLS/DASH)** | Very High | Single-quality delivery for MVP |
| **Payment-gated access** | Medium | Requires payment infrastructure; defer to v2 |
| **Multi-tier caching (CDN)** | High | Simple in-memory cache sufficient for MVP scale |
| **Advanced analytics** | Medium | Basic counters sufficient for MVP |
| **ProRes/RAW support** | Medium | Professional formats require transcoding |
| **Live streaming** | Very High | Entirely different architecture |
| **Key rotation** | Medium | Defer to v2; adds significant complexity |

### 1.3 Input Validation Rules

The system enforces constraints at upload time:

```
┌─────────────────────────────────────────────────────────────────┐
│                 UPLOAD VALIDATION                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  PRE-UPLOAD VALIDATION (Client-side + Server confirmation)      │
│  ├── File size ≤ 5 GB                                           │
│  │   └── Reject: "File exceeds 5 GB limit"                      │
│  ├── File extension ∈ {.mp4, .mov, .webm}                       │
│  │   └── Reject: "Unsupported format. Use MP4, MOV, or WebM"    │
│  └── MIME type ∈ {video/mp4, video/quicktime, video/webm}       │
│      └── Reject: "Invalid file type"                            │
│                                                                 │
│  POST-UPLOAD VALIDATION (Server-side, after chunks assembled)   │
│  ├── Container ∈ {MP4, MOV, WebM}                               │
│  │   └── Reject: "Invalid container format"                     │
│  ├── Video codec ∈ {H.264, H.265/HEVC, VP8, VP9}                │
│  │   └── Reject: "Unsupported video codec"                      │
│  ├── Audio codec ∈ {AAC, MP3, Opus, Vorbis, none}               │
│  │   └── Reject: "Unsupported audio codec"                      │
│  ├── Duration ≤ 300 seconds (5 minutes)                         │
│  │   └── Reject: "Video exceeds 5 minute limit"                 │
│  ├── Resolution ≤ 4K (3840x2160)                                │
│  │   └── Reject: "Resolution exceeds 4K limit"                  │
│  └── Bitrate ≤ 150 Mbps                                         │
│      └── Reject: "Bitrate too high; please re-encode"           │
│                                                                 │
│  ON VALIDATION SUCCESS                                          │
│  └── Encrypt chunks with Seal → Store to Walrus → Register      │
│                                                                 │
│  ON VALIDATION FAILURE                                          │
│  └── Delete temporary chunks; return error; no charge           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. Technical Architecture

### 2.1 System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                 WUBE MVP ARCHITECTURE                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                      ┌─────────────┐                            │
│                      │   Client    │                            │
│                      │ Application │                            │
│                      └──────┬──────┘                            │
│                             │                                   │
│                      ┌──────┴──────┐                            │
│                      │  Wube SDK   │                            │
│                      │ (Chunking)  │                            │
│                      └──────┬──────┘                            │
│                             │                                   │
│              ┌──────────────┼──────────────┐                    │
│              │              │              │                    │
│              ▼              ▼              ▼                    │
│       ┌──────────┐   ┌──────────┐   ┌──────────┐                │
│       │  Upload  │   │   API    │   │ Playback │                │
│       │ Service  │   │  Server  │   │ Service  │                │
│       │+Encrypt  │   │          │   │+Decrypt  │                │
│       └────┬─────┘   └────┬─────┘   └────┬─────┘                │
│            │              │              │                      │
│            │         ┌────┴────┐         │                      │
│            │         │ Postgres│         │                      │
│            │         │Metadata │         │                      │
│            │         │+Manifest│         │                      │
│            │         └─────────┘         │                      │
│            │              │              │                      │
│            │              ▼              │                      │
│            │    ┌─────────────────┐      │                      │
│            │    │  Seal Network   │      │                      │
│            │    │ (Key Management)│      │                      │
│            │    │ Policy Storage  │      │                      │
│            │    └─────────────────┘      │                      │
│            │                             │                      │
│            ▼                             ▼                      │
│       ┌─────────────────────────────────────┐                   │
│       │           Walrus Storage            │                   │
│       │   (Encrypted chunks per video)      │                   │
│       │  EncChunk1│EncChunk2│...│EncChunkN  │                   │
│       └─────────────────────────────────────┘                   │
│                             │                                   │
│                             ▼                                   │
│       ┌─────────────────────────────────────┐                   │
│       │         Sui Blockchain              │                   │
│       │  VideoAsset + AccessPolicy objects  │                   │
│       └─────────────────────────────────────┘                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.2 Seal Encryption Architecture

Seal provides policy-based encryption where access is determined by on-chain conditions:

```
┌─────────────────────────────────────────────────────────────────┐
│                 SEAL ENCRYPTION MODEL                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ENCRYPTION FLOW (Upload)                                       │
│                                                                 │
│  1. Video validated and chunked                                 │
│  2. For each chunk:                                             │
│     ├── Generate content encryption key (CEK)                   │
│     ├── Encrypt chunk with CEK (AES-256-GCM)                    │
│     ├── Encrypt CEK with Seal (policy-bound)                    │
│     └── Store encrypted chunk to Walrus                         │
│  3. Store encrypted CEKs in manifest                            │
│  4. Register VideoAsset + AccessPolicy on Sui                   │
│                                                                 │
│  DECRYPTION FLOW (Playback)                                     │
│                                                                 │
│  1. Viewer requests playback                                    │
│  2. Playback service fetches AccessPolicy from Sui              │
│  3. Verify viewer satisfies policy:                             │
│     ├── Public: Always allowed                                  │
│     ├── Owner-only: viewer == owner                             │
│     ├── Shared list: viewer ∈ allowed_addresses                 │
│     └── NFT-gated: viewer owns required NFT                     │
│  4. If authorized:                                              │
│     ├── Request decryption keys from Seal                       │
│     ├── Seal verifies policy on-chain                           │
│     ├── Seal returns CEKs for requested chunks                  │
│     └── Playback service decrypts and streams                   │
│  5. If unauthorized:                                            │
│     └── Return 403 Forbidden                                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.3 Access Policy Types

```
┌─────────────────────────────────────────────────────────────────┐
│                 ACCESS POLICY TYPES                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. PUBLIC                                                      │
│     ├── Policy: "allow_all"                                     │
│     ├── Encryption: Still encrypted (defense in depth)          │
│     ├── Decryption: Automatic for any viewer                    │
│     └── Use case: Free content, previews, public announcements  │
│                                                                 │
│  2. OWNER_ONLY                                                  │
│     ├── Policy: "viewer == video.owner"                         │
│     ├── Encryption: Standard Seal encryption                    │
│     ├── Decryption: Only owner can decrypt                      │
│     └── Use case: Personal videos, drafts, private archive      │
│                                                                 │
│  3. SHARED_LIST                                                 │
│     ├── Policy: "viewer ∈ allowed_addresses[]"                  │
│     ├── Encryption: Standard Seal encryption                    │
│     ├── Decryption: Listed addresses can decrypt                │
│     ├── Management: Owner can add/remove addresses              │
│     └── Use case: Team videos, private shares, collaborations   │
│                                                                 │
│  4. NFT_GATED                                                   │
│     ├── Policy: "viewer.owns(nft_collection_id)"                │
│     ├── Encryption: Standard Seal encryption                    │
│     ├── Decryption: NFT holders can decrypt                     │
│     ├── Verification: On-chain NFT ownership check              │
│     └── Use case: Exclusive content, membership perks           │
│                                                                 │
│  POLICY UPDATES (Without Re-encryption)                         │
│  ├── Change visibility: Public ↔ Owner-only                     │
│  ├── Modify shared list: Add/remove addresses                   │
│  ├── Change NFT requirement: Different collection               │
│  └── Seal re-evaluates policy on each access request            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.4 Chunked Upload with Encryption

```
┌─────────────────────────────────────────────────────────────────┐
│                 UPLOAD FLOW (WITH ENCRYPTION)                   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. INITIATION                                                  │
│     Client: POST /videos/upload/init                            │
│     ├── file_name, file_size, content_type                      │
│     ├── metadata: { title, description }                        │
│     └── access_policy: { type, params }                         │
│                                                                 │
│     Server Response:                                            │
│     ├── upload_id: "upl_abc123"                                 │
│     ├── chunk_size: 50,000,000 (50 MB)                          │
│     ├── total_chunks: 50                                        │
│     └── encryption_public_key (for client-side encrypt option)  │
│                                                                 │
│  2. CHUNK UPLOAD (Parallel, Resumable)                          │
│     Client uploads raw chunks                                   │
│     Server receives and stores temporarily                      │
│                                                                 │
│  3. COMPLETION & ENCRYPTION                                     │
│     Client: POST /videos/upload/{upload_id}/complete            │
│                                                                 │
│     Server Processing:                                          │
│     ├── Verify all chunks received                              │
│     ├── Reassemble temporarily for validation                   │
│     ├── FFprobe: Validate format, duration, codec               │
│     ├── If valid:                                               │
│     │   ├── For each chunk:                                     │
│     │   │   ├── Generate CEK (content encryption key)           │
│     │   │   ├── Encrypt chunk with CEK                          │
│     │   │   ├── Seal-encrypt CEK with access policy             │
│     │   │   └── Upload encrypted chunk to Walrus                │
│     │   ├── Generate manifest with encrypted CEKs               │
│     │   ├── Store manifest to Walrus                            │
│     │   ├── Create AccessPolicy object on Sui                   │
│     │   ├── Register VideoAsset on Sui (refs policy)            │
│     │   └── Fire completion webhook                             │
│     └── If invalid:                                             │
│         └── Delete temp chunks; return error                    │
│                                                                 │
│     Response:                                                   │
│     ├── video_id: "vid_xyz789"                                  │
│     ├── status: "ready"                                         │
│     ├── playback_url: "https://..."                             │
│     ├── access_policy_id: "0x..."                               │
│     └── metadata: { duration, resolution, ... }                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.5 Playback with Decryption

```
┌─────────────────────────────────────────────────────────────────┐
│                 PLAYBACK FLOW (WITH DECRYPTION)                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. PLAYBACK REQUEST                                            │
│     Browser: GET /videos/{video_id}/stream                      │
│     Header: Range: bytes=0-                                     │
│     Auth: Bearer token (wallet signature or API key)            │
│                                                                 │
│  2. AUTHORIZATION CHECK                                         │
│     Playback Service:                                           │
│     ├── Fetch VideoAsset from Sui (get policy_id)               │
│     ├── Fetch AccessPolicy from Sui                             │
│     ├── Identify viewer (from auth token)                       │
│     └── Evaluate policy:                                        │
│         ├── PUBLIC → Authorized                                 │
│         ├── OWNER_ONLY → Check viewer == owner                  │
│         ├── SHARED_LIST → Check viewer in list                  │
│         └── NFT_GATED → Check NFT ownership on-chain            │
│                                                                 │
│  3. KEY RETRIEVAL (If Authorized)                               │
│     Playback Service → Seal Network:                            │
│     ├── Request CEKs for required chunks                        │
│     ├── Seal verifies policy satisfaction                       │
│     └── Seal returns decryption keys                            │
│                                                                 │
│  4. DECRYPTION & STREAMING                                      │
│     ├── Fetch encrypted chunk(s) from Walrus                    │
│     ├── Decrypt with CEK                                        │
│     ├── Cache decrypted chunk (medium TTL, memory/disk hybrid)  │
│     └── Stream to viewer with Content-Range header              │
│                                                                 │
│  5. RESPONSE                                                    │
│     HTTP/1.1 206 Partial Content                                │
│     Content-Type: video/mp4                                     │
│     Content-Range: bytes 0-50000000/2500000000                  │
│     [Decrypted video data]                                      │
│                                                                 │
│  CACHING CONSIDERATIONS                                         │
│  ├── Encrypted chunks: Can cache indefinitely                   │
│  ├── Decrypted chunks: Cache briefly (60 min) per session       │
│  ├── CEKs: Cache per viewer session (memory only)               │
│  └── Policy evaluation: Cache for 10 minutes                    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.6 An Example Manifest Structure (With Encryption)

```json
{
  "version": "1.0",
  "video_id": "vid_xyz789",
  "created_at": "2026-02-15T10:30:00Z",
  "file_name": "my_video.mp4",
  "content_type": "video/mp4",
  "total_size": 2500000000,
  "duration_ms": 245000,
  "resolution": {
    "width": 3840,
    "height": 2160
  },
  "video_codec": "h264",
  "audio_codec": "aac",
  "bitrate_kbps": 81632,
  
  "encryption": {
    "scheme": "seal-aes-256-gcm",
    "policy_object_id": "0xpolicy123...",
    "video_asset_id": "0xvideo456..."
  },
  
  "chunks": [
    {
      "index": 0,
      "blob_id": "wal_enc_chunk_001",
      "encrypted_size": 50000128,
      "plaintext_size": 50000000,
      "offset": 0,
      "encrypted_cek": "seal:abc123...",
      "iv": "base64:random_iv_1...",
      "auth_tag": "base64:tag_1..."
    },
    {
      "index": 1,
      "blob_id": "wal_enc_chunk_002",
      "encrypted_size": 50000128,
      "plaintext_size": 50000000,
      "offset": 50000000,
      "encrypted_cek": "seal:def456...",
      "iv": "base64:random_iv_2...",
      "auth_tag": "base64:tag_2..."
    }
  ],
  
  "checksum": "sha256:full_plaintext_hash..."
}
```

### 2.7 An Example Smart Contract Architecture (subject to change)

```
┌─────────────────────────────────────────────────────────────────┐
│              SMART CONTRACT ARCHITECTURE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  MODULE: wube::video                                            │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  VideoAsset {                                           │    │
│  │    id: UID,                                             │    │
│  │    owner: address,                                      │    │
│  │    manifest_blob_id: String,                            │    │
│  │    title: String,                                       │    │
│  │    description: Option<String>,                         │    │
│  │    duration_ms: u64,                                    │    │
│  │    file_size: u64,                                      │    │
│  │    resolution: String,                                  │    │
│  │    chunk_count: u64,                                    │    │
│  │    access_policy_id: ID,    // Reference to policy      │    │
│  │    created_at: u64,                                     │    │
│  │  }                                                      │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                 │
│  MODULE: wube::access_policy                                    │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  AccessPolicy {                                         │    │
│  │    id: UID,                                             │    │
│  │    video_id: ID,                                        │    │
│  │    owner: address,                                      │    │
│  │    policy_type: PolicyType,                             │    │
│  │    // Type-specific fields:                             │    │
│  │    allowed_addresses: Option<vector<address>>,          │    │
│  │    required_nft_type: Option<String>,                   │    │
│  │    updated_at: u64,                                     │    │
│  │  }                                                      │    │
│  │                                                         │    │
│  │  enum PolicyType {                                      │    │
│  │    Public,                                              │    │
│  │    OwnerOnly,                                           │    │
│  │    SharedList,                                          │    │
│  │    NftGated,                                            │    │
│  │  }                                                      │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                 │
│  FUNCTIONS                                                      │
│  ├── register_video(manifest, metadata, policy) -> VideoAsset   │
│  ├── transfer_video(video, recipient)                           │
│  ├── update_metadata(video, title, desc)                        │
│  ├── delete_video(video)                                        │
│  │                                                              │
│  │  // Access Policy Management                                 │
│  ├── set_public(policy)                                         │
│  ├── set_owner_only(policy)                                     │
│  ├── set_shared_list(policy, addresses[])                       │
│  ├── add_to_shared_list(policy, address)                        │
│  ├── remove_from_shared_list(policy, address)                   │
│  ├── set_nft_gated(policy, nft_type)                            │
│  └── check_access(policy, viewer) -> bool                       │
│                                                                 │
│  EVENTS                                                         │
│  ├── VideoCreated { video_id, owner, policy_id }                │
│  ├── VideoTransferred { video_id, from, to }                    │
│  ├── VideoDeleted { video_id, owner }                           │
│  ├── PolicyUpdated { policy_id, policy_type }                   │
│  └── AccessGranted { policy_id, viewer }                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 3. Skill Mix Required

Adding Seal encryption increases the team requirements:

| Role | Allocation | Responsibilities |
|------|------------|------------------|
| **Backend Engineer** | 2 FTE | Upload service with chunking; playback service with byte-range handling; Walrus integration; manifest management |
| **Sui/Move Developer** | 1 FTE | VideoAsset + AccessPolicy contracts; on-chain registration; policy verification logic |
| **Cryptography/Security Engineer** | 1 FTE | Seal integration; encryption/decryption flows; key management; security review |
| **Full-Stack/SDK Engineer** | 1 FTE | TypeScript SDK with encryption handling; embeddable player with auth; developer console; documentation |
| **DevOps** | 1 FTE | Deployment; monitoring; CI/CD; caching infrastructure |
| **Product/QA** | 1 FTE | Requirements validation; security testing; documentation review |

**Total: 6 FTE** over the project lifecycle.


## 4. Planned Deliverables

### Phase 0: Design & Setup (Weeks 1-2)

- Technical architecture document
- API contract specification (OpenAPI)
- Chunked upload protocol specification
- **Seal integration design document**
- **Access policy schema design**
- Smart contract interface design
- Development environment setup
- Walrus integration spike
- **Seal integration spike**

### Phase 1: Upload Service & Chunking (Weeks 3-6)

- Chunk upload endpoint with integrity verification
- Upload session management (init, status, resume, complete)
- Parallel upload handling
- Temporary chunk storage
- File reassembly for validation
- Format/codec/duration validation via FFprobe
- **Chunk encryption with Seal**
- Walrus blob upload for encrypted chunks
- **Manifest generation with encrypted CEKs**

### Phase 2: On-Chain Integration (Weeks 5-8)

- VideoAsset Move module
- **AccessPolicy Move module**
- **Policy types: Public, OwnerOnly, SharedList, NftGated**
- Registration, transfer, delete functions
- **Policy update functions**
- **Access verification functions**
- Event emission
- On-chain/off-chain synchronization
- Sui SDK integration in backend

### Phase 3: Playback Service with Decryption (Weeks 8-12)

- **Policy verification flow**
- **Seal key retrieval for authorized viewers**
- **Chunk decryption**
- Manifest-based chunk lookup
- Byte-range request handling
- Chunk fetching from Walrus
- **Decrypted chunk caching (short TTL)**
- Response streaming
- **Auth token verification (wallet signature)**

### Phase 4: API & Developer Experience (Weeks 10-14)

- REST API implementation
  - `POST /videos/upload/init` - initiate with access policy
  - `PUT /videos/upload/{id}/chunks/{n}` - upload chunk
  - `GET /videos/upload/{id}/status` - check progress
  - `POST /videos/upload/{id}/complete` - finalize + encrypt
  - `GET /videos/{id}` - retrieve metadata
  - `GET /videos/{id}/stream` - **authenticated playback**
  - `PATCH /videos/{id}` - update metadata
  - **`PATCH /videos/{id}/policy` - update access policy**
  - `DELETE /videos/{id}` - remove video
  - `GET /videos` - list user's videos
- TypeScript SDK with **encryption abstraction**
- Embeddable player component **with wallet auth flow**
- Developer console (API key management, video library, **policy management**)
- Webhook configuration

### Phase 5: Documentation & Launch (Weeks 14-16)

- API reference documentation
- SDK documentation with examples
- **Access control guide**
- **Security documentation**
- Integration quickstart guide
- Deployment to production
- Security review and remediation
- Beta testing with 3-5 ecosystem partners

---

## 5. Projected Schedule

**Total duration: 14-16 weeks**

```
┌─────────────────────────────────────────────────────────────────┐
│                 PROJECT SCHEDULE                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Week:  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16         │
│         │  │  │  │  │  │  │  │  │  │  │  │  │  │  │  │          │
│                                                                 |
|  P0: Design & Setup (+ Seal Design)                             │
│         |-------|                                               │
│                                                                 │
│  P1: Upload Service & Encryption                                │
│             |----------------|                                  │
│                                                                 │
│  P2: On-Chain + Access Policies                                 │
│                 |---------------|                               │
│                                                                 │
│  P3: Playback Service + Decryption                              │
│                         |-------------------|                   │
│                                                                 │
│  P4: API & Developer Experience                                 │
│                                 |-------------------|            │
│                                                                 │
│  P5: Documentation & Launch                                     │
│                                             |-----------|       │
│                                                                 │
│  KEY MILESTONES:                                                │
│  • Week 2:  Architecture + Seal design approved                 │
│  • Week 6:  Encrypted upload pipeline functional                │
│  • Week 8:  Access policies on testnet                          │
│  • Week 12: Authenticated playback functional                   │
│  • Week 14: SDK published                                       │
│  • Week 16: Production launch                                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 6. Cost Estimates

### 6.1 Development Costs

| Component | Effort (Hours) | Cost |
|-----------|----------------|------|
| Phase 0: Design & Setup (+ Seal) | 300 |   |
| Phase 1: Upload + Encryption | 600 |   |
| Phase 2: On-Chain + Policies | 300 |   |
| Phase 3: Playback + Decryption | 600 |   |
| Phase 4: API & Developer Experience | 400 |   |
| Phase 5: Documentation & Launch | 240 |   |
| **Development Subtotal** | **2440** | **$183.5K** |

### 6.2 Additional Costs

| Component | Cost | Notes |
|-----------|------|-------|
| Infrastructure (dev + staging) | $6K-10K | API servers, caching, Seal integration |
| Walrus storage (testing) | $2K-4K | Encrypted chunk storage |
| Security audit (focused) | $25K-32K | Encryption flows, smart contracts, access control |
| **Additional Subtotal** | | **$33K-46K** |

### 6.3 Total Cost Summary

| Category | Estimate |
|----------|--------------|
| Development | $183.5 |
| Infrastructure & Testing | $14K |
| Security Audit | $32K |
| **TOTAL** | **$229.5K** |

**Target: $200K** — achievable if audits are deferred until version 2 (post MVP).

## 7. Proposed Technical Stack (subject to change)

### 7.1 Backend

| Technology | Purpose |
|------------|---------|
| **Node.js (Bun runtime)** | API server; upload handling; playback service |
| **PostgreSQL** | Video metadata; manifests; upload sessions; user accounts |
| **Redis** | Chunk caching; session state; **decrypted chunk cache**; rate limiting |
| **FFprobe** | Metadata extraction; format/codec validation |
| **Walrus SDK** | Blob storage integration |
| **@mysten/sui** | On-chain interaction |
| **Seal SDK** | **Encryption/decryption; key management** |

### 7.2 Cryptography

| Technology | Purpose |
|------------|---------|
| **Seal Protocol** | Policy-based encryption; key management |
| **AES-256-GCM** | Symmetric encryption for video chunks |
| **libsodium** | Cryptographic primitives |

### 7.3 Frontend / SDK

| Technology | Purpose |
|------------|---------|
| **TypeScript** | SDK implementation with encryption handling |
| **React** | Embeddable player component with auth flow |
| **@mysten/dapp-kit** | **Wallet connection for viewer authentication** |
| **Next.js** | Developer console; documentation site |

### 7.4 Infrastructure

| Technology | Purpose |
|------------|---------|
| **Railway / Render** | API and playback service hosting |
| **Supabase / Neon** | Managed PostgreSQL |
| **Upstash** | Managed Redis for caching |
| **GitHub Actions** | CI/CD |
| **Sentry** | Error tracking |

---

## 8. Sample API Specification (subject to change)

### 8.1 Upload Endpoints

```yaml
POST /videos/upload/init
  Description: Initiate chunked upload session with access policy
  Request:
    file_name: string (required)
    file_size: number (bytes, required, max 5GB)
    content_type: string (required)
    title: string (required)
    description: string (optional)
    access_policy:
      type: "public" | "owner_only" | "shared_list" | "nft_gated"
      allowed_addresses: string[] (for shared_list)
      nft_type: string (for nft_gated)
  Response:
    upload_id: string
    chunk_size: number
    total_chunks: number
    expires_at: timestamp

PUT /videos/upload/{upload_id}/chunks/{chunk_number}
  Description: Upload a single chunk
  Headers:
    Content-Type: application/octet-stream
    Content-MD5: string
  Request: Binary chunk data
  Response:
    chunk_number: number
    status: "received" | "invalid_checksum"
    
GET /videos/upload/{upload_id}/status
  Description: Check upload progress
  Response:
    upload_id: string
    status: "in_progress" | "encrypting" | "complete" | "failed"
    chunks_received: number
    chunks_total: number

POST /videos/upload/{upload_id}/complete
  Description: Finalize upload, encrypt, and register
  Response:
    video_id: string
    status: "ready" | "validation_failed"
    playback_url: string
    access_policy_id: string
```

### 8.2 Video Endpoints

```yaml
GET /videos/{video_id}
  Description: Get video metadata (public info only)
  Response:
    id: string
    title: string
    description: string
    duration_ms: number
    resolution: { width, height }
    file_size: number
    access_policy:
      type: string
      # Details hidden for non-owners
    owner: address
    created_at: timestamp

GET /videos/{video_id}/stream
  Description: Stream video (requires authorization)
  Headers:
    Authorization: Bearer <wallet_signature | api_key>
    Range: bytes=start-end (optional)
  Response:
    200/206: Video stream (if authorized)
    403: Forbidden (if policy not satisfied)

PATCH /videos/{video_id}
  Description: Update video metadata
  Auth: Owner only
  Request:
    title: string (optional)
    description: string (optional)
  Response: Updated video object

PATCH /videos/{video_id}/policy
  Description: Update access policy
  Auth: Owner only
  Request:
    type: "public" | "owner_only" | "shared_list" | "nft_gated"
    allowed_addresses: string[] (for shared_list)
    nft_type: string (for nft_gated)
  Response:
    policy_id: string
    type: string
    updated_at: timestamp

DELETE /videos/{video_id}
  Description: Delete video and all encrypted chunks
  Auth: Owner only
  Response:
    success: boolean
    chunks_deleted: number

GET /videos
  Description: List user's videos
  Auth: Required
  Response:
    videos: Video[]
    total: number
```

### 8.3 SDK Interface

```typescript
import { WubeClient } from '@wube/sdk';

const wube = new WubeClient({ apiKey: 'wube_xxx' });

// Upload with access control
const video = await wube.upload(file, {
  title: 'Exclusive Content',
  description: 'For NFT holders only',
  accessPolicy: {
    type: 'nft_gated',
    nftType: '0x123::my_nft::MyNFT',
  },
  onProgress: (progress) => {
    console.log(`${progress.percent}% - ${progress.stage}`);
    // Stages: 'uploading' | 'encrypting' | 'registering'
  },
});

// Upload with shared list
const privateVideo = await wube.upload(file, {
  title: 'Team Update',
  accessPolicy: {
    type: 'shared_list',
    allowedAddresses: [
      '0xalice...',
      '0xbob...',
    ],
  },
});

// Update access policy (no re-upload needed)
await wube.updatePolicy(video.id, {
  type: 'public',  // Make it public
});

// Add viewer to shared list
await wube.addToSharedList(video.id, '0xcharlie...');

// Get playback URL (for authorized viewers)
const playback = await wube.getPlaybackUrl(video.id, {
  viewerWallet: '0xviewer...',  // Will verify access
});

// Embeddable player with built-in auth
<WubePlayer 
  videoId={video.id}
  onAccessDenied={() => console.log('Not authorized')}
/>
```

---

## 9. Security Considerations

### 9.1 Encryption Security

| Aspect | Implementation |
|--------|----------------|
| **Chunk encryption** | AES-256-GCM (authenticated encryption) |
| **Key management** | Seal protocol (threshold cryptography) |
| **Key derivation** | Unique CEK per chunk (no key reuse) |
| **IV handling** | Random IV per chunk; stored in manifest |
| **Integrity** | GCM auth tags verify chunk integrity |

### 9.2 Access Control Security

| Aspect | Implementation |
|--------|----------------|
| **Policy storage** | On-chain (tamper-proof) |
| **Policy evaluation** | Seal verifies on-chain state |
| **NFT verification** | Real-time on-chain ownership check |
| **Session management** | Short-lived tokens; wallet signatures |
| **Rate limiting** | Per-viewer limits on key requests |

### 9.3 Operational Security

| Aspect | Implementation |
|--------|----------------|
| **Decrypted data** | Never persisted to disk; memory-only cache |
| **Cache TTL** | Decrypted chunks: 5-30 minutes max |
| **Audit logging** | All access attempts logged |
| **Key escrow** | None; Seal threshold prevents single-point compromise |


---

## 10. Risk Assessment

### 10.1 Technical Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **Seal integration complexity** | Medium | High | Early spike; engage Mysten for support |
| **Decryption latency** | Medium | Medium | Aggressive caching; optimize key retrieval |
| **Policy evaluation performance** | Medium | Medium | Cache policy results; batch verification |
| **Walrus + Seal interaction issues** | Low | High | Test thoroughly; have fallback patterns |

### 10.2 Security Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **Encryption implementation flaw** | Low | Critical | Use proven libraries; security review |
| **Policy bypass vulnerability** | Low | Critical | On-chain verification; audit |
| **Key leakage** | Low | Critical | Memory-only handling; no persistence |
| **Replay attacks** | Low | Medium | Nonces; timestamp validation |

### 10.3 Operational Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **Seal network unavailability** | Low | High | Graceful degradation; retry logic |
| **Increased infrastructure costs** | Medium | Medium | Monitor closely; optimize caching |

---

## 11. Success Metrics

### Possible MVP Success Criteria

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Upload success rate** | > 98% | Automated monitoring |
| **Encryption overhead** | < 30% of upload time | Performance testing |
| **Playback start time** | < 5 seconds | Client-side measurement |
| **Policy evaluation latency** | < 500ms | Server-side measurement |
| **Decryption throughput** | > 30 MB/s | Load testing |
| **API availability** | > 99.5% | Uptime monitoring |
| **Authorized access success** | > 99.9% | Monitoring |
| **Unauthorized access blocked** | 100% | Security testing |
| **Schedule adherence** | ≤ 16 weeks | Project tracking |

---

## 12. Conclusion

Project Wube with Seal encryption delivers **production-ready encrypted video infrastructure** for the Sui/Walrus ecosystem. By combining strategic constraints with powerful access control, we create a platform that centralized alternatives cannot match: **true ownership with programmable privacy**.

### What We're Building

| Capability | Description |
|------------|-------------|
| **Chunked Upload** | Reliable upload for files up to 8 GB |
| **Seal Encryption** | Policy-based encryption for all content |
| **Flexible Access Control** | Public, owner-only, shared list, NFT-gated |
| **Transparent Playback** | Seamless decryption for authorized viewers |
| **On-Chain Ownership** | VideoAsset objects with policy management |

### Key Differentiators vs. Centralized Platforms

| Aspect | Mux / Cloudflare | Wube |
|--------|------------------|------|
| **Data location** | Their servers | Walrus (decentralized) |
| **Access control** | Their auth system | On-chain policies |
| **Encryption** | At rest (they hold keys) | Seal (user controls access) |
| **Ownership** | Platform owns relationship | User owns VideoAsset |
| **Token-gating** | Not native | Native NFT verification |
| **Portability** | Vendor lock-in | Open, transferable |

### Investment Summary

| Metric | Value |
|--------|-------|
| **Budget** | $197K **covers infra as well** (target: <$200K, 3rd party audit costs are separate) |
| **Timeline** | 16 weeks |
| **Team** | 6-8 FTE (depending on need) |
| **Deliverable** | Encrypted video infrastructure with policy-based access |

### Adjacent MVP Steps

1. **Seal integration spike:** Validate encryption/decryption flow
2. **Policy design review:** Confirm access policy types meet market needs
3. **Walrus + Seal interop:** Test encrypted blob storage patterns
4. **Security architecture review:** External review of encryption design
5. **Identify beta partners:** 3-5 projects needing encrypted video

---

<p align="center">
  <strong>Levuka Venture Labs FZCO</strong><br>
  February 2026
</p>
