# Voice-Assistant-Linux-Docker-Control

# About the Project -

This project implements a voice-controlled personal assistant using Python. The assistant performs various tasks, interacts with users through voice commands, accesses web services, and executes system commands based on user input.

![](/voice_assistant_images/home_page.png)

Simplify your daily tasks with this voice assistant and get started with great ease.

# What is Python ?

Python is a high-level, interpreted programming language recognized for its simplicity and readability. Its clean syntax and ease of learning make it a popular choice for a wide range of applications, from web development using frameworks like Django and Flask, to data analysis and machine learning with libraries such as Pandas, NumPy, TensorFlow, and PyTorch. Python's versatility extends to scripting, automation, and scientific computing. Its cross-platform compatibility, extensive standard library, and vibrant community contribute to its widespread adoption among beginners and seasoned developers alike.

# What is Linux ?


Linux is an open-source operating system kernel initially developed by Linus Torvalds in 1991. It's the core component of various Unix-like operating systems known as Linux distributions (distros). Linux is highly customizable and used across a broad spectrum of devices, from servers and supercomputers to embedded systems and smartphones (Android is built on a modified Linux kernel). It's characterized by its stability, security, and the freedom it offers users to modify, distribute, and improve the software. Linux provides a command-line interface along with graphical user interfaces through desktop environments, making it a versatile choice for both tech enthusiasts and professionals.

---

# Features

- __Voice Interaction:__ Utilizes speech recognition and text-to-speech capabilities to interact with users.  
- __Web Browsing:__ Opens web browsers for popular platforms like YouTube, Google, Gmail, Netflix, Prime Video, and fetches news and COVID-19 statistics.  
- __Software Execution:__ Launches common software applications like Notepad, Calculator, Paint, Chrome, File Explorer, and more.  
- __System Utilities:__ Executes system commands for Linux-based environments (e.g., Docker operations, date, calendar, file listing).

# Requirements

Python 3.x  
__Libraries:__ pyttsx3, tkinter, subprocess, speech_recognition, wikipedia, datetime, pyjokes, cv2, pynput, PIL, webbrowser, geopy, paramiko (for SSH), among others.

# Setup Instructions

- __Python Installation:__ Install Python 3.x on your system.
Library Installation: Install necessary libraries using pip. For example: pip install pyttsx3.  
- __System Configuration:__ Ensure proper configurations for microphone access and required software installations.
Environment Preparation: Set up the necessary software environments (Linux) if using Linux-based commands.  
- __Run the Program:__ Execute the main Python file.



---

# Code

        import os
        import pyttsx3
        import tkinter as tk
        import subprocess
        import time 
        import speech_recognition as sr    
        import wikipedia
        import datetime
        import pyjokes 
        import cv2
        from pynput.keyboard import Controller
        keyboard = Controller()
        from PIL import Image, ImageDraw
        import webbrowser
        from tkinter import PhotoImage, Button
        from tkinter import simpledialog
        from geopy.geocoders import Nominatim
        from tkinter import messagebox
        import paramiko


This code snippet imports several Python libraries and modules. Here's a breakdown of each import:

- __os:__ Provides functions for interacting with the operating system, enabling operations like file and directory manipulation.

- __pyttsx3:__ A text-to-speech conversion library that allows the program to convert text into speech.

- __tkinter (as tk):__ A standard GUI (Graphical User Interface) toolkit for Python, used for creating and managing graphical interfaces.

- __subprocess:__ Enables the creation of new processes, allowing interaction with system commands and pipelines.

- __time:__ Offers various time-related functions, such as sleep to pause program execution for a specified duration.

- __speech_recognition (as sr):__ Allows the program to recognize speech input from the microphone and perform actions based on the recognized speech.

- __wikipedia:__ Provides an interface to access Wikipedia content, allowing the program to retrieve information from Wikipedia articles.

- __datetime:__ Offers classes for manipulating dates and times in Python.

- __pyjokes:__ A library used to generate random jokes, allowing the program to display jokes dynamically.

- __cv2:__ Refers to OpenCV, a computer vision library primarily used for image and video processing.

- __pynput.keyboard:__ Specifically imports the Controller class from the pynput library, enabling simulation of keyboard inputs.

- __PIL (Python Imaging Library):__ Contains various modules for image processing, including Image and ImageDraw for creating and manipulating images.

- __webbrowser:__ Allows the program to open web browsers and display web-based content.

- __PhotoImage, Button (from tkinter):__ Additional elements from tkinter used for working with images and creating buttons in the GUI.

- __simpledialog, messagebox:__ Additional tkinter modules for creating dialog boxes and handling user interactions.

- __geopy.geocoders (Nominatim):__ A geocoding library used to convert addresses into geographical coordinates and vice versa, here specifically importing the Nominatim class.

- __paramiko:__ A module enabling SSH connectivity and secure file transfers, often used for remote operations and automation through SSH (Secure Shell) connections.

These imports encompass a range of functionalities, from graphical interface creation to speech recognition, image processing, web browsing, and remote connectivity, providing a comprehensive set of tools for diverse application development.

__code:__

        def speak(text):
            engine.say(text)
            print(text)
            engine.runAndWait() 

This code defines a function called speak that takes in a text parameter. Within this function:

- __engine.say(text)__ - This line uses a text-to-speech engine to convert the provided text into speech.
- __print(text)__ - This line prints the provided text to the console.
- __engine.runAndWait()__ - This command runs the speech engine to say the provided text and waits for the speech to complete before proceeding with the program's execution.  

__code:__

        def establish_ssh_connection(name, ip, username, password, cmd):
            try:
                ssh_client = paramiko.SSHClient()
                ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())  
                ssh_client.connect(hostname=ip, username=username, password=password)  
                print(cmd)
                stdin, stdout, stderr = ssh_client.exec_command(cmd)

                output = stdout.read().decode()
                print(output)
                status_label.config(text=output)
                ssh_client.close()
                return True
            except Exception as e:
                print("Error:", e)
                status_label.config(text=f"Error: {e}")
                return False
 
The `establish_ssh_connection` function attempts to create an SSH connection to a remote server using Python's `paramiko` library. It starts by setting up an SSH client, configuring the policy for host key management, and then tries to connect to the specified server using the provided credentials (IP address, username, password). Once connected, it executes a command on the remote server and captures the output. This function is equipped to handle exceptions that might occur during the connection or command execution and provides feedback through console logs or by updating a status label with the output or error messages. If successful, it returns `True`; otherwise, if an error occurs, it returns `False`.

__code:__

        def wishMe():
            hour=datetime.datetime.now().hour
            if hour >= 0 and hour < 12:
                speak("Hello,Good Morning")
            elif hour >= 12 and hour < 18:
                speak("Hello,Good Afternoon")
            else:
                speak("Hello,Good Evening")


The `wishMe()` function greets the user based on the current time of the day. It uses the `datetime` module to retrieve the current hour. Depending on the hour, it uses the `speak()` function to vocalize an appropriate greeting: `"Good Morning"` if the time is between 00:00 to 11:59, `"Good Afternoon"` if it's between 12:00 to 17:59, and `"Good Evening"` for any later hours.

__code:__

        def get_audio(): 
           r = sr.Recognizer() 
           audio = '' 
           with sr.Microphone() as source: 
               print("Listening") 
               audio = r.listen(source, phrase_time_limit = 3) 
               print("Stop.") 
           try: 
              text = r.recognize_google(audio, language ='en-US') 
               print('You: ' + text)
               return text
          except:
               return "Error Recognizing Voice. Try speaking    clearly and in a  quieter place."

This `get_audio()` function captures audio input from the microphone using the SpeechRecognition library (`sr`). It initializes a Recognizer instance `r`, creates an empty string `audio`, and opens the microphone as the source. While it listens, it prints "Listening" and waits for up to 3 seconds (`phrase_time_limit`) for speech input. Once the listening stops, it attempts to recognize the speech using Google's speech recognition service (`r.recognize_google()`), specifying the language as English (United States). If it successfully recognizes the speech, it prints the recognized text and returns it. If there's an issue or if no speech is recognized, it returns an error message suggesting speaking clearly and in a quieter environment.

__code:__

        def note(text):
            date = datetime.datetime.now()
            file_name = str(date).replace(":", "-") + "-note.txt"

           with open(file_name, "w") as f:
               f.write(text)
            subprocess.run(["notepad", file_name],      capture_output=True)

This `note()` function takes text input as an argument and creates a note with that text content. It generates a filename based on the current date and time, replacing colons (which aren't allowed in filenames) with hyphens, and appending "-note.txt" to create a file name string. 

Then, it opens a file with that name in write mode, writes the provided text into the file, and closes it. Finally, it utilizes `subprocess.run()` to open the default text editor (Notepad on Windows) with the newly created note file. This function essentially creates a text file with the given text content and opens it for viewing/editing.

__code:__



        def date():
            now = datetime.datetime.now()
            month_name = now.month
            day_name = now.day
            month_names = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
            ordinalnames = [ '1st', '2nd', '3rd', ' 4th', '5th', '6th', '7th', '8th', '9th', '10th', '11th', '12th', '13th', '14th', '15th', '16th', '17th', '18th', '19th', '20th', '21st', '22nd', '23rd','24rd', '25th', '26th', '27th', '28th', '29th', '30th', '31st'] 
            speak("Today is "+ month_names[month_name-1] +" " + ordinalnames[day_name-1] + '.')
  
  The `date()` function retrieves the current date and formats it to be spoken aloud. It uses the `datetime` module to get the current date and extracts the month and day information. The month is converted into its respective name (from a list of month names) and the day into its ordinal format (like "1st", "2nd", "3rd", etc.). Finally, using the `speak()` function, it announces the formatted date, stating the month name and day in a human-readable way.

  __code:__

        def Process_audio():

            run = 1
            if __name__=='__main__':
                while run==1:

                    statement = get_audio().lower()
                    results = ''
                    run +=1

                    if "hello" in statement or "hi" in statement:
                        wishMe()     
        
            
                    elif "good bye" in statement or "ok bye" in statement or "bye"      in statement:
                        speak('Your personal assistant is shutting down, Good bye')
                        root.destroy()


                    elif 'wikipedia' in statement:
                        try:
                            speak('Searching Wikipedia...')
                            statement = statement.replace("wikipedia", "")
                            results = wikipedia.summary(statement, sentences = 3)
                            speak("According to Wikipedia")
                            wikipedia_screen(results)
                        except:
                            speak("Error")



                    elif 'joke' in statement:
                        speak(pyjokes.get_joke()) 
 
     
                    elif 'open youtube' in statement:
                        webbrowser.open_new_tab("https://www.youtube.com")
                        speak("youtube is open now")
                        time.sleep(5)



                    elif 'open google' in statement:
                     webbrowser.open_new_tab("https://www.google.com")
                        speak("Google chrome is open now")
                        time.sleep(5)



                    elif 'open gmail' in statement:
                        webbrowser.open_new_tab("mail.google.com")
                        speak("Google Mail open now")
                        time.sleep(5)


                    elif 'open netflix' in statement:
                        webbrowser.open_new_tab("netflix.com/browse") 
                        speak("Netflix open now")



                    elif 'open prime video' in statement:
                        webbrowser.open_new_tab("primevideo.com") 
                        speak("Amazon Prime Video open now")
                        time.sleep(5)

                       

                    elif 'news' in statement:
                     news = webbrowser.open_new_tab("https://timesofindia.indiatimes.com/city/agra")
                        speak('Here are some headlines from the Times of India, Happy reading')
                        time.sleep(6)

                 elif 'cricket' in statement:
                        news = webbrowser.open_new_tab("cricbuzz.com")
                        speak('This is live news from cricbuzz')
                        time.sleep(6)


                    elif 'corona' in statement:
                       news = webbrowser.open_new_tab("https://www.worldometers.info/coronavirus/")
                        speak('Here are the latest covid-19 numbers')
                        time.sleep(6)


                    elif 'time' in statement:
                        strTime=datetime.datetime.now().strftime("%H:%M:%S")
                        speak(f"the time is {strTime}")


                    elif 'date' in statement:
                        date()
         

                 elif 'who are you' in statement or 'what can you do' in statement:
                        speak('I am your personal Voice assistant. I am programmed to perform minor tasks on Windows and Linux')



                    elif "who made you" in statement or "who created you" in statement or "who discovered you" in statement:
                        speak("I was built by Engineer Harsh Pandey")


            
                 elif 'make a note' in statement:
                        statement = statement.replace("make a note", "")
                        note(statement)
      

                    elif 'note this' in statement:    
                       statement = statement.replace("note this", "")
                       note(statement)   
      

                    elif 'open' or 'execute' or 'start' or 'run' in statement:
                       for software_name in software_path:
                            if software_name in statement:
                                speak(f" {software_name} is opening now")
                                open_software(software_path[software_name])
       
                        else:
                            status_label.config(text="Software not found.")

                    speak(results)


The `Process_audio()` function listens for voice commands continuously and executes various actions based on the recognized commands. It utilizes speech recognition to understand spoken commands and perform specific tasks. Here's a breakdown of its functionalities:

1. **Greetings and Goodbye:**
   - Responds to greetings like "hello" or "hi" and bids farewell if the user says "goodbye" or "bye."

2. **Information Retrieval:**
   - Searches Wikipedia based on the query provided.
   - Fetches jokes from a library and speaks them aloud.

3. **Opening Websites:**
   - Opens various websites such as YouTube, Google, Gmail, Netflix, and Prime Video in separate tabs using the web browser.

4. **Fetching News and COVID-19 Stats:**
   - Opens news websites like Times of India and Cricbuzz for news and cricket updates, respectively.
   - Displays the latest COVID-19 statistics from a specific webpage.

5. **Time, Date, and Assistant Information:**
   - Tells the current time and date.
   - Provides information about itself when asked who created it.

6. **Note Taking and Software Execution:**
   - Takes notes by creating text files with the content spoken.
   - Attempts to open software based on user commands if available in the `software_path` dictionary.

7. **Speaking Results:**
   - Reads out the results gathered or actions taken based on the recognized command.

Overall, this function acts as a voice-controlled assistant capable of performing various tasks such as web browsing, information retrieval, note-taking, and providing specific information upon user commands.

__code:__



        def Process_linux_audio():

            run = 1
           if __name__=='__main__':
               while run==1:

                  statement = get_audio().lower()
                  results = ''
                  run +=1
                 global nm, ip1, usrnm, pswd, cmd1

                 if 'start docker' in statement:
                     cmd1 = "systemctl start docker"
                     speak("starting docker")
            
                    elif 'start apache' in statement:
                        cmd1 = "systemctl start httpd"
                        speak("starting apache")

                    elif 'stop docker' in statement:
                        cmd1 = "systemctl stop docker"
                        speak("stopping docker")

                    elif 'stop docker' in statement:
                        cmd1 = "systemctl stop httpd"
                        speak("stopping apache")
            
                    elif 'docker images' in statement:
                        cmd1 = "docker images"

                 elif 'docker container' in statement:
                        cmd1 = "docker ps -a"

                    elif 'stop all docker containers' in statement:
                       cmd1 = "docker stop $(docker ps -aq)"
            
                    elif 'run' in statement or 'start' in statement  and 'docker' in statement  and 'container' in statement:
                        cmd1 = "docker run hello-world"

                    elif 'open' or 'execute' or 'start' or 'run' in statement:
                     for software_name in software_linux_path:
                         if software_name in statement:
                             speak(f" running {software_name} on linux")
                             cmd1 = software_linux_path[software_name]
       
                     else:
                            status_label.config(text="Software not found.")

                    print("Connecting with the following details:")
                    print("Name:", nm)
                    print("IP:", ip1)
                    print("Username:", usrnm)
                    print("Password:", pswd)
                    establish_ssh_connection(nm, ip1, usrnm, pswd, cmd1)


                    print("command running on linux")
                    speak("command running on linux")

This `Process_linux_audio()` function listens for voice commands related to Linux system operations and executes them via SSH (Secure Shell) using the `establish_ssh_connection()` function. Here's a summary of its functionalities:

1. **Starting and Stopping Services:**
   - Recognizes commands to start and stop Docker and Apache services using specific system commands (`systemctl`).
   - Constructs the appropriate command (`cmd1`) for each operation and speaks confirmation messages.

2. **Interacting with Docker:**
   - Provides commands to fetch Docker images and Docker container statuses (`docker images` and `docker ps -a`, respectively).
   - Includes a command to stop all running Docker containers (`docker stop $(docker ps -aq)`).

3. **Running Docker Containers:**
   - Contains a condition to run Docker containers with the `hello-world` image (`docker run hello-world`).

4. **Executing Other Commands:**
   - Attempts to execute other commands based on voice input, searching for matches in `software_linux_path`.
   - If found, it sets the `cmd1` variable with the appropriate command.

5. **SSH Connection and Execution:**
   - Establishes an SSH connection to a Linux machine using details like name, IP, username, and password (`establish_ssh_connection()`).
   - Passes the constructed command (`cmd1`) to the SSH connection for execution.
   - Displays details of the connection and the command being executed.

6. **Announcing Linux Command Execution:**
   - Prints messages to indicate that a command is being executed on the Linux system.

Overall, this function acts as a bridge between voice commands related to Linux operations and their execution on a remote Linux system via SSH.

__code:__


        def open_software(software_name):
            try:
                subprocess.run(software_name, capture_output=True)
            except Exception as e:
                status_label.config(text=f"Error: {e}")
        
The `open_software()` function is designed to execute software programs using Python's `subprocess` module. Its purpose is to open specific software based on the name or path provided as an argument. Upon receiving the software name, it attempts to run the software through `subprocess.run()`. If successful, the function launches the specified software. However, if an exception occurs during this process (for example, due to an incorrect software name or path), it catches the exception and updates a status label (`status_label`) with an error message, indicating the failure to execute the software. Overall, it's a utility function used to launch software applications using Python.

__code:__

        def click_photo():
            cap=cv2.VideoCapture(0)
            cap
            status ,photo =cap.read()
            cv2.imwrite("pic.jpg",photo)
            cv2.imshow("My photo",photo)
            cv2.waitKey(5000)
            cv2.destroyAllWindows()
            cap.release()

This code snippet defines a function `click_photo()` that captures an image from the default camera using OpenCV in Python. It follows these steps:

1. **Camera Initialization:** It initializes the default camera for video capture.
2. **Capture Frame:** Reads a single frame from the camera feed and saves it as `photo`.
3. **Image Saving:** Saves the captured frame as an image named "pic.jpg".
4. **Display Image:** Displays the captured image in a window named "My photo".
5. **Wait Key:** Waits for a key press for 5 seconds (5000 milliseconds).
6. **Window Closure:** Closes the image display window.
7. **Release Resources:** Releases the camera resources.

This function allows you to take a photo using the default camera and stores it as an image named "`pic.jpg`".

__code:__

        def crop_pic():
            cap=cv2.VideoCapture(0)
            cap
            status ,photo =cap.read()
            cv2.imwrite("pic.jpg",photo)
            cv2.imshow("My photo",photo[200:540,200:430])
            cv2.waitKey(5000)
            cv2.destroyAllWindows()
            cap.release()

The `crop_pic()` function initiates the camera to capture a single frame, saving it as an image named "pic.jpg." It showcases a specified cropped section of the captured image in a window titled "My photo." After displaying this section for 5 seconds, it closes the window and releases the resources used for capturing the image. Essentially, it captures, crops, briefly displays, and closes an image section from the camera feed.

__code:__


        def capture_video():
            cap=cv2.VideoCapture(0)
            while True:
                status ,photo=cap.read()
                cv2.imshow("My photo",photo)
                if cv2.waitKey(5)==13:
                    break
            cv2.destroyAllWindows()
        
The `capture_video()` function utilizes OpenCV to capture a live video stream from the default camera (index 0). It continuously reads frames from the camera feed and displays each frame in a window titled "My photo" using `cv2.imshow()`. The function runs indefinitely until the user presses the Enter key (ASCII code 13), at which point the window is closed, and the resources used for capturing and displaying the video are released with `cv2.destroyAllWindows()`. Essentially, this function allows the real-time display of video from the camera until the user decides to exit the window.

__code:__

        def capture_crop_video():
            cap=cv2.VideoCapture(0)
            while True:
                status ,photo=cap.read()
                photo[0:200,0:200]=photo[200:400,200:400]
                cv2.imshow("My photo",photo)
                if cv2.waitKey(5)==13:
                    break
            cv2.destroyAllWindows()

The `capture_crop_video()` function, leveraging OpenCV, captures a live video feed from the default camera (index 0). In a continuous loop, it reads frames from the camera feed, crops a specific region from the current frame (from coordinates [200:400, 200:400]) and places it in another region (at coordinates [0:200, 0:200]). It displays the altered frame in a window titled "My photo" using `cv2.imshow()`. The function runs continuously until the user presses the Enter key (ASCII code 13), at which point the window closes, and the resources used for capturing and displaying the video are released via `cv2.destroyAllWindows()`. Essentially, this function showcases a real-time video stream with a specific cropped region displayed within the window.

__code:__
      
        def image_100_100():
            width, height = 800, 600
            image = Image.new("RGB", (width, height), (255, 255, 255))
            draw = ImageDraw.Draw(image)
            stripe_height = height // 3
            draw.rectangle([(0, 0), (width, stripe_height)], fill=(255, 153, 51))
            draw.rectangle([(0, stripe_height), (width, 2 * stripe_height)], fill=(255, 255, 255))
            draw.rectangle([(0, 2 * stripe_height), (width, height)], fill=(0, 128, 0))
            chakra_radius = min(width, height) // 8
            chakra_center = (width // 2, stripe_height + (stripe_height // 2))
            draw.ellipse(
            [
                (chakra_center[0] - chakra_radius, chakra_center[1] - chakra_radius),
                (chakra_center[0] + chakra_radius, chakra_center[1] + chakra_radius),
            ],
            fill=(0, 56, 168),
            )

            image.save("indian_flag.png")
            image.show()

The `image_100_100()` function creates an image of size 800x600 pixels using the Python Imaging Library (PIL). It generates an image with three horizontal stripes: the top stripe is an orange color, the middle one is white, and the bottom one is green (resembling the Indian flag). Additionally, it draws a blue circular shape at the center of the image. The resulting image is saved as "indian_flag.png" and displayed using the default image viewer. This function essentially creates an Indian flag in a digital image format using Python's PIL library.

__code:__
            
        def get_coordinates():
            location_name = simpledialog.askstring("User Input", "Enter place:")
            
            if location_name:
                geolocator = Nominatim(user_agent="location_finder")
                location = geolocator.geocode(location_name)
                
                if location is None:
                    messagebox.showerror("Error", f"Coordinates not found for '{location_name}'.")
                else:
                    latitude = location.latitude
                    longitude = location.longitude
                    result_str = f"Coordinates for '{location_name}': Latitude = {latitude}, Longitude = {longitude}."
                    messagebox.showinfo("Coordinates", result_str)    


The `get_coordinates()` function prompts the user to input a location using a dialog box. Once a location is provided, it utilizes the `Nominatim` geocoding service from the `geopy` library to retrieve the geographical coordinates (latitude and longitude) of the input location. If the location is found, a message box displays the coordinates, whereas if the location is not found, it shows an error message indicating that the coordinates for the provided location were not found. Overall, this function serves to retrieve and display the coordinates of a user-input location.

__code:__    

        def clear_status():
            status_label.config(text="cleared")

The `clear_status()` function updates the text content of a label widget named `status_label` to the string "cleared". This function is likely part of a graphical user interface (GUI) application, where `status_label` is a visual element used to display status or information to the user. Invoking `clear_status()` changes the displayed text on this label to indicate that the status or information has been cleared or reset.

__code:__

        def create_button(parent, label, command):
            button = tk.Button(parent,font=("Arial",10,"bold"), text=label,width=20,height=2, command=command)
            return button

This `create_button` function creates a button within a graphical user interface (GUI) toolkit using the `tkinter` library. It takes three parameters: `parent` (the parent widget or frame where the button will be placed), `label` (the text displayed on the button), and `command` (the function that will be executed when the button is clicked).

The function uses `tk.Button` to generate a button element, setting various attributes like the font, text, width, height, and command. Then, it returns the created button, allowing it to be placed within the GUI by attaching it to a parent widget or frame.

__code:__

        def connect(popup):
            global nm, ip1, usrnm, pswd, cmd1
            name = name_entry.get()
            ip = ip_entry.get()
            username = username_entry.get()
            password = password_entry.get()
            cmd = 'date'
            nm, ip1, usrnm, pswd, cmd1 = name, ip, username, password, cmd

            print("Connecting with the following details:")
            print("Name:", name)
            print("IP:", ip)
            print("Username:", username)
            print("Password:", password)
            
            
            connected = establish_ssh_connection(name, ip, username, password, cmd)
            if connected:
                status_label.config(text="Connected via SSH")
                print("Connected")
                global ssh_enabled
                ssh_enabled = True
                toggle_button.config(text="SSH Enabled", bg="palevioletred1")
                popup.destroy()
            else:
                status_label.config(text="Failed to connect via SSH")
                print("Failed")
    
The `connect` function is part of a program handling GUI interactions. It's primarily responsible for gathering user input from different entry fields (presumably related to establishing an SSH connection) and calling the `establish_ssh_connection` function to attempt a connection based on the provided details.

It retrieves the `name`, `ip`, `username`, and `password` entered in the respective entry widgets (`name_entry`, `ip_entry`, `username_entry`, `password_entry`). After setting these values and a default command, it attempts to establish an SSH connection using the `establish_ssh_connection` function.

If the connection succeeds (`connected` is `True`), it updates the status label to indicate a successful SSH connection, sets a global flag (`ssh_enabled`) to `True`, changes the text and background color of a button (likely indicating SSH status), and destroys the popup window (`popup`). Conversely, if the connection fails, it updates the status label accordingly.

 __code:__
       
        def login_button_clicked():
            popup = tk.Toplevel(root)

            tk.Label(popup, text="Name:").grid(row=0, column=0)
            tk.Label(popup, text="IP:").grid(row=1, column=0)
            tk.Label(popup, text="Username:").grid(row=2, column=0)
            tk.Label(popup, text="Password:").grid(row=3, column=0)

            global name_entry, ip_entry, username_entry, password_entry
            name_entry = tk.Entry(popup)
            ip_entry = tk.Entry(popup)
            username_entry = tk.Entry(popup)
            password_entry = tk.Entry(popup, show="*")

            name_entry.grid(row=0, column=1)
            ip_entry.grid(row=1, column=1)
            username_entry.grid(row=2, column=1)
            password_entry.grid(row=3, column=1)

            # Connect button
            connect_button = tk.Button(popup, text="Connect", command=lambda popup=popup: connect(popup))
            connect_button.grid(row=4, column=0, columnspan=2, pady=10)    

The `login_button_clicked` function is part of a graphical user interface (GUI) setup. When executed, it creates a popup window (`Toplevel`) that includes entry fields for `Name`, `IP`, `Username`, and `Password`. These fields are accompanied by respective labels indicating their purpose.

It defines `Entry` widgets for each of these fields (`name_entry`, `ip_entry`, `username_entry`, `password_entry`) and places them within the popup window in a grid layout using `grid` method. Additionally, it creates a 'Connect' button (`connect_button`) that, upon clicking, triggers the `connect` function while passing the `popup` reference as an argument to establish an SSH connection based on the provided details.

__code:__

        def toggle_ssh():
            global ssh_enabled
            ssh_enabled = not ssh_enabled
            if ssh_enabled:
                toggle_button.config(text="SSH Enabled", bg="palevioletred1")
                print(ssh_enabled)
            else:
                toggle_button.config(text="SSH Disabled", bg="lightgoldenrod1")
                print(ssh_enabled)

        def command_location():
            if ssh_enabled:
                Process_linux_audio()
            else:
                Process_audio()

The `toggle_ssh` function and `command_location` function are related to managing the state of SSH (Secure Shell) functionality in a larger program.

- `toggle_ssh`: This function toggles the state of the SSH connection. It modifies the `ssh_enabled` global variable, switching it between `True` and `False`. Depending on its state, it changes the appearance of a button (`toggle_button`) in the graphical user interface to visually indicate whether SSH is enabled or disabled.

- `command_location`: This function checks if SSH is enabled (`ssh_enabled`). If SSH is enabled, it initiates a process related to Linux commands (`Process_linux_audio`). If SSH is disabled, it triggers a different process (`Process_audio`). Essentially, it decides which set of functions to execute based on the SSH connection's state.

__code:__

        engine = pyttsx3.init('sapi5')  
        voices = engine.getProperty('voices')  
        engine.setProperty('voice', voices[1].id)

        wishMe()

The code initializes a text-to-speech engine using the `pyttsx3` library. It sets the voice property to the second voice available (`voices[1]`) among the voices provided by the system's Speech API ('sapi5' in this case). Then, it calls the `wishMe()` function. The `wishMe()` function typically greets the user based on the current time, saying "Good Morning," "Good Afternoon," or "Good Evening" based on the time of the day retrieved using the `datetime` library.

__code:__

        software_path = {
            "notepad": "notepad",
            "calculator": "calc",
           "paint": "mspaint",
            "chrome":"chrome",
            "explorer":"explorer",
           "vlc":"vlc",
            "word": "winword",
            "powerpoint": "powerpnt",
            "excel": "excel"
            # Add more software names and paths here
        }



        software_linux_path = {
            "date": "date",
            "calendar": "cal",
            "list": "ls -l",
            "present working directory":"pwd",
            "who am i":"whoami",
            # Add more software names and paths here
        }


        ssh_enabled = False

        root = tk.Tk()
        s_w=root.winfo_screenwidth()
        s_h=root.winfo_screenheight()
        root.title("Main Window")
        root.geometry(f"{s_w}x{s_h}")
        root.configure(bg="palegreen1")

        title_label = tk.Label(root, text="Welcome to your Assisstant",width=30,height=3, font="title_font", fg="blue")
        title_label.pack(pady=15)


        microphone_photo = PhotoImage(file = "assistant_logo.png")
        microphone_button = Button(image=microphone_photo, command = command_location)
        microphone_button.pack(pady=10)

        frame1 = tk.Frame(root, bg="palegreen1")
        frame1.pack()

        login_button = tk.Button(frame1, text="Login to linux", font=("bold"), bg="lightgoldenrod1", command=login_button_clicked)
        login_button.pack(side=tk.LEFT, padx=25, pady=20)

        toggle_button = tk.Button(frame1, text="SSH Disabled", font=("bold"), bg="lightgoldenrod1", command=toggle_ssh)
        toggle_button.pack(side=tk.LEFT, padx=25, pady=20)


        buttons_frame = tk.Frame(root, bg="aqua")
        buttons_frame.pack(padx=20, pady=20, fill="both",  expand=True)




        button_notepad = create_button(buttons_frame, "NOTEPAD",lambda: open_software("notepad"))
        button_calculator = create_button(buttons_frame, "CALCULATOR", lambda: open_software("calc"))
        button_paint = create_button(buttons_frame, "PAINT", lambda: open_software("mspaint"))
        button_chrome = create_button(buttons_frame, "CHROME", lambda: open_software("chrome"))
        button_cmd = create_button(buttons_frame, "COMMAND PROMPT", lambda: os.startfile("cmd.exe"))
        button_explorer = create_button(buttons_frame, "EXPLORER", lambda: open_software("explorer"))
        button_vlc = create_button(buttons_frame, "VLC", lambda: open_software("vlc"))
        button_taskmgr = create_button(buttons_frame, "TASK MANAGER",lambda: os.system("taskmgr"))
        button_photo = create_button(buttons_frame,  "CLICK PHOTO", click_photo)
        button_croppic = create_button(buttons_frame, "CROP PHOTO",crop_pic)
        button_video = create_button(buttons_frame, "CAPTURE VIDEO",capture_video)
        button_cropvideo = create_button(buttons_frame,"CROP VIDEO",capture_crop_video)
        button_image= create_button(buttons_frame,"IMAGE 100*100",image_100_100)
        button_coordinates = create_button(buttons_frame,"GEO COORDINATES" ,lambda:get_coordinates())

        button_notepad.grid(row=0, column=0, padx=100, pady=30)
        button_calculator.grid(row=0, column=1, padx=100, pady=30)
        button_paint.grid(row=0, column=2, padx=100, pady=30)
        button_chrome.grid(row=0, column=3, padx=100, pady=30)
        button_cmd.grid(row=1, column=0, padx=100, pady=30)
        button_explorer.grid(row=1, column=1, padx=100, pady=30)
        button_vlc.grid(row=1, column=2, padx=100, pady=30)
        button_taskmgr.grid(row=1, column=3, padx=100, pady=30)
        button_image.grid(row=2, column=1,padx=100, pady=30)
        button_coordinates.grid(row=2, column=0, padx=100, pady=30)
        button_photo.grid(row=2, column=2, padx=100, pady=30)
        button_croppic.grid(row=2, column=3, padx=100, pady=30)
        button_video.grid(row=3, column=0, padx=100, pady=30)
        button_cropvideo.grid(row=3, column=1, padx=100, pady=30)

        buttons = [
            button_notepad, button_calculator, button_paint, button_chrome,
            button_cmd, button_explorer, button_vlc, button_taskmgr,
            button_photo, button_croppic, button_video, button_cropvideo,
            button_image, button_coordinates
        ]

        for button in buttons:
            button.configure(bg="lightskyblue1")


        status_label = tk.Label(root, text="", fg="red", bg ="palegreen1")
        status_label.pack(pady=10)
        clear_button = tk.Button(root, text="Clear Status",fg="blue",font=("Arial", 20, "bold"),width=25 ,command=clear_status)
        clear_button.pack()


        root.mainloop()

This block of code creates a graphical user interface (`GUI`) using the Tkinter library in Python. It generates a window containing buttons and functionalities to interact with the system, run various programs (like Notepad, Calculator, Chrome, etc.), perform image and video-related operations (click photos, capture video, crop photos, etc.), retrieve geographical coordinates, and manage a few system-related tasks. It integrates SSH functionality for connecting to Linux systems, toggling SSH access, and executing commands based on user input or button clicks. The GUI layout contains buttons for different functionalities, a status label for displaying messages, and a '`Clear Status`' button to reset the displayed status.

---

# Usage

- Run the Python file associated with the project.  
- Interact with the assistant using voice commands listed in the code.  
- Enjoy the functionalities like browsing, software execution, system commands, and more.

The assistant can work effectively in both the host OS as well as can be used for executing commands using voice on linux based guest OS by connecting to it via SSH.


![](/voice_assistant_images/home_page.png)

The home page that opens when the assistant is run.

![](/voice_assistant_images/login_to_linux.png)

You can use SSH to connect to the Linux machine by providing the `Username`,  `IP address` and `password`. After that, a Linux instance can execute the commands.

![](/voice_assistant_images/ssh_connected_1.png)

The `SSH disabled` button becomes `SSH enabled` and changes color as soon as the SSH connection is established. We also receive a status update that says, "`Connected via SSH.`"

![](/voice_assistant_images/ssh_connected_2.png)

When using SSH to connect, try speaking "`open calendar`." You should see the following results from the `cal` command:

![](/voice_assistant_images/linux_calendar.png)

When using SSH to connect, try speaking "`what is the date today`." You should see the following results from the `date` command:

![](/voice_assistant_images/linux_date.png)

You receive the following status update if your attempt to connect to SSH fails for any reason.

![](/voice_assistant_images/ssh_failed.png)

---

Similarly, the voice assistant's functionality and command set can be enhanced to accommodate a wider range of commands as needed. 



### P.S. - Any suggestions and improvements are warmly welcome.!

