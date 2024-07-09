# to-do-list
import json

class Task:
    def __init__(self, description, completed=False):
        self.description = description
        self.completed = completed

    def __repr__(self):
        return f"Task(description='{self.description}', completed={self.completed})"

def add_task(tasks):
    description = input("Enter task description: ")
    task = Task(description)
    tasks.append(task)

def view_tasks(tasks):
    if not tasks:
        print("No tasks available.")
        return
    for i, task in enumerate(tasks):
        status = "Done" if task.completed else "Not Done"
        print(f"{i + 1}. {task.description} [{status}]")

def update_task(tasks):
    if not tasks:
        print("No tasks available.")
        return
    view_tasks(tasks)
    try:
        task_index = int(input("Enter task number to update: ")) - 1
        if task_index < 0 or task_index >= len(tasks):
            print("Invalid task number.")
            return
        new_description = input("Enter new description: ")
        tasks[task_index].description = new_description
    except ValueError:
        print("Invalid input. Please enter a number.")

def delete_task(tasks):
    if not tasks:
        print("No tasks available.")
        return
    view_tasks(tasks)
    try:
        task_index = int(input("Enter task number to delete: ")) - 1
        if task_index < 0 or task_index >= len(tasks):
            print("Invalid task number.")
            return
        tasks.pop(task_index)
    except ValueError:
        print("Invalid input. Please enter a number.")

def mark_complete(tasks):
    if not tasks:
        print("No tasks available.")
        return
    view_tasks(tasks)
    try:
        task_index = int(input("Enter task number to mark as complete: ")) - 1
        if task_index < 0 or task_index >= len(tasks):
            print("Invalid task number.")
            return
        tasks[task_index].completed = True
    except ValueError:
        print("Invalid input. Please enter a number.")

def save_tasks(tasks, filename='tasks.json'):
    with open(filename, 'w') as file:
        json.dump([task.__dict__ for task in tasks], file)

def load_tasks(filename='tasks.json'):
    try:
        with open(filename, 'r') as file:
            tasks_data = json.load(file)
            return [Task(**data) for data in tasks_data]
    except FileNotFoundError:
        return []

def main():
    tasks = load_tasks()
    while True:
        print("\nTo-Do List Application")
        print("1. Add Task")
        print("2. View Tasks")
        print("3. Update Task")
        print("4. Delete Task")
        print("5. Mark Task as Complete")
        print("6. Save and Exit")
        choice = input("Enter your choice: ")
        if choice == '1':
            add_task(tasks)
        elif choice == '2':
            view_tasks(tasks)
        elif choice == '3':
            update_task(tasks)
        elif choice == '4':
            delete_task(tasks)
        elif choice == '5':
            mark_complete(tasks)
        elif choice == '6':
            save_tasks(tasks)
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()



