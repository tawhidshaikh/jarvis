import pyttsx3
import speech_recognition as sr
import wikipedia

listener = sr.Recognizer()
engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)


def talk(text):
     engine.say(text)
     engine.runAndWait()


def take_command():
   try:
      with sr.Microphone() as source:
        print('listening...')
        voice = listener.listen(source)
        command = listener.recognize_google(voice)
        command = command.lower()
        if 'jarvis' in command:
            command = command.replace('jarvis', '')
            print(command)
   except:
      pass
   return command


def run_jarvis():
    command = take_command()
    print(command)
    if 'who' in command():
        person = command.replace('who', '')
        info = wikipedia.summary(person, 2)
        print(info)
        talk(info)
    elif 'where' in command():
        place = command.replace('where', '')
        info = wikipedia.summary(place, 2)
        print(info)
        talk(info)
    elif 'what' in command():
        thing = command.replace('what', '')
        info = wikipedia.summary(thing, 2)
        print(info)
        talk(info)
    elif 'when' in command():
        time = command.replace('when', '')
        info = wikipedia.summary(time, 2)
        print(info)
        talk(info)
    elif 'how' in command():
        event = command.replace('how', '')
        info = wikipedia.summary(event, 2)
        print(info)
        talk(info)

while True:
    run_jarvis()
