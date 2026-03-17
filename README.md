import socket
import tkinter as tk
import threading
def scan_ports():
    ip = entry_ip.get()
    text_output.delete(1.0, tk.END)
    text_output.insert(tk.END, f"Scanning IP: {ip}\n\n")
    ports = [21, 22, 23, 25, 53, 80, 110, 139, 143, 443, 3306, 3389]
    for port in ports:
        try:
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.settimeout(0.5)
            result = s.connect_ex((ip, port))
  if result == 0:
                text_output.insert(tk.END, f"Port {port} : OPEN\n")
            else:
                text_output.insert(tk.END, f"Port {port} : CLOSED\n")
            s.close()
        except Exception as e:
            text_output.insert(tk.END, f"Error on port {port}\n")
    text_output.insert(tk.END, "\nScan Completed "
def start_scan():
    thread = threading.Thread(target=scan_ports)
    thread.start()

root = tk.Tk()
root.title("Python Port Scanner")
root.geometry("420x380")
title = tk.Label(root, text="Port Scanner Tool", font=("Arial", 14, "bold"))
title.pack(pady=5)
label_ip = tk.Label(root, text="Enter IP Address:")
label_ip.pack()
entry_ip = tk.Entry(root, width=30)
entry_ip.insert(0, "127.0.0.1")
entry_ip.pack(pady=5)
btn_scan = tk.Button(root, text="Start Scan", bg="lightblue", command=start_scan)
btn_scan.pack(pady=10)
text_output = tk.Text(root, height=15, width=50)
text_output.pack()
root.mainloop()
