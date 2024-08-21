import speech_recognition as sr
import pyttsx3 # type: ignore #type = ignore


# Initialize the text-to-speech engine
engine = pyttsx3.init()

def speak(text):
    """Convert the text to speech."""
    engine.say(text)
    engine.runAndWait()

def listen():
    """Listen for speech and return the recognized text."""
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        audio = recognizer.listen(source)
        try:
            command = recognizer.recognize_google(audio)
            print(f"You said: {command}")
            return command.lower()
        except sr.UnknownValueError:
            speak("Sorry, I didn't understand that.")
            return None
        except sr.RequestError:
            speak("Sorry, there was an issue with the speech recognition service.")
            return None

def process_command(command):
    """Process the recognized command."""
    if 'hello' in command or 'hi' in command:
        speak("Hello! How can I help you today?")
    elif 'search' in command:
        query = command.replace('search', '').strip()
        if query:
            speak(f"Searching for {query}")
            for result in 'search' (query, num_results=1):
                speak(f"I found this: {result}")
                break
        else:
            speak("Please provide a search query.")
    elif 'stop' in command:
        speak("Goodbye!")
        return False
    else:
        speak("Sorry, I didn't understand that command.")
    return True

def main():
    """Main function to run the virtual assistant."""
    speak("Hello! I am your virtual assistant. How can I help you?")
    while True:
        command = listen()
        if command:
            should_continue = process_command(command)
            if not should_continue:
                break

if __name__ == "__main__":
    main()





