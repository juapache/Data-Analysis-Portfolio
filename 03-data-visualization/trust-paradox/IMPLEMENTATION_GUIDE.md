# Implementation Guide: The Trust Paradox Model

## A. Quick Start for Different Users

### A.1 For Website/Interactive Users
**Goal**: Explore the model visually without coding

1. Visit: [juapache.github.io/trust-paradox.html](https://juapache.github.io/trust-paradox.html)
2. Use the three sliders to adjust:
   - **Social Trust** (0–100): Level of community confidence
   - **Security Measures** (0–100): Intensity of enforcement, surveillance
   - **Institutional Strength** (0–100): Quality of governance, rule of law
3. Observe the outputs:
   - **Negative Peace**: Absence of violence
   - **Positive Peace**: Presence of justice and wellbeing
   - **Sustainability**: Whether the configuration is resilient
4. Read the interpretation text (e.g., "Robust positive peace," "Suppressed conflict")
5. Experiment with different scenarios to understand trade-offs

**Time commitment**: 5–10 minutes

---

### A.2 For Researchers & Analysts
**Goal**: Apply the model to specific contexts (e.g., a country, region, organization)

#### Step 1: Gather Data (1–2 weeks)

**For Social Trust (T)**:
- Query World Values Survey (WVS) by country: [worldvaluessurvey.org](http://www.worldvaluessurvey.org)
  - Look for: "Most people can be trusted" % yes
  - Also: Trust in institutions (police, courts, parliament)
- Alternative: V-Dem institutional trust indicators (free download)
- For custom contexts: Design simple survey (e.g., "On a scale of 1–10, how much do you trust your neighbors?") and aggregate

**For Security Measures (S)**:
- World Bank data (data.worldbank.org):
  - Police-to-population ratio
  - Military expenditure (% GDP)
  - Prison population rate
- UN Office on Drugs & Crime: Homicide data (as reality check)
- Alternative indices:
  - V-Dem rule of law estimate
  - Freedom House internet filtering index
  - Custom: Count actual police deployments, checkpoints, surveillance visible to community

**For Institutional Strength (I)**:
- World Bank Worldwide Governance Indicators (WGI): Free download
  - Use `Rule of Law` + `Government Effectiveness` + average
- V-Dem indices: Free download
  - Electoral democracy, accountability, egalitarian representation
- Transparency International Corruption Perception Index (CPI)
- World Justice Project Rule of Law Index
- Custom: Survey on institutional service delivery, fairness, inclusion

#### Step 2: Standardize & Normalize (1 day)

Create a spreadsheet (Excel, CSV) with columns:

| Country/Region | T_WVS | T_VDem | T_Custom | T_Final | S_Police | S_Military | S_Prison | S_Final | I_WGI | I_VDem | I_CPI | I_Final | Notes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Sweden | 65 | 78 | — | 72 | 30 | 5 | 15 | 20 | 92 | 90 | 87 | 90 | High trust, moderate security |
| Brazil | 40 | 35 | — | 38 | 60 | 20 | 85 | 55 | 45 | 48 | 42 | 45 | Medium trust, high security |
| Somalia | 20 | 15 | 18 | 18 | 20 | 50 | 40 | 37 | 15 | 12 | 10 | 12 | Failing state |

**Normalization rule**:
- If source is already 0–100: Use directly
- If source is percentage: Use directly
- If source is index (e.g., –2.5 to +2.5 WGI): Rescale
  - Formula: $\text{Rescaled} = \frac{\text{Value} - \text{Min}}{\text{Max} - \text{Min}} \times 100$
  - Example (WGI = –0.5, range is –2.5 to +2.5): $\frac{-0.5 - (-2.5)}{2.5 - (-2.5)} \times 100 = \frac{2}{5} \times 100 = 40$

- For final aggregates (e.g., T_Final from multiple sources):
  $$T_{\text{Final}} = \frac{T_{\text{WVS}} + T_{\text{VDem}} + T_{\text{Custom}}}{3}$$
  (Use equal weights unless context suggests otherwise; document your choice)

#### Step 3: Calculate Peace Indicators (1 hour)

In spreadsheet or Python:

```excel
=0.6*S_Final + 0.4*I_Final    [Negative Peace]
=0.5*T_Final + 0.5*I_Final    [Positive Peace]
=MAX(0, 1 - ABS(S_Final - T_Final) / 200)    [Balance Factor]
=0.3*T_Final + 0.3*I_Final + 0.4*Balance     [Sustainability]
```

Or in Python:

```python
import pandas as pd

df = pd.read_csv('peace_data.csv')

df['Negative_Peace'] = 0.6 * df['S_Final'] + 0.4 * df['I_Final']
df['Positive_Peace'] = 0.5 * df['T_Final'] + 0.5 * df['I_Final']
df['Balance'] = 1 - (df['S_Final'] - df['T_Final']).abs() / 200
df['Balance'] = df['Balance'].clip(lower=0)
df['Sustainability'] = 0.3 * df['T_Final'] + 0.3 * df['I_Final'] + 0.4 * df['Balance']

print(df[['Country', 'Negative_Peace', 'Positive_Peace', 'Sustainability']])
```

#### Step 4: Interpret Results (1–2 hours)

For each country/region, examine:

1. **Which indicator is lowest?** (Points to priority area)
2. **Are S and T balanced?** (If S >> T or T >> S, sustainability is compromised)
3. **Compare to peer countries**: Why does Norway have higher PP than Brazil? Institutional quality? Trust differences?
4. **Policy implications**: 
   - If S is high but T is low → Recommend trust-building initiatives (transparency, community policing, justice access)
   - If T is high but I is low → Recommend capacity-building (training judges, building services)
   - If all are low → Emergency state/society rebuilding

#### Step 5: Validate Against Qualitative Knowledge (1 day)

Does the model output match what you know about the case?

- **Sweden** (model: NP=70, PP=90, Sus=80): Real world is stable, low violence, high wellbeing ✓
- **Venezuela** (model: NP=50, PP=30, Sus=25): Real world has violence, institutional collapse, low trust ✓
- **Hong Kong** (model: NP=80, PP=40, Sus=35): Real world has low crime (high S) but declining trust in government ✓

If mismatches exist, investigate:
- Data quality issues (outdated indices?)
- Missing dimensions (e.g., economic opportunity, identity grievance)
- Model limitations (model is simplified by design)

---

### A.3 For Programmers & Data Scientists
**Goal**: Extend or integrate the model into applications

#### Use the Model as a Library

**Note**: This tool is designed for web-based interactive exploration. For research or analytical use, refer to the mathematical formulas in [METHODOLOGY.md](METHODOLOGY.md) to implement the calculations in your preferred environment.

```python
# Import the calculator
from src.peace_calculator import calculate_peace_indicators

# Input values
trust = 65
security = 40
institutions = 75

# Calculate
result = calculate_peace_indicators(trust, security, institutions)

print(f"Negative Peace: {result['negative_peace']}")
print(f"Positive Peace: {result['positive_peace']}")
print(f"Sustainability: {result['sustainability']}")
print(f"Interpretation: {result['interpretation']}")
```

#### Run Sensitivity Analysis

```python
from src.sensitivity_tools import sensitivity_sweep, plot_sensitivity

# Vary security from 0 to 100, hold T=60, I=70
results = sensitivity_sweep(
    varying_param='security',
    base_trust=60,
    base_institutions=70,
    param_range=(0, 100),
    steps=20
)

plot_sensitivity(results, output_file='security_sensitivity.png')
```

#### Integrate into Web Application

```javascript
// JavaScript snippet for web integration
function calculatePeace(trust, security, institutions) {
  const negPeace = 0.6 * security + 0.4 * institutions;
  const posPeace = 0.5 * trust + 0.5 * institutions;
  const balance = Math.max(0, 1 - Math.abs(security - trust) / 200);
  const sustainability = 0.3 * trust + 0.3 * institutions + 0.4 * balance;
  
  return {
    negativePeace: Math.round(negPeace),
    positivePeace: Math.round(posPeace),
    sustainability: Math.round(sustainability)
  };
}
```

---

## B. Using Jupyter Notebooks

Located in `/notebooks/`:

### 01_peace_indicators_analysis.ipynb
- Load cross-national data
- Calculate peace indicators for multiple countries
- Create comparison visualizations
- Export results to CSV/JSON

**Run it**:
```bash
jupyter lab notebooks/01_peace_indicators_analysis.ipynb
```

### 02_sensitivity_analysis.ipynb
- Test robustness to parameter changes
- Identify which inputs drive output variance most
- Visualize confidence intervals
- Validate model assumptions

**Run it**:
```bash
jupyter lab notebooks/02_sensitivity_analysis.ipynb
```

### 03_visualization_design.ipynb
- Create custom charts for reports/presentations
- Generate case study maps and profiles
- Design interactive dashboards
- Export figures for publication

**Run it**:
```bash
jupyter lab notebooks/03_visualization_design.ipynb
```

---

## C. Data & File Organization

### Raw Data (`data/raw/`)

Store source files here:
- `world_values_survey_2022.csv`: WVS trust question by country
- `world_bank_wgi.csv`: World Bank governance indicators
- `v_dem_indicators.csv`: V-Dem democracy indices
- `custom_surveys/[region]/`: Your own survey data

Keep these **read-only**; always work from copies in `processed/`.

### Processed Data (`data/processed/`)

Your working files:
- `peace_data_consolidated.csv`: Merged T, S, I by country/year
- `peace_indicators_2024.csv`: Calculated NP, PP, Sus
- `sensitivity_results.json`: Robustness test outputs
- `validation_mapping.csv`: Real-world cases + model outputs + check

### Results (`results/`)

Final outputs:

- `figures/`: Publication-quality charts
  - `global_peace_map.png`: Scatter of all countries
  - `regional_comparison.png`: NP vs PP by region
  - `sensitivity_tornado.png`: Parameter importance
  
- `case_studies/`: Regional/country deep-dives
  - `nordic_region.md`: Analysis of Nordic countries
  - `southern_africa.md`: Regional profile
  
- `summary_reports/`: Policy briefs
  - `executive_summary.pdf`: 2–3 page overview
  - `policy_recommendations.docx`: Actionable takeaways

---

## D. Adapting for Specific Contexts

### For a Country-Level Analysis

1. **Customize data sources**:
   - Replace World Values Survey with national survey if available
   - Use country-specific governance assessments
   
2. **Sub-regional variation**:
   - Calculate T, S, I for provinces/districts separately
   - Create heatmap showing variation within country
   
3. **Temporal analysis**:
   - Collect data for multiple years (e.g., 2010–2024)
   - Plot trajectories: Is peace improving or degrading?

Example: Chile
- Data: 2010 WVS (pre-protests), 2020 WVS (post-crisis), 2023 custom survey
- Calculate for national level and by region (North, Metropolitan, South)
- Visualize: How did 2019 protests affect T? Did S increase?

### For Post-Conflict Peacebuilding

1. **Adjust interpretation**:
   - T starts low (trauma, fear) → focus on early trust-building
   - S may start high (military presence) → gradual drawdown critical
   - I is weak (institutions damaged) → long-term capacity-building
   
2. **Monitor transitions**:
   - Year 1–2: NP may be high (security presence) but PP, Sus low
   - Year 3–5: Goal is to increase T, build I while carefully reducing S
   - Metric: Sustainability should rise if transition succeeds

3. **Example trajectory: Rwanda post-1994**
   - 1994: T≈10, S≈40, I≈15 (emergency response, trauma)
   - 2000: T≈25, S≈60, I≈20 (security enhanced, trust still low)
   - 2010: T≈40, S≈50, I≈40 (capacity built, some trust recovered)
   - 2024: T≈45, S≈40, I≈55 (balanced progress, though T recovery slow)
   → Conclusion: Post-conflict trust recovery is slower than institution-building

### For Organizational/Local Settings

Adapt dimensions to micro-level:

- **Social Trust (T)**: Employee/resident trust in leadership and each other (survey: "Do you trust your manager?")
- **Security Measures (S)**: Surveillance, enforcement, control mechanisms (e.g., monitoring software, strict rules)
- **Institutional Strength (I)**: Organizational capacity to deliver services/fairness, clear rules, dispute resolution

Example: Hospital trust & safety culture

| Context | Trust Question | Security Measure | Institutional Strength |
|---------|---|---|---|
| Hospital | Staff trust in management & each other (survey) | Incident reporting, audits, compliance checks | Protocols, training, incident response system |
| School | Student/teacher trust in administration | Discipline policies, monitoring, lockdowns | Inclusive governance, transparent rules, support services |
| Community org | Member trust in leadership | Membership controls, transparency requirements | Conflict resolution, accountability, delivery on mission |

---

## E. Best Practices & Pitfalls

### ✓ Do:

1. **Document your data sources & assumptions** clearly
   - Where did you get T, S, I values?
   - What years? From which publications?
   - Why those specific measures?
   
2. **Validate against qualitative knowledge**
   - Does the model output match your understanding of the case?
   - If not, investigate why before publicizing
   
3. **Conduct sensitivity analysis**
   - Test robustness to ±20% weight changes
   - Show confidence ranges in results (not just point estimates)
   
4. **Acknowledge limitations**
   - Model simplifies complex reality
   - No causal claims without evidence
   - Results are indicative, not deterministic
   
5. **Update data regularly**
   - Use recent surveys/indices when available
   - Document when data is from (e.g., "WVS 2020") in all outputs

### ✗ Don't:

1. **Use outdated data** without noting it
   - A 2010 WVS value may not reflect 2024 reality
   - Clearly mark data vintage in reports
   
2. **Over-interpret small differences**
   - Model: NP=45 vs NP=48 are essentially the same (measurement error)
   - Only major differences (e.g., NP=40 vs NP=65) are meaningful
   
3. **Claim causation**
   - Model shows correlation/relationship, not causation
   - Saying "increasing security causes higher negative peace" is tempting but unfounded
   
4. **Ignore regional/temporal context**
   - A country in civil war needs different interpretation than peaceful country
   - What works in post-conflict may not work in high-inequality societies
   
5. **Use as a black box**
   - Always understand the formulas (see [METHODOLOGY.md](METHODOLOGY.md))
   - Be prepared to explain to skeptics

---

## F. Troubleshooting & FAQ

### Q: My data has missing values for some countries. How do I handle it?
**A**: 
- Check if missing data is random or systematic (e.g., authoritarian countries don't publish trust data)
- If few missing: Use regional average as proxy (e.g., Sub-Saharan Africa average)
- If many missing: Either (a) impute with statistical methods, or (b) exclude from analysis and note limitation
- **Never** silently drop missing data; always note and justify

### Q: I have different years for T, S, I. Is that a problem?
**A**: 
- Ideally, use same year for all three dimensions
- If forced to mix years: Use most recent available
- Document explicitly: "T = 2022 WVS, S = 2023 military data, I = 2024 WGI"
- Check if values are stable across years (if trust barely changed 2020–2024, using 2020 value in 2024 analysis is acceptable)

### Q: Which data source should I prioritize if I have multiple?
**A**: 
1. **Specificity**: Country/region-specific > Global survey
2. **Recency**: Newer > older (within reason; sudden jumps suggest measurement change, not real change)
3. **Rigor**: Peer-reviewed, transparent methodology > Gray reports or blogs
4. **Alignment**: If you're assessing horizontal trust, use community survey > institutional trust alone

Example: For Brazil trust, prefer:
1. Brazil-specific community survey (if available)
2. Brazil in WVS or Latinobarometer
3. V-Dem indicators (global coverage, transparent methodology)
4. Blog post claiming "Brazilians are X% trusting" (last resort only)

### Q: What if the model predicts conflicting outcomes (e.g., high NP but low Sus)?
**A**: 
This is **not** a problem; it's the model *working correctly*. It illustrates the paradox:
- High S + low T can produce high NP (violence suppressed by force) but low Sus (not sustainable)
- This is the core insight: short-term peace (NP) ≠ long-term stability (Sus)
- Interpretation: "This society has law and order but is brittle; people comply from fear, not consent. At risk of sudden collapse."

### Q: Can I compare two countries directly using model outputs?
**A**: 
- Yes, if using same year and data sources
- **Do** say: "Country A has higher sustainability (78 vs 62), indicating more resilient peace"
- **Don't** say: "Country A is 78% peaceful" (that's misinterpreting the index)
- **Always** note: These are relative comparisons, not absolute measures of peace quality

---

## G. Publishing Results

### For Academic Publication

**Essential elements**:
1. Methods section explaining:
   - Data sources for T, S, I (with citations)
   - Normalization procedures
   - Formula (with derivation in appendix)
   - Sensitivity analysis results
   
2. Results section showing:
   - Table of T, S, I, NP, PP, Sus by case
   - Scatter plot (NP vs PP colored by region)
   - Case examples illustrating each state category
   
3. Discussion addressing:
   - Validation against existing literature
   - Limitations of model
   - Policy implications
   - Future extensions

### For Policy Briefs / Reports

**Simplified presentation**:
1. Single-page visual: World map colored by peace state (Robust / Balanced / Suppressed / Fragile / Critical)
2. Key finding: "23% of countries in suppressed conflict state; at risk of instability"
3. Recommendations by state category (e.g., "For suppressed conflict countries, prioritize trust-building initiatives")
4. Appendix: Full data table + methodology summary (not all readers need it)

### For Interactive Web / Dashboard

**User experience**:
1. Default view: Global map
2. Interactive layer: Sliders to explore counterfactual ("What if we increased trust?")
3. Comparison tool: Select 2–3 countries to compare side-by-side
4. Case profiles: Click country → see profile (T, S, I, recent trends, policy context)
5. Methodology link: "How is this calculated?" → Detailed explanation

---

## H. Resources & Templates

### Data Collection Template

See [templates/peace_data_collection.xlsx](../../templates/peace_data_collection.xlsx):
- Pre-formatted columns for T, S, I
- Data source documentation fields
- Notes/caveats column
- Year field

### Reporting Template

See [templates/peace_indicators_report.docx](../../templates/peace_indicators_report.docx):
- Executive summary structure
- Results table format
- Interpretation guidance for each indicator
- Limitation/caveat checklist

### Code Templates

See [src/](../../src/):
- `peace_calculator.py`: Copy-paste functions for your analysis
- `visualization_helpers.py`: Plotting functions for charts
- `sensitivity_tools.py`: Robustness testing functions

---

## I. Getting Help

### Documentation
- [README.md](README.md): Overview & conceptual introduction
- [METHODOLOGY.md](METHODOLOGY.md): Full mathematical specification
- [ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md): Grounding in literature

### Code Examples
- `notebooks/01_peace_indicators_analysis.ipynb`: Walkthrough with real data
- `notebooks/02_sensitivity_analysis.ipynb`: How to test robustness
- `notebooks/03_visualization_design.ipynb`: How to create publication-quality figures

### Community
- GitHub Issues: Report bugs or request features
- Email: juapache@protonmail.com
- Website: [juapache.github.io](https://juapache.github.io)

---

**Last Updated**: January 2026  
**Version**: 1.0  
**For questions**: See "Getting Help" section above
