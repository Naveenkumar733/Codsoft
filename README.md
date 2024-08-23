import os
from datetime import datetime

class Task:
    def __init__(self, description, due_date=None):
        self.description = description
        self.due_date = due_date
        self.completed = False
        self.created_at = datetime.now()

    def mark_complete(self):
        self.completed = True

    def mark_incomplete(self):
        self.completed = False

    def __str__(self):
        status = "Completed" if self.completed else "Pending"
        due = f", Due: {self.due_date}" if self.due_date else ""
        return f"[{status}] {self.description} (Created: {self.created_at.strftime('%Y-%m-%d %H:%M:%S')}{due})"

class ToDoApp:
    def __init__(self):
        self.tasks = []

    def add_task(self, description, due_date=None):
        task = Task(description, due_date)
        self.tasks.append(task)
        print(f"Task '{description}' added to the list.")

    def view_tasks(self):
        if not self.tasks:
            print("No tasks in the list.")
        else:
            print("Your to-do list:")
            for idx, task in enumerate(self.tasks, start=1):
                print(f"{idx}. {task}")

    def remove_task(self, task_number):
        if 0 < task_number <= len(self.tasks):
            removed_task = self.tasks.pop(task_number - 1)
            print(f"Task '{removed_task.description}' removed from the list.")
        else:
            print("Invalid task number.")

    def complete_task(self, task_number):
        if 0 < task_number <= len(self.tasks):
            self.tasks[task_number - 1].mark_complete()
            print(f"Task '{self.tasks[task_number - 1].description}' marked as complete.")
        else:
            print("Invalid task number.")

    def incomplete_task(self, task_number):
        if 0 < task_number <= len(self.tasks):
            self.tasks[task_number - 1].mark_incomplete()
            print(f"Task '{self.tasks[task_number - 1].description}' marked as incomplete.")
        else:
            print("Invalid task number.")

    def clear_tasks(self):
        self.tasks.clear()
        print("All tasks have been cleared.")

def main():
    app = ToDoApp()

    while True:
        print("\nTo-Do List Application")
        print("1. create Task")
        print("2. View Tasks")
        print("3. Remove Task")
        print("4. Mark Task as Complete")
        print("5. Mark Task as Incomplete")
        print("6. Clear All Tasks")
        print("7. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            description = input("Enter the task description: ")
            due_date = input("Enter the due date (YYYY-MM-DD) or leave blank: ")
            due_date = due_date if due_date else None
            app.add_task(description, due_date)
        elif choice == '2':
            app.view_tasks()
        elif choice == '3':
            task_number = int(input("Enter the task number to remove: "))
            app.remove_task(task_number)
        elif choice == '4':
            task_number = int(input("Enter the task number to mark as complete: "))
            app.complete_task(task_number)
        elif choice == '5':
            task_number = int(input("Enter the task number to mark as incomplete: "))
            app.incomplete_task(task_number)
        elif choice == '6':
            app.clear_tasks()
        elif choice == '7':
            print("Exiting the application.")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
