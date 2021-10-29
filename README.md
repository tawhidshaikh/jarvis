import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
from flask import Flask

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
            if 'alexa' in command:
                command = command.replace('alexa', '')
                print(command)
    except:
        pass
    return command


def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing ' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who is' in command:
        person = command.replace('who is', '')
        info = wikipedia.summary(person, 1)
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
    elif 'date' in command:
        talk('sorry, I have a headache')
    elif 'are you single' in command:
        talk('I am in a relationship with wifi')
    else:
        talk('Please say the command again.')


while True:
    run_alexa()
