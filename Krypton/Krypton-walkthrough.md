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