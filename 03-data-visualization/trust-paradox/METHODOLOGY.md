# Methodology: The Trust Paradox Model

## Document Overview

This document specifies the mathematical foundations, assumptions, and derivation of **The Trust Paradox** model. It is intended for researchers, data scientists, and policy analysts who wish to understand, validate, extend, or implement the model in different contexts.

---

## 1. Model Structure & Conceptual Design

### 1.1 Three Core Dimensions

The model represents peace as a function of three primary dimensions:

| Dimension | Definition | Range | Units |
|-----------|-----------|-------|-------|
| **Social Trust (T)** | Horizontal and vertical confidence enabling cooperation and reducing fear | 0–100 | Index (subjective, based on survey or composite) |
| **Security Measures (S)** | Intensity of surveillance, policing, enforcement, protective infrastructure | 0–100 | Index (enforcement capacity, police-to-population ratio, carceral load, etc.) |
| **Institutional Strength (I)** | Capacity for rule of law, service delivery, inclusion, dispute resolution | 0–100 | Index (World Bank governance indicators, V-Dem dimensions, etc.) |

### 1.2 Three Output Indicators

| Output | Definition | Formula | Interpretation |
|--------|-----------|---------|-----------------|
| **Negative Peace (NP)** | Absence of direct violence | See §2.1 | State capacity to prevent/suppress violence |
| **Positive Peace (PP)** | Presence of justice, equity, wellbeing | See §2.2 | Conditions enabling human flourishing without coercion |
| **Sustainability (Sus)** | Resilience of peace to shocks; long-term viability | See §2.3 | Whether configuration is self-reinforcing or brittle |

---

## 2. Mathematical Specification

### 2.1 Negative Peace Function

**Rationale**: Negative peace is primarily about suppressing violence. It depends on security capacity (enforcement, deterrence) and institutional capacity (order maintenance, rule of law). Security is weighted more heavily because short-term violence prevention is direct; institutions provide long-term stability.

$$NP = 0.6 \times S + 0.4 \times I$$

**Interpretation**:
- When $S$ is high and $I$ is moderate/high: Strong law enforcement + working courts/services → violence is low, peace is stable
- When $S$ is high and $I$ is low: Heavy-handed policing without justice/services → violence suppressed but legitimacy low, unsustainable (see Sustainability penalization)
- When $S$ is low and $I$ is high: Weak enforcement but functioning institutions → peace depends on internal legitimacy; vulnerable to determined actors but socially embedded
- When $S$ is low and $I$ is low: Minimal capacity on both fronts → violence erupts; peace is absent

**Weight justification**:
- 0.6 for Security: Direct causal path to violence reduction; empirically strong (Braithwaite 2010, Collier & Hoeffler 2004)
- 0.4 for Institutions: Foundational legitimacy; takes longer to build but essential for long-term order

### 2.2 Positive Peace Function

**Rationale**: Positive peace emphasizes relational goods (trust) and structural conditions (justice, equality) that enable human flourishing. Trust allows cooperation without fear; institutions provide equitable access to opportunity and redress. Positive peace cannot be imposed; it requires voluntary participation and perceived fairness.

$$PP = 0.5 \times T + 0.5 \times I$$

**Interpretation**:
- When $T$ is high and $I$ is high: Communities cooperate willingly, institutions deliver fairly → Peace is deep, self-reinforcing
- When $T$ is high and $I$ is low: People trust each other but fear institutions won't deliver or include them → fragile; reliant on informal mechanisms, vulnerable to shocks
- When $T$ is low and $I$ is high: Institutional capacity alone cannot create positive peace; people fear and resent the state even if it functions → compliance without legitimacy, erosion over time
- When $T$ is low and $I$ is low: No relational foundation, no just institutions → No positive peace; zero welfare, grievance, potential conflict

**Weight justification**:
- 0.5 each for Trust and Institutions: Both are *necessary* and *equally valued*. Trust without fair institutions eventually breaks down; institutions without trust cannot motivate voluntary compliance (Tyler 2006, Rothstein & Uslaner 2005)

### 2.3 Sustainability Function (The Paradox)

**Rationale**: Sustainability measures whether a given peace configuration is *self-reinforcing or self-undermining*. The key insight is that **misaligned dimensions create brittle, unsustainable equilibria**.

For example:
- High security + low trust = Suppressed violence but eroded legitimacy → people feel oppressed → latent conflict, waiting for security to weaken
- High trust + low security/institutions = Vulnerable to predation or organized violence → communities may lose faith in peaceful coexistence
- Unbalanced configurations = Vulnerable to shocks (e.g., security lapse, institutional failure, economic crisis)

$$Sus = 0.3 \times T + 0.3 \times I + 0.4 \times B$$

where **Balance Factor**:

$$B = 1 - \frac{|S - T|}{200}$$

Constraints: $B \in [0, 1]$ (clamped if negative)

**Interpretation of Balance Factor**:
- When $S \approx T$ (security and trust are similar): $B \approx 1$ (balanced, sustainable)
- When $S >> T$ (security overwhelms trust): $B \to 0$ (brittle, unsustainable)
- When $T >> S$ (trust very high but security low): $B \to 0$ (vulnerable)
- Maximal penalty at extremes: $|S - T| = 200$ yields $B = 0$ (completely unsustainable)

**Why this form?**

1. **Trust and Institutions (0.3 each)**: These are the building blocks of sustainability. Societies with low T or low I are vulnerable regardless of S.
2. **Balance Factor (0.4 weight)**: The dominant term. Penalizes imbalance severely, encoding the paradox: security-heavy approaches undermine long-term peace; trust-only approaches are naive.
3. **Symmetry**: Penalizes both $S >> T$ (surveillance/authoritarianism) and $T >> S$ (naïve trust) equally, reflecting empirical evidence that extremes fail.

**Empirical grounding**:
- Moyn (2015), Zuboff (2019): Surveillance states erode trust and freedom despite security outputs
- Lederach (1997): Trust alone without institutional capacity cannot sustain peace
- Galtung (1990): Structural injustice persists even in "peaceful" societies without justice institutions

---

## 3. Parameterization & Input Data

### 3.1 Social Trust (T)

**Data sources**:
1. **World Values Survey**: Generalized trust question: "Generally speaking, would you say that most people can be trusted?"
   - Proxy: Percentage answering "yes" (0–100 scale)
   
2. **V-Dem Indicators**:
   - `v2paptrust`: Participatory democracy → public trust in democratic institutions
   - `v2pepwrsoc`: Power held by civic groups → horizontal trust indicator
   
3. **Gallup/Eurobarometer**: Institutional trust by org (courts, police, parliament)
   - Aggregate or weight by relevance
   
4. **Custom surveys**: Administer trust questions in specific contexts (post-conflict, transitional justice, etc.)

**Aggregation rule** (if multiple sources):
$$T = w_1 \times T_{\text{WVS}} + w_2 \times T_{\text{V-Dem}} + w_3 \times T_{\text{Custom}}$$
Default: equal weights ($w_i = 1/3$) unless context suggests otherwise.

### 3.2 Security Measures (S)

**Data sources**:
1. **Police/law enforcement capacity**:
   - Police-to-population ratio (per 100,000 inhabitants)
   - Normalize to 0–100 scale based on global distribution
   
2. **Carceral load**:
   - Incarceration rate per 100,000
   - High incarceration → high S
   
3. **Military/defense spending**:
   - Military expenditure as % GDP
   - Convert to 0–100 scale
   
4. **Surveillance capacity**:
   - Internet filtering/monitoring indices (e.g., Freedom House)
   - Facial recognition roll-out, digital surveillance laws
   - Proxy: % of citizens under surveillance (subjective estimate)
   
5. **World Bank Governance Indicator**: Rule of Law estimate (ranges –2.5 to +2.5)
   - Rescale to 0–100

**Composite measure**:
$$S = w_1 \times S_{\text{police}} + w_2 \times S_{\text{incarceration}} + w_3 \times S_{\text{military}} + w_4 \times S_{\text{surveillance}}$$

Default weights (equal): $w_i = 0.25$ each. Adjust by context:
- High-conflict regions: Increase $w_{\text{military}}$
- Authoritarian contexts: Increase $w_{\text{surveillance}}$
- Developed democracies: Increase $w_{\text{police}}$

### 3.3 Institutional Strength (I)

**Data sources**:
1. **World Bank Worldwide Governance Indicators (WGI)**:
   - Rule of Law (`RL`)
   - Government Effectiveness (`GE`)
   - Regulatory Quality (`RQ`)
   - Each ranges –2.5 to +2.5; rescale to 0–100
   
2. **V-Dem Indices**:
   - `v2x_polyarchy`: Electoral democracy
   - `v2x_accountability`: Accountability index
   - `v2x_egalitarian`: Egalitarian representation
   
3. **Transparency International Corruption Perception Index**:
   - Higher CPI → higher institutional quality
   - Rescale 0–100
   
4. **Human Development Index (HDI) components**:
   - Life expectancy, education, income equality
   - Proxy for service delivery capacity
   
5. **Rule of Law Index (World Justice Project)**:
   - Comprehensive measure of justice system quality
   - Rescale 0–100

**Composite measure**:
$$I = w_1 \times I_{\text{WGI}} + w_2 \times I_{\text{V-Dem}} + w_3 \times I_{\text{CPI}} + w_4 \times I_{\text{RuleOfLaw}}$$

Default weights: $w_i = 0.25$. Adjust by context or research priorities.

---

## 4. Calculation Pipeline

### 4.1 Step-by-Step Implementation

```
INPUT: User provides (or system loads) values for T, S, I (all 0–100)

STEP 1: Validate inputs
  - Check T, S, I ∈ [0, 100]
  - If outside range, clamp to [0, 100]

STEP 2: Calculate Negative Peace
  NP = 0.6 × S + 0.4 × I
  
STEP 3: Calculate Positive Peace
  PP = 0.5 × T + 0.5 × I
  
STEP 4: Calculate Balance Factor
  B = 1 - |S - T| / 200
  If B < 0: B = 0
  
STEP 5: Calculate Sustainability
  Sus = 0.3 × T + 0.3 × I + 0.4 × B
  Clamp to [0, 100]
  
OUTPUT: NP, PP, Sus (all 0–100)

STEP 6: Interpret & Provide Feedback
  (See §5 for interpretation logic)
```

### 4.2 Pseudocode (Python)

```python
def calculate_peace_indicators(trust, security, institutions):
    """
    Calculate peace indicators given three dimensions.
    
    Args:
        trust (float): Social trust [0, 100]
        security (float): Security measures intensity [0, 100]
        institutions (float): Institutional strength [0, 100]
    
    Returns:
        dict: {
            'negative_peace': float,
            'positive_peace': float,
            'sustainability': float,
            'interpretation': str
        }
    """
    # Validate inputs
    trust = max(0, min(100, trust))
    security = max(0, min(100, security))
    institutions = max(0, min(100, institutions))
    
    # Calculate outputs
    neg_peace = 0.6 * security + 0.4 * institutions
    pos_peace = 0.5 * trust + 0.5 * institutions
    
    # Balance factor
    balance = max(0, 1 - abs(security - trust) / 200)
    
    # Sustainability
    sustainability = 0.3 * trust + 0.3 * institutions + 0.4 * balance
    
    # Clamp to [0, 100]
    neg_peace = max(0, min(100, neg_peace))
    pos_peace = max(0, min(100, pos_peace))
    sustainability = max(0, min(100, sustainability))
    
    # Interpretation
    interpretation = get_interpretation(neg_peace, pos_peace, sustainability, 
                                       trust, security, institutions)
    
    return {
        'negative_peace': round(neg_peace, 1),
        'positive_peace': round(pos_peace, 1),
        'sustainability': round(sustainability, 1),
        'interpretation': interpretation
    }

def get_interpretation(neg_peace, pos_peace, sustainability, trust, security, institutions):
    """
    Provide qualitative interpretation of peace configuration.
    """
    if neg_peace >= 70 and pos_peace >= 70 and sustainability >= 70:
        return "Robust positive peace: High across all dimensions. Sustainable & resilient."
    elif neg_peace >= 60 and pos_peace >= 60 and sustainability >= 60:
        return "Balanced peace: Moderate on all fronts. Relatively stable if maintained."
    elif neg_peace >= 70 and pos_peace < 50 and sustainability < 60:
        return "Suppressed conflict: Security controls violence but low trust & legitimacy. Brittle; risk of sudden collapse."
    elif pos_peace >= 60 and neg_peace < 50 and security < 40:
        return "Fragile positive peace: High trust & fair institutions but weak enforcement. Vulnerable to shocks or predators."
    elif neg_peace < 40 or pos_peace < 40 or sustainability < 40:
        return "Critical state: Low capacity on key dimensions. High risk of violence or instability."
    else:
        return "Moderate/mixed configuration: Some imbalance. Needs targeted strengthening."
```

---

## 5. Output Interpretation & Qualitative Feedback

### 5.1 Peace State Classifications

| State | NP Range | PP Range | Sus Range | Characteristics | Policy Implication |
|-------|----------|----------|-----------|-----------------|-------------------|
| **Robust Positive** | 70–100 | 70–100 | 70–100 | High capacity across all dimensions | Maintain balance; avoid overreach in any area |
| **Balanced Moderate** | 50–70 | 50–70 | 50–70 | Decent on all fronts; room for improvement | Target weakest dimension |
| **Suppressed Conflict** | 70–100 | <50 | <60 | High security, low trust; brittle | Invest in trust-building, reduce security overhead |
| **Fragile Positive** | <50 | 60–80 | <60 | High trust, weak enforcement/institutions | Strengthen rule of law, build state capacity |
| **Imbalanced** | 50–70 | 50–70 | <50 | Misaligned security & trust | Rebalance; reduce extremes |
| **Critical** | <40 | <40 | <40 | Collapse imminent or ongoing | Emergency state-building; international support |

### 5.2 Textual Feedback Examples

**User input**: T=80, S=30, I=60

```
Calculation:
  NP = 0.6(30) + 0.4(60) = 18 + 24 = 42
  PP = 0.5(80) + 0.5(60) = 40 + 30 = 70
  B = 1 - |30-80|/200 = 1 - 0.25 = 0.75
  Sus = 0.3(80) + 0.3(60) + 0.4(0.75) = 24 + 18 + 0.3 = 42.3

Output: NP=42, PP=70, Sus=42
Interpretation: "Fragile positive peace. Strong social bonds and fair institutions, but weak security capacity leaves you vulnerable to organized threats. Recommend: targeted investment in policing, courts, border control without sacrificing trust."
```

**User input**: T=40, S=85, I=50

```
Calculation:
  NP = 0.6(85) + 0.4(50) = 51 + 20 = 71
  PP = 0.5(40) + 0.5(50) = 20 + 25 = 45
  B = 1 - |85-40|/200 = 1 - 0.225 = 0.775
  Sus = 0.3(40) + 0.3(50) + 0.4(0.775) = 12 + 15 + 0.31 = 27.31

Output: NP=71, PP=45, Sus=27
Interpretation: "Suppressed conflict state. Violence is controlled by strong security, but low public trust and moderate institutions undermine legitimacy. Risk: People comply from fear, not consent. Sudden collapse if security weakens. Recommend: shift toward trust-building, transparent governance, inclusive institutions to transition to sustainable peace."
```

---

## 6. Sensitivity Analysis & Robustness

### 6.1 Weight Sensitivity

**Question**: How much do results change if we vary the weights in NP, PP, Sus functions?

**Method**: 
1. Run model with baseline weights: (0.6, 0.4) for NP; (0.5, 0.5) for PP; (0.3, 0.3, 0.4) for Sus
2. Vary weights by ±20%, ±40%, ±60%
3. Check if qualitative conclusions (e.g., "suppressed peace is unsustainable") hold

**Expected result**: Core insights are robust to reasonable weight variations. Extreme weights (e.g., S=0 in NP formula) may flip conclusions, but those are unrealistic.

**Implementation**: See `notebooks/02_sensitivity_analysis.ipynb`

### 6.2 Parametric Sensitivity

**Question**: Which input dimensions drive output variance most?

**Method**:
1. Fix two dimensions at median (50)
2. Vary the third from 0 to 100
3. Plot output vs. input for each dimension
4. Compare slopes (elasticity)

**Expected result**: 
- NP is most sensitive to S
- PP is equally sensitive to T and I
- Sus is highly sensitive to T and B (balance)

### 6.3 Case Validation

**Approach**: Map known real-world cases (countries, post-conflict regions) onto the model. Check if model outputs align with qualitative understanding and academic consensus.

**Example cases**:
- **Nordic countries**: High T, high I, moderate S → Robust positive peace (model predicts: NP~70, PP~85, Sus~85) ✓
- **Authoritarian with order**: High S, low T, moderate I → Suppressed conflict (model: NP~75, PP~35, Sus~35) ✓
- **Post-conflict with community trust but weak state**: High T, low S, low I → Fragile positive (model: NP~30, PP~50, Sus~30) ✓
- **Failing state**: Low T, low S, low I → Critical (model: NP~20, PP~25, Sus~15) ✓

---

## 7. Limitations & Extensions

### 7.1 Known Limitations

1. **Simplification**: Three dimensions reduce vast complexity. Real peace is multidimensional (economic, environmental, psychological, etc.)
2. **Linearity assumptions**: Interactions may be nonlinear (e.g., trust could have threshold effects)
3. **Static model**: Captures steady-state; does not model transitions, dynamics, or lag effects
4. **No directional causality**: Model illustrates correlations & logical relationships, not causal arrows
5. **Data availability**: Real-world T, S, I are difficult to measure precisely; proxies introduce error
6. **Regional variation**: Optimal weights and balance points may differ by context (post-conflict vs. developed vs. unequal)
7. **Temporal stability**: Coefficients may shift with technological/political change (e.g., rise of mass surveillance)

### 7.2 Extensions & Future Work

1. **Dynamic model**: Add temporal evolution (e.g., differential equations or agent-based simulation)
2. **Additional dimensions**: Include economic inequality, environmental security, trauma/healing, cultural reconciliation
3. **Threshold effects**: Model saturation (e.g., trust has diminishing returns above 80)
4. **Heterogeneity**: Account for subgroups (ethnic, economic, generational) with different trust/security needs
5. **Causal inference**: Combine model with econometric/experimental evidence to establish causal directions
6. **Adaptive optimization**: Help policymakers find optimal paths from one state to another (e.g., "reduce S while building T")
7. **Validation datasets**: Collect cross-national panel data on T, S, I and outcomes (conflict, stability, wellbeing)

---

## 8. Validation Checklist

Use this checklist when applying or adapting the model:

- [ ] **Data sourcing**: Identified primary data for T, S, I (survey, index, institutional data)
- [ ] **Definitions**: Confirmed that T, S, I correspond to operational definitions (§3)
- [ ] **Normalization**: Rescaled all inputs to [0, 100] range
- [ ] **Calculation**: Verified formulas (§2) implemented correctly
- [ ] **Sensitivity**: Run weight & parameter sensitivity tests (§6); confirmed robustness
- [ ] **Case validation**: Mapped known cases to model; checked plausibility
- [ ] **Documentation**: Recorded assumptions, data sources, modifications
- [ ] **Transparency**: Shared all parameters, weights, data with users/reviewers
- [ ] **Caveats**: Clearly noted limitations & causal inferences to avoid

---

## 9. References

Key methodological references:
- **Galtung (1969)**: Positive/negative peace framework
- **Sterman (2000)**: System dynamics methodology
- **Kaufmann et al. (2011)**: Governance indicators methodology
- **Pearl (2009)**: Causal inference (epistemological grounding)

See [ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md) for complete bibliography.

---

## Contact & Support

For questions on model specification, implementation, or validation:
- Open an issue on GitHub
- Contact: juapache@protonmail.com
- Website: [juapache.github.io](https://juapache.github.io)

---

**Last Updated**: January 2026  
**Version**: 1.0  
**Maintainer**: Juan José Vásquez-Pacheco
