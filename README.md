Reference Guide
import plotly.graph_objects as go

# Define nursing guide data with all topics
data = {
    "Topic": [
        "Lab Value Reference Ranges", 
        "Common Medications", 
        "Medication Therapeutic Ranges", 
        "IV Gauge Sizes and Colors", 
        "Types of IV Fluids and Their Uses",
        "Vital Signs",
        "Disease Management",
        "EKG Interpretation",
        "ABG Interpretation"
    ],
    "Information": [
        # Lab Value Reference Ranges
        [
            ["WBC", "4,500 - 11,000 cells/mcL"],
            ["RBC", "4.7 - 6.1 million cells/mcL (men), 4.2 - 5.4 million cells/mcL (women)"],
            ["Hemoglobin", "13.8 - 17.2 g/dL (men), 12.1 - 15.1 g/dL (women)"],
            ["Hematocrit", "40.7% - 50.3% (men), 36.1% - 44.3% (women)"],
            ["Platelets", "150,000 - 450,000 platelets/mcL"],
            ["Sodium", "135 - 145 mEq/L"],
            ["Potassium", "3.5 - 5.0 mEq/L"],
            ["Chloride", "98 - 106 mEq/L"],
            ["Calcium", "8.5 - 10.2 mg/dL"],
            ["Glucose", "70 - 110 mg/dL (fasting)"]
        ],
        
        # Common Medications
        [
            ["Aspirin", "Anti-inflammatory, pain relief, antiplatelet"],
            ["Lisinopril", "Antihypertensive, ACE inhibitor"],
            ["Metformin", "Controls blood sugar in type 2 diabetes"],
            ["Omeprazole", "Proton pump inhibitor, reduces stomach acid"],
            ["Albuterol", "Bronchodilator, used for asthma and COPD"]
        ],
        
        # Medication Therapeutic Ranges
        [
            ["Digoxin", "0.5 - 2.0 ng/mL"],
            ["Lithium", "0.6 - 1.2 mmol/L"],
            ["Phenytoin", "10 - 20 mcg/mL"],
            ["Vancomycin", "10 - 20 mcg/mL (trough level)"],
            ["Theophylline", "5 - 15 mcg/mL"]
        ],
        
        # IV Gauge Sizes and Colors
        [
            ["18 Gauge", "Green - commonly used for blood transfusions and surgeries"],
            ["20 Gauge", "Pink - standard gauge for most IV fluids and medications"],
            ["22 Gauge", "Blue - suitable for pediatric and elderly patients"],
            ["24 Gauge", "Yellow - often used for very fragile veins"],
            ["16 Gauge", "Gray - used for trauma and rapid fluid replacement"]
        ],
        
        # Types of IV Fluids and Their Uses
        [
            ["Normal Saline (0.9% NaCl)", "Isotonic - used for dehydration, shock, and resuscitation"],
            ["Lactated Ringers", "Isotonic - used in surgery, trauma, and burn patients"],
            ["D5W (5% Dextrose in Water)", "Isotonic in bag, hypotonic in body - used for hypoglycemia, dehydration"],
            ["0.45% Sodium Chloride (Half NS)", "Hypotonic - used for cellular dehydration"],
            ["D10W (10% Dextrose in Water)", "Hypertonic - used for severe hypoglycemia"]
        ],
        
        # Vital Signs
        [
            ["Temperature", "Normal range: 36.1-37.2°C (97-99°F)"],
            ["Pulse", "60-100 bpm for adults"],
            ["Respirations", "12-20 breaths per minute for adults"],
            ["Blood Pressure", "Normal <120/80 mmHg"],
            ["Pain Assessment", "Use a standardized pain scale (0-10)"]
        ],
        
        # Disease Management
        [
            ["Diabetes", "Monitor blood glucose, administer insulin, educate on diet"],
            ["Hypertension", "Monitor BP, lifestyle changes, give antihypertensives"],
            ["Heart Failure", "Assess for edema, monitor weights, educate on sodium restriction"],
            ["COPD", "Breathing exercises, oxygen therapy, avoid respiratory irritants"],
            ["Asthma", "Use bronchodilators, assess triggers, educate on inhaler use"]
        ],
        
        # EKG Interpretation
        [
            ["Normal Sinus Rhythm", "Regular rhythm with rate of 60-100 bpm"],
            ["Atrial Fibrillation", "Irregularly irregular rhythm, absence of P waves"],
            ["Ventricular Tachycardia", "Wide QRS complexes, rapid heart rate >100 bpm"],
            ["Ventricular Fibrillation", "Chaotic electrical activity, no discernible QRS complexes"],
            ["Asystole", "Flatline, absence of electrical activity"]
        ],
        
        # ABG Interpretation
        [
            ["pH", "Normal range: 7.35 - 7.45"],
            ["PaCO2", "Normal range: 35 - 45 mmHg (respiratory parameter)"],
            ["HCO3", "Normal range: 22 - 26 mEq/L (metabolic parameter)"],
            ["Respiratory Acidosis", "pH < 7.35, PaCO2 > 45 mmHg"],
            ["Metabolic Alkalosis", "pH > 7.45, HCO3 > 26 mEq/L"]
        ]
    ]
}

# Create table traces for each topic
table_traces = []
for i, topic in enumerate(data["Topic"]):
    table_traces.append(
        go.Table(
            header=dict(
                values=["Category", "Details"],
                fill_color="lightblue",
                align="left"
            ),
            cells=dict(
                values=[[row[0] for row in data["Information"][i]], [row[1] for row in data["Information"][i]]],
                fill_color="lavender",
                align="left"
            ),
            visible=(i == 0)  # Only the first topic is visible initially
        )
    )

# Create figure with all table traces
fig = go.Figure(data=table_traces)

# Add dropdown menu to control topic visibility
fig.update_layout(
    updatemenus=[
        {
            "buttons": [
                {
                    "label": topic,
                    "method": "update",
                    "args": [
                        {"visible": [j == i for j in range(len(data["Topic"]))]},  # Show only selected topic's table
                        {"title": f"Nursing Guide: {topic}"}
                    ]
                }
                for i, topic in enumerate(data["Topic"])
            ],
            "direction": "down",
            "showactive": True,
        }
    ],
    title="Comprehensive Nursing Student Interactive Guide",
)

fig.show()
