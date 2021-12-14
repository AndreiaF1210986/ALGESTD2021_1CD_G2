# ALGESTD2021_1D_G2
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include<time.h>
#define  MAX_DADORES 500
#define MAX_CIDADES 14
#define MAX_CONCELHOS 5

typedef struct dt
{
    int dia;
    int mes;
    int ano;

} data_tipo;

typedef struct dador
{
    int num; //Numero do Dador (formato inclui os 6 primeiros digitos: DDDDDD)
    char nome[26];  //Nome do dadorente (maximo 25 carateres uteis)
    data_tipo dt;   //Data de nascimento (formato obrigatorio: DD-MM-AAAA)
    float peso;
    int numero_de_dadivas;
    char tipo_sanguineo [3];
    char rh;   //Rh ('+' ou '-')
} dador_tipo;

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
int validar_hora(int hora, int minutos)
{
    int horaminutosvalidos=0;

    int horavalida=0;
    int minutosvalidos=0;

    if(hora>=0 && hora<=23)
        horavalida=1;

    if(minutos>=0 && minutos<=59)
        minutosvalidos=1;

    if(horavalida && minutosvalidos)
        horaminutosvalidos=1;

    return horaminutosvalidos;
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
    char cidade[18];
    data_tipo data;
    concelho_tipo concelho[5];
} local_recolha_tipo;
   void inicializar_local_recolha(local_recolha_tipo local_recolha[], int *qtdLocaisRecolha)
 {
 strcpy(local_recolha[0].cidade,"Porto");
    local_recolha[0].data.dia=28;
    local_recolha[0].data.mes=11;
    local_recolha[0].data.ano=2021;

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

    strcpy(local_recolha[0].concelho[4].nome,"Póvoa de Varzim");
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

    strcpy(local_recolha[1].concelho[3].nome,"Guimarães");
    strcpy(local_recolha[1].concelho[3].local,"Antiga Escola Primaria De Urgeses Rua Costa Guimaraes 1877");
    strcpy(local_recolha[1].concelho[3].brigada,"ASSOCIACAO DADORES GUIMARAES - URGESES");
    local_recolha[1].concelho[3].hora_de_abertura=9;
    local_recolha[1].concelho[3].min_abertura=00;
    local_recolha[1].concelho[3].hora_fecho=12;
    local_recolha[1].concelho[3].min_fecho=30;


    strcpy(local_recolha[1].concelho[4].nome,"Barcelos");
    strcpy(local_recolha[1].concelho[4].local,"Bombeiros Voluntarios Barcelos");
    strcpy(local_recolha[1].concelho[4].brigada,"ASSOCIACAO HUMANITARIA DADORES SANGUE BARCELOS");
    local_recolha[1].concelho[4].hora_de_abertura=9;
    local_recolha[1].concelho[4].min_abertura=00;
    local_recolha[1].concelho[4].hora_fecho=12;
    local_recolha[1].concelho[4].min_fecho=30;



    strcpy(local_recolha[2].cidade,"Aveiro");
    local_recolha[2].data.dia=14;
    local_recolha[2].data.mes=12;
    local_recolha[2].data.ano=2021;



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

    strcpy(local_recolha[2].concelho[4].nome,"Arouca");
    strcpy(local_recolha[2].concelho[4].local,"Centro Paroquial De Mansores - Arouca");
    strcpy(local_recolha[2].concelho[4].brigada,"MANSORES");
    local_recolha[2].concelho[4].hora_de_abertura=16;
    local_recolha[2].concelho[4].min_abertura=00;
    local_recolha[2].concelho[4].hora_fecho=20;
    local_recolha[2].concelho[4].min_fecho=00;


    *qtdLocaisRecolha=*qtdLocaisRecolha+3;
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

void inserir_local_recolha (local_recolha_tipo local_recolha[],  int *qtdLocaisRecolha)
{
 int n,v;

    do
    {
        printf("\nNome da cidade:");
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
        printf("Concelho:");
        scanf ("%s", &local_recolha [*qtdLocaisRecolha].concelho->nome);
        printf ("Local:");
        scanf ("%s", &local_recolha [*qtdLocaisRecolha].concelho->local);
        printf ("Brigada:");
        scanf ("%s", &local_recolha [*qtdLocaisRecolha].concelho->brigada);
        printf ("hora abertura:");
        fflush(stdin);
        scanf ("%d", &local_recolha [*qtdLocaisRecolha].concelho->hora_de_abertura);
        printf("minutos de abertura:");
        fflush(stdin);
        scanf("%d", &local_recolha[*qtdLocaisRecolha].concelho->min_abertura);
        printf("Hora de fecho:");
        fflush(stdin);
        scanf("%d", &local_recolha[*qtdLocaisRecolha].concelho->hora_fecho);
        printf("Min de fecho:");
        fflush(stdin);
        scanf ("%d", &local_recolha[*qtdLocaisRecolha].concelho->min_fecho);

        printf ("Se deseja inserir outro local digite 1 se pretende sair digite 2:");
        scanf ("%d", &n);
    }
    while (n==1);
}
void mostrar_locais(local_recolha_tipo local_recolha[MAX_CIDADES], int *qtdLocaisRecolha)
{
    for (int i = 0; i < *qtdLocaisRecolha; i++)
    {
        printf("cidade:             %s\n", local_recolha[i].cidade);
        printf("data_recolha de recolha: %d-%02d-%02d\n", local_recolha[i].data.ano, local_recolha[i].data.mes, local_recolha[i].data.dia);

        for (int j = 0; j < MAX_CONCELHOS; j++)
        {
            if (strcmp(local_recolha[i].concelho[j].nome, "-") == 0) //nao aparece se nao for preenchido
                break;
            printf("  nome do concelho:        %s\n", local_recolha[i].concelho[j].nome);
            printf("  local:                   %s\n", local_recolha[i].concelho[j].local);
            printf("  brigada:                 %s\n", local_recolha[i].concelho[j].brigada);

            printf("  horas de abertura:       %02d:%02d h\n", local_recolha[i].concelho[j].hora_de_abertura, local_recolha[i].concelho[j].min_abertura);
            printf("  horas de fecho:          %02d:%02d h\n", local_recolha[i].concelho[j].hora_fecho, local_recolha[i].concelho[j].min_fecho);
            printf("\n");
        }
        printf("-------------------------------------------------------------------------------------------------------\n\n");
    }
}
void listar_locais(local_recolha_tipo local_recolha[MAX_CIDADES], int *qtdLocaisRecolha)
{
    printf("locais de recolha: \n");
    for (int i = 0; i < *qtdLocaisRecolha; i++)
    {
        printf("\t%d).\t%s\n", i + 1, local_recolha[i].cidade);
    }
    printf(".\n");
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
    for (int k = 0; k < *qtdLocaisRecolha; k++) //Verifica se o local de recolha introduzido existe no registo e, se tal for verdade, elimina os dados desse local
    {
        if (strcmp(local_recolha[k].cidade, local_a_eliminar) == 0)
        {
            for (int y = k; y < *qtdLocaisRecolha; y++) //for (int y = k; y < *qtdLocaisRecolha - 1; y++)
            {
                local_recolha[y] = local_recolha[y + 1]; //pegar nos que vem a seguir e colocam os superiores na posição inferior
            }
            printf("Local eliminado! \n");
            flag = 1;
            break;
        }
    }
    if (flag != 1)
    {
        printf("Local de recolha nao encontrado! \n"); //se não for encontrado o local ele tira um
    }
    else
    {
        *qtdLocaisRecolha -= 1;
    }
}

void mostrar_LocaisRecolha_Abertos(local_recolha_tipo *local_recolha, int *qtdLocalRecolha)
{
    // declare a char buffer
    char stringbuffer[100];

    data_tipo data;
    concelho_tipo concelho;

    do
    {

        printf("Introduza a data pretendida.\n");
        printf("Dia (dd): ");
        scanf("%d", &data.dia);

        printf("Mes (mm): ");
        scanf("%d", &data.mes);

        printf("Ano (aaaa): ");
        scanf("%d", &data.ano);


    }
    while(!validar_data(data.dia,data.mes,data.ano));

    do
    {
        printf("Introduza a hora de abertura (formato \"hh:mm\"): ");
        fflush(stdin);
        fgets(stringbuffer,100,stdin);
        sscanf(stringbuffer,"%d:%d",&concelho.hora_de_abertura,&concelho.min_abertura);
    }
    while(!validar_hora(concelho.hora_de_abertura,concelho.min_abertura));
    do
    {
        printf("Introduza a hora de fecho (formato \"hh:mm\"): ");
        fflush(stdin);
        fgets(stringbuffer,100,stdin);
        sscanf(stringbuffer,"%d:%d",&concelho.hora_fecho,&concelho.min_fecho);
    }
     while(!validar_hora(concelho.hora_fecho,concelho.min_fecho));

    for(int i=0; i<*qtdLocalRecolha; i++)
    {
        if(local_recolha[i].data.ano == data.ano
           && local_recolha[i].data.mes == data.mes
           && local_recolha[i].data.dia == data.dia)
        {

            for(int j=0; j<5; j++)
            {
                if(local_recolha[i].concelho[j].hora_de_abertura >= concelho.min_abertura
                        //&& horaabertura.minutos >= localrecolhas[i].concelhos[j].hora_abertura->minutos
                        && local_recolha[i].concelho[j].hora_fecho<=concelho.min_fecho
                        //&& localrecolhas[i].concelhos[j].hora_fecho->minutos<=horafecho.minutos
                  )
                {
                    mostrar_locais(local_recolha, &qtdLocalRecolha);
                    printf("\n");

                }
            }
        }
    }
}


int menu_principal ()
{
    int mp;
    printf("1_Gestao de Dadores de Sangue\n");
    printf("2_Gestao de Locais de Recolha de Sangue\n");
    printf("3_Recolha de Sangue\n");
    printf("4_Estatisticas\n");
    printf("0_Sair\n");
    scanf("%d", &mp);

    return mp;

}

int menu1 ()
{
    int m1;
    printf("1_Inserir Dador\n");
    printf("2_Eliminar Dador\n");
    printf("3_Consultar Dadores Galardoados\n");
    printf("4_Listar Todos Os Dadores\n");
    printf("0_Sair\n");
    scanf("%d", &m1);

    return m1;

}

int menu_2 ()
{
    int m2;
    printf("1-Registar dados de um Local de Recolha\n");
    printf("2-Eliminar Local de Recolha\n");
    printf("3-Mostrar Local de Recolha abertos em determinado periodo\n");
    printf("4-Listar Local de Recolha\n");
    printf("0-Sair\n");
    scanf("%d", &m2);
    return m2;
}

int main()
{
    int qtdDADORES=0,mp,m1;
    dador_tipo dador[MAX_DADORES];
    local_recolha_tipo local_recolha [MAX_CIDADES];
    concelho_tipo concelho [MAX_CONCELHOS];
    int qtdLocaisRecolha,m2;
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

                    if(qtdDADORES < MAX_DADORES)
                    {
                        inserir_dador (dador, &qtdDADORES);
                    }
                    else
                        printf("Não é possivel inserir mais dadores\n");

                    break;
                case 2:
                    mostrar_dadores (dador, qtdDADORES);
                    eliminar_dador (dador, &qtdDADORES);
                    break;
                case 3:
                    consultar_dadores_galardoados (dador, qtdDADORES);
                    break;
                case 4:
                    mostrar_dadores (dador, qtdDADORES);
                    break;
                }
            }
            while (m1 != 0);
            break;
            case 2:
            system("cls");
            inicializar_local_recolha(local_recolha, &qtdLocaisRecolha);
            do
            {
                m2 = menu_2 ();
                switch (m2)
                {
                case 1:
                    if(qtdLocaisRecolha < MAX_CIDADES)
                    {
                       inserir_local_recolha (local_recolha, &qtdLocaisRecolha);
                    }
                    else
                        printf("Não é possivel inserir mais cidades\n");

                    break;

                case 2:
                    mostrar_locais(local_recolha, &qtdLocaisRecolha);
                    eliminar_local_recolha (local_recolha, &qtdLocaisRecolha);
                    break;

                case 3:
                    mostrar_LocaisRecolha_Abertos(local_recolha, &qtdLocaisRecolha);
                    mostrar_locais(local_recolha, &qtdLocaisRecolha);
                    break;

                case 4:
                    listar_locais(local_recolha, &qtdLocaisRecolha);
                    break;
                    default:;
                }
            }
            while (m2 !=0);
            break;
        }
    }
    while (mp != 0);
    return 0;
}
