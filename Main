import tkinter as tk
from tkinter import ttk
import random
import string
import socket
import psutil



class Tab1:
    def __init__(self, master):
        self.master = master

        # create label and entry widgets for password length
        self.label = ttk.Label(self.master, text="Password length:")
        self.label.pack(padx=10, pady=10)
        self.label = ttk.Label(self.master, text="(only numbers)")
        self.label.pack(padx=10, pady=10)
        self.entry = ttk.Entry(self.master)
        self.entry.pack(padx=10, pady=10)

        # create button to generate password
        self.button = ttk.Button(self.master, text="Generate Password")
        self.button.pack(padx=10, pady=10)
        self.button.bind("<Button-1>", self.generate_password)

        # create label widget to display password
        self.password_label = tk.Text(self.master, height=1, width=30)
        self.password_label.pack(padx=10, pady=10)

    def generate_password(self, event):
        # get password length from entry widget
        length = int(self.entry.get())

        # define characters to use in password
        characters = string.ascii_letters + string.digits + string.punctuation

        # generate password
        password = "".join(random.choice(characters) for _ in range(length))

        # clear the text box before adding the new password
        self.password_label.delete(1.0, tk.END)

        # insert generated password in the text box
        self.password_label.insert(tk.END, password)

        # select the generated password
        self.password_label.tag_add("sel", "1.0", "end")
    
class Tab2:
    def __init__(self, master):
        self.master = master
        self.frame = tk.Frame(self.master)
        self.frame.pack()
        self.label = tk.Label(self.frame, text="Enter a website URL:")
        self.label.pack(side="left")
        self.label = tk.Label(self.frame, text="DO NOT ADD HTTPS://!")
        self.label.pack(side="bottom")
        self.entry = tk.Entry(self.frame)
        self.entry.pack(side="left")
        self.btn = tk.Button(self.frame, text="Lookup IP", command=self.lookup_ip)
        self.btn.pack(side="left")
        self.output = tk.Text(self.master, state="disabled")
        self.output.pack()

    def lookup_ip(self):
        url = self.entry.get()
        try:
            ip = socket.gethostbyname(url)
            self.output.configure(state="normal")
            self.output.delete("1.0", tk.END)
            self.output.insert(tk.END, f"The IP address of {url} is: {ip}")
            self.output.configure(state="disabled")
        except socket.gaierror:
            self.output.configure(state="normal")
            self.output.delete("1.0", tk.END)
            self.output.insert(tk.END, f"Could not resolve {url}")
            self.output.configure(state="disabled")

class Tab3:
    def __init__(self, parent):
        self.parent = parent
        self.frame = ttk.Frame(parent)
        
        
        self.host_label = ttk.Label(self.frame, text="Host:")
        self.host_label.grid(column=0, row=0, pady=5, padx=5, sticky=tk.W)
        self.host_entry = ttk.Entry(self.frame)
        self.host_entry.grid(column=1, row=0, pady=5, padx=5, sticky=tk.W)
        
        self.start_port_label = ttk.Label(self.frame, text="Start Port:")
        self.start_port_label.grid(column=0, row=1, pady=5, padx=5, sticky=tk.W)
        self.start_port_entry = ttk.Entry(self.frame)
        self.start_port_entry.grid(column=1, row=1, pady=5, padx=5, sticky=tk.W)
        
        self.end_port_label = ttk.Label(self.frame, text="End Port:")
        self.end_port_label.grid(column=0, row=2, pady=5, padx=5, sticky=tk.W)
        self.end_port_entry = ttk.Entry(self.frame)
        self.end_port_entry.grid(column=1, row=2, pady=5, padx=5, sticky=tk.W)
        
        self.result_label = ttk.Label(self.frame, text="")
        self.result_label.grid(column=0, row=4, columnspan=2, pady=10, padx=5)
        
        self.scan_button = ttk.Button(self.frame, text="Scan Ports", command=self.scan_ports)
        self.scan_button.grid(column=0, row=3, pady=10, padx=5)
        
        self.frame.pack(padx=10, pady=10)
    
    def scan_ports(self):
        host = self.host_entry.get()
        start_port = int(self.start_port_entry.get())
        end_port = int(self.end_port_entry.get())
        open_ports = []
        
        self.result_label.config(text="Scanning...")
        
        for port in range(start_port, end_port+1):
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            s.settimeout(0.1)
            try:
                s.connect((host, port))
                open_ports.append(port)
                s.close()
            except:
                pass
        
        if open_ports:
            self.result_label.config(text=f"Open ports: {', '.join(map(str, open_ports))}")
        else:
            self.result_label.config(text="No open ports found.")

class Tab4:
    def __init__(self, master):
        self.master = master
        

        # Create the labels to display the stats
        self.cpu_label = tk.Label(master, text="CPU: ")
        self.total_memory_label = tk.Label(master, text="Total memory: ")
        self.available_memory_label = tk.Label(master, text="Available memory: ")
        self.disk_usage_label = tk.Label(master, text="Disk usage: ")
        self.network_io_label = tk.Label(master, text="Network I/O: ")

        # Pack the labels into the window with some padding
        self.cpu_label.pack(padx=10, pady=5)
        self.total_memory_label.pack(padx=10, pady=5)
        self.available_memory_label.pack(padx=10, pady=5)
        self.disk_usage_label.pack(padx=10, pady=5)
        self.network_io_label.pack(padx=10, pady=5)

        # Start the update_stats function
        self.update_stats()

    def update_stats(self):
        # Get the CPU usage as a percentage
        cpu_percent = psutil.cpu_percent()
        # Get the total system memory and available memory
        memory = psutil.virtual_memory()
        total_memory = round(memory.total / (1024 * 1024), 2)
        available_memory = round(memory.available / (1024 * 1024), 2)
        # Get the disk usage for the root partition
        disk_usage = psutil.disk_usage('/')
        disk_usage_percent = disk_usage.percent
        # Get the network I/O statistics
        net_io_counters = psutil.net_io_counters()
        bytes_sent = round(net_io_counters.bytes_sent / (1024 * 1024), 2)
        bytes_received = round(net_io_counters.bytes_recv / (1024 * 1024), 2)
        # Update the labels with the new stats
        self.cpu_label.config(text=f"CPU: {cpu_percent}%")
        self.total_memory_label.config(text=f"Total memory: {total_memory} MB")
        self.available_memory_label.config(text=f"Available memory: {available_memory} MB")
        self.disk_usage_label.config(text=f"Disk usage: {disk_usage_percent}%")
        self.network_io_label.config(text=f"Network I/O: {bytes_sent} MB sent, {bytes_received} MB received")
        # Schedule the function to run again after 1 second
        self.master.after(1000, self.update_stats)

class MyGUI:
    def __init__(self, master):
        self.master = master
        self.master.title("Yofe's CyberTool")

        # create notebook widget
        self.notebook = ttk.Notebook(self.master)

        # create frames for three tabs
        self.frame1 = ttk.Frame(self.notebook)
        self.frame2 = ttk.Frame(self.notebook)
        self.frame3 = ttk.Frame(self.notebook)
        self.frame4 = ttk.Frame(self.notebook)
        
        # add tabs to notebook
        self.notebook.add(self.frame1, text="Password Generator")
        self.notebook.add(self.frame2, text="Website Address")
        self.notebook.add(self.frame3, text="Scan for open ports")
        self.notebook.add(self.frame4, text ="My System")
        
        # create tab content
        self.tab1_content = Tab1(self.frame1)
        self.tab2_content = Tab2(self.frame2)
        self.tab3_content = Tab3(self.frame3)
        self.tab4_content = Tab4(self.frame4)
        # pack notebook widget
        self.notebook.pack()



if __name__ == '__main__':
    root = tk.Tk()
    root.geometry("400x400")
    app = MyGUI(root)
    root.mainloop()
