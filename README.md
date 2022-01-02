#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include<time.h>
#define  MAX_DADORES 500
#define  MAX_RECOLHAS 500
#define MAX_CIDADES 14
#define MAX_CONCELHOS 5

typedef struct dt
{
    int dia;
    int mes;
    int ano;

} data_tipo;

typedef struct
{
    int num; //Numero do Dador (formato inclui os 6 primeiros digitos: DDDDDD)
    char nome[26];  //Nome do dadorente (maximo 25 carateres uteis)
    data_tipo dt;   //Data de nascimento (formato obrigatorio: DD-MM-AAAA)
    float peso;
    int numero_de_dadivas;
    char tipo_sanguineo [3];
    char rh;   //Rh ('+' ou '-')
} dador_tipo;

int procurar_dador (dador_tipo dador[], int num, int qtdDADORES)
{
    fflush(stdin);

    for (int i = 0; i < qtdDADORES; i++)
    {
        if (dador[i].num == num)
        {
            return i;
        }
    }
    return -1;
}

int validar_data(int dia, int mes, int ano)
{
    int m[13];
    if(mes > 0 && mes < 13)
    {
        m[1] = 32;  //janeiro
        m[2] = 29;  //fevereiro
        m[3] = 32;  //março
        m[4] = 31;  //abril
        m[5] = 32;  //maio
        m[6] = 31;  //junho
        m[7] = 32;  //julho
        m[8] = 32;  //agosto
        m[9] = 31;  //setembro
        m[10]= 32;  //outubro
        m[11]= 31;  //novembro
        m[12]= 32;  //dezembro
        if(((((ano%400)==0)||((ano%100)!=0))
                &&((ano%4)==0)))                 //verifica se o ano é bissexto
            m[2]+=1;                         //se o ano for bissexto fevereiro tem mais um dia
        if(dia > 0  && dia < m[mes] && ano>1900 && ano<2100)         //verifica se o dia do mes é válido e se o ano é válido
            return 1;
        else
            return 0;
    }
    else
        return 0;
}

void inicializar_dadores(dador_tipo dador[], int *qtdDADORES) // Insere 5 dadores, assim quando corremos o programa já tem 5 dadores
{
    dador[0].num=111111;
    strcpy(dador[0].nome,"Bill Gates");
    dador[0].dt.dia=28;
    dador[0].dt.mes=10;
    dador[0].dt.ano=1955;
    dador[0].peso=68.77;
    dador[0].numero_de_dadivas=110;
    strcpy(dador[0].tipo_sanguineo,"O");
    dador[0].rh='+';

    dador[1].num=111112;
    strcpy(dador[1].nome,"Dennis Ritchie");
    dador[1].dt.dia=9;
    dador[1].dt.mes=9;
    dador[1].dt.ano=1941;
    dador[1].peso=70.77;
    dador[1].numero_de_dadivas=63;
    strcpy(dador[1].tipo_sanguineo,"AB");
    dador[1].rh='-';

    dador[2].num=111113;
    strcpy(dador[2].nome,"Marcelo Rebelo de Sousa");
    dador[2].dt.dia=12;
    dador[2].dt.mes=12;
    dador[2].dt.ano=1948;
    dador[2].peso=55.77;
    dador[2].numero_de_dadivas=2;
    strcpy(dador[2].tipo_sanguineo,"O");
    dador[2].rh='+';

    dador[3].num=111114;
    strcpy(dador[3].nome,"Catarina Furtado");
    dador[3].dt.dia=25;
    dador[3].dt.mes=8;
    dador[3].dt.ano=1972;
    dador[3].peso=71.77;
    dador[3].numero_de_dadivas=21;
    strcpy(dador[3].tipo_sanguineo,"AB");
    dador[3].rh='+';

    dador[4].num=111115;
    strcpy(dador[4].nome,"Greta Thunberg");
    dador[4].dt.dia=3;
    dador[4].dt.mes=1;
    dador[4].dt.ano=2003;
    dador[4].peso=57.77;
    dador[4].numero_de_dadivas=43;
    strcpy(dador[4].tipo_sanguineo,"A");
    dador[4].rh='-';

    *qtdDADORES=5;
}
int gerar_numero (int lim_inferior, int lim_superior)  //gera um numero dentro dos limites definidos
{
    return (lim_inferior + (rand() % lim_superior));
}

void inserir_dador (dador_tipo dador[], int *qtdDADORES) //permite o registo de um novo dador
{
    int n,v;

    do
    {
        srand (time(NULL));
        dador[*qtdDADORES].num=gerar_numero (100000,1000000);  //gera um número com 6 algarismos
        printf ("Numero de dador:%d", dador[*qtdDADORES].num);  //apresenta o numero de dador
        printf("\nNome do dador:"); //pergunta o numero do dador
        fflush(stdin);
        gets (dador [*qtdDADORES].nome);
        printf ("Data de nascimento\n");
        printf("Dia:");  //pergunta o dia de nascimento
        scanf ("%d", &dador [*qtdDADORES].dt.dia);
        printf("Mes:");  //pergunta o mes de nascimento
        scanf ("%d", &dador [*qtdDADORES].dt.mes);
        printf("Ano:");  //pergunta o ano de nascimento
        scanf ("%d", &dador [*qtdDADORES].dt.ano );
        v=validar_data (dador [*qtdDADORES].dt.dia, dador [*qtdDADORES].dt.mes,dador [*qtdDADORES].dt.ano);  //valida a data de nascimento introduzida
        while(v == 0)
        {
            printf("Data de nascimento invalida, introduza novamente: ");
            printf("Dia:");
            scanf ("%d", &dador [*qtdDADORES].dt.dia);
            printf("Mes:");
            scanf ("%d", &dador [*qtdDADORES].dt.mes);
            printf("Ano:");
            scanf ("%d", &dador [*qtdDADORES].dt.ano );
            v = validar_data(dador [*qtdDADORES].dt.dia, dador [*qtdDADORES].dt.mes,dador [*qtdDADORES].dt.ano);
        }
        printf("Peso:");  //pergunta o peso
        scanf ("%f", &dador [*qtdDADORES].peso);
        printf ("Numero de dadivas:");  //pergunta o numero de dadivas

        scanf ("%d", &dador [*qtdDADORES].numero_de_dadivas);
        printf ("Tipo sanguineo:");  //pergunta o tipo sanguineo
        scanf ("%s", &dador [*qtdDADORES].tipo_sanguineo);
        fflush(stdin);
        printf ("Rh:");  //pergunta o rh
        fflush(stdin);
        scanf ("%c", &dador [*qtdDADORES].rh);
        while ((dador [*qtdDADORES].rh !='+') && (dador [*qtdDADORES].rh!='-'))
        {
            printf("Insira novamente\n");
            scanf("%c", &dador [*qtdDADORES].rh);
        }
        printf ("Se deseja inserir outro dador digite 1 se pretende sair digite 2:");
        scanf ("%d", &n);
        *qtdDADORES+=1;
    }
    while (n==1);

}

void eliminar_dador (dador_tipo dador[], int *qtdDADORES) //permite eliminar um dador atrasvés do numero de dador
{
    int d,k,m,flag=0;
    printf("Introduza o numero de dador que pretende eliminar\n");
    scanf ("%d", &d);
    for (k = 0; k < *qtdDADORES; k++)
    {
        if (d==dador[k].num)
        {
            printf("Dador existente\n");
            for(m = k; m < *qtdDADORES-1; m++)
            {
                dador[m] = dador[m+1];
            }
            printf("Registo de dador eliminado!\n");
            flag = 1;
            break;
        }
    }
    if(flag != 1)
    {
        printf(" Dador não encontrado!\n");
    }
    else
    {
        *qtdDADORES -= 1;
    }


}

void consultar_dadores_galardoados (dador_tipo dador[], int qtdDADORES)  //permite consultar os dadores galardoados e a sua respetiva medalha
{
    int p;
    for (p=0; p<qtdDADORES; p++)
    {
        if (dador[p].numero_de_dadivas>=100)
        {
            printf ("MEDALHA DOURADA+CERTIFICADO\n");
            printf("Dador|    Numero|                      Nome|        Data| Peso|Dadivas|Tipo Sanguineo| Rh\n");
            printf ("%5d|%10d|%26s|%4d/%2d/%4d|%5.2f|%7d|%14s|%3c\n",p, dador[p].num, dador[p].nome, dador[p].dt.dia, dador[p].dt.mes, dador [p].dt.ano, dador[p].peso, dador[p].numero_de_dadivas, dador[p].tipo_sanguineo,dador[p].rh);
        }
        else if (dador [p].numero_de_dadivas>=60)
        {
            printf ("\nMEDALHA DOURADA\n");
            printf("Dador|    Numero|                      Nome|        Data| Peso|Dadivas|Tipo Sanguineo| Rh\n");
            printf ("%5d|%10d|%26s|%4d/%2d/%4d|%5.2f|%7d|%14s|%3c\n",p, dador[p].num, dador[p].nome, dador[p].dt.dia, dador[p].dt.mes, dador [p].dt.ano, dador[p].peso, dador[p].numero_de_dadivas, dador[p].tipo_sanguineo,dador[p].rh);

        }
        else if (dador [p].numero_de_dadivas>=40)
        {
            printf ("\nMEDALHA PRATEADA\n");
            printf("Dador|    Numero|                      Nome|        Data| Peso|Dadivas|Tipo Sanguineo| Rh\n");
            printf ("%5d|%10d|%26s|%4d/%2d/%4d|%5.2f|%7d|%14s|%3c\n",p, dador[p].num, dador[p].nome, dador[p].dt.dia, dador[p].dt.mes, dador [p].dt.ano, dador[p].peso, dador[p].numero_de_dadivas, dador[p].tipo_sanguineo,dador[p].rh);
        }
        else if (dador [p].numero_de_dadivas>=20)
        {
            printf ("\nMEDALHA COBREADA\n");
            printf("Dador|    Numero|                      Nome|        Data| Peso|Dadivas|Tipo Sanguineo| Rh\n");
            printf ("%5d|%10d|%26s|%4d/%2d/%4d|%5.2f|%7d|%14s|%3c\n",p, dador[p].num, dador[p].nome, dador[p].dt.dia, dador[p].dt.mes, dador [p].dt.ano, dador[p].peso, dador[p].numero_de_dadivas, dador[p].tipo_sanguineo,dador[p].rh);
        }
        else if (dador [p].numero_de_dadivas>=10)
        {
            printf ("\nDIPLOMA DAS 10 DADIVAS\n");
            printf("Dador|    Numero|                      Nome|        Data| Peso|Dadivas|Tipo Sanguineo| Rh\n");
            printf ("%5d|%10d|%26s|%4d/%2d/%4d|%5.2f|%7d|%14s|%3c\n",p, dador[p].num, dador[p].nome, dador[p].dt.dia, dador[p].dt.mes, dador [p].dt.ano, dador[p].peso, dador[p].numero_de_dadivas, dador[p].tipo_sanguineo,dador[p].rh);
        }

    }
}

void mostrar_dadores(dador_tipo dador[], int qtdDADORES)  //mostra todos os dadores presentes até ao momento em formato de tabela
{
    int k;
    printf("Dador|    Numero|                      Nome|        Data| Peso|Dadivas|Tipo Sanguineo| Rh\n");
    for(k=0; k<qtdDADORES; k++)
    {
        printf ("%5d|%10d|%26s|%4d/%2d/%4d|%5.2f|%7d|%14s|%3c\n",k, dador[k].num, dador[k].nome, dador[k].dt.dia, dador[k].dt.mes, dador [k].dt.ano, dador[k].peso, dador[k].numero_de_dadivas, dador[k].tipo_sanguineo,dador[k].rh);

    }
}


typedef struct
{
    char nome[26];
    char local[51];
    char brigada[51];
    int hora_de_abertura, min_abertura; /// Hora de abertura (formato obrigatório: HH:MM)
    int hora_fecho, min_fecho; /// Hora de fecho (formato obrigatório: HH:MM)

} concelho_tipo;

typedef struct
{
    data_tipo data;
    concelho_tipo concelho[5];
    char cidade[18];
    int numConcelhos;
} local_recolha_tipo;

void inicializar_local_recolha(local_recolha_tipo local_recolha[], int *qtdLocaisRecolha)
{
    strcpy(local_recolha[0].cidade,"Porto");
    local_recolha[0].data.dia=28;
    local_recolha[0].data.mes=11;
    local_recolha[0].data.ano=2021;
    local_recolha[0].numConcelhos = 5;

    strcpy(local_recolha[0].concelho[0].nome,"Paredes");
    strcpy(local_recolha[0].concelho[0].local,"Delegação Cruz Vsobreira Av S.Pedro 603 Paredes");
    strcpy(local_recolha[0].concelho[0].brigada,"Cruz Vermelha Portuguesa-núcleo de sobreira");
    local_recolha[0].concelho[0].hora_de_abertura=9;
    local_recolha[0].concelho[0].min_abertura=00;
    local_recolha[0].concelho[0].hora_fecho=12;
    local_recolha[0].concelho[0].min_fecho=30;


    strcpy(local_recolha[0].concelho[1].nome,"Vila Nova de Gaia");
    strcpy(local_recolha[0].concelho[1].local,"Capela Nova de Gestosa-Rua de Gende");
    strcpy(local_recolha[0].concelho[1].brigada,"SANDIM (GAIA)");
    local_recolha[0].concelho[1].hora_de_abertura=9;
    local_recolha[0].concelho[1].min_abertura=00;
    local_recolha[0].concelho[1].hora_fecho=13;
    local_recolha[0].concelho[1].min_fecho=00;


    strcpy(local_recolha[0].concelho[2].nome,"Paços de Ferreira");
    strcpy(local_recolha[0].concelho[2].local,"Associação Empresarial Paços de Ferreira");
    strcpy(local_recolha[0].concelho[2].brigada,"ASSOCIACAO DADORES P FERREIRA-ASSC EMPRES PACOS FERREIRA");
    local_recolha[0].concelho[2].hora_de_abertura=14;
    local_recolha[0].concelho[2].min_abertura=30;
    local_recolha[0].concelho[2].hora_fecho=19;
    local_recolha[0].concelho[2].min_fecho=00;

    strcpy(local_recolha[0].concelho[3].nome,"Felgueiras");
    strcpy(local_recolha[0].concelho[3].local,"Pav. Gim. Moutelas -Rua Dr. Luis Gonzaga Fonseca Moreira");
    strcpy(local_recolha[0].concelho[3].brigada,"ASSOCIACAO DADORES GUIMARAES - FELGUEIRAS");
    local_recolha[0].concelho[3].hora_de_abertura=9;
    local_recolha[0].concelho[3].min_abertura=00;
    local_recolha[0].concelho[3].hora_fecho=12;
    local_recolha[0].concelho[3].min_fecho=30;

    strcpy(local_recolha[0].concelho[4].nome,"Povoa de Varzim");
    strcpy(local_recolha[0].concelho[4].local,"Rua Almirante Reis, 2, 1 Dt 4490 Povoa Varzim");
    strcpy(local_recolha[0].concelho[4].brigada,"ASSOCIACAO POVOA VARZIM - POVOA DE VARZIM");
    local_recolha[0].concelho[4].hora_de_abertura=14;
    local_recolha[0].concelho[4].min_abertura=00;
    local_recolha[0].concelho[4].hora_fecho=19;
    local_recolha[0].concelho[4].min_fecho=00;


    strcpy(local_recolha[1].cidade,"Braga");
    local_recolha[1].data.dia=11;
    local_recolha[1].data.mes=12;
    local_recolha[1].data.ano=2021;
    local_recolha[1].numConcelhos = 3;


    strcpy(local_recolha[1].concelho[0].nome,"Braga");
    strcpy(local_recolha[1].concelho[0].local,"Museu D Diogo De Sousa Braga");
    strcpy(local_recolha[1].concelho[0].brigada,"DADORES DE BRAGA");
    local_recolha[1].concelho[0].hora_de_abertura=9;
    local_recolha[1].concelho[0].min_abertura=00;
    local_recolha[1].concelho[0].hora_fecho=12;
    local_recolha[1].concelho[0].min_fecho=30;

    strcpy(local_recolha[1].concelho[1].nome,"Vizela");
    strcpy(local_recolha[1].concelho[1].local,"Escola Secundaria Vizela");
    strcpy(local_recolha[1].concelho[1].brigada,"ASSOCIACAO DADORES VIZELA - VIZELA");
    local_recolha[1].concelho[1].hora_de_abertura=9;
    local_recolha[1].concelho[1].min_abertura=00;
    local_recolha[1].concelho[1].hora_fecho=12;
    local_recolha[1].concelho[1].min_fecho=30;

    strcpy(local_recolha[1].concelho[2].nome,"Esposende");
    strcpy(local_recolha[1].concelho[2].local,"Centro Paroquial De Belinho - Esposende");
    strcpy(local_recolha[1].concelho[2].brigada,"ASSOCIACAO DADORES ESPOSENDE - BELINHO");
    local_recolha[1].concelho[2].hora_de_abertura=9;
    local_recolha[1].concelho[2].min_abertura=00;
    local_recolha[1].concelho[2].hora_fecho=12;
    local_recolha[1].concelho[2].min_fecho=30;



    strcpy(local_recolha[2].cidade,"Aveiro");
    local_recolha[2].data.dia=14;
    local_recolha[2].data.mes=12;
    local_recolha[2].data.ano=2021;
    local_recolha[2].numConcelhos = 4;



    strcpy(local_recolha[2].concelho[0].nome,"Ovar");
    strcpy(local_recolha[2].concelho[0].local,"Junta De Freguesia De Sao Vicente Pereira Jusa");
    strcpy(local_recolha[2].concelho[0].brigada,"SAO VICENTE DE PEREIRA JUSA (OVAR)");
    local_recolha[2].concelho[0].hora_de_abertura=8;
    local_recolha[2].concelho[0].min_abertura=30;
    local_recolha[2].concelho[0].hora_fecho=12;
    local_recolha[2].concelho[0].min_fecho=30;



    strcpy(local_recolha[2].concelho[1].nome,"Santa Maria da Feira");
    strcpy(local_recolha[2].concelho[1].local,"Centro Social De Argoncilhe");
    strcpy(local_recolha[2].concelho[1].brigada,"ARGONCILHE (FEIRA)");
    local_recolha[2].concelho[1].hora_de_abertura=9;
    local_recolha[2].concelho[1].min_abertura=00;
    local_recolha[2].concelho[1].hora_fecho=13;
    local_recolha[2].concelho[1].min_fecho=00;

    strcpy(local_recolha[2].concelho[2].nome,"Vagos");
    strcpy(local_recolha[2].concelho[2].local,"Salao Situado Rua Igreja 1Andar Lado Poente Da Igreja");
    strcpy(local_recolha[2].concelho[2].brigada,"SANTA CATARINA (VAGOS)");
    local_recolha[2].concelho[2].hora_de_abertura=9;
    local_recolha[2].concelho[2].min_abertura=00;
    local_recolha[2].concelho[2].hora_fecho=13;
    local_recolha[2].concelho[2].min_fecho=00;

    strcpy(local_recolha[2].concelho[3].nome,"Vale de Cambra");
    strcpy(local_recolha[2].concelho[3].local,"Centro Social E Paroquial De Aroes");
    strcpy(local_recolha[2].concelho[3].brigada,"AROES (VALE DE CAMBRA)");
    local_recolha[2].concelho[3].hora_de_abertura=9;
    local_recolha[2].concelho[3].min_abertura=00;
    local_recolha[2].concelho[3].hora_fecho=13;
    local_recolha[2].concelho[3].min_fecho=00;


    *qtdLocaisRecolha=3;
}



int validar_local(local_recolha_tipo local_recolha[], char novo_nome_cidade[18], int *qtdLocaisRecolha)
{
    int cidade_existe=0;
    for (int i=0; i<*qtdLocaisRecolha; i++)
    {
        int resultado = strcmp(local_recolha[i].cidade, novo_nome_cidade);
        if (resultado==0)
        {
            cidade_existe=1;
            break;
        }
    }
    return cidade_existe;
}

void inserir_local_recolha (local_recolha_tipo local_recolha[],  int *qtdLocaisRecolha )
{
    int numCi,numCo,l,v,k,qtdConcelhos;
    printf("Numero de cidades que vao ser introduzidas: ");
    scanf("%d", &numCi);
    for (k=0; k<numCi; k++)
    {
        printf("\nCidade:");
        scanf("%s", &local_recolha[*qtdLocaisRecolha].cidade);
        printf ("Data de recolha\n");
        printf("Dia:");
        scanf ("%d", &local_recolha [*qtdLocaisRecolha].data.dia);
        printf("Mes:");
        scanf ("%d", &local_recolha [*qtdLocaisRecolha].data.mes);
        printf("Ano:");
        scanf ("%d", &local_recolha [*qtdLocaisRecolha].data.ano );
        v=validar_data (local_recolha [*qtdLocaisRecolha].data.dia, local_recolha[*qtdLocaisRecolha].data.mes,local_recolha [*qtdLocaisRecolha].data.ano);
        while(v == 0)
        {
            printf("Data de recolha invalida, introduza novamente: ");
            printf("Dia:");
            scanf ("%d", &local_recolha [*qtdLocaisRecolha].data.dia);
            printf("Mes:");
            scanf ("%d", &local_recolha [*qtdLocaisRecolha].data.mes);
            printf("Ano:");
            scanf ("%d", &local_recolha [*qtdLocaisRecolha].data.ano);
            v = validar_data(local_recolha [*qtdLocaisRecolha].data.dia, local_recolha [*qtdLocaisRecolha].data.mes,local_recolha [*qtdLocaisRecolha].data.ano);
        }
        printf ("Numero de concelhos que vao ser introduzidos:");
        scanf("%d", &numCo);
        if(qtdConcelhos + numCo <= 5)
        {
            for (l=0; l < numCo; l++)
            {
                qtdConcelhos = local_recolha[*qtdLocaisRecolha].numConcelhos; //guarda o numero de concelhos ja existente na cidade
                printf("\nConcelho: ");
                scanf("%s", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].nome);
                printf("\nLocal: ");
                scanf("%s", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].local);
                printf("\nBrigada: ");
                scanf("%s", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].brigada);
                printf("\nHoras: ");
                scanf("%d", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].hora_de_abertura);
                printf("\nMinutos: ");
                scanf("%d", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].min_abertura);
                printf("\nHoras: ");
                scanf("%d", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].hora_fecho);
                printf("\nMinutos: ");
                scanf("%d", &local_recolha[*qtdLocaisRecolha].concelho[qtdConcelhos].min_fecho);
                local_recolha[*qtdLocaisRecolha].numConcelhos += 1;
            }
        }
        else
        {
            printf("Excedeu o limite de Concelhos!");
        }
        *qtdLocaisRecolha += 1;
    }

}
void mostrar_locais(local_recolha_tipo local_recolha[], int qtdLocaisRecolha)
{
    system ("cls");
    int i, j, numConcelhos;
    local_recolha_tipo f;

    for(i = 0; i < qtdLocaisRecolha; i++)
    {
        for(j= i+1; j < qtdLocaisRecolha; j++)
        {

            if(strcmp(local_recolha[i].cidade, local_recolha[j].cidade) > 0)
            {
                f = local_recolha[i];
                local_recolha[i] = local_recolha[j];
                local_recolha[j] = f;
            }
        }
    }

    printf(" Cidade|      Data|                Nome|                                                                                        Local|                                                Brigada| Abertura|Fecho \n\n");
    for(i=0; i<qtdLocaisRecolha; i++)
    {


        numConcelhos = local_recolha[i].numConcelhos;
        for(j=0; j < numConcelhos; j++)
        {
            printf ("%7s|%2d/%2d/%4d|%20s|%93s|%55s|%6d:%2d|%2d:%2d\n\n", local_recolha[i].cidade, local_recolha[i].data.dia, local_recolha[i].data.mes, local_recolha[i].data.ano, local_recolha[i].concelho[j].nome, local_recolha[i].concelho[j].local, local_recolha[i].concelho[j].brigada, local_recolha[i].concelho[j].hora_de_abertura,local_recolha[i].concelho[j].min_abertura, local_recolha[i].concelho[j].hora_fecho,local_recolha[i].concelho[j].min_fecho);
        }
    }

}


//Permite eliminar o registo de um local de recolha
void eliminar_local_recolha(local_recolha_tipo local_recolha[], int *qtdLocaisRecolha)
{
    char local_a_eliminar[18];
    int local;

    printf("Introduza o local que pretende eliminar:\n");
    scanf("%s", &local_a_eliminar);
    fflush(stdin);
    int flag = 0;
    for (int k = 0; k < *qtdLocaisRecolha; k++)
    {
        if (strcmp(local_recolha[k].cidade, local_a_eliminar) == 0)
        {
            for (int y = k; y < *qtdLocaisRecolha; y++)
            {
                local_recolha[y] = local_recolha[y + 1];
            }
            printf("Local eliminado! \n");
            flag = 1;
            break;
        }
    }
    if (flag != 1)
    {
        printf("Local de recolha nao encontrado! \n");
    }
    else
    {
        *qtdLocaisRecolha -= 1;
    }
}

void mostrar_LocaisRecolha_Abertos(local_recolha_tipo local_recolha[], int qtdLocaisRecolha)
{
    system ("cls");
    int k, n, numConcelhos;
    int horas, minutos;
    int flag=0;

    printf("Insira a hora que pretende consultar:\nHora: ");
    scanf("%d", &horas);
    printf("Minutos: ");
    scanf("%d", &minutos);

    printf(" Cidade|      Data|                Nome|                                                                                        Local|                                                Brigada| Abertura|Fecho \n\n");

    for(k=0; k<qtdLocaisRecolha; k++)
    {
        flag = 0;
        numConcelhos = local_recolha[k].numConcelhos;

        for(n=0; n < numConcelhos; n++)
        {
            if(local_recolha[k].concelho[n].hora_de_abertura < horas && local_recolha[k].concelho[n].hora_fecho > horas)
            {
                flag = 1;
                printf ("%7s|%2d/%2d/%4d|%20s|%93s|%55s|%6d:%2d|%2d:%2d\n\n", local_recolha[k].cidade, local_recolha[n].data.dia, local_recolha[k].data.mes, local_recolha[k].data.ano, local_recolha[k].concelho[n].nome, local_recolha[k].concelho[n].local, local_recolha[k].concelho[n].brigada, local_recolha[k].concelho[n].hora_de_abertura,local_recolha[k].concelho[n].min_abertura, local_recolha[k].concelho[n].hora_fecho,local_recolha[k].concelho[n].min_fecho);
            }
            else if(local_recolha[k].concelho[n].hora_de_abertura == horas && local_recolha[k].concelho[n].min_abertura <= minutos)
            {
                if(local_recolha[k].concelho[n].hora_fecho > horas)
                {
                    flag = 1;
                    printf ("%7s|%2d/%2d/%4d|%20s|%93s|%55s|%6d:%2d|%2d:%2d\n\n", local_recolha[k].cidade, local_recolha[n].data.dia, local_recolha[k].data.mes, local_recolha[k].data.ano, local_recolha[k].concelho[n].nome, local_recolha[k].concelho[n].local, local_recolha[k].concelho[n].brigada, local_recolha[k].concelho[n].hora_de_abertura,local_recolha[k].concelho[n].min_abertura, local_recolha[k].concelho[n].hora_fecho,local_recolha[k].concelho[n].min_fecho);
                }
                else if(local_recolha[k].concelho[n].hora_fecho == horas && local_recolha[k].concelho[n].min_fecho >= minutos)
                {
                    flag = 1;
                    printf ("%7s|%2d/%2d/%4d|%20s|%93s|%55s|%6d:%2d|%2d:%2d\n\n", local_recolha[k].cidade, local_recolha[n].data.dia, local_recolha[k].data.mes, local_recolha[k].data.ano, local_recolha[k].concelho[n].nome, local_recolha[k].concelho[n].local, local_recolha[k].concelho[n].brigada, local_recolha[k].concelho[n].hora_de_abertura,local_recolha[k].concelho[n].min_abertura, local_recolha[k].concelho[n].hora_fecho,local_recolha[k].concelho[n].min_fecho);
                }
            }
        }
    }
}

typedef struct inf
{
    char sexo;
    float temp;
    int pre_sis;
    int pre_dia;
    int periodo;
    int num_vezes;
    int idade;
} inf_dador;

typedef struct
{
    data_tipo data;
    char concelho[26];
    int num;
    inf_dador inf;
    int qtdSANGUE;
    int horas;
    int minutos;
    char *estado;
} recolha_sangue;

void registar_recolha(recolha_sangue recolhas[], local_recolha_tipo local_recolha[], dador_tipo dadores[],int qtdDADORES, int qtdRECOLHAS, int qtdLocalRecolha)
{
    int num;
    int i,k,m, j;
    char concelho[26];
    int horas, minutos;
    int flag_concelho = 0;
    int localk = 0, concelhoj = 0;
    int qtdSANGUE = 0;
    int flag_local = 0;
    int flag_registo_efetuado = 0;
    int flag_dador=0;
    dador_tipo *dador;

    do
    {
        printf("Insira o numero do dador: ");
        scanf("%d", &num);
        for(m= 0; m < qtdDADORES; m++)
        {
            if(dadores[m].num == num)
            {
                flag_dador= 1;
                dador = &(dadores[m]);
            }
        }

        if(flag_dador == 0)
            printf("Dador inexistente!\n");
    }
    while(flag_dador == 0);


    for(i=0; i<qtdRECOLHAS; i++)
    {
        if(num == recolhas[i].num && recolhas[i].qtdSANGUE == 0 && recolhas[i].estado == 'S')
        {
            do
            {
                printf("Concelho de doacao:");
                scanf("%s", &concelho);

                for(k = 0; k < qtdLocalRecolha; k++)
                {
                    int numConcelhos = local_recolha[k].numConcelhos;
                    for(j = 0; j < numConcelhos; j++)
                    {
                        if(strcmp(local_recolha[k].concelho[j].nome, concelho) == 0)
                        {
                            flag_concelho = 1;
                            localk = k;
                            concelhoj = j;
                            break;
                        }
                    }
                    if(flag_concelho != 0)
                        break;
                }
            }
            while(flag_concelho == 0);

            strcpy(recolhas[i].concelho, concelho);

            printf("\nHora: ");
            scanf("%d", &horas);
            printf("Minutos: ");
            scanf("%d", &minutos);
            recolhas[i].horas = horas;
            recolhas[i].minutos = minutos;
            if ((local_recolha[localk].concelho[concelhoj].hora_de_abertura < horas && local_recolha[localk].concelho[concelhoj].hora_fecho > horas) || ((local_recolha[localk].concelho[concelhoj].hora_de_abertura == horas && local_recolha[localk].concelho[concelhoj].min_abertura <= minutos) && (local_recolha[localk].concelho[concelhoj].hora_fecho > horas) || (local_recolha[localk].concelho[concelhoj].hora_fecho == horas && local_recolha[localk].concelho[concelhoj].min_fecho >= minutos)))
            {

                printf("LOCAL ABERTO \n");
                do
                {
                    printf("Quantidade de sangue:");
                    scanf("%d", &qtdSANGUE);
                }
                while(qtdSANGUE <= 0 && qtdSANGUE > 450);

                recolhas[i].qtdSANGUE = qtdSANGUE;
                flag_local = 1;
                dadores->numero_de_dadivas = dadores->numero_de_dadivas + 1;
                printf("REGISTO DE RECOLHA EFETUADO\n");

            }

            if(flag_local == 0)
            {
                printf("LOCAL DE RECOLHA ENCERRADO");
            }
            flag_registo_efetuado = 1;
            break;
        }
    }

    if(flag_registo_efetuado == 0)
    {
        printf("DADOR INVALIDO\n");
    }
}

void medir_sinais_vitais (recolha_sangue recolhas[], dador_tipo dadores[], int qtdDADORES, int *qtdRECOLHAS)
{
    int k,num,dia,mes,ano,v;
    int periodo,num_vezes,idade,pre_sis,pre_dia;
    char sexo;
    float temp;
    int flag=0;
    char *a;
    dador_tipo *dador;
    data_tipo data;

    do
    {
        printf("Numero do dador: ");
        scanf("%d", &num);
        for(k = 0; k< qtdDADORES; k++)
        {
            if(dadores[k].num == num)
            {
                flag = 1;
                dador = &(dadores[k]);
                break;
            }

        }

        if(flag == 0)
            printf("DADOR NAO EXISTE\n");

    }
    while(flag == 0);

    printf ("Nome: %s\n",dador->nome);
    fflush(stdin);

    do
    {
        printf("Data da recolha: \n");
        printf("Dia: ");
        scanf("%d", &dia);
        printf("Mes: ");
        scanf("%d", &mes);
        printf("Ano: ");
        scanf ("%d", &ano);
        v = validar_data(dia, mes, ano); //se retornar 1, a data e valida e a flag fica a 1
        if(v == 0)
        {
            printf("Data invalida. Introduza novamente. \n");
            printf("Dia: ");
            scanf("%d", &dia);
            printf("Mes: ");
            scanf("%d", &mes);
            printf("Ano: ");
            scanf ("%d", &ano);
            v = validar_data(dia, mes, ano);

        }
    }
    while(v == 0);

    data.dia=dia;
    data.mes=mes;
    data.ano=ano;
    recolhas[*qtdRECOLHAS].data = data;
    recolhas[*qtdRECOLHAS].num = num;
    strcpy(recolhas[*qtdRECOLHAS].concelho, "NULL");

    printf ("Sexo:");
    fflush(stdin);
    scanf ("%c", &sexo);
    while (sexo != 'F' && sexo != 'M' && sexo != 'f' && sexo != 'm')
    {
        printf ("Digite novamente!");
        fflush(stdin);
        scanf ("%c", &sexo);
    }
    printf ("Periodo de doacao em dias:");
    scanf ("%d", &periodo);
    printf ("Numero de vezes que doou este ano:");
    scanf ("%d", &num_vezes);
    printf ("Temperatura:");
    scanf("%f", &temp);
    printf ("Pressao sistolica:");
    scanf("%d", &pre_sis);
    printf ("Pressao diastolica:");
    scanf("%d", &pre_dia);

    recolhas[*qtdRECOLHAS].inf.sexo= sexo;
    recolhas[*qtdRECOLHAS].inf.periodo=periodo;
    recolhas[*qtdRECOLHAS].inf.num_vezes=num_vezes;

    recolhas[*qtdRECOLHAS].inf.temp=temp;
    recolhas[*qtdRECOLHAS].inf.pre_sis=pre_sis;
    recolhas[*qtdRECOLHAS].inf.pre_dia=pre_dia;
    recolhas[*qtdRECOLHAS].estado = 'N';

    idade = ano - dador->dt.ano;
    if(mes < dador->dt.mes)
    {
        idade -= 1;
    }
    else if(mes == dador->dt.mes && dia < dador->dt.dia)
    {
        idade -= 1;
    }

    recolhas[*qtdRECOLHAS].inf.idade=idade;

    if((num_vezes<3 || (sexo == 'F' || sexo == 'f') ) && (num_vezes<4 || (sexo == 'M' || sexo == 'm' )))
    {
        if (periodo>=62)
        {
            if (idade>18 && idade <64)
            {
                if (temp<38)
                {
                    if (pre_sis>=100 && pre_sis<=180)
                    {
                        if (pre_dia>=60 && pre_dia<=100 )
                        {
                            recolhas[*qtdRECOLHAS].estado = 'S';
                            printf ("APTO\n");
                        }
                        else if(idade >= 65)
                        {
                            printf("Tem autorizacao medica? Responda S/N");
                            scanf("%c", &a);
                            if(a == 'S')
                            {
                                recolhas[*qtdRECOLHAS].estado = 'S';
                                printf("APTO\n");
                            }

                        }
                    }
                }
            }

        }
    }

    if (recolhas[*qtdRECOLHAS].estado == 'N')
        printf ("INAPTO\n");

    recolhas[*qtdRECOLHAS].qtdSANGUE = 0;
    *qtdRECOLHAS = *qtdRECOLHAS + 1;
}

void editar_rastreio(recolha_sangue recolhas[],local_recolha_tipo local_recolha[], dador_tipo dadores[],int qtdDADORES, int qtdRECOLHAS, int qtdLocalRecolha)
{
    char op_menu_alterar_rastreio;
    int i,j,num,editar_d,editar_m,editar_a,k,recolha,numConcelhos,dia_novo,mes_novo,ano_novo,v;
    int flag_concelho=0,localk,concelhoj,flag_dador=0,flag=0;
    char concelho[26];
    int periodo,num_vezes,idade,sexo,temp,pre_sis,pre_dia,qtdSANGUE;
    char aux;
    dador_tipo *dador;
    recolha_sangue *editar;

    do
    {
        printf("Numero do dador: ");
        scanf("%d", &num);
        for(k = 0; k< qtdDADORES; k++)
        {
            if(dadores[k].num == num)
            {
                flag_dador = 1;
                dador = &(dadores[k]);
                break;
            }

        }

        if(flag_dador == 0)
            printf("DADOR NAO EXISTE\n");

    }
    while(flag_dador == 0);

    printf("Data de rastreio a editar:\n");
    printf("Dia:");
    scanf("%d", &editar_d);
    printf("\nMes:");
    scanf("%d", &editar_m);
    printf("\nAno:");
    scanf("%d", &editar_a);

    for(k = 0; k < qtdRECOLHAS; k++)
    {
        if(recolhas[k].data.dia == editar_d && recolhas[k].data.mes == editar_m && recolhas[k].data.ano == editar_a)
        {
            editar = &(recolhas[k]);
            recolha = 1;
            break;
        }
    }
    if(recolha == 0)
    {
        printf("NAO EXISTE\n");
        return;
    }

    system("cls");
    printf("M E N U   E D I T A R   R A S T R E I O\n");
    printf(" O QUE PRETENDE ALTERAR \n");
    printf(" 1 - CONCELHO\n");
    printf(" 2 - SINAIS VITAIS\n");
    printf(" 3 - QUANTIDADE DE SANGUE\n");
    printf(" 4 - DATA\n");
    printf(" 0 - SAIR \n");
    printf("     OPCAO:");

    fflush(stdin);
    op_menu_alterar_rastreio = getchar();

    switch (op_menu_alterar_rastreio)
    {
    case '1':
    {
        do
        {
            printf("Concelho de doacao:");
            scanf("%s", &concelho);

            for(k = 0; k < qtdLocalRecolha; k++)
            {
                int numConcelhos = local_recolha[k].numConcelhos;
                for(j = 0; j < numConcelhos; j++)
                {
                    if(strcmp(local_recolha[k].concelho[j].nome, concelho) == 0)
                    {
                        flag_concelho = 1;
                        localk = k;
                        concelhoj = j;
                        break;
                    }
                }
                if(flag_concelho != 0)
                    break;
            }
        }
        while(flag_concelho == 0);

        strcpy(editar->concelho, concelho);

        for (i=0; i<qtdRECOLHAS; i++)
        {
            if (recolhas[i].num == num && recolhas[i].data.dia == editar_d && recolhas[i].data.mes == editar_m && recolhas[i].data.ano == editar_a)
            {
                printf("LISTA DE RECOLHA ATUALIZADA\n");
                printf("Apto: %c\n", recolhas[i].estado);
                printf("Data: %d/%d/%d\n",recolhas[i].data.dia,recolhas[i].data.mes,recolhas[i].data.ano);
                printf("Sexo: %c\n", recolhas[i].inf.sexo);
                printf("Periodo de doacao: %d\n", recolhas[i].inf.periodo);
                printf("Numero de vezes que doou este ano: %d\n", recolhas[i].inf.num_vezes);
                printf("Idade: %d\n", recolhas[i].inf.idade);
                printf("Temperatura: %1.2f\n", recolhas[i].inf.temp);
                printf("Pressao sistolica: %d\n", recolhas[i].inf.pre_sis);
                printf("Pressao diastolica: %d\n", recolhas[i].inf.pre_dia);
                printf("Quantidade de sangue: %d\n", recolhas[i].qtdSANGUE);
                printf("Concelho de doacao: %s\n", strcpy(recolhas[i].concelho, concelho));
                printf("Horas: %d\n", recolhas[i].horas);
                printf("Minutos: %d\n", recolhas[i].minutos);
            }


        }

        break;

    }

    case '2':
    {
        printf ("Sexo:");
        scanf ("%c", &sexo);
        fflush(stdin);
        scanf ("%c", &sexo);
        while (sexo != 'F' && sexo != 'M' && sexo != 'f' && sexo != 'm')
        {
            printf ("Digite novamente!");
            fflush(stdin);
            scanf ("%c", &sexo);
        }
        printf ("Periodo de doacao em dias:");
        scanf ("%d", &periodo);
        printf ("Numero de vezes que doou este ano:");
        scanf ("%d", &num_vezes);
        printf ("Temperatura:");
        scanf("%f", &temp);
        printf ("Pressao sistolica:");
        scanf("%d", &pre_sis);
        printf ("Pressao diastolica:");
        scanf("%d", &pre_dia);

        editar->inf.sexo=sexo;
        editar->inf.periodo=periodo;
        editar->inf.num_vezes=num_vezes;
        editar->inf.temp=temp;
        editar->inf.pre_sis=pre_sis;
        editar->inf.pre_dia=pre_dia;

        if((num_vezes<3 || (sexo == 'F' || sexo == 'f') ) && (num_vezes<4 || (sexo == 'M' || sexo == 'm' )))
        {
            if (periodo>=62)
            {
                if (temp<38)
                {
                    if (pre_sis>=100 && pre_sis<=180)
                    {
                        if (pre_dia>=60 && pre_dia<=100 )
                        {
                            flag=1;
                            printf ("APTO\n");
                        }
                    }

                }
            }
        }
        if (flag=0)
            printf("INAPTO\n");
        editar->estado = 'N';
        strcpy(editar->concelho, "NULL");
        editar->qtdSANGUE = 0;


        for (i=0; i<qtdRECOLHAS; i++)
        {
            if (recolhas[i].num == num && recolhas[i].data.dia == editar_d && recolhas[i].data.mes == editar_m && recolhas[i].data.ano == editar_a)
            {
                printf("\n\nLISTA DE RECOLHA ATUALIZADA\n");
                printf("Apto:%c\n", editar->estado);
                printf("Data: %d/%d/%d\n",recolhas[i].data.dia,recolhas[i].data.mes,recolhas[i].data.ano);
                printf(" Sexo: %c\n", editar->inf.sexo);
                printf(" Periodo de doacao: %d\n",  editar->inf.periodo);
                printf("Numero de vezes que doou este ano: %d\n", editar->inf.num_vezes);
                printf(" Idade: %d\n", recolhas[i].inf.idade);
                printf(" Temperatura: %1.2f\n", editar->inf.temp);
                printf(" Pressao sistolica: %d\n", editar->inf.pre_sis);
                printf(" Pressao diastolica: %d\n", editar->inf.pre_dia);
                printf(" Quantidade de sangue: %d\n", recolhas[i].qtdSANGUE);
                printf("Concelho de doacao: %s\n", recolhas[i].concelho);
                printf(" Horas: %d\n", recolhas[i].horas);
                printf(" Minutos: %d\n", recolhas[i].minutos);
            }


        }
        break;

    }

    case '3':
    {
        if(editar->estado == 'N')
        {
            printf("INAPTO");
            break;
        }

        do
        {
            printf("Quantidade de sangue:");
            scanf("%d", &qtdSANGUE);
        }
        while(qtdSANGUE <= 0 && qtdSANGUE > 450);

        editar->qtdSANGUE = qtdSANGUE;
        for (i=0; i<qtdRECOLHAS; i++)
        {
            if (recolhas[i].num == num && recolhas[i].data.dia == editar_d && recolhas[i].data.mes == editar_m && recolhas[i].data.ano == editar_a )
            {
                printf("LISTA DE RECOLHA ATUALIZADA\n");
                printf("Apto:%c\n", editar->estado);
                printf("Data: %d/%d/%d\n",recolhas[i].data.dia,recolhas[i].data.mes,recolhas[i].data.ano);
                printf(" Sexo: %c\n", recolhas[i].inf.sexo);
                printf(" Periodo de doacao: %d\n", recolhas[i].inf.periodo);
                printf("Numero de vezes que doou este ano: %d\n", recolhas[i].inf.num_vezes);
                printf(" Idade: %d\n", recolhas[i].inf.idade);
                printf(" Temperatura: %1.2f\n", recolhas[i].inf.temp);
                printf(" Pressao sistolica: %d\n", recolhas[i].inf.pre_sis);
                printf(" Pressao diastolica: %d\n", recolhas[i].inf.pre_dia);
                printf(" Quantidade de sangue: %d\n", editar->qtdSANGUE);
                printf("Concelho de doacao: %s\n", recolhas[i].concelho);
                printf(" Horas: %d\n", recolhas[i].horas);
                printf(" Minutos: %d\n", recolhas[i].minutos);
            }


        }

        break;

    }

    case '4':
    {
        do
        {

            printf ("Insira a nova data\n");
            printf ("Dia:");
            scanf ("%d", &dia_novo);
            printf ("Mes:");
            scanf ("%d", &mes_novo);
            printf ("Ano:");
            scanf ("%d", &ano_novo);
            v = validar_data(dia_novo, mes_novo, ano_novo);
            if(v == 0)
            {
                printf("Data invalida. Introduza novamente. \n");
                printf("Dia: ");
                scanf("%d", &dia_novo);
                printf("Mes: ");
                scanf("%d", &mes_novo);
                printf("Ano: ");
                scanf ("%d", &ano_novo);
                v = validar_data(dia_novo, mes_novo, ano_novo);

            }
        }
        while(v == 0);

        editar->data.dia = dia_novo;
        editar->data.mes = mes_novo;
        editar->data.ano = ano_novo;
        idade = editar->data.ano - dador->dt.ano;
        if(editar->data.mes < dador->dt.mes)
        {
            idade -= 1;
        }
        else if(editar->data.mes == dador->dt.mes && editar->data.dia < dador->dt.dia)
        {
            idade -= 1;
        }

        if (idade >= 18 && idade <= 64)
        {
            editar->estado = 'S';
            for (i=0; i<qtdRECOLHAS; i++)
            {
                if (recolhas[i].num == num && editar->data.dia == editar_d && editar->data.mes == editar_m && editar->data.ano == editar_a)
                {
                    printf("LISTA DE RECOLHA ATUALIZADA\n");
                    printf("Apto: %c\n", editar->estado);
                    printf("Data: %d/%d/%d\n",editar->data.dia,editar->data.mes,editar->data.ano);
                    printf("Sexo: %c\n", recolhas[i].inf.sexo);
                    printf("Periodo de doacao: %d\n", recolhas[i].inf.periodo);
                    printf("Numero de vezes que doou este ano: %d\n", recolhas[i].inf.num_vezes);
                    printf("Idade: %d\n", recolhas[i].inf.idade);
                    printf("Temperatura: %1.2f\n", recolhas[i].inf.temp);
                    printf("Pressao sistolica: %d\n", recolhas[i].inf.pre_sis);
                    printf("Pressao diastolica: %d\n", recolhas[i].inf.pre_dia);
                    printf("Quantidade de sangue: %d\n", recolhas[i].qtdSANGUE);
                    printf("Concelho de doacao: %s\n",recolhas [i].concelho);
                    printf("Horas: %d\n", recolhas[i].horas);
                    printf("Minutos: %d\n", recolhas[i].minutos);
                }

            }

        }
        else if(idade >= 65)
        {
            printf("Tem autorizacao medica? Responda S/N");
            scanf("%c", &aux);
            if(aux == 'S')
            {
                editar->estado = 'S';
                for (i=0; i<qtdRECOLHAS; i++)
                {
                    if (recolhas[i].num == num && editar->data.dia == editar_d && editar->data.mes == editar_m && editar->data.ano == editar_a )
                    {
                        printf("LISTA DE RECOLHA ATUALIZADA\n");
                        printf("Apto: %c\n", editar->estado);
                        printf("Data: %d/%d/%d\n",editar->data.dia,editar->data.mes,editar->data.ano);
                        printf("Sexo: %c\n", recolhas[i].inf.sexo);
                        printf("Periodo de doacao: %d\n", recolhas[i].inf.periodo);
                        printf("Numero de vezes que doou este ano: %d\n", recolhas[i].inf.num_vezes);
                        printf("Idade: %d\n", recolhas[i].inf.idade);
                        printf("Temperatura: %1.2f\n", recolhas[i].inf.temp);
                        printf("Pressao sistolica: %d\n", recolhas[i].inf.pre_sis);
                        printf("Pressao diastolica: %d\n", recolhas[i].inf.pre_dia);
                        printf("Quantidade de sangue: %d\n", recolhas[i].qtdSANGUE);
                        printf("Concelho de doacao: %s\n",recolhas [i].concelho);
                        printf("Horas: %d\n", recolhas[i].horas);
                        printf("Minutos: %d\n", recolhas[i].minutos);
                    }
                }
            }

        }
        else if (idade<18 || aux!= 'S')
        {
            editar->estado = 'N';
            strcpy(editar->concelho, "NULL");
            editar->qtdSANGUE = 0;
            for (i=0; i<qtdRECOLHAS; i++)
            {
                if (recolhas[i].num == num && editar->data.dia == editar_d && editar->data.mes == editar_m && editar->data.ano == editar_a )
                {
                    printf("LISTA DE RECOLHA ATUALIZADA\n");
                    printf("Apto: %c\n", editar->estado);
                    printf("Data: %d/%d/%d\n",editar->data.dia,editar->data.mes,editar->data.ano);
                    printf("Sexo: %c\n", recolhas[i].inf.sexo);
                    printf("Periodo de doacao: %d\n", recolhas[i].inf.periodo);
                    printf("Numero de vezes que doou este ano: %d\n", recolhas[i].inf.num_vezes);
                    printf("Idade: %d\n", recolhas[i].inf.idade);
                    printf("Temperatura: %1.2f\n", recolhas[i].inf.temp);
                    printf("Pressao sistolica: %d\n", recolhas[i].inf.pre_sis);
                    printf("Pressao diastolica: %d\n", recolhas[i].inf.pre_dia);
                    printf("Quantidade de sangue: %d\n", recolhas[i].qtdSANGUE);
                    printf("Concelho de doacao: %s\n",recolhas [i].concelho);
                    printf("Horas: %d\n", recolhas[i].horas);
                    printf("Minutos: %d\n", recolhas[i].minutos);
                }
            }
        }


        break;


    }
    }
}

void historico_recolhas_dador (dador_tipo dadores[], recolha_sangue recolhas[],int qtdRECOLHAS, int qtdDADORES)
{
    int num,k,i;
    int flag_dador=0;
    dador_tipo *dador;

    do
    {
        printf("Numero do dador: ");
        scanf("%d", &num);
        for(k = 0; k< qtdDADORES; k++)
        {
            if(dadores[k].num == num)
            {
                flag_dador = 1;
                dador = &(dadores[k]);
                break;
            }

        }

        if(flag_dador == 0)
            printf("DADOR NAO EXISTE\n");

    }
    while(flag_dador == 0);


    printf ("LISTA DE RECOLHAS\n");
    for (i=0; i<qtdRECOLHAS; i++)
    {
        if (recolhas[i].num == num && recolhas[i].estado == 'S' )
        {
            printf ("Apto|      Data|Concelho de doacao|Horas|Minutos|Quantidade de Sangue|Sexo|Idade|Periodo de doacao|Numero de vezes|Temperatura|Pressao Sistolica|Pressao Diastolica\n");
            printf ("%4c|%2d/%2d/%4d|%18s|%5d|%7d|%20d|%4c|%5d|%17d|%15d|%10.2f|%17d|%17d\n",recolhas[i].estado,recolhas[i].data.dia,recolhas[i].data.mes, recolhas[i].data.ano,recolhas[i].concelho,recolhas[i].horas,recolhas[i].minutos,recolhas[i].qtdSANGUE,recolhas[i].inf.sexo,recolhas[i].inf.idade,recolhas[i].inf.periodo,recolhas[i].inf.num_vezes,recolhas[i].inf.temp,recolhas[i].inf.pre_sis,recolhas[i].inf.pre_dia);
        }
        if  (recolhas[i].num == num && recolhas[i].estado == 'N' )
        {
            printf ("Apto|      Data|Sexo|Idade|Periodo de doacao|Numero de vezes|Temperatura|Pressao Sistolica|Pressao Diastolica\n");
            printf ("%4c|%2d/%2d/%4d|%4c|%5d|%17d|%15d|%10.2f|%18d|%17d\n",recolhas[i].estado,recolhas[i].data.dia,recolhas[i].data.mes, recolhas[i].data.ano,recolhas[i].inf.sexo,recolhas[i].inf.idade,recolhas[i].inf.periodo,recolhas[i].inf.num_vezes,recolhas[i].inf.temp,recolhas[i].inf.pre_sis,recolhas[i].inf.pre_dia);

        }

    }


}

void percentagem_tipo_sanguineo (dador_tipo dador,int *qtdDADORES)
{
    char i, rh,f;
    printf ("Tipo sanguineo desejado:");
    scanf ("%c",rh);
    printf ("Fator desejado:");
    scanf ("%c",f);
    for (i=0; i<*qtdDADORES; i++)
    {
        {

        }
    }
}

int menu_principal ()
{
    int mp;
    printf("      M E N U   P R I N C I P A L\n");
    printf("      1- GESTAO DADORES DE SANGUE\n");
    printf("      2- GESTAO DE LOCAIS DE RECOLHA DE SANGUE\n");
    printf("      3- RECOLHA DE SANGUE\n");
    printf("      4- ESTATISTICAS\n");
    printf("      0- SAIR\n");
    scanf("%d", &mp);

    return mp;

}

int menu1 ()
{
    int m1;
    printf("      M E N U   G E S T A O   D A D O R E S   D E   S A N G U E\n");
    printf("      1- INSERIR DADOR\n");
    printf("      2- ELIMINAR DADOR\n");
    printf("      3- CONSULTAR DADORES GALARDOADOS\n");
    printf("      4- LISTAR TODOS OS DADORES\n");
    printf("      0- SAIR\n");
    scanf("%d", &m1);

    return m1;

}

int menu_2 ()
{
    int m2;
    printf("      M E N U   G E S T A O   D E   L O C A I S   D E   R E C O L H A   D E   S A N G U E\n");
    printf("      1- REGISTAR DADOS DE UM LOCAL DE RECOLHA\n");
    printf("      2- ELIMINAR LOCAL DE RECOLHA\n");
    printf("      3- MOSTRAR LOCAIS DE RECOLHA ABERTOS EM DETERMINADO PERIODO\n");
    printf("      4- LISTAR LOCAIS DE RECOLHA\n");
    printf("      0- SAIR\n");
    scanf("%d", &m2);
    return m2;
}

int menu_3 ()
{
    int m3;
    printf("      M E N U   R E C O L H A   D E   S A N G U E\n");
    printf("      1- NOVA RECOLHA DE SANGUE\n");
    printf("      2- EDITAR RECOLHA\n");
    printf("      3- MEDIR SINAIS VITAIS\n");
    printf("      3- HISTORICO RECOLHAS DE SANGUE DE UM DADOR\n");
    scanf("%d", &m3);
    return m3;
}

int main()
{
    int qtdDADORES=0,mp,m1,num;
    int pos = -1;
    int qtdLocaisRecolha=0,m2;
    int qtdRECOLHAS=0,m3;
    dador_tipo dador[MAX_DADORES];
    local_recolha_tipo local_recolha [MAX_CIDADES];
    concelho_tipo concelho [MAX_CONCELHOS];
    inf_dador inf;
    recolha_sangue recolhas[MAX_RECOLHAS];
    inicializar_local_recolha(local_recolha, &qtdLocaisRecolha);
    do
    {
        mp = menu_principal ();
        switch (mp)
        {
        case 1:
            system("cls");
            inicializar_dadores(dador, &qtdDADORES);
            do
            {
                m1 = menu1 ();
                switch (m1)
                {
                case 1:
                    system("cls");
                    if(qtdDADORES < MAX_DADORES)
                    {
                        inserir_dador (dador, &qtdDADORES);
                    }
                    else
                        printf("Não é possivel inserir mais dadores\n");

                    break;
                case 2:
                    system("cls");
                    mostrar_dadores (dador, qtdDADORES);
                    eliminar_dador (dador, &qtdDADORES);
                    break;
                case 3:
                    system("cls");
                    consultar_dadores_galardoados (dador, qtdDADORES);
                    break;
                case 4:
                    system("cls");
                    mostrar_dadores (dador, qtdDADORES);
                    break;
                }
            }
            while (m1 != 0);
            system("cls");
            break;
        case 2:
            system("cls");
            do
            {
                m2 = menu_2 ();
                switch (m2)
                {
                case 1:
                    system("cls");
                    if(qtdLocaisRecolha < MAX_CIDADES)
                    {
                        inserir_local_recolha (local_recolha, &qtdLocaisRecolha);
                    }
                    else
                        printf("Não é possivel inserir mais cidades\n");

                    break;

                case 2:
                    system("cls");
                    mostrar_locais(local_recolha, &qtdLocaisRecolha);
                    eliminar_local_recolha (local_recolha, &qtdLocaisRecolha);
                    break;

                case 3:
                    system("cls");
                    mostrar_LocaisRecolha_Abertos(local_recolha, qtdLocaisRecolha);
                    break;

                case 4:
                    system("cls");
                    mostrar_locais(local_recolha, qtdLocaisRecolha);
                    break;
                }
            }
            while (m2 !=0);
            system("cls");
            break;
        case 3:
            system("cls");
            do
            {
                m3 = menu_3 ();
                switch (m3)
                {
                case 1:
                    system("cls");
                    registar_recolha(recolhas,local_recolha,dador,qtdDADORES,qtdRECOLHAS,qtdLocaisRecolha);
                    break;
                case 2:
                    system("cls");
                    editar_rastreio(recolhas,local_recolha,dador,qtdDADORES,qtdRECOLHAS,qtdLocaisRecolha);
                    break;
                case 3:
                    system("cls");
                    inicializar_dadores(dador, &qtdDADORES);
                    mostrar_dadores (dador, qtdDADORES);
                    medir_sinais_vitais(recolhas,dador,qtdDADORES,&qtdRECOLHAS);
                    break;
                case 4:
                    system("cls");
                    historico_recolhas_dador (dador,recolhas,qtdDADORES,qtdRECOLHAS);
                    break;

                }

            }
            while (m3 !=0);
            system("cls");
            break;
        }
    }
    while (mp != 0);

    return 0;
}
