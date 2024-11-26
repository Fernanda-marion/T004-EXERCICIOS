# T004-EXERCICIOS


Exercícios - while e Do-while

EX1)

#include <stdio.h>
#include <unistd.h> 

#define TEMPERATURA_MIN 20.0
#define TEMPERATURA_MAX 25.0


void ajustarVentilacao(float temperatura) {
    if (temperatura < TEMPERATURA_MIN) {
        printf("Ventilação desligada para aquecer o ambiente.\n");
    } else if (temperatura > TEMPERATURA_MAX) {
        printf("Ventilação ligada para resfriar o ambiente.\n");
    } else {
        printf("Ventilação em modo normal.\n");
    }
}

int main() {
    float temperaturaAtual;

    printf("Iniciando monitoramento de temperatura...\n");

    while (1) {
        printf("Informe a temperatura atual (°C): ");
        scanf("%f", &temperaturaAtual);

        printf("Temperatura atual: %.2f°C\n", temperaturaAtual);

        if (temperaturaAtual < TEMPERATURA_MIN || temperaturaAtual > TEMPERATURA_MAX) {
            printf("ALERTA: Temperatura fora do intervalo seguro!\n");
        }

        ajustarVentilacao(temperaturaAtual);

       
        sleep(1);
    }

    return 0;
}


EX2)
#include <stdio.h>
#include <unistd.h> 

#define NIVEL_CRITICO 15.0
#define NIVEL_COMPLETO 100.0

int main() {
    float nivelCombustivel;

    printf("Sistema de monitoramento de nível de combustível iniciado.\n");

    while (1) {
        printf("Informe o nível de combustível atual (em %%): ");
        scanf("%f", &nivelCombustivel);

        if (nivelCombustivel < 0 || nivelCombustivel > NIVEL_COMPLETO) {
            printf("Erro: nível de combustível inválido! Informe um valor entre 0 e 100.\n");
            continue;
        }

        printf("Nível de combustível atual: %.2f%%\n", nivelCombustivel);

        if (nivelCombustivel < NIVEL_CRITICO) {
            printf("ALERTA: Nível de combustível crítico! Por favor, recarregue o veículo.\n");
        } else if (nivelCombustivel >= NIVEL_COMPLETO) {
            printf("Nível de combustível completo. Monitoramento encerrado.\n");
            break;
        } else {
            printf("Nível de combustível em estado aceitável.\n");
        }

        
        sleep(1);
    }

    return 0;
    
}

EX3)

#include <stdio.h>

#define META_PASSOS 10000

int main() {
    int passosAtuais, passosTotais = 0;

    printf("Aplicativo de monitoramento de passos iniciado.\n");
    printf("Meta diária: %d passos.\n", META_PASSOS);

    while (passosTotais < META_PASSOS) {
        printf("\nInforme a quantidade de passos dados: ");
        scanf("%d", &passosAtuais);

        if (passosAtuais < 0) {
            printf("Erro: a quantidade de passos não pode ser negativa.\n");
            continue;
        }

        passosTotais += passosAtuais;

        printf("Passos totais até o momento: %d\n", passosTotais);

        if (passosTotais >= META_PASSOS) {
            printf("Parabéns! Você atingiu ou ultrapassou a meta diária de %d passos.\n", META_PASSOS);
            break;
        } else {
            printf("Faltam %d passos para atingir a meta.\n", META_PASSOS - passosTotais);
        }
    }

    printf("\nContinue se movendo para manter a saúde em dia!\n");
    return 0;
}


EX4)


#include <stdio.h>

#define DEPOSITO_MINIMO 500.00

int main() {
    float deposito;

    printf("Bem-vindo ao sistema bancário.\n");
    printf("Para abrir uma conta, é necessário um depósito inicial mínimo de R$ %.2f.\n", DEPOSITO_MINIMO);

    while (1) {
        printf("\nInforme o valor do depósito inicial: R$ ");
        scanf("%f", &deposito);

        if (deposito >= DEPOSITO_MINIMO) {
            printf("Depósito de R$ %.2f realizado com sucesso! Conta aberta.\n", deposito);
            break;
        } else {
            printf("Erro: o valor do depósito deve ser no mínimo R$ %.2f.\n", DEPOSITO_MINIMO);
        }
    }

    return 0;
}

DESAFIO=

#include <stdio.h>
#include <math.h>
#include <stdlib.h>

#define LIMIAR_VOLATILIDADE 5.0


double calcularMedia(double *precos, int n) {
    double soma = 0.0;
    for (int i = 0; i < n; i++) {
        soma += precos[i];
    }
    return soma / n;
}


double calcularDesvioPadrao(double *precos, int n, double media) {
    double somaDesvios = 0.0;
    for (int i = 0; i < n; i++) {
        somaDesvios += pow(precos[i] - media, 2);
    }
    return sqrt(somaDesvios / n);
}

int main() {
    int numDias;
    char opcao;

    do {
        printf("Informe o número de dias que deseja analisar: ");
        scanf("%d", &numDias);

        if (numDias <= 0) {
            printf("Erro: O número de dias deve ser maior que zero.\n");
            continue;
        }

        double *precos = (double *)malloc(numDias * sizeof(double));
        if (precos == NULL) {
            printf("Erro: Falha ao alocar memória.\n");
            return 1;
        }

        printf("Informe os preços das ações para cada dia:\n");
        for (int i = 0; i < numDias; i++) {
            printf("Dia %d: R$ ", i + 1);
            scanf("%lf", &precos[i]);
        }

        
        double media = calcularMedia(precos, numDias);
        double desvioPadrao = calcularDesvioPadrao(precos, numDias, media);

        printf("\nResultados da análise:\n");
        printf("Média dos preços: R$ %.2f\n", media);
        printf("Desvio padrão: %.2f%%\n", desvioPadrao);

        if (desvioPadrao < LIMIAR_VOLATILIDADE) {
            printf("Desempenho das ações: ESTÁVEL\n");
        } else {
            printf("Desempenho das ações: VOLÁTIL\n");
        }

        free(precos);

        
        printf("\nDeseja realizar uma nova análise? (S/N): ");
        scanf(" %c", &opcao);

    } while (opcao == 'S' || opcao == 's');

    printf("Programa encerrado. Obrigado por utilizar a análise de desempenho de ações.\n");
    return 0;
}


Exercicios - Do while

EX1)

#include <stdio.h>
#include <string.h>

#define TAMANHO 10

int main() {
    int x = TAMANHO / 2, y = TAMANHO / 2; 
    char comando[10];

    printf("Bem-vindo ao controle do robô!\n");
    printf("Espaço: %dx%d metros.\n", TAMANHO, TAMANHO);
    printf("Comandos disponíveis: frente, tras, esquerda, direita, sair.\n");
    printf("O robô começa na posição (%d, %d).\n", x, y);

    while (1) {
        printf("\nInforme um comando: ");
        scanf("%s", comando);

        if (strcmp(comando, "sair") == 0) {
            printf("Encerrando o programa. Obrigado!\n");
            break;
        } else if (strcmp(comando, "frente") == 0) {
            if (y < TAMANHO - 1) {
                y++;
                printf("O robô se moveu para frente. Nova posição: (%d, %d).\n", x, y);
            } else {
                printf("Movimento inválido: o robô atingiu o limite superior.\n");
            }
        } else if (strcmp(comando, "tras") == 0) {
            if (y > 0) {
                y--;
                printf("O robô se moveu para trás. Nova posição: (%d, %d).\n", x, y);
            } else {
                printf("Movimento inválido: o robô atingiu o limite inferior.\n");
            }
        } else if (strcmp(comando, "esquerda") == 0) {
            if (x > 0) {
                x--;
                printf("O robô se moveu para a esquerda. Nova posição: (%d, %d).\n", x, y);
            } else {
                printf("Movimento inválido: o robô atingiu o limite esquerdo.\n");
            }
        } else if (strcmp(comando, "direita") == 0) {
            if (x < TAMANHO - 1) {
                x++;
                printf("O robô se moveu para a direita. Nova posição: (%d, %d).\n", x, y);
            } else {
                printf("Movimento inválido: o robô atingiu o limite direito.\n");
            }
        } else {
            printf("Comando inválido! Por favor, insira um comando válido.\n");
        }
    }

    return 0;
}



EX2)

#include <time.h>

#define DISTANCIA_LIMITE 10.0

// Função para simular a leitura do sensor
double lerSensor() {
    // Simula uma distância aleatória entre 5 e 50 cm
    return 5.0 + (rand() % 4600) / 100.0;
}

int main() {
    double distancia;
    char continuar;

    printf("Sistema de leitura do sensor de distância iniciado.\n");
    printf("O programa será encerrado automaticamente ao detectar uma distância menor que %.2f cm.\n", DISTANCIA_LIMITE);

    srand(time(NULL)); 

    do {
        distancia = lerSensor();
        printf("Distância medida: %.2f cm\n", distancia);

        if (distancia < DISTANCIA_LIMITE) {
            printf("Alerta: Distância abaixo de %.2f cm! Encerrando o programa.\n", DISTANCIA_LIMITE);
            break;
        }

        printf("Deseja continuar a leitura? (S/N): ");
        scanf(" %c", &continuar);

    } while (continuar == 'S' || continuar == 's');

    printf("Leitura do sensor encerrada.\n");
    return 0;
}


EX3)

#include <stdio.h>

int main() {
    int opcao;

    printf("Controle de Atuação do Robô\n");
    printf("=================================\n");
    printf("Selecione uma ação para o robô:\n");
    printf("1. Ligar uma lâmpada\n");
    printf("2. Tocar um som\n");
    printf("3. Mover um braço\n");
    printf("4. Encerrar o programa\n");

    do {
        printf("\nInforme sua escolha (1-4): ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                printf("O robô ligou uma lâmpada.\n");
                break;
            case 2:
                printf("O robô tocou um som.\n");
                break;
            case 3:
                printf("O robô moveu um braço.\n");
                break;
            case 4:
                printf("Encerrando o programa. Obrigado por usar o controle do robô!\n");
                break;
            default:
                printf("Opção inválida. Por favor, selecione uma opção válida (1-4).\n");
                break;
        }
    } while (opcao != 4);

    return 0;
}

EX4)

#include <stdio.h>

int main() {
    float nivelBateria;

    printf("Sistema de Monitoramento de Bateria do Robô\n");
    printf("===========================================\n");

    do {
        printf("\nInforme o nível de bateria atual (em %%): ");
        scanf("%f", &nivelBateria);

        if (nivelBateria <= 20.0) {
            printf("Atenção: Bateria baixa! O nível está em %.2f%%.\n", nivelBateria);
            printf("Recarregue o robô o mais rápido possível.\n");
        } else {
            printf("Bateria suficiente. Nível atual: %.2f%%.\n", nivelBateria);
        }

    } while (nivelBateria <= 20.0);

    printf("\nO robô possui bateria suficiente agora. Monitoramento encerrado.\n");

    return 0;
}

EX5)

#include <stdio.h>
#include <string.h>

#define GRID_SIZE 5

int main() {
    int x = 2, y = 2;  // Posição inicial do robô no centro do grid 5x5
    char comando[10];

    printf("Simulação de Navegação Autônoma do Robô\n");
    printf("Grid de %dx%d. Posição inicial: (%d, %d)\n", GRID_SIZE, GRID_SIZE, x, y);

    do {
        printf("\nComandos disponíveis: cima, baixo, esquerda, direita, parar\n");
        printf("Informe o comando: ");
        scanf("%s", comando);

        
        if (strcmp(comando, "cima") == 0) {
            if (x > 0) {
                x--;
                printf("Robô moveu para cima. Nova posição: (%d, %d)\n", x, y);
            } else {
                printf("Erro: o robô não pode se mover para fora do grid.\n");
            }
        } else if (strcmp(comando, "baixo") == 0) {
            if (x < GRID_SIZE - 1) {
                x++;
                printf("Robô moveu para baixo. Nova posição: (%d, %d)\n", x, y);
            } else {
                printf("Erro: o robô não pode se mover para fora do grid.\n");
            }
        } else if (strcmp(comando, "esquerda") == 0) {
            if (y > 0) {
                y--;
                printf("Robô moveu para a esquerda. Nova posição: (%d, %d)\n", x, y);
            } else {
                printf("Erro: o robô não pode se mover para fora do grid.\n");
            }
        } else if (strcmp(comando, "direita") == 0) {
            if (y < GRID_SIZE - 1) {
                y++;
                printf("Robô moveu para a direita. Nova posição: (%d, %d)\n", x, y);
            } else {
                printf("Erro: o robô não pode se mover para fora do grid.\n");
            }
        } else if (strcmp(comando, "parar") == 0) {
            printf("Robô parou. Encerrando a simulação.\n");
            break;
        } else {
            printf("Comando inválido. Por favor, insira um comando válido.\n");
        }

    } while (1);

    return 0;
}

DEESAFIO 2 = ......

Exercícios práticos usando Arduino e conceitos de estrutura de re-
petição

1) int cameraData[10];

2) cameraData[3] = analogRead(A1);

3)A forma de representação : float temperaturas[5] = {25.5, 26.0, 24.8, 27.3, 26.5}; Estamos 5 valores e esses valores estão presentes na chave










