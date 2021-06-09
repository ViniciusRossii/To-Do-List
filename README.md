# To Do List
Lista de afazeres para gerenciar suas tarefas.
***
# Explicação dos Códigos

### Adicionar Tarefa
Assim que o evento é disparado, um prompt é exibido para inserir a tarefa. Após o tratamento do texto, o elemento é criado.
```
add.addEventListener('click', () => { // Adicionar Tarefa
    taskName = prompt('Insira o nome da tarefa:')
    // Tratando Dados
    if (taskName == null) {
        alert("Insira um nome válido.")
        return
    }
    taskName = taskName.trim()
    if (taskName.length == 0) {
        alert("Insira um nome válido.")
        return
    }
    else if (taskName.length > 40) {
        alert("Insira um nome de até 40 caracteres.")
        return
    }
    // Criando Tarefa
    const task = document.createElement('li')
    task.innerHTML = `${tasks.length + 1}. ${taskName}`
    tasks.push(taskName)
    localStorage.setItem('tasks', JSON.stringify(tasks))
    ul.appendChild(task)
})
```

### Editar Tarefa
Assim que o evento é disparado, dois prompts são exibidos. Caso o usuário tenha inserido os dados corretamente, o valor é editado e todas as tarefas são recarregadas.
```
edit.addEventListener('click', () => { // Editando Tarefa
    if (ul.childElementCount == 0) {
        alert("Sem tarefas adicionadas.")
        return
    }
    whatEdit = prompt("Insira o número da tarefa que você deseja editar:")
    // Tratando Dados
    if (whatEdit == null) {
        alert("Insira um número válido.")
        return
    }
    whatEdit = whatEdit.trim()
    if (whatEdit.length == 0) {
        alert("Insira um número válido.")
    }
    else if (isNaN(whatEdit) == true || whatEdit == 0) {
        alert("Insira um número válido.")
        return
    }
    else if (whatEdit > ul.childElementCount) {
        alert("Insira um número válido.")
    }
    newName = prompt("Insira o novo nome:")
    if (newName == null) {
        alert("Insira um nome válido.")
        return
    }
    newName = newName.trim()
    if (newName.length == 0) {
        alert("Insira um nome válido.")
        return
    }
    else if (newName.length > 40) {
        alert("Insira um nome de até 40 caracteres.")
        return
    }
    tasks[whatEdit - 1] = newName
    localStorage.setItem('tasks', JSON.stringify(tasks)) // Salvando
    loadTasks() // Recarregando
})
```
### Load Tasks
Load Tasks é a função que carrega todas as tarefas salvas no localStorage.
```
function loadTasks() {
    if (localStorage.getItem('tasks') == null) return // Caso não tenha nada salvo, não carregar nada
    ul.innerHTML = "" // Removendo todas as tarefas já carregadas
    tasks = JSON.parse(localStorage.getItem('tasks')) // Pegando informações do localStorage
    for (var c = 0; c < tasks.length; c++) { // Gerando todas as tasks salvas no Array
        const savedLi = document.createElement('li')
        ul.appendChild(savedLi)
        setTaskName(savedLi, c)
    }
}
```
### Excluir Tarefa
Assim que o evento é disparado, um prompt será exibido esperando o input com o número da tarefa. Caso o número seja válido, a tarefa em questão será excluída.
```
del.addEventListener('click', () => { // Removendo Tarefa
    if (ul.childElementCount == 0) {
        alert("Sem tarefas adicionadas.")
        return
    }
    whatDelete = prompt('Insira o número da tarefa que você deseja remover:')
    // Tratando Dados
    if (whatDelete == null) {
        alert("Insira um número válido.")
        return
    }
    whatDelete = whatDelete.trim()
    if (whatDelete.length == 0) {
        alert("Insira um número válido.")
        return
    }
    else if (isNaN(whatDelete) == true || whatDelete == 0) {
        alert("Insira um número válido.")
        return
    }
    else if (whatDelete > ul.childElementCount) {
        alert("Insira um número válido.")
    }
    tasks.splice(whatDelete - 1, 1) // Removendo Tarefa da Array
    localStorage.setItem('tasks', JSON.stringify(tasks)) // Salvando
    loadTasks() // Recarregando
})
```
### Excluir todas as tarefas
Assim que o evento é disparado, um confirm é exibido. Caso seja confirmado, todas as tarefas serão removidas.
```
deleteALl.addEventListener('click', () => {
    if (ul.childElementCount == 0) {
        alert("Sem tarefas adicionadas.")
        return
    }
    const areUSure = confirm("Deseja apagar todas as tarefas?")
    if (areUSure == false) {
        return
    }
    tasks = []
    localStorage.setItem('tasks', JSON.stringify(tasks)) // Salvando
    loadTasks() // Recarregando
})
```
***
## Aparência
![aparencia](https://user-images.githubusercontent.com/67524727/121366994-4f2de680-c910-11eb-9e7a-33eefcae43dc.png)
***
##### Feito por Vinicius Rossi.