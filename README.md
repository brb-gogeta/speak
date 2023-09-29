import pyttsx3
from selenium import webdriver
from selenium.webdriver.support.ui import Select
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from time import sleep

def speak(text):
    engine = pyttsx3.init("sapi5")
    voices = engine.getProperty('voices')
    engine.setProperty('voice', voices[0].id)
    engine.setProperty('rate', 170)
    print("")
    print(f"You : {text}.")
    print("")
    engine.say(text)
    engine.runAndWait()

chrome_options = Options()
chrome_options.add_argument('--log-level=3')
chrome_options.headless = True
Path = "jarvis advance/Database/chromedriver.exe" 
driver = webdriver.Chrome(executable_path=Path, options=chrome_options)
driver.maximize_window()

website = r"https://ttsmp3.com/text-to-speech/British%20English"
driver.get(website)
ButtonSelection = Select(driver.find_element(by=By.XPATH, value='/html/body/div[4]/div[2]/form/select'))
ButtonSelection.select_by_visible_text('British English / Brian')

def speak(text):
    Lengthoftext = len(str(text))
    
    if Lengthoftext == 0:
        pass
    else:
        print("")
        print(f"AI : {text}.")
        print("")
        Data = str(text)
        xpathofsec = 'html/body/div[4]/div[2]/form/textarea'
        driver.find_element(By.XPATH, value=xpathofsec).send_keys(Data)
        driver.find_element(By.XPATH, value='//*[@id="vorlesenbutton"]').click()
        driver.find_element(By.XPATH, value="html/body/div[4]/div[2]/form/textarea")
        
        if Lengthoftext >= 30:
            sleep(4)
        elif Lengthoftext >= 40:
            sleep(6)
        elif Lengthoftext >= 55:
            sleep(8)
        elif Lengthoftext >= 70:
            sleep(10)
        elif Lengthoftext >= 100:
            sleep(13)
        elif Lengthoftext >= 120:
            sleep(14)
        else:
            sleep(2)

def TranslationEngToFr(Text):
    line = str(Text)
    translate = Translator()
    result = translate.translate(line, src='en', dest='fr')
    data = result.text
    print(f"Assistant : {data}.")
    return data

def Speak(text):
    engine = pyttsx3.init()
    engine.setProperty('rate', 150)
    engine.say(text)
    engine.runAndWait()

def Assistant():
    while True:
        print("You can start speaking now (in Hindi or English), or type 'exit' to quit.")
        query = MicExecution()
        
        if 'exit' in query:
            print("Assistant: Goodbye!")
            break
        
        if query:
            print(f"You: {query}")
            print("Translating to English...")
            translated_query = TranslationHinToEng(query)
            print(f"You (English): {translated_query}")

if __name__ == "__main__":
    input("Appuyez sur Entrée pour démarrer l'assistant...")
    speak("Hello Jarvis")
    Assistant()

    driver.quit()

