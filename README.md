import speech_recognition as sr
import pyttsx3

# Initialize the speech engine
engine = pyttsx3.init()

# Function to speak text
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to listen to the user's command
def listen():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        audio = recognizer.listen(source)
        try:
            command = recognizer.recognize_google(audio)
            print(f"You said: {command}")
            return command
        except sr.UnknownValueError:
            print("Sorry, I did not understand that.")
            return ""
        except sr.RequestError:
            print("Could not request results from Google Speech Recognition service.")
            return ""

# Main function to run the AI assistant
def run_jarvis():
    speak("Hello, I am Jarvis. How can I assist you today?")
    while True:
        command = listen().lower()
        if 'exit' in command:
            speak("Goodbye!")
            break
        elif 'your name' in command:
            speak("I am Jarvis, your personal assistant.")
        elif 'time' in command:
            from datetime import datetime
            current_time = datetime.now().strftime("%H:%M")
            speak(f"The current time is {current_time}.")
        else:
            speak("I am not sure how to help with that.")

if __name__ == "__main__":
    run_jarvis()

