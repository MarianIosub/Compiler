#include <stdio.h>
#include <string.h>

struct var{
    char nume[250];
    char tip[20];                            
    char domeniu[20];                        
    int val;
    float val_f;
}dataVar[500];

int nrVar;
int error;
int structVar;
char toPrint[500];

int check_varDec(char* nume1){
    for(int i=0;i<nrVar;i++){
        if(!strcmp(dataVar[i].nume,nume1) && strcmp(dataVar[i].domeniu,"funct_arg"))
            return 1;
    }
    return 0;
}


void insert_var(char* nume1, float val1, char* tip1, char* domeniu1){
    if(check_varDec(nume1))
        error=1;
    strcpy(dataVar[nrVar].nume,nume1);
    dataVar[nrVar].val=val1;
    strcpy(dataVar[nrVar].tip,tip1);
    if(!strcmp(tip1,"float"))
        dataVar[nrVar].val_f=val1;
    strcpy(dataVar[nrVar].domeniu,domeniu1);
    if(structVar>0 && strcmp(dataVar[nrVar].domeniu,"struct_var"))
        strcpy(dataVar[nrVar].domeniu,"var_inside_struct");
    nrVar++;
}
void insert_f(char * nume1,char* tip1, char* domeniu1){
    if(check_varDec(nume1))
        error=1;
    strcpy(dataVar[nrVar].nume,nume1);
    strcpy(dataVar[nrVar].tip,tip1);
    strcpy(dataVar[nrVar].domeniu,domeniu1);
    if(structVar>0)
        strcpy(dataVar[nrVar].domeniu,"struct_function");
    nrVar++;
}
void insert_struct(char * nume1, char* domeniu1){
    if(check_varDec(nume1))
        error=1;
    strcpy(dataVar[nrVar].nume,nume1);
    strcpy(dataVar[nrVar].domeniu,domeniu1);
    if(structVar>0)
        strcpy(dataVar[nrVar].domeniu,"struct_inside_struct");
    nrVar++;
}

void check_existence(char * numeVar){
    int ok=0;
    for(int i=0;i<nrVar && !ok;i++){
        if(!strcmp(dataVar[i].nume,numeVar) && !strcmp(dataVar[i].domeniu,"global")){
            ok=1;
        }
        if(!strcmp(dataVar[i].nume,numeVar) && !strcmp(dataVar[i].domeniu,"var_inside_struct") && structVar>0){
            ok=1;
        }
    }
    if(ok==0){
        error=2;
        printf("%s\n",numeVar);
    }
}

void check_struct(char * numeStr, int cod){
    int ok=0;
    if(cod==1){
        for(int i=0;i<nrVar && !ok;i++){
            if(!strcmp(dataVar[i].nume,numeStr)&& !strcmp(dataVar[i].domeniu,"struct_var") ){
                ok=1;
            }
        }
    }
    if(cod==2){
        for(int i=0;i<nrVar && !ok;i++){
            if(!strcmp(dataVar[i].nume,numeStr)&& !strcmp(dataVar[i].domeniu,"var_inside_struct")){
                ok=1;
            }
        }
    }
    if(ok==0)
        error=2;
}

void decode_error(){
    if(error==0)
        printf("CORECT SEMANTIC!\n");
    else if(error==1)
        printf("Semantic error. Variable declared more than once\n");
    else if(error==2)
        printf("Semantic error. Variable used in expression or assignment but not declared\n");    
}

void print_var(){
    FILE * wr;
    wr=fopen("symbol_table.txt","w+");
    for(int i=0;i<nrVar;i++){
        if(!strcmp(dataVar[i].domeniu,"funct_arg") || !strcmp(dataVar[i].domeniu,"global_function") 
        || !strcmp(dataVar[i].domeniu,"global_struct") || !strcmp(dataVar[i].domeniu,"struct_inside_struct") 
        || !strcmp(dataVar[i].domeniu,"struct_function") || !strcmp(dataVar[i].domeniu,"struct_var")
        || strstr(dataVar[i].tip,"matrice") || strstr(dataVar[i].tip,"vector"))
            fprintf(wr,"%s %s %s \n",dataVar[i].domeniu,dataVar[i].tip,dataVar[i].nume);
        else{
            if(!strcmp(dataVar[i].tip,"float"))
                fprintf(wr,"%s %s %s = %f\n",dataVar[i].domeniu,dataVar[i].tip,dataVar[i].nume,dataVar[i].val_f);

            else if(!strcmp(dataVar[i].tip,"char"))
                fprintf(wr,"%s %s %s = '%c'\n",dataVar[i].domeniu,dataVar[i].tip,dataVar[i].nume,dataVar[i].val);

            else
                fprintf(wr,"%s %s %s = %d\n",dataVar[i].domeniu,dataVar[i].tip,dataVar[i].nume,dataVar[i].val);
        }
    }
}

int getVal(char* numeVar){
    for(int i=0;i<nrVar;i++)
        if(!strcmp(numeVar,dataVar[i].nume))
            return dataVar[i].val;
}

void updateVal(char* numeVar, int value){
    for(int i=0;i<nrVar;i++)
    if(!strcmp(numeVar,dataVar[i].nume))
        dataVar[i].val=value;
}
