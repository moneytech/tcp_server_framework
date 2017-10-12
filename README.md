# tcp_server_framework 
A simple tcp server framework, just for fun:  
(1) For one connected socket, one thread processing;  
(2) Only 2 APIs (start_tcp_server, stop_tcp_server) provided for application.  

## Example  

	#include <unistd.h>
	#include "tcp_server_framework.h"
	
	/* enum definitions */
	typedef enum
	{
	    EXIT_CODE_SUCCESS = 0,
	    EXIT_CODE_ERROR
	} EXIT_CODE;
	
	/* function declarations */
	
	/* function definitions */
	
	
	int main(void)
	{
	    /* local variables definitions */
	    TCP_SERVER_HANDLE handle = INVALID_TCP_SERVER_HANDLE;
	    listen_addr addr_array[] = {{"\0", 9001, NULL, NULL}, {"\0", 9002, NULL, NULL}, {"\0", 9003, NULL, NULL}};
	    
	    /* code body */
	    handle = start_tcp_server(addr_array, (sizeof(addr_array) / sizeof(addr_array[0])));
	    if (INVALID_TCP_SERVER_HANDLE == handle)
	    {
	        goto MAIN_ERR_END;
	    }
	
	    sleep(30);
	    stop_tcp_server(handle);
	    return EXIT_CODE_SUCCESS;
	    
	MAIN_ERR_END:
	    return EXIT_CODE_ERROR;
	}
Build and run it: 

	$ gcc -g -pthread -o tcp_server_framework_test main.c tcp_server_framework.c
	$ ./tcp_server_framework_test
