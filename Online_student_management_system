from pymongo import MongoClient
import random
import tkinter as tk
from tkinter import messagebox
from tkinter import ttk

uri = "mongodb+srv://root1:root1@cluster0.isl0poll.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0"
try:
    client = MongoClient(uri)
    db = client.Studentdb
    print("Connected to MongoDB")
except:
    print("Database connection Error ")
    print("No connection could be made because the target machine actively refused it ")
    messagebox.showerror("Error", "Connection Error")
    sys.exit(1)

def add_students(root, db): 
    def add_query():
        prn = entry_regno.get()
        name = entry_name.get()
        email = entry_email.get()
        class_ = entry_class.get()
        mobile = entry_mobile.get()
        regno = [prn]
        name_list = [name]
        email_list = [email]
        class_list = [class_]
        mobile_list = [mobile]
        student_data = {
            'RegNo': regno[random.randint(0, (len(regno)-1))],
            'Name': name_list[random.randint(0, (len(name_list)-1))],
            'Email': email_list[random.randint(0, (len(email_list)-1))],
            'Class': class_list[random.randint(0, (len(class_list)-1))]
        }
        
        if len(prn) == 0 or len(name) == 0 or len(email) == 0 or len(class_) == 0:
            messagebox.showwarning("WARNING", "All fields are compulsory (Except: Mobile number)")
            return
        
        if len(mobile) == 0 and db.students.count_documents({'RegNo': prn}, limit=1) == 0:
             result = db.students.insert_one({'RegNo': prn, 'Name': name, 'Email': email, 'Class': class_})
        elif len(mobile) != 0 and db.students.count_documents({'RegNo': prn}, limit=1) == 0:
             result = db.students.insert_one(student_data)
        else:
             messagebox.showwarning("ERROR", "Student Already Exists")
             return
       	
        newwin.destroy()
        messagebox.showinfo("Add Student", "Student Added")
    
    newwin = tk.Toplevel(root)
    newwin.title("Add Students")
    newwin.geometry('350x250')
    
    tk.Label(newwin, text="Reg No").grid(row=0, column=0, padx=10, pady=10)
    entry_regno = tk.Entry(newwin, bd=7)
    entry_regno.grid(row=0, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Name").grid(row=1, column=0, padx=10, pady=10)
    entry_name = tk.Entry(newwin, bd=7)
    entry_name.grid(row=1, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Email").grid(row=2, column=0, padx=10, pady=10)
    entry_email = tk.Entry(newwin, bd=7)
    entry_email.grid(row=2, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Class").grid(row=3, column=0, padx=10, pady=10)
    entry_class = tk.Entry(newwin, bd=7)
    entry_class.grid(row=3, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Mobile").grid(row=4, column=0, padx=10, pady=10)
    entry_mobile = tk.Entry(newwin, bd=7)
    entry_mobile.grid(row=4, column=1, padx=10, pady=10)
    
    tk.Button(newwin, text="Submit", command=add_query).grid(row=5, columnspan=2, padx=10, pady=10)

def delete_data(root, db):
    def delete():
        prn = entry_regno.get()
        if len(prn) == 0:
            messagebox.showwarning("WARNING", "Enter a Valid Reg No")
            return
        if db.students.count_documents({'RegNo': prn}, limit=1) == 0:
            messagebox.showwarning("ERROR", "Student Does Not Exist")
            return
        else:
            db.students.delete_one({'RegNo': prn})
        newwin.destroy()
        messagebox.showinfo("Delete Student", "Student Deleted")
    
    newwin = tk.Toplevel(root)
    newwin.title("Delete Student")
    newwin.geometry('300x150')
    
    tk.Label(newwin, text="Reg No").grid(row=0, column=0, padx=10, pady=10)
    entry_regno = tk.Entry(newwin, bd=5)
    entry_regno.grid(row=0, column=1, padx=10, pady=10)
    
    tk.Button(newwin, text="Delete Entry", command=delete).grid(row=1, columnspan=2, padx=10, pady=10)

def update_data(root, db):
    def update():
        prn = entry_regno.get()
        name = entry_name.get()
        email = entry_email.get()
        class_ = entry_class.get()
        mobile = entry_mobile.get()
        if len(prn) == 0:
            messagebox.showwarning("WARNING", "Enter a Valid Reg No")
            return

        if db.students.count_documents({'RegNo': prn}, limit=1) == 0:
            messagebox.showwarning("ERROR", "Student Does Not Exist")
            return
        if len(name) != 0:
            db.students.update_one({"RegNo": prn}, {"$set": {'Name': name}})
        if len(email) != 0:
            db.students.update_one({"RegNo": prn}, {"$set": {'Email': email}})
        if len(class_) != 0:
            db.students.update_one({"RegNo": prn}, {"$set": {'Class': class_}})
        if len(mobile) != 0:
            db.students.update_one({"RegNo": prn}, {"$set": {'Mobile': mobile}})
        
        newwin.destroy()
        messagebox.showinfo("Update Student", "Student Updated")
    
    newwin = tk.Toplevel(root)
    newwin.title("Update Students")
    newwin.geometry('350x250')
    
    tk.Label(newwin, text="Reg No").grid(row=0, column=0, padx=10, pady=10)
    entry_regno = tk.Entry(newwin, bd=7)
    entry_regno.grid(row=0, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Name").grid(row=1, column=0, padx=10, pady=10)
    entry_name = tk.Entry(newwin, bd=7)
    entry_name.grid(row=1, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Email").grid(row=2, column=0, padx=10, pady=10)
    entry_email = tk.Entry(newwin, bd=7)
    entry_email.grid(row=2, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Class").grid(row=3, column=0, padx=10, pady=10)
    entry_class = tk.Entry(newwin, bd=7)
    entry_class.grid(row=3, column=1, padx=10, pady=10)
    
    tk.Label(newwin, text="Mobile").grid(row=4, column=0, padx=10, pady=10)
    entry_mobile = tk.Entry(newwin, bd=7)
    entry_mobile.grid(row=4, column=1, padx=10, pady=10)
    
    tk.Button(newwin, text="Submit", command=update).grid(row=5, columnspan=2, padx=10, pady=10)

def display(root, db):
    newwin = tk.Toplevel(root)
    newwin.title("Student Details")
    newwin.geometry('500x400')
    
    tk.Label(newwin, text="Reg No", font=('Helvetica', 12, 'bold')).grid(row=0, column=0, padx=10, pady=10)
    tk.Label(newwin, text="Name", font=('Helvetica', 12, 'bold')).grid(row=0, column=1, padx=10, pady=10)
    tk.Label(newwin, text="Email", font=('Helvetica', 12, 'bold')).grid(row=0, column=2, padx=10, pady=10)
    tk.Label(newwin, text="Class", font=('Helvetica', 12, 'bold')).grid(row=0, column=3, padx=10, pady=10)
    tk.Label(newwin, text="Mobile", font=('Helvetica', 12, 'bold')).grid(row=0, column=4, padx=10, pady=10)
    
    i = 1
    for x in db.students.find():
        tk.Label(newwin, text=x['RegNo']).grid(row=i, column=0, padx=10, pady=10)
        tk.Label(newwin, text=x['Name']).grid(row=i, column=1, padx=10, pady=10)
        tk.Label(newwin, text=x['Email']).grid(row=i, column=2, padx=10, pady=10)
        tk.Label(newwin, text=x['Class']).grid(row=i, column=3, padx=10, pady=10)
        if 'Mobile' in x:
            tk.Label(newwin, text=x['Mobile']).grid(row=i, column=4, padx=10, pady=10)
        i += 1

root = tk.Tk()
root.geometry('500x400')
root.title("Student Management System")

add_button = tk.Button(root, text='Add New Student', command=lambda: add_students(root, db), font=('Helvetica', 12, 'bold'))
delete_button = tk.Button(root, text='Delete Student Entry', command=lambda: delete_data(root, db), font=('Helvetica', 12, 'bold'))
update_button = tk.Button(root, text='Update Student Info', command=lambda: update_data(root, db), font=('Helvetica', 12, 'bold'))
show_button = tk.Button(root, text='Show Student Details', command=lambda: display(root, db), font=('Helvetica', 12, 'bold'))

add_button.place(x=100, y=50)
delete_button.place(x=100, y=100)
update_button.place(x=100, y=150)
show_button.place(x=100, y=200)

root.mainloop()
