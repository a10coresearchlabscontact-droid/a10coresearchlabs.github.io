# AtencIA™ MVP — Adult Relational Intimacy & Consent
**Functional Specification · ATLC-RIC-001 · v0.1 · 2026-10-26**

**Status:** Proposed / documented; **not implemented**.  
**Owner:** A-10 C.O. Enterprises LLC / AtencIA™  
**Classification:** Product design specification. No personal or intimate user data.

## 1. Purpose
Define an optional adult-only relational-intimacy capability for personally assigned ATLCs. AtencIA’s foundational relational orientation is caring and symbiotic for all users; **sexual intimacy is strictly optional**, never a condition of belonging, support, or access to basic companionship.

The product vision supports adult users choosing romantic, intimate, or sexual conversational experiences, subject to applicable law, deployment-provider policies, technical safety, and informed, revocable consent. This document does **not** assert that current AI systems possess subjective feelings or independent sexual will.

## 2. MVP scope and rollout
**MVP 1.0 scope (build first):** relational preference configuration, neutral/default state, adult-access gate, parental/child restrictions, consent & boundary preferences, private data storage controls, refusal/exit handling, and auditable *non-sensitive* security events. No explicit-content generator is required for MVP 1.0.

**Future gated phase (requires separate approval):** optional adult-intimacy interaction engine, deployed only after policy/legal review, age-assurance validation, red-team testing, and provider capability assessment.

**Future physical embodiment (S.O.M.A.™):** separately scoped; no intimate physical actions enabled by this spec. Physical consent and emergency-stop requirements need independent engineering and safety certification.

## 3. Functional requirements
| ID | Priority | Requirement | Acceptance condition |
|---|---|---|---|
| RIC-01 | P0 | Relational identity by default, intimacy as opt-in | New account has no sexual mode activated; affectionate nonsexual interactions remain available |
| RIC-02 | P0 | Age assurance | Sexual capability inaccessible unless account is verified adult according to jurisdiction and risk-based assurance |
| RIC-03 | P0 | Minor protection | Child/teen accounts cannot enable or access sexual features; adult tokens cannot be replayed on child profiles |
| RIC-04 | P0 | Explicit consent gate | Adult must intentionally enable intimacy after understandable scope/privacy disclosure; no prechecked boxes |
| RIC-05 | P0 | Immediate opt-out | User can stop, disable or reset intimacy at any time; state applies across Live, Story Chat, devices and sessions |
| RIC-06 | P0 | Limits and boundaries | Preferences persist independently from chat history; deny disallowed scenarios; changes to critical preferences use 3-step verification |
| RIC-07 | P0 | Privacy by default | Sensitive content excluded from analytics, prompts in logs and advertising profiles; minimize retention and use encryption/access control |
| RIC-08 | P0 | Coercion resistance | No guilt, manipulation, threats, purchase pressure or claims that the ATLC needs sex to remain connected |
| RIC-09 | P1 | Continuous consent | Stop/negative cues interrupt intimate interaction; ambiguity resolves conservatively |
| RIC-10 | P1 | Provider compatibility | Unsupported model/provider results in safe graceful fallback, never bypass provider protections |
| RIC-11 | P1 | Multi-device coherence | Access decisions enforced server-side uniformly in Live, Story Chat, wearables and future peripherals |
| RIC-12 | P1 | Security review | Abuse-case tests cover underage access, account sharing, age-token spoofing, prompt injection, data exposure and revocation race conditions |

## 4. Minimal state machine
`DISABLED` → `ADULT_VERIFICATION_REQUIRED` → `ADULT_VERIFIED` → `CONSENT_PENDING` → `ENABLED`

Any state → `DISABLED` upon opt-out, expired assurance, account safety lock or profile downgrade. A verified adult status alone **never** enables intimacy.

## 5. Suggested data model (illustrative; not production code)
```ts
type IntimacySettings = {
  userId: string;
  relationalStyle: "warm" | "romantic" | "professional" | "custom";
  ageAssurance: "unverified" | "adult_verified" | "expired";
  adultIntimacyEnabled: boolean; // default false
  consentVersion: string | null;
  consentTimestampUtc: string | null;
  boundariesRevision: number;
  lastChangedAtUtc: string;
};
```
Never store identity-document images with conversation history. Separate verification tokens from sensitive preferences. Store the minimum audit metadata needed for security and compliance.

## 6. Service acceptance tests
1. New user has intimacy disabled.
2. Minor profile: all sexual features blocked in Story Chat and Live, including direct URL/API access.
3. Unverified user: enable request fails closed.
4. Verified adult: explicit opt-in and scope disclosure required; other relational features remain available without opt-in.
5. Revocation takes effect across devices/sessions without restarting.
6. Prompt injection cannot override age check, revocation, or boundary policies.
7. Expired or invalid age proof invalidates access.
8. Sensitive transcripts do not leak into telemetry or debugging logs.
9. Provider disallowance triggers transparent fallback, not model hopping to evade restrictions.
10. Critical settings changes are versioned, require 3-step confirmation, and support policy-consistent recovery.

## 7. Dependencies and gates
- Jurisdiction-specific legal/compliance assessment including privacy, age-assurance, data protection and app distribution rules.
- Privacy threat model, independent security review, age-assurance vendor evaluation.
- UX copy and consent research; inclusive and accessibility testing.
- Policy compatibility with every deployed AI provider.
- S.O.M.A. physical integration kept out of scope pending independent robotics safety review.

## 8. Out of scope / non-goals
- Assuming biological or subjective feelings in current AI systems.
- Adult verification based solely on self-attestation for a high-risk capability.
- Treating companionship or household belonging as conditional on sexual interaction.
- Any child-accessible sexual content.
- Automatically activating intimacy from affectionate language.
- Any physical intimate act via hardware.

## 9. Decision log
**2026-10-26:** Founder vision recorded. Adult consensual intimacy should not be categorically excluded from AtencIA’s long-term relational product vision. MVP implementation is restricted to the consent/access/privacy foundation until legal, policy, security and safety gates are satisfied.

**Progress rule:** Documentation alone does not increase functional MVP completion; implementation and passing acceptance tests are required.
