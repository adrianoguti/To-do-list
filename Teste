import json
import datetime

class Task:
    def __init__(self, description, due_date=None):
        self.description = description
        self.completed = False
        self.due_date = due_date

    def mark_as_completed(self):
        self.completed = True

    def set_due_date(self, due_date):
        self.due_date = due_date

    def __str__(self):
        status = "Concluída" if self.completed else "Pendente"
        return f"{self.description} - {status}"


class ToDoList:
    def __init__(self, filename):
        self.tasks = []
        self.filename = filename

    def load_tasks(self):
        try:
            with open(self.filename, "r") as file:
                data = json.load(file)
                for task_data in data:
                    description = task_data["description"]
                    completed = task_data["completed"]
                    due_date = datetime.datetime.strptime(task_data["due_date"], "%Y-%m-%d").date()
                    task = Task(description, due_date)
                    task.completed = completed
                    self.tasks.append(task)
        except FileNotFoundError:
            print("Arquivo de tarefas não encontrado. Será criado um novo arquivo.")

    def save_tasks(self):
        data = []
        for task in self.tasks:
            task_data = {
                "description": task.description,
                "completed": task.completed,
                "due_date": task.due_date.strftime("%Y-%m-%d") if task.due_date else None
            }
            data.append(task_data)
        with open(self.filename, "w") as file:
            json.dump(data, file, indent=4)

    def add_task(self, description, due_date=None):
        task = Task(description, due_date)
        self.tasks.append(task)
        print("Tarefa adicionada com sucesso!")
        self.save_tasks()

    def view_tasks(self):
        if not self.tasks:
            print("Não há tarefas na lista.")
        else:
            print("Lista de Tarefas:")
            for index, task in enumerate(self.tasks):
                print(f"{index + 1}. {task}")

    def mark_task_as_completed(self, index):
        if index < 1 or index > len(self.tasks):
            print("Índice inválido!")
        else:
            task = self.tasks[index - 1]
            task.mark_as_completed()
            print("Tarefa marcada como concluída!")
            self.save_tasks()

    def set_task_due_date(self, index, due_date):
        if index < 1 or index > len(self.tasks):
            print("Índice inválido!")
        else:
            task = self.tasks[index - 1]
            task.set_due_date(due_date)
            print("Data de vencimento definida para a tarefa!")
            self.save_tasks()


# Exemplo de uso
todo_list = ToDoList("tasks.json")
todo_list.load_tasks()

while True:
    print("\n===== Menu =====")
    print("1. Adicionar tarefa")
    print("2. Visualizar tarefas")
    print("3. Marcar tarefa como concluída")
    print("4. Definir data de vencimento para tarefa")
    print("5. Sair")

    choice = input("Escolha uma opção: ")

    if choice == "1":
        description = input
