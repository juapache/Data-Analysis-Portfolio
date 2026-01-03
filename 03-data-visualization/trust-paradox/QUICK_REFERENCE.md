# The Trust Paradox: Quick Reference Card

## Core Formula

```
Negative Peace  = 0.6 × Security + 0.4 × Institutions
Positive Peace  = 0.5 × Trust + 0.5 × Institutions
Sustainability  = 0.3 × Trust + 0.3 × Institutions + 0.4 × Balance
                  where Balance = max(0, 1 - |Security - Trust| / 200)
```

---

## Dimensions (0–100 scale)

| Dimension | Definition | Why It Matters | Data Source |
|-----------|-----------|---|---|
| **Social Trust (T)** | Horizontal (citizen-to-citizen) & vertical (citizen-to-state) confidence | Enables cooperation; reduces need for force; foundation of legitimacy | World Values Survey, V-Dem, custom surveys |
| **Security Measures (S)** | Policing, enforcement, surveillance, protective capacity | Prevents/suppresses violence; but can erode trust if excessive | Police ratio, military spending, incarceration rate, surveillance indices |
| **Institutional Strength (I)** | Rule of law, service delivery, inclusive governance, dispute resolution | Delivers justice & opportunity; legitimate exercise of state power | World Bank WGI, V-Dem, CPI, WJP Rule of Law Index |

---

## Outputs (0–100 scale)

| Output | Meaning | Good Range | Red Flags |
|--------|---------|-----------|----------|
| **Negative Peace** | Absence of direct violence | 60–100 | <40 = violence risk; >85 = possibly oppressive |
| **Positive Peace** | Presence of justice, wellbeing, equity | 60–100 | <40 = grievance/structural injustice; >85 = possibly unrealistic |
| **Sustainability** | Resilience to shocks; self-reinforcing or brittle | 60–100 | <40 = brittle; vulnerable to sudden collapse |

---

## Peace States (Interpretation)

```
High NP, Low PP, Low Sus
├─ "Suppressed Conflict"
├─ High security controls violence but low trust
├─ Example: Heavy-handed police state
└─ Policy: Build trust, increase transparency

Low NP, High PP, Low Sus
├─ "Fragile Positive"
├─ Strong trust & fairness but weak enforcement
├─ Example: Post-conflict trust, but security gap
└─ Policy: Build state capacity carefully

High NP, High PP, High Sus
├─ "Robust Positive Peace"
├─ Balanced across all dimensions
├─ Example: Stable democratic society
└─ Policy: Maintain balance, avoid overreach

Low All
├─ "Critical/Failing"
├─ Collapse or ongoing conflict
├─ Example: Failed state, civil war
└─ Policy: Emergency rebuilding
```

---

## Key Insight: The Paradox

**Heavy security alone cannot create sustainable peace.**

- ✅ Security suppresses violence (↑ NP)
- ❌ But erodes trust if not balanced (↓ PP, ↓ Sus)
- ✅ Trust enables voluntary cooperation (↑ PP)
- ❌ But vulnerable without enforcement (↓ NP if no I)
- ✅ Institutions deliver fairness & services (↑ PP, ↑ NP)
- ❌ But take time to build

**Solution**: Balance all three dimensions. Model penalizes extreme imbalance (e.g., S >> T) because such configurations are brittle.

---

## Calculation Steps

1. **Gather data**: Get T, S, I values (0–100) for your case
2. **Insert into formulas**: Use above (or Python/spreadsheet)
3. **Read outputs**: NP, PP, Sus scores
4. **Interpret**: Match to peace state descriptions above
5. **Validate**: Does output match real-world knowledge?
6. **Act**: Identify which dimension to prioritize

---

## Data Quick Reference

### Social Trust (T)
- **Primary source**: World Values Survey (worldvaluessurvey.org)
  - Question: "Most people can be trusted?" (% yes, 0–100)
- **Alternatives**: V-Dem institutional trust; national surveys

### Security Measures (S)
- **Composite from**:
  - Police-to-population ratio (per 100k, normalized)
  - Incarceration rate (per 100k, normalized)
  - Military spending (% GDP, normalized)
  - Surveillance capacity estimate
- **Source**: World Bank, UN, national statistics

### Institutional Strength (I)
- **Primary sources**:
  - World Bank Governance Indicators (WGI)
  - V-Dem democracy indices
  - Transparency International CPI
- **Rescale to 0–100 if needed**: (Value - Min) / (Max - Min) × 100

---

## Common Scenarios & What They Mean

| Scenario | T | S | I | NP | PP | Sus | Interpretation |
|----------|---|---|---|----|----|----|---|
| Nordic country | 75 | 35 | 90 | 72 | 82 | 78 | Robust; model citizen behavior |
| Authoritarian order | 30 | 85 | 50 | 74 | 40 | 32 | Suppressed; at collapse risk |
| Post-conflict (early) | 20 | 60 | 30 | 48 | 25 | 21 | Emergency phase; slow recovery expected |
| High-inequality democracy | 50 | 50 | 55 | 52 | 52 | 48 | Moderate; vulnerable to crisis |
| Failed state | 15 | 25 | 10 | 18 | 12 | 10 | Critical; requires external support |

---

## Best Practices

✅ **Do**:
- Use recent data (within 2–3 years)
- Document your sources & methods
- Validate against real-world knowledge
- Run sensitivity tests (±20% weights)
- Acknowledge limitations

❌ **Don't**:
- Use as deterministic prediction
- Over-interpret 2–3 point differences
- Claim causation (model shows correlation)
- Apply without understanding context
- Ignore data quality issues

---

## Reading Guide

**5 minutes**: This card + README.md § "Core Concept"

**30 minutes**: This card + README.md (full) + METHODOLOGY.md § 1–2

**2 hours**: All documentation + one notebook

**1 week**: Full documentation + data gathering & case analysis

---

## Formulas in Plain English

### Negative Peace
"Violence is suppressed by strong security and maintained by institutional order. Neither alone is sufficient."

### Positive Peace
"People cooperate willingly when they trust each other and believe institutions are fair. Both equally important."

### Sustainability
"A peace configuration is brittle if security and trust are mismatched. Balance matters as much as absolute levels."

---

## If You Remember Nothing Else...

The **Trust Paradox** teaches us:

1. **Negative peace (absence of violence) ≠ Positive peace (presence of justice)**
2. **Security without trust is brittle** → collapse when enforcement lapses
3. **Trust without institutions is naive** → vulnerable to predators
4. **Institutions are the bridge** → legitimate security, earned trust
5. **Balance matters** → extremes in any dimension undermine sustainability

---

## Resources

| Need | Go To |
|------|-------|
| Understand the model | [README.md](README.md) |
| Apply to your case | [IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md) |
| Dive deep / validate | [METHODOLOGY.md](METHODOLOGY.md) |
| Academic grounding | [ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md) |
| Navigate all docs | [INDEX.md](INDEX.md) |
| Play interactively | [juapache.github.io/trust-paradox.html](https://juapache.github.io/trust-paradox.html) |

---

**Last Updated**: January 2026  
**License**: CC-BY-NC 4.0  
**Questions?** See [INDEX.md](INDEX.md) § "Contact & Support"
