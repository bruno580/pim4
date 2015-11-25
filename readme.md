	
	#include <stdio.h>
	#include <string.h>
	#include <stdlib.h>
	// Variaveis globais para guardar os assentos dos passageiros, independente de onde sejam chamadas as variaveis
	int bus001[50]={0},bus002[50]={0},bus003[50]={0},bus004[50]={0};
	
	// Estrutura para armazenar os dados
	typedef struct passagem{
		int cod_onibus, assento;
		char nome[67], destino[20], horario[8];
		int idade;
		char estudante[2]; // S ou N pra validar se é estudante
		float valor;
		struct passagem * proximo;
	} Passagem;
	
	// Função para iniciar a lista apontando para NULL
	Passagem* inicia(){
		return NULL;
	}
	
	// Função que determina a tarifação do sistema
	Tarifa (int cod_onibus, float desconto){
		float valor;
		if (cod_onibus == 001)(valor=68.00); // Se destino for Campinas -> Santos atribui o preço de R$ 68.00
		if (cod_onibus == 002)(valor=49.00); // Se destino for Campinas -> Sao Paulo, atribui o preço de R$ 49.00
		if (cod_onibus == 003)(valor=78.00); // Se destino for Campinas -> Minas Gerais, atribui o preço de R$ 78.00
		if (cod_onibus == 004)(valor=17.00); // Se destino for Campinas -> Jaguariuna, atribui o preço de R$ 17.00
		valor=valor*desconto; // Atribui desconto se aplicavel.
		return valor;
	}
	
	// Função que busca o assento na hora da venda, para evitar que duas pessoas ocupem a mesma poltrona
	int buscaAssento(int onibus[50]){
		int i=1;
		while ( onibus[i] != 0 ) {
	 	   		i++;
			};
 			onibus[i]=i;
 		return onibus[i];
	}
	
	Passagem* exibe(Passagem* lista){
		Passagem* aux;
		for (aux = lista; aux != NULL; aux = aux->proximo){
			printf("\n---------------------- Passagem ------------------------\n");
			printf("Codigo do Onibus: 00%d | Assento: %d \n", aux->cod_onibus, aux->assento);
			printf("Destino.......: %s \n", aux->destino);
			printf("Passageiro....: %s", aux->nome);
			printf("Idade.........: %d \n", aux->idade);
			printf("Estudante.....: %s \n", aux->estudante);
			printf("Preco total: R$ %3.2f", aux->valor);
			printf("\n--------------------------------------------------------\n");
		}
	return lista;
	}
	
	Passagem* fechaCaixa(Passagem* lista){
		int contador=0;
		float saldo=0;
		Passagem* aux;
		for (aux = lista; aux != NULL; aux = aux->proximo){
			saldo=saldo+aux->valor;
			contador++;
		}
		printf("\n--------------- Resumo Financeiro ---------------------\n\n");
		printf("Quantidade de passagens vendidas: %d \n", contador);
		printf("Valor total das vendas..........: R$ %3.2f \n", saldo);
		printf("\n--------------------------------------------------------\n");
	}	
	
	// Função principal para venda de passagens.
	// Cria um novo nó na lista ligada usando a estrutura definida da linha 6 a 13.
	Passagem* insere(Passagem* lista, int cod_onibus){
		char estudante_aux[2]; 
		float desconto=1;
		// Cria novo nó e aloca a memória dinamicamente
		Passagem* nova_passagem = (Passagem*)malloc(sizeof(Passagem));
		// Atribui os valores do novo nó
		nova_passagem->cod_onibus = cod_onibus;
		printf("Nome do passageiro.....: ");
		fgets(nova_passagem->nome,16,stdin);
		fflush(stdin);
		printf("Idade..................: ");
		scanf("%d", &nova_passagem->idade);
		fflush(stdin);
		printf("Estudante? (S/N).......: ");
		fgets(estudante_aux,2,stdin);
		fflush(stdin);
		strcpy(nova_passagem->estudante,estudante_aux);
		if (*estudante_aux == 'S')(desconto=0.5);
		nova_passagem->valor = Tarifa(cod_onibus,desconto);
		if (cod_onibus == 001) {
			nova_passagem->assento=buscaAssento(bus001);
			strcpy(nova_passagem->destino,"Santos");
			strcpy(nova_passagem->horario,"10:00hrs");
		}
		if (cod_onibus == 002) {
			nova_passagem->assento=buscaAssento(bus002);
			strcpy(nova_passagem->destino,"Sao Paulo");
			strcpy(nova_passagem->horario,"10:45hrs");
		}
		if (cod_onibus == 003) {
			nova_passagem->assento=buscaAssento(bus003);
			strcpy(nova_passagem->destino,"Minas Gerais");
			strcpy(nova_passagem->horario,"11:30hrs");
		}
		if (cod_onibus == 004) {
			nova_passagem->assento=buscaAssento(bus004);
			strcpy(nova_passagem->destino,"Jaguariuna");
			strcpy(nova_passagem->horario,"13:00hrs");
		}
		nova_passagem->proximo = lista;
		// Exibe informações da venda na tela
		system("cls");
		printf("\nVenda concluida com exito, a passagem sera exibida a seguir.\n");
			printf("\n---------------------- Passagem ------------------------\n");
			printf("Codigo do Onibus: 00%d | Assento: %d \n", nova_passagem->cod_onibus, nova_passagem->assento);
			printf("Destino.......: %s | Horario de partida: %s \n", nova_passagem->destino, nova_passagem->horario);
			printf("Passageiro....: %s", nova_passagem->nome);
			printf("Idade.........: %d \n", nova_passagem->idade);
			printf("Estudante.....: %s \n", nova_passagem->estudante);
			printf("Preco total: R$ %3.2f", nova_passagem->valor);
			printf("\n--------------------------------------------------------\n");
		return nova_passagem;
	}
	
	// Função que exibe o itinerário e quantidade de poltronas disponiveis
	void itinerario(int bus001[],int bus002[],int bus003[],int bus004[]){
		int vagas1=0, vagas2=0, vagas3=0, vagas4=0, i;
		for( i = 1; i <= 50; i++ ) {
  			if( bus001[i] == 0 ) {
	 		vagas1++;
  			}
	 };
	 for( i = 1; i <= 50; i++ ) {
  			if( bus002[i] == 0 ) {
	 		vagas2++;
  			}
	 };
	 for( i = 1; i <= 50; i++ ) {
	 		if( bus003[i] == 0 ) {
		 		vagas3++;
  			}
    	};
	 for( i = 1; i <= 50; i++ ) {
  			if( bus004[i] == 0 ) {
	 		vagas4++;
  			}
	    };
		printf("Onibus 001: \n Origem: Campinas / Destino: Santos \n Horario de saida: 10:00 / Assentos disponiveis: %d\n\n",vagas1);
		printf("Onibus 002: \n Origem: Campinas / Destino: Sao Paulo \n Horario de saida: 10:45 / Assentos disponiveis: %d\n\n",vagas2);
		printf("Onibus 003: \n Origem: Campinas / Destino: Minas Gerais \n Horario de saida: 11:30 / Assentos disponiveis: %d\n\n",vagas3);
		printf("Onibus 004: \n Origem: Campinas / Destino: Jaguariuna \n Horario de saida: 13:00 / Assentos disponiveis: %d\n\n",vagas4);
	}
	
	// Main
	int main(){
		// Variaveis
		int operador;
		float desconto=1; // Sera atribuido 0.5 em caso de estudante, 0 em caso de Idoso (até 2 passagens) senão for nem estudante nem idoso será 1.
		Passagem* lista;
		lista = inicia();
		int onibus,assento,i;
		int cod_onibus;
		
		// Menu interativo
		while (operador!=4)
		{
			system("cls");
			printf("***** Sistema de venda de passagens ******\n\n");
			printf("Menu principal\n\n");
			printf("1 - Vender passagem \n");
			printf("2 - Consultar vendas \n");
			printf("3 - Consultar Itinerario \n");
			printf("4 - Fechar caixa e sair \n");
			scanf("%d",&operador);
		switch (operador)
			{
				case 1:
				{
					system("cls");
					printf("***** Iniciando venda de passagem *****\n\n");
					printf("\n\nObserve o Itinerario e selecione um destino\n");
					itinerario(bus001,bus002,bus003,bus004);
					printf("\n\nInforme o codigo do Onibus desejado: ");
					scanf("%d", &onibus);
					fflush(stdin);
					system("cls");
					if (onibus == 001 || onibus == 002 || onibus == 003 || onibus == 004)(
						lista = insere(lista, onibus)
					); 
					else (
						printf("\nERRO: Numero invalido... venda cancelada.\n\n")
						);
					system("pause");
					break;
				}
				case 2:
				{
					system("cls");
					printf("***** Exibindo vendas do dia ******\n\n");
					lista = exibe(lista);
					system("pause");
					break;
				}
				case 3:
				{
					system("cls");
					printf("****** Consultar Itinerario *******\n\n");
					itinerario(bus001,bus002,bus003,bus004);
					system("pause");
					break;
				}
				case 4:
				{
				// Apenas dá um break para sair do case, fechar o caixa e sair do programa
				break;
				}
				default:
					printf("Opcao invalida!");
			}
		}
		system("cls");
		printf("****** Fechamento de caixa ******\n\n");
		fechaCaixa(lista);
		system("pause");
		return 0;
	}