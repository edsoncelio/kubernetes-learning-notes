# Comandos para debug/troubleshooting

#### `kubectl logs <pod-name>`
Ver os logs do pod, observações:
* se o pod que quiser ver não estiver no namespace default, usar o parâmetro -n <namespace-name>
* se o pod tiver multiplos containers, usar o parâmetro -c <container-name>
* por padrão, são exibidos os logs e depois o comando encerra, para acompanhar em tempo real adicionar o parâmetro -f

#### `kubectl exec -it <pod-name> -- bash`
Abrir uma sessão do bash dentro do pod, observações:
* se o pod que quiser ver não estiver no namespace default, usar o parâmetro -n <namespace-name>

#### `kubectl attach -it <pod-name>`

TODO

#### `kubectl cp <pod-name>:</path/to/remote/file> </path/to/local/file>`
Copiar arquivos de um pod para um diretório local, observações:
* se o pod que quiser ver não estiver no namespace default, usar o parâmetro -n <namespace-name>
  
#### `kubectl port-forward <pod-name> 8080:80`
Encaminhar o tráfego da máquina local para o pod, observações:
* se o pod que quiser ver não estiver no namespace default, usar o parâmetro -n <namespace-name>

#### `kubectl top pods`
Exibir todos os pods e uso de recursos (se quiser ver em um namespace específico usar -n)

#### `kubectl top nodes`
Exibir o total de CPU e memória em uso pelos nodes
