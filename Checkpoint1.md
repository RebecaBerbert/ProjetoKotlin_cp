*********** Descrição do projeto ******************

Este projeto é um aplicativo Android desenvolvido em Android Studio utilizando Kotlin e Jetpack Compose, com o objetivo principal de demonstrar a navegação entre telas e a passagem de parâmetros utilizando o Navigation Component.

*********** Objetivo da Prova ******************

O objetivo da prova é testar se entendemos o projeto e cada commit realizado, especificamente os commits de implementação de parâmetros, tanto os obrigatórios, como os opcionais.

EXPLICAÇÃO DOS COMMITS (Será feita a partir das linhas implementadas em cada commit)

*********** Explicação do Commit "Passagem de parâmetros obrigatórios na tela de Perfil" ******************

A tela de perfil deixar de ser fixa e passar a receber um nome via navegação, exibindo esse valor na interface.

1. Definição da rota com parâmetro obrigatório

"perfil/{nome}"

  - {nome} agora precisa ser informado sempre, o que antes não era necessário, já que a rota não necessitava de um parâmetro
  - Se tentarmos navegar apenas para "perfil", o app não encontrará a rota.

 --------------------

2. Captura do parâmetro

"val nome: String? = it.arguments?.getString("nome", "Usuário Genérico")"

 
 -Pega o valor enviado na navegação
 -Se não vier nada → usa "Usuário Genérico"

 --------------------


3. Envio para a tela

"nome!!"

  - dá a confirmação que a informação não é nula

 --------------------


4. Alteração na navegação (MenuScreen)

"navController.navigate("perfil/Fulano de Tal")"

 - Agora estamos passando um valor "Fulano de tal" preenchendo o {nome} da rota

 --------------------


5. Alteração na interface

"text = "PERFIL - $nome""

 - Agora a tela mostra o nome do usuário e se torna uma Interface dinâmica


*********** Explicação do Commit "Passagem de parâmetros opcionais na tela de Pedidos" ******************

Esse commit mostra como utilizar parâmetros opcionais de forma dinâmica, possibilitando a personalização da tela sem que ela dependa obrigatoriamente desses valores.

1. Alteração da Rota
"route = "pedidos?cliente={cliente}"

 - Transforma o parâmetro em opcioal

 --------------------

2. Definição do argumento opcional
"arguments = listOf(navArgument("cliente") {
    defaultValue = "Cliente Genérico"
})"


 - É criado o parâmetro "cliente"
 - Define-se um valor padrão
 Resultado:
 - Se não passar nada → "Cliente Genérico"
 - Se passar → usa o valor enviado

 --------------------

3. Captura do parâmetro de navegação

"it.arguments?.getString("cliente")"

 - O valor da rota é capturado e enviado para a tela PedidosScreen

 --------------------

4. Alteração na função da tela (PedidosScreen)

"fun PedidosScreen(modifier: Modifier = Modifier, navController: NavController, cliente: String?)"

 - Adicionou o parâmetro cliente: String? -> o "?" sinifica que pode ser nulo (já que é opcional)

 --------------------

5. Uso do parâmetro na UI

"text = "PEDIDOS - $cliente""

 - Mostra o nome do cliente na tela


*********** Explicação do Commit "Inserindo valor ao parâmetro opcional na tela de Pedidos" ******************

Esse commit fecha o ciclo anterior, adicionando valor para o parâmetro opcional

1. Alteração na navegação

"onClick = { navController.navigate("pedidos?cliente=Cliente XPTO") },"

 - Acessa a rota "pedidos" -> Passa o parâmetro cliente -> Envia o valor "Cliente XPTO", substituindo o anteriormente "Cliente genérico"


*********** Explicação do Commit "Passagem de múltiplos parâmetros" ******************

Agora a navegação não irá passar apenas o nome, mas sim a idade também

1. Alteraão da rota

" route = "perfil/{nome}/{idade}","

 - Agora existem 2 parâmetros obrigatórios, já que a idade foi adicionada

 --------------------

2. Definição dos argumentos

"arguments = listOf(
    navArgument("nome") { type = NavType.StringType },
    navArgument("idade") { type = NavType.IntType }
)"

 - foi implementado o nome como String e a idade como Int
 - o Navigation valida o tipo automaticamente

 --------------------

3. Captura dos parâmetros

"val nome: String? = it.arguments?.getString("nome", "Usuário Genérico")
 val idade: Int? = it.arguments?.getInt("idade", 0)"

 - Pega os dois valores da rota
 - Define valores padrão caso algo dê errado, não quebrando o app

 --------------------

4. Perfil Screen

 - A PerfilScreen foi modificada para receber os dois parâmetros e exibi-los na interface.

