from sklearn.tree import DecisionTreeClassifier
import numpy as np

# Example dataset (Symptoms data)
X_train = np.array([
    [1, 1, 1, 0, 1, 1, 1, 1, 0],  # Flu
    [1, 1, 1, 1, 1, 0, 0, 1, 0],  # Pneumonia
    [1, 1, 0, 0, 1, 1, 0, 1, 0],  # Common Cold
    [1, 1, 1, 0, 1, 1, 1, 1, 1],  # COVID-19
    [1, 0, 1, 1, 1, 1, 0, 1, 0],  # Tuberculosis
    [0, 1, 0, 0, 1, 1, 0, 1, 0],  # Strep Throat
    [1, 1, 1, 0, 1, 0, 0, 1, 0],  # Bronchitis
    [1, 1, 1, 0, 1, 0, 1, 0, 1]   # Malaria
])

# Target variable (diseases)
y_train = ['Flu', 'Pneumonia', 'Common Cold', 'COVID-19', 'Tuberculosis', 'Strep Throat', 'Bronchitis', 'Malaria']

# Train a Decision Tree Classifier
model = DecisionTreeClassifier()
model.fit(X_train, y_train)

# Function to predict disease
def predict_disease(symptoms):
    prediction = model.predict([symptoms])
    return prediction[0]

# Medicine Suggestions for Non-Serious Diseases
def suggest_medicine(disease):
    medicines = {
        'Common Cold': [
            'Paracetamol (for fever and pain)',
            'Decongestants (for nasal congestion)',
            'Vitamin C (boosts immunity)',
            'Honey and Ginger (soothing sore throat)'
        ],
        'Flu': [
            'Oseltamivir (Tamiflu) - if caught early',
            'Paracetamol (for fever)',
            'Vitamin C (for immune support)'
        ],
        'Bronchitis': [
            'Cough Syrup (Expectorants)',
            'Paracetamol (for fever)',
            'Warm fluids (soothing the throat)'
        ]
    }
    if disease in medicines:
        return medicines[disease]
    return None

# Chatbot Function
def healthcare_chatbot():
    print("Welcome to the Healthcare Chatbot!")
    print("Please answer the following questions to help predict your disease.")
    
    symptoms = []
    
    # Ask about symptoms
    symptoms.append(int(input("Do you have a fever? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have a cough? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have shortness of breath? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have chest pain? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Are you feeling fatigued? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have a sore throat? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have muscle aches? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have a headache? (1 for Yes, 0 for No): ")))
    symptoms.append(int(input("Do you have nausea or vomiting? (1 for Yes, 0 for No): ")))
    
    # Predict the disease
    disease = predict_disease(symptoms)
    
    print(f"Based on your symptoms, you might have: {disease}")
    
    # Suggest seeing a doctor for serious diseases
    serious_diseases = ['Pneumonia', 'COVID-19', 'Tuberculosis', 'Malaria']
    if disease in serious_diseases:
        print("We recommend visiting a doctor immediately for a proper diagnosis.")
    else:
        print("For instant relief, you can try the following medicines:")
        medicines = suggest_medicine(disease)
        if medicines:
            for medicine in medicines:
                print(f"- {medicine}")
        else:
            print("No medicine suggestions available for this disease. Please consult a healthcare professional.")

# Run the chatbot
if __name__ == "__main__":
    healthcare_chatbot()

