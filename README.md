# to-do-list
import json
import os


TASKS_FILE = 'tasks.json'

def load_tasks():
    if os.path.exists(TASKS_FILE):
        with open(TASKS_FILE, 'r') as file:
            return json.load(file)
    return []


def save_tasks(tasks):
    with open(TASKS_FILE, 'w') as file:
        json.dump(tasks, file)


def add_task(tasks):
    task = input("Enter the task: ")
    tasks.append({"task": task, "completed": False})
    save_tasks(tasks)
    print("Task added!")


def view_tasks(tasks):
    if not tasks:
        print("No tasks found!")
    else:
        for idx, task in enumerate(tasks, 1):
            status = "Done" if task["completed"] else "Not Done"
            print(f"{idx}. {task['task']} - {status}")


def update_task(tasks):
    view_tasks(tasks)
    task_no = int(input("Enter the task number to update: ")) - 1
    if 0 <= task_no < len(tasks):
        tasks[task_no]['task'] = input("Enter the new task description: ")
        tasks[task_no]['completed'] = input("Is the task completed? (yes/no): ").strip().lower() == 'yes'
        save_tasks(tasks)
        print("Task updated!")
    else:
        print("Invalid task number!")


def delete_task(tasks):
    view_tasks(tasks)
    task_no = int(input("Enter the task number to delete: ")) - 1
    if 0 <= task_no < len(tasks):
        tasks.pop(task_no)
        save_tasks(tasks)
        print("Task deleted!")
    else:
        print("Invalid task number!")


def main_menu():
    tasks = load_tasks()
    while True:
        print("\nTo-Do List Application")
        print("1. View Tasks")
        print("2. Add Task")
        print("3. Update Task")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Choose an option: ").strip()
        if choice == '1':
            view_tasks(tasks)
        elif choice == '2':
            add_task(tasks)
        elif choice == '3':
            update_task(tasks)
        elif choice == '4':
            delete_task(tasks)
        elif choice == '5':
            break
        else:
            print("Invalid choice! Please try again.")

if __name__ == "__main__":
    main_menu()
