#include <stdio.h>
#include <stdlib.h>
#include <locale.h>


struct Cliente {
    char nome[100];
    char cpf[15];
    int tipoAtendimento;
};



void cadastrarAtendimento(struct Cliente atendimentos[], int *contador) {
    struct Cliente novoCliente;

    printf("Digite o nome do cliente: ");
    fgets(novoCliente.nome, sizeof(novoCliente.nome), stdin);
    novoCliente.nome[strcspn(novoCliente.nome, "\n")] = '\0';

    printf("Digite o CPF do cliente: ");
    fgets(novoCliente.cpf, sizeof(novoCliente.cpf), stdin);
    novoCliente.cpf[strcspn(novoCliente.cpf, "\n")] = '\0'; 
	
	system("pause");
  
    printf("Escolha o tipo de atendimento:\n");
    printf("1 - Abertura de Conta.\n");
    printf("2 - Caixa.\n");
    printf("3 - Gerente Pessoa Física.\n");
    printf("4 - Gerente Pessoa Jurídica.\n");
    printf("Opção: ");
    scanf("%d", &novoCliente.tipoAtendimento);
	fflush(stdin);
	
    atendimentos[*contador] = novoCliente;
    (*contador)++;

    printf("Atendimento cadastrado com sucesso!\n");
    system("cls");
    
}


void listarAtendimentos(struct Cliente atendimentos[], int contador) {
    for (int i = 0; i < contador; i++) {
        printf("Nome: %s\n", atendimentos[i].nome);
        printf("CPF: %s\n", atendimentos[i].cpf);
        printf("Tipo Atendimento - %d - ", atendimentos[i].tipoAtendimento);

        switch (atendimentos[i].tipoAtendimento) {
            case 1:
                printf("1 - Abertura de Conta.\n");
                break;
            case 2:
                printf("2 - Caixa.\n");
                break;
            case 3:
                printf("3 - Gerente Pessoa Física.\n");
                break;
            case 4:
                printf("4 - Gerente Pessoa Jurídica.\n");
                break;
            default:
                printf("Tipo de Atendimento Inválido.");
        }

        printf("\n===============================\n");
    }
	
	system("pause");
    
}


void listarAtendimentoPorSetor(struct Cliente atendimentos[], int contador) {
    int tipoAtendimento;

    printf("Escolha o tipo de atendimento para listar:\n");
    printf("1 - Abertura de Conta\n");
    printf("2 - Caixa\n");
    printf("3 - Gerente Pessoa Física\n");
    printf("4 - Gerente Pessoa Jurídica\n");
    printf("Opção: ");
    scanf("%d", &tipoAtendimento);
    fflush(stdin);

    printf("\nListagem do tipo de atendimento escolhido:\n");

    for (int i = 0; i < contador; i++) {
        if (atendimentos[i].tipoAtendimento == tipoAtendimento) {
        	printf("===============================\n");
            printf("Nome: %s\n", atendimentos[i].nome);
            printf("CPF: %s\n", atendimentos[i].cpf);
            printf("Tipo Atendimento - %d\n", atendimentos[i].tipoAtendimento);
            printf("===============================\n");
        }
    }

    system("pause");
}

int main() {
    setlocale(LC_ALL, "Portuguese");

    struct Cliente atendimentos[100];  // Capacidade para 100 atendimentos
    int contador = 0;
    int escolha;

    do {
        printf("\nBem-vindo ao sistema de atendimento\n");
        printf("1 - Solicitar Atendimento\n");
        printf("2 - Listar Atendimentos Registrados\n");
        printf("3 - Listar Atendimento por Setor\n");
        printf("4 - Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &escolha);
        fflush(stdin);

        switch (escolha) {
            case 1:
                cadastrarAtendimento(atendimentos, &contador);
                break;
            case 2:
                listarAtendimentos(atendimentos, contador);
                break;
            case 3:
                listarAtendimentoPorSetor(atendimentos, contador);
                break;
            case 4:
                printf("Encerrando Atendimento!\n");
                break;
            default:
                printf("Opção inválida. Tente novamente.\n");
        }

    } while (escolha != 4);

    return 0;
}
