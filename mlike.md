import sys, os, re, json, requests
import random
from datetime import datetime
from time import sleep

#bang mau
maul=rand(31,37)
maui="\033[1;"{maul}"m"

os.system('clear')
sr="\033[1;32m[✓] \033[1;97m=> \033[1;33m"
key='''Key Hợp Lệ'''
t_bao='''\033[1;31mThông báo :'''
logo = '''

\033[1;33m████████╗██████╗░██╗░░░██╗███╗░░░██╗░██████╗ 
\033[1;94m╚══██╔══╝██╔══██╗██║░░░██║████╗░░██║██╔════╝
\033[1;36m ░░██║░░░██████╔╝██║░░░██║██╔██╗░██║██║░░░███╗
\033[1;31m ░░██║░░░██╔══██╗██║░░░██║██║╚██╗██║██║░░░██ ║
\033[1;95m ░░██║░░░██║░░██║╚██████╔╝██║ ╚████║╚██████╔╝
\033[1;32m ░░╚═╝░░░╚═╝░░╚═╝ ╚═════╝░╚═╝  ╚═══╝ ╚═════╝ 

'''
print("\n")
def logo_chạy(a):
    from time import sleep
    a = a.split('\n')
    c = ''
    for j in range(0, len(a)):
        b = a[j] + '\n'
        for i in b:
            c += i
            print(c, end='\r')
            sleep(0.02)
        c=''
logo_chạy(logo)
tbao= requests.get("https://pastebin.com/raw/SBK3KwSX").text
link = requests.get("https://pastebin.com/raw/YXWJQd7v").text
mk1 = requests.get("https://pastebin.com/raw/P9Z86nHE").text
mk2 = requests.get("https://pastebin.com/raw/9GH9d0wA").text
print("-"*50)
logo_chạy(t_bao)
print(f"{sr} {tbao}")
print("\033[1;94m-"*50)
print(f"{sr} {link}")

# =====================================

makey = input(f"{sr} Nhập Key : ")
while True:
    if makey not in [mk1, mk2]:
        print(f"{sr} Keyy Sai !!!")
        makey = input(f"{sr} Nhập lại Key : ")
    else:
        logo_chạy(key)
        sleep(1)
        break
        sleep(3)
os.system('clear')
print("\033[1;94m-"*50)
atho=input('Nhập authorization: ') #input authorization
#url xem qc & tổng xu
url='http://mlikeapiv21.yosarete.com:8092/api/user/credit/set/ads'
url_tổng_xu='http://mlikeapiv21.yosarete.com:8092/api/user/credit/get/all'
os.system('clear')
#headers
headers={
    'user-agent': 'Dart/2.10 (dart:io)',
    'content-length': '0',
    'authorization':atho,
    'host':'mlikeapiv21.yosarete.com:8092'
}

job=0
#vòng lặp
while(True):
    #xem qc
    xem_qc=requests.post(url=url,headers=headers)
    status=xem_qc.json()['status']
    
    if status== 200:#200=> xem qc thành công
        job=job+1 #số job tăng 1
        t=datetime.now().strftime("%H:%M:%S") #thời gian thực
        credit=xem_qc.json()['credit'] #số credit được cộng
        
        #check tổng xu
        all_xu=requests.post(url=url_tổng_xu,headers=headers)
        tổng=all_xu.json()['credit'] #lấy tổng xu ra từ json
        
        print('\033[1;34m[\033[1;97m'+t+'\033[1;34m]\033[1;97m'," \033[1;97mYou've gained " +str(credit)+ 'credits',' =\033[1;34m ' +str(tổng))
        #Chờ
        for time in range(10 , -1, -1):
            print(choice(rand)+'Wait',time ,end=' \r')
            sleep(1)
    #status không bằng 200=> hết qc
    else:
        all_xu=requests.post(url=url_tổng_xu,headers=headers)
        tổng=all_xu.json()['credit'] 
        t=datetime.now().strftime("%H:%M:%S") #thời gian thực
        print('\033[1;34m[\033[1;97m'+t+'\033[1;34m]\033[1;97m'," \033[1;97mYou've filled the limit =\033[1;34m " +str(tổng))
        for time in range(3600 , -1, -1):
            print(choice(rand)+' Wait', time ,end=' \r')
            sleep(1)
