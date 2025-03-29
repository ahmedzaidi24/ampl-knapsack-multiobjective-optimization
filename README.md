# Grocery Planning with AMPL: Knapsack-Based Multi-Objective Optimization

## 🧠 Overview
This repository presents a series of **AMPL models** for solving a multi-stage **knapsack problem** rooted in a real-world grocery shopping scenario. Built for the **MATH5007 – Simulation & Optimization** unit at Curtin University, the project explores weight, volume, and quantity-based constraints across multiple bag configurations. It culminates in a **multi-objective optimization (MOO)** model to balance value maximization and item count.

---

## 🛒 Scenario
You're planning a bike-based grocery trip with limited carrying capacity. Each product has:
- A **value** (utility/priority)
- A **weight** (kg)
- Optionally, a **volume** (VU)

You must decide what to carry, how many of each item, and across how many bags — all while trying to get the **most value** and **most items**.

---

## 📈 Optimization Objectives
### 📍 Core Objectives
- **Activity 1**: Maximize the number of items (subject to total weight ≤ 3.5kg)
- **Activity 2**: Maximize total value instead of quantity
- **Activity 3**: Expand to **2 or more bags** with capacity restrictions
- **Activity 4**: Add **volume** as a new constraint (shopping_3.dat)
- **Activity 5**: Allow up to **2 of each item**

### 🎯 Multi-Objective Optimization (Activity 6)
- Formulated a combined weighted objective:  
  `maximize z_combined = weighted sum of value and item count`
- Introduced deviation constraint `Q` to find trade-offs between value and quantity:
```ampl
maximize z_combined {k in OBJ}: sum {j in 1..nrbags , i in OBJECTS} values[i,k] * x[j,i];
minimize z : Q;
s.t. c_dev {k in OBJ}:
  weights[k] * ((targets[k] - sum {j in 1..nrbags, i in OBJECTS} values[i,k] * x[j,i]) / targets[k]) <= Q;
```

---

## 🧮 Results & Interpretations
| Activity | Description | Bags | Capacity | Result |
|---------|-------------|------|----------|--------|
| 1       | Maximize items         | 1    | 3.5kg     | Predicted 3–4 items            |
| 2       | Maximize value         | 1    | 3.5kg     | Achieved 328 value, 15 items   |
| 3       | Two bags               | 2    | 3.5kg x 2 | More variety and higher value |
| 4       | 4 bags, half capacity  | 4    | 1.75kg    | Increased product coverage     |
| 5       | Weight + Volume limit  | 2    | 3.5kg, 15VU | Reduced flexibility        |
| 6       | Multi-objective        | 2    | Mixed     | 16 items, value ~317–328      |

Weight tweaking of value objective between **13 and 34** produced the sweet spot of **16 items** in the multi-objective case.

---

## 📂 Files Included
| File | Description |
|------|-------------|
| `a3_20972008_answers.docx` | Full model answers with code, logic, and rationale |
| `Knapsack Worksheet.pdf` | Scenario and prompt outline |
| `shopping_1.dat` | Base dataset (not shown here) |
| `shopping_2.dat` | For multi-bag scenario |
| `shopping_3.dat` | Includes volume data |
| `shopping_moo.mod` | AMPL model for multi-objective optimization |
| `*.mod / *.dat` | Supporting model/data files as per naming conventions |

---

## 🛠 Tools Used
- **AMPL** – Algebraic Modeling Language
- **Knapsack Optimization**, **Multi-Objective Optimization**
- Weight/volume constraints, custom datasets, deviation functions

---

## 👤 Author
**Syed Muhammad Ahmed Zaidi**  
Curtin University – MATH5007 (Simulation & Optimization)  
Student ID: 20972008

---

## 📄 License
Academic use only. For reuse in industry or commercial settings, please contact the author.

---

## 🚀 Status
✅ Fully solved, modeled, and tested | 🧠 Multi-objective strategies explored | 💼 AMPL implementation complete
