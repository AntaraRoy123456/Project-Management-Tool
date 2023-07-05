# Project-Management-Tool
It is a basic code structure for a project management tool that includes a framework for social media sites and task assignment functionality.

class User:
    def __init__(self, name):
        self.name = name
        self.tasks = []

    def assign_task(self, task, assignee):
        assignee.tasks.append(task)
        print(f"Task '{task}' assigned to {assignee.name}.")

class Task:
    def __init__(self, description):
        self.description = description
        self.assignee = None

    def assign(self, assignee):
        self.assignee = assignee
        assignee.tasks.append(self)
        print(f"Task '{self.description}' assigned to {assignee.name}.")

class ProjectManagementTool:
    def __init__(self):
        self.users = []

    def create_user(self, name):
        user = User(name)
        self.users.append(user)
        print(f"User '{user.name}' created.")

    def create_task(self, description):
        task = Task(description)
        print(f"Task '{task.description}' created.")
        return task

    def assign_task(self, task, assignee_name):
        assignee = next((user for user in self.users if user.name == assignee_name), None)
        if assignee:
            assignee.assign_task(task, assignee)
        else:
            print(f"User '{assignee_name}' not found.")

# Example usage
project_management_tool = ProjectManagementTool()

project_management_tool.create_user("Alice")
project_management_tool.create_user("Bob")
project_management_tool.create_user("Charlie")

task1 = project_management_tool.create_task("Implement login functionality")
task2 = project_management_tool.create_task("Design user profile page")
task3 = project_management_tool.create_task("Write API documentation")

project_management_tool.assign_task(task1, "Bob")
project_management_tool.assign_task(task2, "Charlie")
project_management_tool.assign_task(task3, "Alice")

alice = next((user for user in project_management_tool.users if user.name == "Alice"), None)
if alice:
    print(f"Tasks assigned to Alice: {', '.join(task.description for task in alice.tasks)}")

