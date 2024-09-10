import os

# Global task list
tasks = []

# Function to load tasks from file
def load_tasks():
    if os.path.exists("tasks.txt"):
        with open("tasks.txt", "r") as file:
            for line in file:
                task, status = line.strip().split(" | ")
                tasks.append({"task": task, "complete": status == "True"})

# Function to save tasks to file
def save_tasks():
    with open("tasks.txt", "w") as file:
        for task in tasks:
            file.write(f"{task['task']} | {task['complete']}\n")

# Function to display the task list
def display_tasks():
    if not tasks:
        print("\nNo tasks available!")
        return
    print("\nCurrent Task List:")
    for i, task in enumerate(tasks, 1):
        status = "Complete" if task["complete"] else "Incomplete"
        print(f"{i}. {task['task']} [{status}]")

# Function to add a new task
def add_task():
    task = input("Enter the new task: ")
    tasks.append({"task": task, "complete": False})
    print(f"Task '{task}' added successfully.")

# Function to edit an existing task
def edit_task():
    display_tasks()
    try:
        task_num = int(input("\nEnter the task number to edit: "))
        if 1 <= task_num <= len(tasks):
            new_task = input("Enter the updated task: ")
            tasks[task_num - 1]["task"] = new_task
            print("Task updated successfully.")
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid task number.")

# Function to delete a task
def delete_task():
    display_tasks()
    try:
        task_num = int(input("\nEnter the task number to delete: "))
        if 1 <= task_num <= len(tasks):
            removed_task = tasks.pop(task_num - 1)
            print(f"Task '{removed_task['task']}' deleted.")
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid task number.")

# Function to mark a task as complete
def mark_task_complete():
    display_tasks()
    try:
        task_num = int(input("\nEnter the task number to mark as complete: "))
        if 1 <= task_num <= len(tasks):
            tasks[task_num - 1]["complete"] = True
            print(f"Task '{tasks[task_num - 1]['task']}' marked as complete.")
        else:
            print("Invalid task number.")
    except ValueError:
        print("Please enter a valid task number.")

# Main menu function
def main_menu():
    while True:
        print("\nTask Manager Menu")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Edit Task")
        print("4. Delete Task")
        print("5. Mark Task as Complete")
        print("6. Save & Exit")

        choice = input("Choose an option: ")

        if choice == '1':
            display_tasks()
        elif choice == '2':
            add_task()
        elif choice == '3':
            edit_task()
        elif choice == '4':
            delete_task()
        elif choice == '5':
            mark_task_complete()
        elif choice == '6':
            save_tasks()
            print("Tasks saved! Exiting the program.")
            break
        else:
            print("Invalid option. Please try again.")

# Load tasks from file if available
load_tasks()

# Run the main menu
main_menu()
