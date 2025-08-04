# Atualizar um arquivo por meio de um algoritmo Python

## Descrição do projeto

Na minha organização, o acesso a conteúdo restrito é controlado por uma lista de IPs permitidos. O arquivo `allow_list.txt` identifica esses endereços IP. Uma lista de remoção separada identifica os IPs que não devem mais ter acesso a esse conteúdo. Eu criei um algoritmo para automatizar a atualização do arquivo `allow_list.txt` e remover esses IPs que não devem mais ter acesso.

## Abrir o arquivo que contém a lista de IPs permitidos

Para a primeira parte do algoritmo, abri o arquivo `allow_list.txt`. Primeiro, atribuí esse nome de arquivo como uma string à variável `import_file`:

```python
import_file = "allow_list.txt"
```

Em seguida, usei uma instrução `with` para abrir o arquivo:

```python
with open(import_file, "r") as file:
```

No meu algoritmo, a instrução `with` é usada com a função `.open()` no modo de leitura para abrir o arquivo da lista de IPs permitidos. O objetivo de abrir o arquivo é permitir que eu acesse os endereços IP armazenados nele. A palavra-chave `with` ajuda a gerenciar os recursos ao fechar automaticamente o arquivo ao sair do bloco with. No código `with open(import_file, "r") as file:`, a função `open()` tem dois parâmetros: o primeiro identifica o arquivo a ser importado, e o segundo indica o que eu quero fazer com ele. Neste caso, `"r"` indica que quero lê-lo. O código também usa a palavra-chave `as` para atribuir o resultado da função `open()` à variável `file`, que será usada dentro do bloco with.

## Ler o conteúdo do arquivo

Para ler o conteúdo do arquivo, usei o método `.read()` para convertê-lo em uma string:

```python
with open(import_file, "r") as file:
    ip_addresses = file.read()
```

Ao usar a função `.open()` com o argumento `"r"` para leitura, posso chamar o método `.read()` dentro do corpo da instrução with. O método `.read()` converte o conteúdo do arquivo em uma string, permitindo que eu a leia. Apliquei o método `.read()` à variável `file` identificada na instrução with e atribuí a saída em forma de string à variável `ip_addresses`.

Resumidamente, esse código lê o conteúdo do arquivo `allow_list.txt` e o converte para o formato de string, o que me permite usá-lo posteriormente para organizar e extrair dados no meu programa Python.

## Converter a string em uma lista

Para remover endereços IP individuais da lista de permitidos, eu precisava que ela estivesse no formato de lista. Por isso, usei o método `.split()` para converter a string `ip_addresses` em uma lista:

```python
ip_addresses = ip_addresses.split()
```

A função `.split()` é chamada ao ser anexada a uma variável do tipo string. Ela funciona convertendo o conteúdo da string em uma lista. O objetivo de dividir `ip_addresses` em uma lista é facilitar a remoção de IPs da lista permitida. Por padrão, a função `.split()` divide o texto por espaços em branco. Neste algoritmo, ela pega os dados armazenados na variável `ip_addresses` (uma string com IPs separados por espaços) e os converte em uma lista de endereços IP. Para armazenar essa lista, reatribui o resultado à própria variável `ip_addresses`.

## Iterar pela lista de remoção

Uma parte fundamental do meu algoritmo envolve iterar pelos endereços IP contidos na `remove_list`. Para isso, usei um laço `for`:

```python
for element in remove_list:
```

O laço `for` em Python repete trechos de código para uma sequência específica. O objetivo geral do `for` em um algoritmo como este é aplicar determinadas instruções a todos os elementos de uma sequência. A palavra-chave `for` inicia o laço, seguida pela variável de iteração `element` e pela palavra-chave `in`, que indica que se deve iterar sobre a sequência `remove_list` e atribuir cada valor à variável `element`.

## Remover IPs que estão na lista de remoção

Meu algoritmo precisa remover da lista `ip_addresses` qualquer endereço IP que também esteja presente na `remove_list`. Como não havia duplicatas em `ip_addresses`, consegui usar o seguinte código para isso:

```python
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)
```

Primeiro, dentro do laço `for`, criei uma condicional que avalia se o elemento atual (`element`) está presente na lista `ip_addresses`. Fiz isso porque aplicar `.remove()` a elementos que não estão na lista resultaria em erro.

Em seguida, dentro dessa condicional, apliquei `.remove()` à lista `ip_addresses`, passando a variável `element` como argumento, de modo que cada endereço IP presente na `remove_list` fosse removido de `ip_addresses`.

## Atualizar o arquivo com a nova lista de IPs

Como etapa final do meu algoritmo, precisei atualizar o arquivo com a nova lista de IPs permitidos. Para isso, primeiro converti a lista novamente em uma string usando o método `.join()`:

```python
ip_addresses = "\n".join(ip_addresses)
```

O método `.join()` combina todos os itens de um iterável em uma única string. Ele é aplicado a uma string que conterá os caracteres separadores entre os itens. Neste algoritmo, usei `.join()` para criar uma string a partir da lista `ip_addresses`, para que pudesse passá-la como argumento do método `.write()` ao escrever no arquivo `allow_list.txt`. Usei a string `"\n"` como separador para instruir o Python a colocar cada elemento em uma nova linha.

Depois, usei outra instrução `with` e o método `.write()` para atualizar o arquivo:

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

Desta vez, usei o segundo argumento `"w"` com a função `open()` na minha instrução with. Esse argumento indica que desejo abrir o arquivo para sobrescrever seu conteúdo. Ao usar esse argumento `"w"`, posso chamar o método `.write()` dentro do bloco with. O método `.write()` grava dados do tipo string em um arquivo específico, substituindo qualquer conteúdo existente.

Neste caso, quis escrever a lista de IPs atualizada no arquivo `allow_list.txt`. Assim, o conteúdo restrito não será mais acessível aos IPs que foram removidos da lista de permitidos. Para reescrever o arquivo, apliquei o método `.write()` ao objeto `file` definido na instrução with, passando a variável `ip_addresses` como argumento para especificar que o conteúdo do arquivo deve ser substituído pelos dados dessa variável.

## Código completo

```python
# Definir o nome do arquivo
import_file = "allow_list.txt"

# Lista de IPs a serem removidos
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

# Abrir e ler o arquivo
with open(import_file, "r") as file:
    ip_addresses = file.read()

# Converter string em lista
ip_addresses = ip_addresses.split()

# Iterar pela lista de remoção e remover IPs
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

# Converter lista de volta para string
ip_addresses = "\n".join(ip_addresses)

# Atualizar o arquivo com a nova lista
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

## Resumo

Criei um algoritmo que remove os endereços IP identificados na variável `remove_list` do arquivo `allow_list.txt`, que contém os IPs permitidos. Esse algoritmo envolve abrir o arquivo, convertê-lo em uma string para leitura, e depois converter essa string em uma lista armazenada na variável `ip_addresses`. Em seguida, iterei pelos IPs em `remove_list`. A cada iteração, avaliei se o elemento estava na lista `ip_addresses`. Se estivesse, apliquei o método `.remove()` para removê-lo. Após isso, usei o método `.join()` para converter `ip_addresses` novamente em string, e então sobrescrevi o conteúdo do arquivo `allow_list.txt` com a lista atualizada de IPs.