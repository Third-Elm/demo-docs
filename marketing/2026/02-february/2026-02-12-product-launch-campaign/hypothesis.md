# Hypothesis: Case Study vs Feature List

**Date**: 2026-02-12
**Campaign**: [Campaign Brief](./campaign-brief.md)
**Status**: Testing

---

## What We Believe

Technical case studies (showing real problem-solving with code) will generate higher signup conversion than feature-focused content (listing what the product does).

## Why We Believe It

- Previous campaigns with tutorials had 2x engagement vs product announcements
- Competitor analysis shows "how-to" content outperforms feature releases
- Developer audience typically distrusts marketing-heavy messaging
- Reddit/HN historically rewards technical depth over promotional content

---

## Variables

### Independent Variable (What We're Changing)

Content format: case study (showing code, problem, solution) vs feature list (product capabilities).

### Dependent Variable (What We're Measuring)

Signup conversion rate from each content piece's tracking link.

### Controlled Variables (What Stays the Same)

- Same landing page for all traffic
- Same targeting parameters by channel
- Same posting times and frequency
- Same visual branding

---

## Success Criteria

| Metric                  | Current Baseline | Target | How We'll Measure     |
| ----------------------- | ---------------- | ------ | --------------------- |
| Case study CTR          | -                | >4%    | UTM tracking links    |
| Feature list CTR        | -                | >2%    | UTM tracking links    |
| Case study conversion   | -                | >8%    | Analytics signup flow |
| Feature list conversion | -                | >4%    | Analytics signup flow |

**Primary success signal**: Case study conversion rate at least 2x feature list rate.

---

## Alternative Hypotheses

1. **Audience segmentation**: Maybe case studies appeal to senior devs while features appeal to junior devs - need to segment results by job title if possible.
2. **Channel effect**: Twitter might prefer one format while LinkedIn prefers another - analyze by channel.
3. **Timing effect**: Early campaign excitement might inflate all metrics - compare within same time periods.

---

## Test Design

### Sample Size

- 50,000 impressions per format minimum
- Target: 1,000 clicks per format for statistical significance

### Duration

Two weeks (campaign duration): 2026-02-15 to 2026-02-28

### Segments

- By channel (Twitter vs LinkedIn)
- By audience segment (developer vs manager) where data available

---

## Risks

| Risk                   | Likelihood | Impact | Mitigation                            |
| ---------------------- | ---------- | ------ | ------------------------------------- |
| Low traffic volume     | Medium     | High   | Extend test duration if needed        |
| Tracking link breakage | Low        | High   | QA all links before launch            |
| External news events   | Low        | Medium | Monitor and pause if major disruption |

---

## Related Documents

- **Campaign Brief**: [campaign-brief.md](./campaign-brief.md)
- **Results**: Will be created at `2026-02-19-product-launch-campaign/results.md`
