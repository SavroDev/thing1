import socket
import random
import inquirer
from threading import Thread
from datetime import date
from colorama import Fore, init, Back

init()
client_color = Fore.WHITE

print ('======================================================')
print ('Conduit V0.4 Client')
print ('Changelog: ')
print ('- Added the ability to remove input boxes after sending')
print ('- Optimised servers')
print ()
print ("Please input today's password down below:")

wordlist = ['mald','seethe','cope','l','ratio',"don't care","didn't ask",'cat','john','no u']

seed = str(date.today())
random.seed (seed)
password_true = random.choice (wordlist) 


while True:
    prompt = '> '
    password = input(prompt).lower()
    print ('\033[1A' + prompt + '\033[K')

    if password == password_true:
        break
    else:
        print (Fore.RED+'Incorrect password, please enter again.')
        print (Fore.RESET)


print ()
print (Fore.GREEN+'Password accepted, welcome back.')
print (Fore.RESET)
print ('Thank you for choosing')
print (Fore.LIGHTGREEN_EX+'======================================================')
print (Fore.LIGHTGREEN_EX+'░█████╗░░█████╗░███╗░░██╗██████╗░██╗░░░██╗██╗████████╗')
print (Fore.LIGHTGREEN_EX+'██╔══██╗██╔══██╗████╗░██║██╔══██╗██║░░░██║██║╚══██╔══╝')
print (Fore.LIGHTGREEN_EX+'██║░░╚═╝██║░░██║██╔██╗██║██║░░██║██║░░░██║██║░░░██║░░░')
print (Fore.LIGHTGREEN_EX+'██║░░██╗██║░░██║██║╚████║██║░░██║██║░░░██║██║░░░██║░░░')
print (Fore.LIGHTGREEN_EX+'╚█████╔╝╚█████╔╝██║░╚███║██████╔╝╚██████╔╝██║░░░██║░░░')
print (Fore.LIGHTGREEN_EX+'░╚════╝░░╚════╝░╚═╝░░╚══╝╚═════╝░░╚═════╝░╚═╝░░░╚═╝░░░')
print (Fore.LIGHTGREEN_EX+'======================================================'+Fore.RESET)
print ()
print ()
print ('Please enter room details below:')
print ()
SERVER_HOST = input('Server Address: ')
ROOM_NUMBER = int(input('Room Number: ')) # server's port
separator_token = "<SEP>" # we will use this to separate the client name & message

SERVER_PORT = (ROOM_NUMBER + 2560)

s = socket.socket()
print(f"[*] Connecting to {SERVER_HOST}, room {ROOM_NUMBER}")
# connect to the server
s.connect((SERVER_HOST, SERVER_PORT))
print("[+] Connected.")
name = input("Temporary Username: ")

import inquirer
questions = [
  inquirer.List('size',
                message="What color do you like?",
                choices=['Red', 'Yellow', 'Green', 'Cyan', 'Blue', 'Purple'],
            ),
]

answer = inquirer.prompt(questions)
if answer == 'Red':
    client_color = Fore.RED
elif answer == 'Yellow':
    client_color = Fore.YELLOW
elif answer == 'Green':
    client_color = Fore.GREEN
elif answer == 'Cyan':
    client_color = Fore.CYAN
elif answer == 'Blue':
    client_color = Fore.BLUE
elif answer == 'Purple':
    client_color = Fore.MAGENTA

welcome = ' has joined the chat'
quitt = ' has quit the chat'
welcome_message = f"{Fore.GREEN}{name}{welcome}{Fore.RESET}"
quitt_message = f"{Fore.YELLOW}{name}{quitt}{Fore.RESET}"
s.send(welcome_message.encode())

def listen_for_messages():
    while True:
        message = s.recv(1024).decode()
        print('\n' + message)

t = Thread(target=listen_for_messages)
t.daemon = True
t.start()

while True:
    prompt = ''
    to_send = input(prompt)
    print ('\033[1A' + prompt + '\033[K')

    if to_send.lower() == 'quit':
        s.send (quitt_message.encode())
        break
    to_send = f"{client_color}{name}{separator_token}{Fore.RESET}{to_send}"
    s.send (to_send.encode())

s.close()
