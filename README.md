# Shashank_Take-Home-Final-Teaching-Data-Science-Concepts
# Data Quality Pipeline: Teaching GIGO Principles

> *A systematic framework for data quality assessment across six dimensions*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org/)

## 🎥 Video Tutorial

**Watch the complete 10-minute walkthrough:**  
[📺 Data Quality Pipeline Tutorial](https://youtu.be/qFpl28Uu_hw)

---

## 📋 Table of Contents

- [Concept Overview](#-concept-overview)
- [The Six Quality Dimensions](#-the-six-quality-dimensions)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Usage Examples](#-usage-examples)
- [Learning Objectives](#-learning-objectives)
- [Documentation](#-documentation)
- [License](#-license)
- [Contact](#-contact)

---

## 🎯 Concept Overview

Data quality determines whether analytical conclusions can be trusted. When datasets contain errors, missing information, or inconsistent formatting, even sophisticated algorithms produce misleading results. This tutorial teaches systematic approaches to identify and correct quality problems before they compromise decision-making.

**The GIGO Principle**: Garbage In, Garbage Out

### Why This Matters

Professional data scientists spend **60-80% of their time** on data quality work, yet most educational programs focus primarily on modeling techniques. This framework addresses that gap by providing:

- **Systematic Detection**: Automated functions to identify six categories of quality issues
- **Strategic Remediation**: Context-appropriate cleaning strategies with documented tradeoffs
- **Rigorous Validation**: Quantitative proof that cleaning improved data reliability
- **Domain Adaptation**: Examples from healthcare, e-commerce, and IoT sensors

### Real-World Impact

Quality failures have real consequences:
- A hospital's 92% accurate model failed in production due to age entry errors (200 years)
- A retailer over-ordered millions in inventory from duplicate transaction records
- An e-commerce site recommended owned products due to inconsistent product IDs

---

## 🔍 The Six Quality Dimensions

This framework systematically addresses six quality dimensions:

| Dimension | Definition | Example Issue | Detection Method |
|-----------|-----------|---------------|------------------|
| **Completeness** | All required values present | 20% of ages missing | Count nulls per column |
| **Uniqueness** | No duplicate records | Same customer twice | Hash-based comparison |
| **Validity** | Values within reasonable ranges | Age = 200 years | IQR/Z-score outlier detection |
| **Consistency** | Uniform data types | Age as "25" and 25 | Type checking and conversion |
| **Accuracy** | Values satisfy business rules | Negative prices | Business rule validation |
| **Uniformity** | Standardized formatting | "NYC" vs "New York" | String pattern analysis |

---

## 🚀 Installation

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Jupyter Notebook or JupyterLab

### Setup
```bash
# Clone the repository
git clone [https://github.com/YOUR_USERNAME/data-quality-gigo-pipeline.git](https://github.com/ShashankJanke15/Shashank_Take-Home-Final-Teaching-Data-Science-Concepts.git)
cd data-quality-gigo-pipeline

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook notebooks/data_quality_pipeline.ipynb
```

### Requirements
```
pandas>=1.5.0
numpy>=1.23.0
matplotlib>=3.6.0
seaborn>=0.12.0
jupyter>=1.0.0
```

---

## 💻 Quick Start

### Running the Tutorial

1. **Open the notebook**:
```bash
   jupyter notebook notebooks/data_quality_pipeline.ipynb
```

2. **Run all cells** to see the complete workflow:
   - Data loading and controlled corruption
   - Quality assessment across six dimensions
   - Strategic cleaning implementations
   - Before/after validation

3. **Try the practice exercise** in Section 7:
   - Employee dataset with realistic quality issues
   - Hands-on TODO sections for independent practice
   - Solutions provided for self-assessment

### Quick Example
```python
import pandas as pd
from data_quality_pipeline import assess_missing_values, detect_duplicates

# Load your dataset
df = pd.read_csv('your_data.csv')

# Assess completeness
missing_report = assess_missing_values(df)

# Check for duplicates
duplicate_report = detect_duplicates(df)

# View quality summary
print(f"Missing values: {len(missing_report)}")
print(f"Duplicate records: {len(duplicate_report)}")
```

---

## 📚 Usage Examples

### Example 1: Basic Quality Assessment
```python
# Import detection functions
from data_quality_pipeline import (
    assess_missing_values,
    detect_duplicates,
    detect_outliers,
    check_data_types,
    check_constraints,
    check_formatting_issues
)

# Load dataset
df = pd.read_csv('customer_data.csv')

# Run comprehensive quality checks
missing = assess_missing_values(df)
duplicates = detect_duplicates(df)
outliers = detect_outliers(df, columns=['age', 'income'])
types = check_data_types(df)
constraints = check_constraints(df)
formatting = check_formatting_issues(df)

# Generate quality report
quality_score = calculate_quality_score(df)
print(f"Overall Quality Score: {quality_score}/100")
```

### Example 2: Cleaning Pipeline
```python
# Import cleaning functions
from data_quality_pipeline import (
    handle_missing_values,
    remove_duplicates,
    handle_outliers,
    fix_data_types,
    enforce_constraints,
    standardize_formatting
)

# Create copy for cleaning
df_clean = df.copy()

# Apply systematic cleaning
df_clean = handle_missing_values(df_clean, strategy='median')
df_clean = remove_duplicates(df_clean, keep='first')
df_clean = handle_outliers(df_clean, columns=['price'], method='cap')
df_clean = fix_data_types(df_clean, {'age': 'float64'})
df_clean = enforce_constraints(df_clean, {'age': (0, 120)})
df_clean = standardize_formatting(df_clean, ['city', 'state'])

# Validate improvements
compare_quality(df, df_clean)
```

### Example 3: Domain-Specific Adaptation (Healthcare)
```python
# Healthcare-specific constraints
healthcare_rules = {
    'age': (0, 120),
    'blood_pressure_systolic': (50, 250),
    'blood_pressure_diastolic': (30, 150),
    'heart_rate': (30, 220),
    'temperature_f': (95, 108)
}

# Apply healthcare-specific validation
df_patients = enforce_constraints(df_patients, healthcare_rules)

# Handle missing lab results (might be clinically meaningful)
# Don't impute - flag instead
df_patients['glucose_missing'] = df_patients['glucose'].isna()
```

### Example 4: Complete Workflow
```python
# Full pipeline from assessment to validation
def quality_pipeline(df):
    """Execute complete quality assessment and cleaning."""
    
    # 1. ASSESS
    print("="*60)
    print("ASSESSING DATA QUALITY")
    print("="*60)
    assess_missing_values(df)
    detect_duplicates(df)
    detect_outliers(df, columns=['numerical_columns'])
    
    # 2. CLEAN
    print("\n" + "="*60)
    print("CLEANING DATA")
    print("="*60)
    df_clean = df.copy()
    df_clean = handle_missing_values(df_clean, strategy='median')
    df_clean = remove_duplicates(df_clean)
    df_clean = handle_outliers(df_clean, columns=['price'], method='cap')
    
    # 3. VALIDATE
    print("\n" + "="*60)
    print("VALIDATING IMPROVEMENTS")
    print("="*60)
    compare_datasets(df, df_clean)
    
    return df_clean

# Execute pipeline
cleaned_data = quality_pipeline(raw_data)
```

---

## 🎓 Learning Objectives

After completing this tutorial, you will be able to:

### Technical Skills
- ✅ **Implement** automated quality checks across six dimensions using Python
- ✅ **Select** appropriate cleaning strategies based on data characteristics and missing data mechanisms (MCAR, MAR, MNAR)
- ✅ **Apply** statistical methods (IQR, Z-score) for outlier detection
- ✅ **Validate** cleaning effectiveness through quantitative metrics and visualizations
- ✅ **Build** reproducible quality pipelines suitable for production deployment

### Analytical Skills
- ✅ **Distinguish** between quality issues requiring correction versus meaningful signal
- ✅ **Evaluate** tradeoffs between data retention and quality improvement
- ✅ **Adapt** generic frameworks to domain-specific constraints (healthcare, finance, IoT)
- ✅ **Interpret** quality metrics in business context for stakeholder communication

### Professional Practices
- ✅ **Document** quality assessment findings and cleaning decisions for reproducibility
- ✅ **Communicate** technical quality work to non-technical audiences
- ✅ **Design** modular, reusable code following software engineering principles
- ✅ **Recognize** when quality problems indicate systemic process failures

### Domain Applications
- ✅ Apply quality frameworks to **healthcare** data with biological constraints
- ✅ Validate **e-commerce** transactions with business rule enforcement
- ✅ Handle **IoT sensor** data with temporal dependencies
- ✅ Understand domain-specific quality requirements and risk tolerances

---


---

## 📖 Documentation

### Complete Learning Materials

1. **[Tutorial Documentation](docs/tutorial_documentation.pdf)**
   - Theoretical foundations for each quality dimension
   - Step-by-step methodology guides
   - Visual diagrams and decision frameworks
   - Hands-on exercises with solutions

2. **[Pedagogical Report](docs/pedagogical_report.pdf)**
   - Teaching philosophy and approach
   - Target audience and learning objectives
   - Implementation analysis and design decisions
   - Assessment methods and effectiveness evaluation

3. **[Video Tutorial](https://youtu.be/qFpl28Uu_hw)** (10 minutes)
   - **Segment 1 (Explain)**: Concept introduction and motivation
   - **Segment 2 (Show)**: Live code walkthrough with demonstrations
   - **Segment 3 (Try)**: Guided exercises and extension challenges

### Key Sections in Notebook

- **Section 1**: Introduction - Why data quality matters
- **Section 2**: Setup and data preparation
- **Section 3**: Quality assessment (6 detection functions)
- **Section 4**: Data cleaning solutions
- **Section 5**: Validation (before/after comparison)
- **Section 6**: Real-world applications (Healthcare, E-commerce, IoT)
- **Section 7**: Student practice exercise (Employee dataset)
- **Section 8**: Conclusion and best practices

---

## 🎬 Video Walkthrough

**Watch the complete tutorial:** [https://youtu.be/qFpl28Uu_hw](https://youtu.be/qFpl28Uu_hw)



---

## 🏆 Features & Highlights

### ✨ What Makes This Framework Unique

- **Systematic Approach**: Six-dimension framework provides comprehensive coverage
- **Educational Focus**: Code emphasizes "why" not just "what" through detailed comments
- **Domain Adaptations**: Healthcare, e-commerce, and IoT examples show versatility
- **Validation Rigor**: Quantitative metrics prove cleaning effectiveness
- **Production Ready**: Modular functions suitable for real-world deployment

### 🎯 Innovation Highlights

- **IoT Sensor Example**: Advanced time-series quality concepts (unique among typical tutorials)
- **Missing Data Mechanisms**: Teaches MCAR, MAR, MNAR distinctions
- **Quality Scoring**: Objective metrics for tracking improvement over time
- **Visual Communication**: Heatmaps, box plots, and comparison charts for stakeholders

---

## 🤝 Contributing

This is an educational project, but suggestions for improvements are welcome!

If you find issues or have enhancement ideas:
1. Open an issue describing the problem or suggestion
2. For code contributions, fork the repository and submit a pull request
3. Ensure all code includes educational comments explaining reasoning

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### What This Means

✅ **Free to use** for personal, academic, or commercial purposes  
✅ **Free to modify** and adapt to your specific needs  
✅ **Free to distribute** and share with others  
✅ **Free to build upon** for your own projects  

⚠️ No warranty provided - use at your own risk  
💡 Attribution appreciated but not required  

---

## 📧 Contact

**Sai Shashank Janke**  
📧 Email: janke.s@northeastern.edu  
🎓 Institution: Northeastern University  
📚 Course: INFO 7390 - Advanced Data Science and Architecture

### Questions or Feedback?

- Open an [Issue](https://github.com/YOUR_USERNAME/data-quality-gigo-pipeline/issues) for bugs or feature requests
- Email me directly for academic or professional inquiries
- Connect on [LinkedIn](YOUR_LINKEDIN_URL) for professional networking

---

## 🙏 Acknowledgments

- **Titanic Dataset**: From seaborn library (public domain historical records)
- **Course Faculty**: INFO 7390 instruction and guidance
- **References**: See full bibliography in [Tutorial Documentation](docs/tutorial_documentation.pdf)

### Key Resources

1. McCallum, Q. E. (2012). *Bad Data Handbook*. O'Reilly Media.
2. Olson, J. E. (2003). *Data Quality: The Accuracy Dimension*. Morgan Kaufmann.
3. McKinney, W. (2022). *Python for Data Analysis* (3rd ed.). O'Reilly Media.

---

## 📊 Project Stats

- **Lines of Code**: ~2,500+ (including comments)
- **Documentation**: 24 pages (Tutorial + Pedagogical Report)
- **Functions**: 12 detection + 6 cleaning + 5 validation
- **Examples**: 3 domain-specific scenarios + 1 bonus (IoT)
- **Exercises**: 2 hands-on practice datasets
- **Visualizations**: Heatmaps, box plots, bar charts, comparison plots

---

## ⭐ Support This Project

If you find this tutorial helpful:
- ⭐ **Star this repository** to show your support
- 🔀 **Fork it** to create your own adaptations
- 📢 **Share it** with others learning data science
- 💬 **Provide feedback** to help improve the materials

---

<div align="center">

**Built with ❤️ for data science education**

*Master data quality, and you'll never trust a dataset at face value again.*

</div>
