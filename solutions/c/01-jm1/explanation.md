The entry point for your Redis implementation is in `src/main.c`.

Study and uncomment the relevant code: 

```c
// Uncomment this block to pass the first stage

int server_fd, client_addr_len;
struct sockaddr_in client_addr;

server_fd = socket(AF_INET, SOCK_STREAM, 0);
if (server_fd == -1) {
	printf("Socket creation failed: %s...\n", strerror(errno));
	return 1;
}

// Since the tester restarts your program quite often, setting SO_REUSEADDR
// ensures that we don't run into 'Address already in use' errors
int reuse = 1;
if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR, &reuse, sizeof(reuse)) < 0) {
	printf("SO_REUSEADDR failed: %s \n", strerror(errno));
	return 1;
}

struct sockaddr_in serv_addr = { .sin_family = AF_INET ,
								 .sin_port = htons(6379),
								 .sin_addr = { htonl(INADDR_ANY) },
								};

if (bind(server_fd, (struct sockaddr *) &serv_addr, sizeof(serv_addr)) != 0) {
	printf("Bind failed: %s \n", strerror(errno));
	return 1;
}

int connection_backlog = 5;
if (listen(server_fd, connection_backlog) != 0) {
	printf("Listen failed: %s \n", strerror(errno));
	return 1;
}

printf("Waiting for a client to connect...\n");
client_addr_len = sizeof(client_addr);

accept(server_fd, (struct sockaddr *) &client_addr, &client_addr_len);
printf("Client connected\n");

close(server_fd);
```

Push your changes to pass the first stage:

```
git add .
git commit -m "pass 1st stage" # any msg
git push origin master
```
