# Tarefa de Estrutura de Dados

Repositório para a entrega da atividade de Estrutura de Dados (24/04)

## Integrantes

- Sillas Rocha da Costa
- Beatriz Miranda

# Atividade

Implementar as seguintes funções relacionadas a listas encadeadas:

- Exercício 1: Elaborar a função void insertBefore(Node*, int);
- Exercício 2: Elaborar a função void deleteNodebyValue(Node**, int);
- Exercício 3: Elaborar a função Node* searchNodebyValue(Node**, int);

# Implementações

## Exercício 1 - insertBefore

```cpp
void insertBefore(Node* ptrLocation, int iPayload) {
    if (ptrLocation == nullptr) {
        cout << "Location é NULL." << endl;
        return;
    }

    Node* newNode = createNode(iPayload); // Cria um novo nó com o payload fornecido

    // Configura os ponteiros do novo nó para inseri-lo antes de ptrLocation
    newNode->ptrNext = ptrLocation;
    newNode->ptrPrev = ptrLocation->ptrPrev;

    // Se o ptrLocation é o primeiro nó da lista
    if (ptrLocation->ptrPrev != nullptr) {
        ptrLocation->ptrPrev->ptrNext = newNode; // Atualiza o próximo do anterior para o novo nó
    }
    ptrLocation->ptrPrev = newNode; // Atualiza o anterior do ptrLocation para o novo nó
}
```

## Exercício 2 - deleteNodebyValue

```cpp
void deleteNodebyValue(Node** head, int iValue)
{
    // Faz a busca do nó
    Node* selected = searchNodebyValue(head, iValue);

    // Verifica se ele foi encontrado
    if (selected == nullptr) return;

    // Por fim, deleta o nó
    deleteNode(head, selected);
    return;
}
```

## Exercício 3 - searchNodebyValue

```cpp
Node* searchNodebyValue(Node** head, int iValue)
{
    // Verifica se a fila é vazia
    if (*head == nullptr)
    {
        cout << "Fila vazia, não foi possível achar o nó." << endl;
        return nullptr;
    }
    // Percorre a lista até encontrar o nó procurado ou chegar ao fim da fila
    Node* current = *head;
    while (current != nullptr && current->iPayload != iValue) current = current->ptrNext;
    // Verifica se não achou o nó na fila
    if (current == nullptr)
    {
        cout << "Não foi possível achar o nó de valor " << iValue << "." << endl;
        return nullptr;
    }
    // Se já foi encontrado apenas o retorna
    return current;
}
```

#### *Obs: Note que a implementação do exercício 3 foi realizada antes da implementação do exercício 2 em virtude da sua dependência, tanto da implementação do exercício 3 quando da implementação da função `deleteNode`, para que fosse evitada a repetição de código.*