# Salvando e gerenciando segredos com secrets
Secrets é um recurso do kubernetes usado para armazenar informações sensíveis, como tokens e senhas que são usadas pelo pods.
Um secret pode ser usado por um pod de 3 formas:
* como um arquivo montado em um volume em 1 ou mais containers
* como variável de ambiente
* pelo kubelet para baixar imagens para o pod

## Criando secrets com o kubectl 

### Criar um secret usando o kubectl a partir de um arquivo:
1. criar um token e salvar em um arquivo, por ex:  
`echo -n 'AHUSHUAHUSHA' > token.txt`  
2. Criar o secret `access-token` a partir do arquivo criado:  
`kubectl create secret acess-token --from-file=token.txt`

### Criar um secret usando o kubectl a partir de string literal:
`kubectl create secret access-token --from-literal=AHUSHUAHUSHA`

### Criar secret manualmente
Os segredos são codificados em base 64, então para criar manualmente:
1. Codificar o token para base64:
`echo -n 'AHUSHUAHUSHA' | base64`
2. Adicionar o valor codificado no manifesto `secrets.yaml`:
```
apiVersion: v1
kind: Secret
metadata:
  name: access-token
type: Opaque
data:
  access-token: DSRtaW4GDSA
```
3. Criar o secret a partir do manifesto:
`kubectl apply -f secrets.yaml`

### Criar secret a partir de um generator
TODO

## Usando secrets nos pods

### Montando secret em um volume:
```
volumeMounts:
    - name: data
      mountPath: "/opt/data"
      readOnly: true
  volumes:
  - name: data
    secret:
      secretName: access-token
```

### Usando secrets como variável de ambiente
```
env:
      - name: SECRET_TOKEN
        valueFrom:
          secretKeyRef:
            name: access-token
            key: username
      - name: SECRET_TOKEN
        valueFrom:
          secretKeyRef:
            name: access-token
            key: access-token
```
