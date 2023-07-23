
//
#include <iostream>
#include <string>
struct Pessoa {
    std::string nome;
    std::string endereco;
    std::string cpf;
    int idade;
    Pessoa* prox;
};
struct Fila {
    Pessoa* inicio;
    Pessoa* fim;
};
Fila filas[5];
bool filaVazia(const Fila& fila) {
    return (fila.inicio == nullptr);
}
void inicializarFila(Fila& fila) {
    fila.inicio = nullptr;
    fila.fim = nullptr;
}
void enfileirar(Fila& fila, const Pessoa& pessoa) {
    Pessoa* novoNo = new Pessoa;
    novoNo->nome = pessoa.nome;
    novoNo->endereco = pessoa.endereco;
    novoNo->cpf = pessoa.cpf;
    novoNo->idade = pessoa.idade;
    novoNo->prox = nullptr;
    if (filaVazia(fila)) {
        fila.inicio = novoNo;
    } else {
        fila.fim->prox = novoNo;
    }
    fila.fim = novoNo;
}
Pessoa desenfileirar(Fila& fila) {
    if (filaVazia(fila)) {
        throw std::runtime_error("Fila vazia. Não é possível desenfileirar.");
    }
    Pessoa* noRemovido = fila.inicio;
    Pessoa pessoaRemovida = *noRemovido;
    fila.inicio = fila.inicio->prox;
    delete noRemovido;
    if (fila.inicio == nullptr) {
        fila.fim = nullptr;
    }
    return pessoaRemovida;
}
void mostrarFila(const Fila& fila) {
    if (filaVazia(fila)) {
        std::cout << "Fila vazia." << std::endl;
        return;
    }
    Pessoa* noAtual = fila.inicio;
    while (noAtual != nullptr) {
        Pessoa pessoa = *noAtual;
        std::cout << "Nome: " << pessoa.nome << std::endl;
        std::cout << "Endereço: " << pessoa.endereco << std::endl;
        std::cout << "CPF: " << pessoa.cpf << std::endl;
        std::cout << "Idade: " << pessoa.idade << std::endl;
        std::cout << "-" << std::endl;
        noAtual = noAtual->prox;
    }
}
int obterOpcao() {
    int opcao;
    std::cout << "Menu:" << std::endl;
    std::cout << "1) Cadastro de paciente" << std::endl;
    std::cout << "2) Fila da semana" << std::endl;
    std::cout << "3) Tirar vacinado e atualizar fila" << std::endl;
    std::cout << "4) Sair" << std::endl;
    std::cout << "Selecione uma opção: ";
    std::cin >> opcao;
    while (std::cin.fail() || opcao < 1 || opcao > 4) {
        std::cin.clear();
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Opção inválida. Digite um número válido: ";
        std::cin >> opcao;
    }
    return opcao;
}
void cadastrarPaciente() {
    Pessoa pessoa;
    std::cout << "Nome: ";
    std::cin >> pessoa.nome;
    std::cout << "Endereço: ";
    std::cin >> pessoa.endereco;
    std::cout << "CPF: ";
    std::cin >> pessoa.cpf;
    std::cout << "Idade: ";
    std::cin >> pessoa.idade;
    if (pessoa.idade >= 5) {
        int dia;
        std::cout << "Digite o dia da semana (1 a 5): ";
        std::cin >> dia;
        while (std::cin.fail() || dia < 1 || dia > 5) {
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            std::cout << "Dia inválido. Digite um número válido: ";
            std::cin >> dia;
        }
        enfileirar(filas[dia - 1], pessoa);
        std::cout << "Pessoa cadastrada com sucesso." << std::endl;
    } else {
        std::cout << "Apenas pessoas com 5 anos ou mais podem ser cadastradas." << std::endl;
    }
}
void tirarVacinado() {
    int dia;
    std::cout << "Digite o dia da semana (1 a 5): ";
    std::cin >> dia;
    while (std::cin.fail() || dia < 1 || dia > 5) {
        std::cin.clear();
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Dia inválido. Digite um número válido: ";
        std::cin >> dia;
    }
    try {
        Pessoa pessoaVacinada = desenfileirar(filas[dia - 1]);
        std::cout << "Primeira pessoa da fila do dia " << dia << ":" << std::endl;
        std::cout << "Nome: " << pessoaVacinada.nome << std::endl;
        std::cout << "Endereço: " << pessoaVacinada.endereco << std::endl;
        std::cout << "CPF: " << pessoaVacinada.cpf << std::endl;
        std::cout << "Idade: " << pessoaVacinada.idade << std::endl;
    } catch (const std::exception& e) {
        std::cout << e.what() << std::endl;
    }
}
void mostrarFila() {
    int dia;
    std::cout << "Digite o dia da semana (1 a 5): ";
    std::cin >> dia;
    while (std::cin.fail() || dia < 1 || dia > 5) {
        std::cin.clear();
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
        std::cout << "Dia inválido. Digite um número válido: ";
        std::cin >> dia;
    }
    std::cout << "Fila do dia " << dia << ":" << std::endl;
    mostrarFila(filas[dia - 1]);
}
int main() {
    for (int i = 0; i < 5; i++) {
        inicializarFila(filas[i]);
    }
    int opcao;
    do {
        opcao = obterOpcao();
        switch (opcao) {
            case 1:
                cadastrarPaciente();
                break;
            case 2:
                mostrarFila();
                break;
            case 3:
                tirarVacinado();
                break;
            case 4:
                std::cout << "Saindo do programa.." << std::endl;
                break;
            default:
                std::cout << "Opção inválida." << std::endl;
                break;
        }
        std::cout << "----------------------" << std::endl;
    } while (opcao != 4);
    return 0;
}
