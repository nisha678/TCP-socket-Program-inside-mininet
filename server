#include<stdio.h>
#include<string.h>
#include<sys/socket.h>
#include<arpa/inet.h>	
#include<unistd.h>		
#include<time.h> 

int main(int argc , char *argv[])
{
    int i, j, k, socket_desc ,client_sock ,c ,read_size;
    struct sockaddr_in server ,client;
    char client_message[2000];							
    time_t rawtime;
    struct tm * timeinfo;
 
    // Create socket
    socket_desc = socket(AF_INET , SOCK_STREAM , 0);
    if (socket_desc == -1)
    {
        printf("Could not create socket");
		return 1;
    }
	
    puts("Socket created");
     
    // Prepare the sockaddr_in structure
    server.sin_family = AF_INET;
    server.sin_addr.s_addr = INADDR_ANY;
    server.sin_port = htons( 8888 );
     
    // Bind
    if( bind(socket_desc,(struct sockaddr *)&server , sizeof(server)) < 0)
    {
        perror("bind failed. Error");
        return 1;
    }
	
    puts("bind done");
     
    // Listen
    listen(socket_desc , 3);
     
    // Accept
    puts("Waiting for incoming connections...");
    c = sizeof(struct sockaddr_in);
     
    //accept connection from an incoming client
    client_sock = accept(socket_desc, (struct sockaddr *)&client, (socklen_t*)&c);
	
    if (client_sock < 0)
    {
        perror("accept failed");
        return 1;
    }
	
    puts("Connection accepted");
     
    //Receive a message from client
    while( (read_size = recv(client_sock , client_message , 2000 , 0)) > 0 )
    {
		time(&rawtime);
		timeinfo = localtime (&rawtime);
	
		if(client_message[0]=='1')
		{
			memset(client_message,0,2000);
			sprintf(client_message,"%s","List of items\n> Mango (Press \"a\" to purchase)\n> Apple (Press \"b\" to purchase)\n> Orange(Press \"c\" to purchase)");
       		write(client_sock , client_message , strlen(client_message));
		}
		else if(client_message[0]=='a')
		{
			//Send the message back to client about the mango
			memset(client_message,0,2000);
			if((20-i)>5)
			{
				sprintf(client_message,"%s : %d : %s","Purchase history:\nMango",20-i,asctime(timeinfo));
				printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
				i++;
			}
			else if((20-i)>0 && (20-i)<=5)
			{
				sprintf(client_message,"%s : %d : %s","Purchase history: ( Warning limited stock )\nMango",20-i,asctime(timeinfo));
				printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
				i++;
			}
			else
			{
				sprintf(client_message,"%s","Mango is Out of Stock");
				printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
			}
		}
		else if(client_message[0]=='b')
        {
			//Send the message back to client about the apple
			memset(client_message,0,2000);
			if((20-j)>5)
			{
				sprintf(client_message,"%s : %d : %s","Purchase history:\nApple",20-j,asctime(timeinfo));
				printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
				j++;
			}
			else if((20-j)>0 && (20-j)<=5)
			{
				sprintf(client_message,"%s : %d : %s","Purchase history: ( Warning limited stock )\nApple",20-j,asctime(timeinfo));
                printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
				j++;
			}
			else
			{
				sprintf(client_message,"%s","Apple is Out of Stock");
				printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
			}
        }
		else if(client_message[0]=='c')
        {
			//Send the message back to client about the Orange
			memset(client_message,0,2000);
			if((20-k)>5)
			{
				sprintf(client_message,"%s : %d : %s","Purchase history:\nOrange",20-k,asctime(timeinfo));
				printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
				k++;
			}
			else if((20-k)>0 && (20-k)<=5)
			{
				sprintf(client_message,"%s : %d : %s","Purchase history: ( Warning limited stock )\nOrange",20-k,asctime(timeinfo));
                printf("%s",client_message);
				write(client_sock , client_message , strlen(client_message));
				k++;
			}
			else
			{
				sprintf(client_message,"%s","Orange is Out of Stock");
				printf(" %s",client_message);  
				write(client_sock , client_message , strlen(client_message));
			}
		}
	}
     
    if(read_size == 0)
    {
        puts("Client disconnected");
        fflush(stdout);
    }
    else if(read_size == -1)
    {
        perror("recv failed");
    }
     
    return 0;
}
