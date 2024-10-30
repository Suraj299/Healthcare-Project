# Healthcare-Project

import speech_recognition as sr
import time

def get_voice_input(question, retries=3):
    recognizer = sr.Recognizer()
    
    # Configure energy threshold for better noise filtering
    recognizer.energy_threshold = 4000  # Higher threshold to ignore low background noise

    with sr.Microphone() as source:
        print(question)
        recognizer.adjust_for_ambient_noise(source, duration=2)  # More time to adjust noise
        
        for attempt in range(retries):
            print("Listening... Please speak clearly.")
            try:
                # Listen with a timeout to prevent hanging
                audio = recognizer.listen(source, timeout=6, phrase_time_limit=10)
                text = recognizer.recognize_google(audio)
                print(f"You said: {text}\n")
                return text
            except sr.UnknownValueError:
                print(f"Attempt {attempt + 1}/{retries}: Could not understand, please try again.")
            except sr.RequestError:
                print("Speech service is unavailable. Check your internet connection.")
                return ""
        
        # If all retries fail
        print("Sorry, I couldn't capture that. Moving to the next question.\n")
        return ""

def healthcare_form():
    print("\n--- Voice-Enabled Healthcare Form ---")
    
    # Voice-based questions
    name = get_voice_input("What is the patient's name?")
    age = get_voice_input("What is the patient's age?")
    gender = get_voice_input("What is the patient's gender?")
    contact_number = get_voice_input("What is the patient's contact number?")
    symptoms = get_voice_input("What symptoms does the patient have?")
    duration = get_voice_input("How long has the patient had these symptoms?")
    medication = get_voice_input("Is the patient taking any medications?")
    follow_up = get_voice_input("When is the follow-up appointment?")

    # Display collected information
    print("\n--- Form Summary ---")
    print(f"Name: {name}")
    print(f"Gender: {gender}")
    print(f"Contact Number: {contact_number}")
    print(f"Symptoms: {symptoms}")
    print(f"Duration: {duration}")
    print(f"Medications: {medication}")
    print(f"Follow-up Appointment: {follow_up}")

if __name__ == "__main__":
    print("Starting the healthcare form... Ensure you are in a quiet environment if possible.")
    time.sleep(2)  # Small delay to let the user prepare
    healthcare_form()
