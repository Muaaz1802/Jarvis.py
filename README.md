import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia
import webbrowser
import os
from PIL import ImageGrab

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
# print(voices[0].id)
engine.setProperty('voice', voices[0].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour >= 0 and hour < 12:
        speak("Good morning!")

    elif hour >= 12 and hour < 18:
        speak("Good Afternoon!")

    else:
        speak("Good Evening!")

    speak("I am Jarvis, I am your assistant, How can I help you.")


def takeCommand():
    # It Takes the command from the user and returns string output!

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"You: {query}\n")

    except Exception as e:
        # print(e)
        print("Sorry! I didn't recognise you. Say it again please!")
        speak("Sorry! I didn't recognise you. Say it again please!")
        return "None"
    return query

def takeSS():
    image = ImageGrab.grab()
    image.show()

if __name__ == "__main__":
    wishMe()

    while True:
        query = takeCommand().lower()

        # Logic for executing tasks based on query
        if 'wikipedia' in query:  # if wikipedia found in the query then this block will be executed
            # Asking info about wikipedia!
            speak('Searching Wikipedia. . . ')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to Wikipedia")
            print(results)
            speak(results)

        elif 'open wikipedia' in query:
            speak("Opening wikipedia")
            webbrowser.open("https://en.wikipedia.org/wiki/Main_Page")

        elif 'who are you' in query:  # Asking about assistant
            speak("I am Jarvis, how may I help you.")

        elif 'open youtube' in query:  # command for opening youtube
            speak("Opening youtube")
            webbrowser.open("youtube.com")

        elif 'open google' in query:  # command for opening google
            speak("Opening Google")
            webbrowser.open("google.com")

        elif 'open stackoverflow' in query:  # command for opening stackoverflow
            speak("Opening Stackoverflow")
            webbrowser.open("stackoverflow.com")

        elif 'open google meet' in query:  # command for opening google meet
            speak("Opening Google Meet")
            webbrowser.open("meet.google.com")

        elif 'play music' in query: # # command for playing music
            music_dir = 'Add your music dir path here'
            songs = os.listdir(music_dir) 
            speak("Playing music")
            print(songs)
            os.startfile(os.path.join(music_dir, songs))

        elif 'the time' in query: # command for knowing time 
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Sir, the time is {strTime}")

        elif 'open code' in query: # command for vscode
            codePath = "Add your vs code path"
            speak("Opening VS code")
            os.startfile(codePath)

        elif 'open discord' in query: # command for opening discord
            discordPath = "add your discord path"
            speak("Opening discord")
            os.startfile(discordPath)

        elif 'open whatsapp' in query: # command for opening whatsapp
            whatsAppPath = "add your whatsapp path"
            speak("Opening whatsapp")
            os.startfile(whatsAppPath)

        elif 'open telegram' in query: # command for opening telegram
            telegramPath = "add your telegram path"
            speak("Opening telegram")
            os.startfile(telegramPath)

        elif 'open zoom' in query: # command for opening zoom
            zoomPath = "add your zoom path"
            speak("Opening Zoom")
            os.startfile(zoomPath)

        elif 'open chrome' in query: # command for opening chrome
            chromePath = "add your chrome path"
            speak("Opening chrome")
            os.startfile(chromePath)    

        elif 'take screenshot' in query:
            takeSS()

        elif 'javris quit' in query: # command for quiting the program
            speak("Good bye!")
            exit()
