# Healthcare-Project

import speech_recognition as sr

def get_voice_input(prompt_text="Please say something..."):
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print(prompt_text)
        recognizer.adjust_for_ambient_noise(source)  # Handle background noise
        audio = recognizer.listen(source)

    try:
        text = recognizer.recognize_google(audio)
        print(f"Recognized: {text}")
        return text
    except sr.UnknownValueError:
        print("Sorry, I could not understand the audio.")
        return ""
    except sr.RequestError as e:
        print(f"Could not request results; {e}")
        return ""

def fill_healthcare_form():
    print("Filling out Healthcare Form with Voice Input...\n")
    
    # Collecting patient details using voice
    name = get_voice_input("What is the patient's name?")
    age = get_voice_input("What is the patient's age?")
    symptoms = get_voice_input("Please describe the symptoms.")
    diagnosis = get_voice_input("What is the diagnosis?")
    medication = get_voice_input("What medications have been prescribed?")

    # Displaying the collected data
    print("\nHealthcare Form Summary:")
    print(f"Patient Name: {name}")
    print(f"Age: {age}")
    print(f"Symptoms: {symptoms}")
    print(f"Diagnosis: {diagnosis}")
    print(f"Medication: {medication}")

if __name__ == "__main__":
    fill_healthcare_form()
