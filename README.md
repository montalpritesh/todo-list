# todo-list
This is repository for todo list using react
import os

FILENAME = "tasks.txt"

def load_tasks():
    """Load tasks from file."""
    if not os.path.exists(FILENAME):
        return []
    with open(FILENAME, "r") as f:
        return [line.strip() for line in f.readlines()]

def save_tasks(tasks):
    """Save tasks to file."""
    with open(FILENAME, "w") as f:
        for task in tasks:
            f.write(task + "\n")

def show_tasks(tasks):
    """Display all tasks."""
    if not tasks:
        print("\n✅ No tasks yet!")
        return
    print("\n📋 Your Tasks:")
    for i, task in enumerate(tasks, start=1):
        print(f"{i}. {task}")

def add_task(tasks):
    """Add a new task."""
    task = input("\nEnter new task: ").strip()
    if task:
        tasks.append(task)
        print("✅ Task added!")
    else:
        print("⚠️ Empty task not added.")

def remove_task(tasks):
    """Remove a task by number."""
    show_tasks(tasks)
    try:
        num = int(input("\nEnter task number to remove: "))
        if 1 <= num <= len(tasks):
            removed = tasks.pop(num - 1)
            print(f"🗑️ Removed: {removed}")
        else:
            print("⚠️ Invalid task number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def main():
    tasks = load_tasks()

    while True:
        print("\n--- TO-DO LIST MENU ---")
        print("1. View tasks")
        print("2. Add task")
        print("3. Remove task")
        print("4. Save & Exit")

        choice = input("Choose an option (1-4): ").strip()

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            remove_task(tasks)
        elif choice == "4":
            save_tasks(tasks)
            print("💾 Tasks saved. Goodbye!")
            break
        else:
            print("⚠️ Invalid choice. Try again.")

if __name__ == "__main__":
    main()