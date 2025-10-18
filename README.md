# Create main window
root = tk.Tk()
root.title("To-Do List Application")
root.geometry("400x500")
root.config(bg="#D9EAFD")

# List to store tasks
tasks = []

# Function to update the listbox
def update_listbox():
    listbox.delete(0, tk.END)
    for task in tasks:
        listbox.insert(tk.END, task)

# Function to add a task
def add_task():
    task = task_entry.get()
    if task != "":
        tasks.append(task)
        update_listbox()
        task_entry.delete(0, tk.END)
    else:
        messagebox.showwarning("Warning", "Please enter a task!")

# Function to delete selected task
def delete_task():
    try:
        selected = listbox.curselection()[0]
        tasks.pop(selected)
        update_listbox()
    except:
        messagebox.showwarning("Warning", "Please select a task to delete!")

# Function to clear all tasks
def clear_tasks():
    if messagebox.askyesno("Confirm", "Do you really want to clear all tasks?"):
        tasks.clear()
        update_listbox()

# Function to mark task as done
def mark_done():
    try:
        index = listbox.curselection()[0]
        task = tasks[index]
        if not task.startswith("✔ "):
            tasks[index] = "✔ " + task
            update_listbox()
    except:
        messagebox.showwarning("Warning", "Please select a task to mark as done!")

# Heading
heading = tk.Label(root, text="📝 To-Do List", font=("Helvetica", 18, "bold"), bg="#D9EAFD", fg="#0A1172")
heading.pack(pady=10)

# Input box
task_entry = tk.Entry(root, width=30, font=("Helvetica", 14))
task_entry.pack(pady=10)

# Buttons
frame = tk.Frame(root, bg="#D9EAFD")
frame.pack(pady=10)

add_button = tk.Button(frame, text="Add Task", width=12, command=add_task, bg="#4CAF50", fg="white")
add_button.grid(row=0, column=0, padx=5)

delete_button = tk.Button(frame, text="Delete Task", width=12, command=delete_task, bg="#E53935", fg="white")
delete_button.grid(row=0, column=1, padx=5)

done_button = tk.Button(frame, text="Mark Done", width=12, command=mark_done, bg="#2196F3", fg="white")
done_button.grid(row=1, column=0, pady=5)

clear_button = tk.Button(frame, text="Clear All", width=12, command=clear_tasks, bg="#9C27B0", fg="white")
clear_button.grid(row=1, column=1, pady=5)

# Listbox to show tasks
listbox = tk.Listbox(root, width=40, height=12, font=("Helvetica", 12), selectbackground="#A3C4F3")
listbox.pack(pady=20)

# Run the application
root.mainloop()
