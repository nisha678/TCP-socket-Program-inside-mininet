#include<stdio.h>
#include<string.h>
#include<sys/socket.h>
#include<arpa/inet.h>
 
int main(int argc , char *argv[])
{
    int sock;
    struct sockaddr_in server;
    char message[1000],server_reply[2000];
     
    // Create socket
    sock = socket(AF_INET , SOCK_STREAM , 0);
    if (sock == -1)
    {
        printf("Could not create socket");
		return 1;
  }
    puts("Socket created");
     
	// Prepare the sockaddr_in structure
    server.sin_addr.s_addr = inet_addr("127.0.0.1");
    server.sin_family = AF_INET;
    server.sin_port = htons( 8888 );
 
    //Connect to remote server
    if (connect(sock , (struct sockaddr *)&server , sizeof(server)) < 0)
    {
        perror("connect failed. Error");
        return 1;
    }
    puts("Connected\n");
     
    // to keep communicating with server
    while(1)
    {
        printf("\npress 1 to list the fruits\npress 2 to exit\n");
        scanf("%s", message);
		printf("\n");
		
		if(message[0]=='1'|| message[0]=='a'|| message[0]=='b'|| message[0]=='c' )
		{
       		 //Send some data
       		 if( send(sock , message , strlen(message) , 0) < 0)
       		 {
           		 puts("Send failed");
          		 return 1;
       		 }
         
       		 //Receive a reply from the server
       		 if( recv(sock , server_reply , 2000 , 0) < 0)
       		 {
           		 puts("recv failed");
           		 break;
       		 }
			 
			 puts(server_reply);
			 memset(server_reply,0,2000);
		}
		else if (message[0]=='2') 
		{ 
			close(sock);
    		return 0;
		}
	}
}
