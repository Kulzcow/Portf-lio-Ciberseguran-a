#**INTRO**

>Krypton é a introdução para codificação/decodificação e criptografia. Nela, o usuário aprende a *procurar* ao invés de simplesmente seguir o código.
>Um laboratório interativo e prático, ensinando como realizar funções um pouco mais avançadas para desvendar senhas próprias.
>É esperado conhecimento sobre as funções do **Bandit**. Não faça esse laboratório antes, muitas coisas vão passar despercebidas, mesmas coisas que serão fáceis caso realize o Camp anterior.

___

## Krypton 0 -> 1

>Bem vindo ao Krypton! Esse nível é fácil. A string a seguir codifica a senha usando Base64:
>S1JZUFRPTklTR1JFQVQ=
>Use essa senha para logar no krypton.labs.overthewire.org com o usuário krypton1 usando SSH na porta 2231. Você pode encontrar as senhas para os próximos níveis em `/krypton`.

Incrivelmente fácil, e retorna para os níveis de decodificação do Bandit. Utilizo o sistema de decodificação do `Base64` após dar `echo` da senha:

```bash
echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d
```

A senha logo aparece ao lado do meu usuário.

___

## Krypton 1 -> 2

>A senha do nível 2 está no arquivo `krypton2`. Está 'codificado' usando uma rotação simples.

É muito simples, apenas utilizando a rotação que aprendemos no Bandit: `ROT13`. Identificando o arquivo, eu utilizo o mesmo 'cheatsheet' do que aprendi no ROT13, copiando das minhas anotações, e colando junto com a cifra:

```bash
cat krypton2 | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

Facilmente assim, adquiro a senha para o próximo nível.

___

## Krypton 2 -> 3

>ROT13 é uma simples cifra de substituição...

Krypton 2 utiliza a cifra de **CAESAR** para fazer a criptografia do arquivo `krypton3`. Existem alguns arquivos dentro da pasta junto com ele, `encrypt` que utiliza a cifra para rapidamente criptografar, `keyfile.dat` que mostra para o encrypt como criptografar, e o `README` mostrando como esses arquivos são utilizados para fazer a criptografia.

Como visto no `README`, crio uma pasta temporária e utilizo o comando `ln -s`, que cria um link a partir do nome do arquivo; basta eu colocar o caminho `/krypton/krypton2/keyfile.dat` e ele está na pasta como se tivesse sido copiado. `encrypt` roda com as permissões de krypton 3, então dou permissão total para a minha pasta.

Rodo agora um `echo` básico com o alfabeto inteiro e salvo em um arquivo chamado `alphabet`, ele será minha base para saber como é feita a criptografia. Usar o arquivo é simples:

```bash
/krypton/krypton2/encrypt [TMPFILE]/alphabet
```

Logo recebo o arquivo `ciphertext`. Agora, tenho a base de como será a senha:

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
M N O P Q R S T U V W X Y Z A B C D E F G H I J K L

Quando abri o `krypton3`, a senha foi dada. Utilizo essa base ao lado, e vejo quais letras utilizar para decriptografar. Por exemplo, **O** na verdade seria o **C**, **Q** seria o **E**, adiante. Com isso, tenho a senha para o próximo Krypton, e conhecimento sobre como decriptografar uma cifra CAESAR.

___

## Krypton 3 -> 4

>Muito bem. Você passou de uma cifra fácil de substituição. A maior fraqueza de uma cifra de substituição é o uso repetido de uma *key* fácil. No último nível...
>Nesse exemplo, o mecanismo da cifra não vai estar disponível para você, o *attacker*. A senha do próximo nível está em `krypton4`.