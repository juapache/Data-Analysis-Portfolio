# The Trust Paradox: Documentation Index

## Quick Navigation

Welcome! This documentation package provides everything you need to understand, use, and extend **The Trust Paradox** model—an interactive visualization exploring how trust, security, and institutions shape sustainable peace.

---

## 📖 Documentation Files

### 1. **README.md** (Start here!)
**What**: High-level overview of the project  
**For**: Everyone  
**Read time**: 10 minutes  
**Contains**: 
- Core concept & the paradox explained
- Key dimensions (trust, security, institutions)
- Audience & use cases
- Repository structure
- Citation & license

👉 [Read README.md](README.md)

---

### 2. **IMPLEMENTATION_GUIDE.md** (How to use it)
**What**: Practical step-by-step guide for different users  
**For**: 
- Website users (interactive exploration)
- Researchers & analysts (apply to your country/region)
- Programmers (integrate into applications)

**Read time**: Varies (skim relevant section)  
**Contains**:
- Quick start for interactive tool
- Research workflow (data gathering → analysis → interpretation)
- Code snippets & Jupyter notebooks
- Context-specific adaptations (post-conflict, organizational, etc.)
- Best practices & troubleshooting
- Publishing guidance

👉 [Read IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md)

---

### 3. **METHODOLOGY.md** (How it works)
**What**: Complete mathematical specification & model details  
**For**: 
- Researchers validating the model
- Data scientists extending it
- Anyone wanting deep understanding

**Read time**: 20–30 minutes  
**Contains**:
- Model structure (3 dimensions, 3 outputs)
- Formulas for Negative Peace, Positive Peace, Sustainability
- Data sourcing & parameterization guidance
- Calculation pipeline & pseudocode
- Output interpretation & qualitative feedback
- Sensitivity analysis methodology
- Limitations & extensions

👉 [Read METHODOLOGY.md](METHODOLOGY.md)

---

### 4. **ACADEMIC_REFERENCES.md** (Grounding in research)
**What**: Comprehensive bibliography & literature review  
**For**: 
- Researchers wanting empirical backing
- Educators preparing courses
- Anyone curious about sources

**Read time**: Varies (reference document)  
**Contains**:
- 39 curated academic sources organized by topic:
  - Peace studies (Galtung, Lederach, Braithwaite)
  - Social trust & capital (Putnam, Fukuyama)
  - Institutional economics (North, Acemoglu & Robinson)
  - Security & legitimacy (Tyler, Moyn)
  - Conflict & peacebuilding
  - Governance quality & measurement
  - And more...
- Reading paths for different audiences
- Data sources for validation

👉 [Read ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md)

---

## 🎯 Which Document Do I Need?

### "I just want to play with the interactive tool"
→ No documentation needed! Just visit [juapache.github.io/trust-paradox.html](https://juapache.github.io/trust-paradox.html)

### "I want to understand what this is about"
→ Read [**README.md**](README.md) (10 min)

### "I want to apply this to my country/organization"
→ Read [**IMPLEMENTATION_GUIDE.md**](IMPLEMENTATION_GUIDE.md) section A.2 (1–2 hours)

### "I want to understand the math & validate the model"
→ Read [**METHODOLOGY.md**](METHODOLOGY.md) (20–30 min) + [**ACADEMIC_REFERENCES.md**](ACADEMIC_REFERENCES.md) for grounding

### "I want to build something with this or extend it"
→ Read [**METHODOLOGY.md**](METHODOLOGY.md) + [**IMPLEMENTATION_GUIDE.md**](IMPLEMENTATION_GUIDE.md) section A.3

### "I'm teaching a class or writing a paper on this"
→ Start with [**README.md**](README.md), then [**ACADEMIC_REFERENCES.md**](ACADEMIC_REFERENCES.md)

---

## 📁 Repository Structure

```
trust-paradox/
├── README.md                          # ← Start here
├── IMPLEMENTATION_GUIDE.md            # ← How to use & apply
├── METHODOLOGY.md                     # ← Model specification
├── ACADEMIC_REFERENCES.md             # ← Literature grounding
├── INDEX.md                           # ← This file
│
├── notebooks/
│   ├── 01_peace_indicators_analysis.ipynb        # Data analysis workflow
│   ├── 02_sensitivity_analysis.ipynb             # Robustness testing
│   ├── 03_visualization_design.ipynb             # Chart creation
│   └── README.md                                 # Notebook guide
│
├── src/
│   ├── peace_calculator.py            # Core model (formulas)
│   ├── visualization_helpers.py       # Plotting utilities
│   ├── sensitivity_tools.py           # Robustness testing
│   └── __init__.py
│
├── data/
│   ├── README.md                      # Data documentation
│   ├── raw/                           # Source files (untouched)
│   ├── processed/                     # Your working files
│   └── external/                      # Reference tables
│
├── results/
│   ├── README.md
│   ├── figures/                       # Charts & visualizations
│   ├── case_studies/                  # Regional analyses
│   └── summary_reports/               # Policy briefs
│
├── requirements.txt                   # Python dependencies
└── LICENSE                            # CC-BY-NC 4.0
```

---

## 🚀 Getting Started Paths

### Path A: Interactive Explorer (5 min)
1. Visit [juapache.github.io/trust-paradox.html](https://juapache.github.io/trust-paradox.html)
2. Move the three sliders
3. Read the interpretation text
4. Experiment with different scenarios

### Path B: Understand the Concept (15 min)
1. Read [README.md](README.md) § "Core Concept"
2. Watch the interactive tool illustrate the concepts
3. Read [README.md](README.md) § "Key Dimensions & Assumptions"

### Path C: Apply to a Country (1 week)
1. Read [IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md) § A.2 (Steps 1–5)
2. Gather data (WVS, World Bank, V-Dem)
3. Run calculations (spreadsheet or Jupyter)
4. Interpret results using [README.md](README.md) § "Outputs & Visualization"

### Path D: Deep Dive for Researchers (2–3 weeks)
1. Read [README.md](README.md) (full)
2. Read [METHODOLOGY.md](METHODOLOGY.md) (full)
3. Read [ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md)
4. Run [notebooks/02_sensitivity_analysis.ipynb](notebooks/)
5. Validate against known cases
6. Extend with own data or modifications

### Path E: Build a Tool (2–4 weeks)
1. Read [METHODOLOGY.md](METHODOLOGY.md)
2. Read [IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md) § A.3 (programming)
3. Study [src/peace_calculator.py](src/)
4. Run [notebooks/01_peace_indicators_analysis.ipynb](notebooks/) for workflow example
5. Adapt code for your application
6. Add custom features (e.g., time-series, regional sub-analysis)

---

## 🔗 External Resources

### Data Sources (Free)
- **World Values Survey**: [worldvaluessurvey.org](http://www.worldvaluessurvey.org)
- **World Bank Indicators**: [data.worldbank.org](http://data.worldbank.org)
- **V-Dem Institute**: [v-dem.net](http://v-dem.net)
- **Transparency International CPI**: [transparency.org](http://transparency.org)
- **Global Peace Index**: [visionofhumanity.org](http://visionofhumanity.org)

### Tools & Platforms
- **Jupyter**: [jupyter.org](http://jupyter.org)
- **Python**: [python.org](http://python.org)
- **GitHub**: [github.com](http://github.com) (for version control)

### Key Academic Sources
See [ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md) for 39+ papers, books, and datasets grounding this work

---

## ❓ Frequently Asked Questions

### Q: Is this a real model or just conceptual?
**A**: It's grounded in academic literature (peace studies, institutional economics, social trust research) but simplified for clarity. The formulas are indicative, not deterministic. Use it to frame thinking and explore trade-offs, not as a prediction tool.

### Q: Can I use this in my research?
**A**: Yes! See [ACADEMIC_REFERENCES.md](ACADEMIC_REFERENCES.md) for citation and [IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md) § G for publishing guidance.

### Q: Which countries/regions have data?
**A**: Countries with World Values Survey and World Bank indicators (150+). See [IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md) § A.2 for data sourcing.

### Q: Can I adapt this for my local/organizational context?
**A**: Yes. See [IMPLEMENTATION_GUIDE.md](IMPLEMENTATION_GUIDE.md) § D "Adapting for Specific Contexts"

### Q: Is the code open-source?
**A**: Yes, under CC-BY-NC 4.0. See [LICENSE](LICENSE).

---

## 🤝 Contributing & Feedback

### How to contribute
1. **Report issues**: GitHub Issues (bugs, unclear documentation)
2. **Suggest improvements**: Open a Discussion or email
3. **Extend the model**: Fork, modify, submit pull request

### Give feedback
- On the interactive tool: Email or GitHub Issues
- On the documentation: GitHub Issues
- On methodology: Direct email (detailed critique welcome)

---

## 📞 Contact & Support

**Website**: [juapache.github.io](https://juapache.github.io)  
**Email**: [your contact email]  
**GitHub**: [juapache/research-workspace](https://github.com/juapache/research-workspace)

---

## 📜 License

This work is licensed under **CC-BY-NC 4.0** (Creative Commons Attribution-NonCommercial).

- ✅ **You may**: Share, adapt, use for non-commercial purposes with attribution
- ❌ **You may not**: Use commercially without explicit permission

See [LICENSE](LICENSE) for details.

---

## 📅 Document Status

| Document | Version | Last Updated | Status |
|----------|---------|--------------|--------|
| README.md | 1.0 | Jan 2026 | Complete |
| IMPLEMENTATION_GUIDE.md | 1.0 | Jan 2026 | Complete |
| METHODOLOGY.md | 1.0 | Jan 2026 | Complete |
| ACADEMIC_REFERENCES.md | 1.0 | Jan 2026 | Complete |

---

**Happy exploring!** 🌍

For any questions, start with this index, then dive into the relevant documentation. Feel free to reach out if something is unclear.

---

**Maintained by**: Juan José Vásquez-Pacheco  
**Last Updated**: January 2026  
**License**: CC-BY-NC 4.0
