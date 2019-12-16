# Tarea3-Sistemas

#include <stdio.h>
#include <omp.h>
#include <time.h>
#include <stdlib.h>
#include <stdint.h>


uint64_t rdtsc()
{
    unsigned long long lo,hi;
    __asm__ __volatile__ ("rdtsc" : "=a" (lo), "=d" (hi));
    return ((uint64_t)hi << 32) | lo;
}
long long randInt(long long k)
{
    srand(rdtsc());
    return (rand() % k) + 1;
}


int main(int argc, char **argv)
{
	
	int AUN = 1;
	clock_t t1, t2, total_t;
	long double det=1;
    int M;
    printf("INSERTE DIMENSION DE LA MATRIZ\n");
    scanf("%d",&M);
    

 FILE *fp; long long P;
 
      long long **A = (long long **) malloc((M)*sizeof(long long*));
    for(int i = 0; i < M; i++){
        A[i] = (long long *) malloc((M)*sizeof(long long*));
    }
   
    
while(AUN){
	AUN=0;

    for(int i = 0; i < M; i++){
        for(int j = 0; j < M; j++){
            A[i][j] = randInt(100);
        }
    }
    
    
    fp = fopen ("arr.txt","w");
    fprintf(fp, "%d\n", M);
    for(P = 0; P < M*M; P++)
    fprintf (fp, "%lld ", A[0][P]);
    fclose (fp);
    

printf("Matriz creada\n");
/*
 for(int i = 0; i < M; i++){
        for(int j = 0; j < M; j++){
            printf("%lld ", A[i][j]);
            if(!(A[i][j] / 10)) printf(" ");
        }
        printf("\n");
    }
  */

  /*
  
  */
  

 /*
 
  */
 
printf("Iniciando t\n");
 t1 = clock();
 for(int k=0; k<M-1; k++){
	 if(A[k][k]==0){
		printf("%lld \n", A[k][k]);
		printf("ERROR\n");
       AUN= 1;
        break;
        }
  for(int i=k; i<M-1 ;i++){
   for(int j=M-1; j>=k; j--){
      A[i+1][j] = A[i+1][j]-((A[i+1][k]*A[k][j])/A[k][k]);
      }
   }
 }
}
for(int i=0; i<M; i++){
	det*=A[i][i];
	}
printf("la determinante es: %Le \n", det);

t2 = clock();
total_t = (long)((t2 - t1)/CLOCKS_PER_SEC);
	printf("TERMINADO\n");
	printf("\n");
	printf("%ld segundos\n", total_t );

/*
 
    for(int i = 0; i < M; i++){
        for(int j = 0; j < M; j++){
			printf("%lld ", A[i][j]);
            if(!(A[i][j] / 10)) printf(" ");
        }
        printf("\n");
    }
  */

    
    


 /*

  */
	return 0;
}
