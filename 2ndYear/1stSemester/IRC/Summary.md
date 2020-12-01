# Introdução às Redes de Comunicação

## **Resumo Funções UDP**

**Endereço IP para Broadcast:**
```c
// 255.255.255.255
serv_addr.sin_addr.s_addr = inet_addr("255.255.255.255");
```

**Ativar o envio para toda a gente:**

```c
setsockopt(sockfd, SOL_SOCKET, SO_BROADCAST (SO_RCVTIMEO), (char *)&opt, sizeof(opt));
```

**Iniciar winsocks:**
```c
WSAStartup(MAKEWORD(2,2), &wsadata);
```

**Criar socket:** 
```c 
SOCKET(PF_INET, SOCK_DGRAM, 0);
// Erro -> INVALID_SOCKET
```

**Associar socket ao endereço de escuta (recebe datagramas de qualquer interface na porta pretendida):**
```c
memset((char*)&serv_addr, 0, sizeof(serv_addr));
serv_addr.sin_family = AF_INET;
serv_addr.sin_addr.s_addr = htonl(...); //inet_addr(...) //string
serv_addr.sin_port = htons(...); //int
```

**Definir timeout:**

```c
struct timeval timeout;
timeout.tv_sec = TIMEOUT;
timeout.tv_usec = 0;
```

**Enviar datagramas:**

```c
// enviar -> socket, valor a enviar(smp fazer a conversao), tamanho do var a enviar, para onde enviar, tamanho
sendto(sockfd, (char*)&sentValue, sizeof(sentValuue), (struct sockaddr*)&serv_addr, sizeof(serv_addr))
// Erro -> SOCKET_ERROR
```

**Receber datagramas:**

```c
//receber -> socket, valor a enviar(smp fazer a conversao), tamanho do var a enviar, para onde enviar, tamanho
nbytes = recvfrom(sockfd, receber, sizeof(response), 0, (struct sockaddr *)&serv_addr, &size);
// Erro -> SOCKET_ERROR
```

**Ver timeout:**

```c
WSAGetLastError() == WSAETIMEDOUT;
```

**Terminar uma string:**

```c
response[nbytes] = '\0';
```

**Fechar socket:**

```c
closesocket(sockfd);
```

**Por o valor total na variável response:**

```c
sprintf(response, "Sum of values: %lf", total);
sprintf_s(response, sizeof(response), "Sum of values: %lf", total);
```

**Verificar se a mensagem recebida foi enviada pelos servidor e não um impostor:**

```c
if (strcmp(inet_ntoa(addr.sin_addr), inet_ntoa(serv_addr.sin_addr)) && atoi(itoa(addr.sin_port==serv_addr.sin_port)))
```

**[Página Inicial](../../../index.md) | [Página Anterior](./Main.md)**