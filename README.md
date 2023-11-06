# spotifyclone
This is small project in which I have created Spotify webpage clone by using HTML and Vanilla CSS.


#include<stdio.h>

#include<stdlib.h>

#include<curses.h>



void main()

{

 int allocated[20][20],max[20][20],available[20]={0},need[20][20],total[20];

 int finish[20]={0};

 int cntProcess,cntRes,process,res,flag,execFlag,executed;



 printf("Enter no. of processes: ");

 scanf("%d",&process);

 printf("\nEnter no. of resources: ");

 scanf("%d",&res);

 printf("\nEnter the maximum instance of each resource:\n");

 for(cntRes=0;cntRes<res;cntRes++)

	{

	 printf("\n\tNo. of instance of resource #%d: ",cntRes);



	 scanf("%d",&total[cntRes]);

	}

 printf("\nEnter the maximum requirement of each process:\n");

 for(cntProcess=0;cntProcess<process;cntProcess++)

	{

	 printf("\nProcess :-%d:\n",cntProcess);

	 for(cntRes=0;cntRes<res;cntRes++)

		{

		 printf("\n\tRequirement for resource :-%d: ",cntRes);



		 scanf("%d",&max[cntProcess][cntRes]);

		}

	}

 printf("\nEnter the current allocation for each process:\n");

 for(cntProcess=0;cntProcess<process;cntProcess++)

	{

	 printf("\nProcess :-%d:\n",cntProcess);

	 for(cntRes=0;cntRes<res;cntRes++)

		{

		 printf("\n\tAllocation for resource :-%d: ",cntRes);



		 scanf("%d",&allocated[cntProcess][cntRes]);

		}

	}



 for(cntRes=0;cntRes<res;cntRes++)

	{ 	

	 for(cntProcess=0;cntProcess<process;cntProcess++)

		{

		 available[cntRes]+=allocated[cntProcess][cntRes];

		}

	 

	 available[cntRes]=total[cntRes]-available[cntRes];

	}

 printf("\nThe available instances of each resource are:\n");

 for(cntRes=0;cntRes<res;cntRes++)

	{

	 printf("\nResource :-%d: %d",cntRes,available[cntRes]);

	}



 for(cntProcess=0;cntProcess<process;cntProcess++)

	{

	 for(cntRes=0;cntRes<res;cntRes++)

		{

		 need[cntProcess][cntRes]=max[cntProcess][cntRes]-allocated[cntProcess][cntRes];

		}

	}

 printf("\n\nThe NEED matrix is:\n\n");

 for(cntProcess=0;cntProcess<process;cntProcess++)

	{

	 for(cntRes=0;cntRes<res;cntRes++)

		{

		 printf("\t%d",need[cntProcess][cntRes]);

		}

	 printf("\n\n");

	}



 printf("\nThe processes are executed in the foll. sequence:\n\n");

 executed=0;

do

{

 for(cntProcess=0,execFlag=0;cntProcess<process;cntProcess++)

	{

	 flag=0;	

	 if(finish[cntProcess]!=0)

		continue;

	 else

		{

		 for(cntRes=0;cntRes<res;cntRes++)

			{

			 if(need[cntProcess][cntRes]>available[cntRes])

				{	

				 flag=1;

				 break;

				}

			}

		 if(flag==0)

			{

			 printf("\tP%d",cntProcess);

			 finish[cntProcess]=1;

			 for(cntRes=0;cntRes<res;cntRes++)

				{

				 available[cntRes]+=allocated[cntProcess][cntRes];

				}

			 execFlag=1;

			 executed++;

			}

		}

	}

 if(execFlag==0)

	{	

	 printf("\n\nThe system is in an UNSAFE state!");

	 break;

	}

 }while(executed<process);



}
