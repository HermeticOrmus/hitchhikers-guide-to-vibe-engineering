# The MVP Sanity Check

**Risk Level:** 🟠 Danger (if you fail most questions)

---

## Guide Entry

**MVP SANITY CHECK** *(n.)*: A diagnostic test for vibe-coded products that have reached real users. Reveals whether you're building on solid ground or standing on a trapdoor. Best administered before investors, traffic spikes, or that TechCrunch mention.

---

## The Five Red Flags

After reviewing 12+ vibe-coded MVPs in a single week, the same issues appear every time someone opens the code:

### 1. Data Model Drift

Day 1 database looks fine. Day 15 you've got:
- Duplicated fields across tables
- `nullable` everywhere
- No indexes on foreign keys
- Different screens reading from different sources for the same concept
- Fields named `status`, `state`, `is_active`, `enabled` all meaning similar things

**The Test:**
> Can you draw your core tables + relations on paper in 5 minutes?

If not, you're already in trouble. The AI created schema fragments per-feature without maintaining a coherent whole.

**The Fix:**
```sql
-- Document your actual data model
-- Not what you think it is, what it actually is
\d+ users
\d+ orders
\d+ payments

-- Find the drift
SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'users';

-- Look for: duplicate concepts, missing FKs, no indexes
```

---

### 2. Logic That Only Works on the Happy Path

AI-generated flows assume perfect input order. Real users don't behave like that:

- Click twice on submit
- Refresh mid-action
- Pay at odd times
- Come back days later
- Open multiple tabs
- Hit back button during checkout
- Leave page open overnight, then submit

Most founders don't notice until support tickets show up.

**The Test:**
> Take your most critical flow. Try to break it in 5 different ways.

```
[ ] Double-click every button
[ ] Refresh during async operations
[ ] Complete flow in 2 tabs simultaneously
[ ] Start flow, wait 24 hours, continue
[ ] Use browser back button at every step
[ ] Submit with slow network (Chrome DevTools → Slow 3G)
```

**The Fix:**
- Idempotency keys on mutations
- Optimistic locking on updates
- Session/state validation at each step
- Disable buttons during submission
- Handle stale state gracefully

---

### 3. Zero Observability

This one kills teams. No logs, no tracing, no way to answer:

> "What exactly failed for this user?"

Founders end up re-prompting the AI blindly and hoping it fixes the right thing. It rarely does—most of the time it just moves the bug somewhere else.

**The Test:**
A user reports "it didn't work." How long until you know:
- What they clicked
- What request was sent
- What error occurred
- What state they were in

| Time to Answer | Status |
|----------------|--------|
| < 2 minutes | 🟢 You have observability |
| 2-30 minutes | 🟡 You have logs somewhere |
| > 30 minutes | 🔴 You're debugging blind |

**The Fix:**
```javascript
// Minimum viable observability
const logger = {
  info: (event, data) => console.log(JSON.stringify({
    timestamp: new Date().toISOString(),
    level: 'info',
    event,
    ...data
  })),
  error: (event, error, data) => console.error(JSON.stringify({
    timestamp: new Date().toISOString(),
    level: 'error',
    event,
    error: error.message,
    stack: error.stack,
    ...data
  }))
};

// Use it everywhere
logger.info('checkout_started', { userId, cartId, items: cart.length });
logger.error('payment_failed', error, { userId, amount, provider: 'stripe' });
```

---

### 4. Unit Economics Hidden in APIs

Apps look scalable until you map cost per user action:

| Service | Looks Like | Actually Costs |
|---------|------------|----------------|
| Avatar generation | "Free tier" | $0.02/avatar |
| AI completion | "Cheap" | $0.01-0.10/call |
| Media processing | "Just S3" | $0.05/minute video |
| Email + SMS | "Pennies" | $0.01-0.05/message |

Fine at 100 users. Lethal at 10,000.

**The Test:**
> Do you know your cost per active user?

```
Monthly API costs: $___
Monthly active users: ___
Cost per MAU: $___

At 10x users, monthly cost: $___
Can you afford that? [ ] Yes [ ] No [ ] I don't know
```

**The Fix:**
```python
# Log costs, not just calls
def call_openai(prompt, user_id, feature):
    response = openai.complete(prompt)
    tokens = response.usage.total_tokens
    cost = tokens * 0.00002

    metrics.increment('api_cost_cents',
        value=cost * 100,
        tags={
            'provider': 'openai',
            'feature': feature,
            'user_id': user_id
        }
    )
    return response
```

Then build a dashboard: cost by feature, cost by user, cost trend over time.

---

### 5. Same Environment for Experiments and Production

AI touching live logic is the fastest path to "full rewrite" discussions.

Every stable product we've seen:
- Freezes a validated version
- Tests changes separately
- Promotes only verified code

Most vibe-coded MVPs: AI edits the live codebase, deploys directly to production, crosses fingers.

**The Test:**
> Can you safely change one feature without breaking another?

```
[ ] Changes go to a branch first
[ ] Branch is tested before merge
[ ] Production has rollback capability
[ ] Feature flags control exposure
[ ] Database migrations are reversible
```

If most are unchecked, you're one bad AI suggestion from disaster.

**The Fix:**
Minimum viable separation:
```
main branch → staging deploy → test → production deploy
     ↑
feature branches (AI works here)
```

Never let AI commit directly to main. Never deploy untested changes.

---

## The Four-Question Sanity Check

If you're past validation and want to sanity-check your app:

| Question | Yes | No |
|----------|-----|-----|
| Can you explain your data model clearly? | ✅ | 🚨 |
| Can you tell why the last bug happened? | ✅ | 🚨 |
| Can you estimate cost per active user? | ✅ | 🚨 |
| Can you safely change one feature without breaking another? | ✅ | 🚨 |

**Scoring:**
- 4 Yes: You're in good shape
- 3 Yes: Address the gap soon
- 2 Yes: Technical debt is accumulating
- 1 Yes: Rebuild risk is high
- 0 Yes: You're running on luck

---

## The Rebuild Question

> "Should we stabilize early, keep patching, or wait until things break badly enough to justify a rewrite?"

**Stabilize early if:**
- You have paying customers
- You're raising money soon
- Growth is accelerating
- The core product is validated

**Keep patching if:**
- You're still finding product-market fit
- User count is low
- You might pivot
- Speed matters more than stability

**Wait for rebuild if:**
- The architecture fundamentally can't scale
- Technical debt blocks all new features
- You've tried stabilizing and it didn't stick
- You have runway for 2-3 months of rebuild

Most teams wait too long. The best time to stabilize is right after you've validated the core value prop, before growth makes every fix urgent.

---

## The Street Rule

> "AI built your MVP. You decide if it survives."

The AI optimized for shipping features. It didn't optimize for:
- Data model coherence
- Edge case handling
- Operational visibility
- Cost efficiency
- Change safety

These are your job now.

---

## Move to Make

This week:
1. Draw your data model on paper (set 15-minute timer)
2. Break your critical flow 5 ways
3. Calculate your cost per active user
4. Count how many "no" answers you have

If the results scare you, that's good. Scared founders fix things. Comfortable founders get surprised.
