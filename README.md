# BRO-S-SKIESHUB-TASK-2
TO CREATE TO-DO LIST APPLICATION

TASKS_FILE = "tasks.txt"

# Load tasks from file into a list
def load_tasks():
    tasks = []
    try:
        with open(TASKS_FILE, "r") as file:
            tasks = [line.strip() for line in file.readlines()]
    except FileNotFoundError:
        # No tasks yet, file will be created later
        pass
    return tasks

# Save list of tasks to file
def save_tasks(tasks):
    with open(TASKS_FILE, "w") as file:
        for task in tasks:
            file.write(task + "\n")

# Show all tasks
def view_tasks(tasks):
    if not tasks:
        print("\n No tasks to show.\n")
    else:
        print("\n To-Do List:")
        for i, task in enumerate(tasks, 1):
            print(f"{i}. {task}")
        print()

# Add a new task
def add_task(tasks):
    task = input("Enter new task: ").strip()
    if task:
        tasks.append(task)
        save_tasks(tasks)
        print(" Task added.\n")
    else:
        print(" Task cannot be empty.\n")

# Remove a task by number
def remove_task(tasks):
    view_tasks(tasks)
    if not tasks:
        return
    try:
        num = int(input("Enter task number to remove: "))
        if 1 <= num <= len(tasks):
            removed = tasks.pop(num - 1)
            save_tasks(tasks)
            print(f" Removed: {removed}\n")
        else:
            print(" Invalid task number.\n")
    except ValueError:
        print(" Please enter a valid number.\n")

# Main menu loop
def main():
    tasks = load_tasks()

    while True:
        print("=== To-Do List Menu ===")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Remove Task")
        print("4. Exit")

        choice = input("Choose an option (1-4): ").strip()

        if choice == "1":
            view_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            remove_task(tasks)
        elif choice == "4":
            print(" Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.\n")

if __name__ == "__main__":
    main()
