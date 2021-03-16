# qa-teste-pratico

Respostas do Teste Prático

**1) De acordo com sua experiência, escreva os possíveis cenários de
testes.**

RESPOSTA

#encoding UTF-8
#Author: Jedilson Silva

@produtosPromocao
Feature: Mensagem

            Eu, como Gerente de Marketing, gostaria que fosse enviada uma mensagem
            para o cliente, participante do clube de clientes, quando pelo menos um
            dos produtos comumente consumidos por ele entrar em promoção.

@formatoMensagem
Scenario: Validar o formato da mensagem

            Given que é enviada a mensagem de aviso de promoção ao cliente
            And O sistema apresenta a mensagem para o cliente
            Then o formato da mensagem é "Olá <nome do cliente>, os seguintes produtos que você costuma consumir estão em promoção! Vem conferir: - <Nome do produto>: <De> por <preço da promoção>"
            

@envioMensagem

Scenario: A mensagem só deve ser enviada para o cliente se o produto que entrar
          em promoção for de consumo do mesmo e o cliente não efetuou sua
          compra nos últimos 5 dias.
          
            Given que o produto em promoção é de consumo do cliente
            And o cliente não efetuou sua compra nos últimos 5 dias
            Then a mensagem é enviada para o cliente
            

@quantidadeProdutoMensagens

Scenario: A mensagem deve conter no máximo 3 produtos de consumo contínuo do
          cliente, sendo estes sempre os mais relevantes para o mesmo.
          
            Given que a mensagem é enviada para o cliente
            And deve ser enviada sempre promoção dos produtos mais relevantes para o cliente
            Then a mensagem contém no máximo 3 produtos
            

@salvaguardarMensagem

Scenario: O sistema deverá salvaguardar a informação de que a mensagem foi enviada para o cliente.

            Given que o cliente tem promoções disponíveis
            And a mensagem é enviada para o cliente
            Then o sistema salva a informação que a mensagem foi enviada
            

**2) Alex precisou ausentar-se do trabalho e a atividade de escrever os
testes unitários dessa User Story foi redirecionada para você.
Utilizando-se de uma linguagem de programação que você tenha
maior familiaridade e conhecimento em TDD, escreva os testes
unitários necessários.**

RESPOSTA

Prezados no momento estou sem skill para responder essa atividade. 

**3) Dada a estrutura de dados relacional abaixo, desenvolva a query que
será responsável por recuperar os 5 produtos de maior incidência
nas compras dos clientes (não levar em consideração a quantidade,
mas apenas se determinado produto apareceu ou não numa
compra) nos últimos 3 meses.**

RESPOSTA

Essa consulta faz o seguinte: conta quantas vezes o produto aparece na tabela produto_compra, orderna do maior para o menor, e esse top 5 pega os 5 primeiros e considera apenas se o produto aparece nos ultimos tres meses. 

SELECT TOP 5 P.NOME, COUNT(ID_PRODUTO) FROM PRODUTO_COMPRA AS PC,PRODUTO AS P
WHERE PC.ID_PRODUTO = P.ID AND (MONTH(DATA) >= MONTH(GETDATE()) - 3)
GROUP BY P.NOME ORDER BY 2 DESC;


**4) Na cerimônia de retrospectiva de uma dada sprint, o time pontuou
as seguintes problemáticas:**
**● Funcionalidades implementadas de forma incompleta**
**● Dificuldade em realizar correções de não conformidades (manutenção do código).**
**● Dificuldade em rastrear os erros apontados nas baterias de testes realizadas.**
**De posse deste feedback, o ScrumMaster do projeto solicitou uma reunião
entre o líder técnico e você para que a "Definição de Pronto" do projeto
fosse revisada. Segue abaixo a definição citada. De acordo com sua
experiência, o que você mudaria nela? Além disso, você acharia necessário
provocar algum outro tipo de ação em conjunto com o time de
desenvolvimento? Comente.**
**Definição de Pronto:**
**1. A funcionalidade/correção foi implementada**
**2. A funcionalidade/correção foi testada no ambiente de QA
3. A funcionalidade/correção está disponível em PROD****

RESPOSTA

● Funcionalidades implementadas de forma incompleta

--- Realizar a homologação da funcionalidade junto aos envolvidos, principalmente o PO do projeto;
--- Inserir a cultura de testes unitários na atividade de desenvolvimento.

● Dificuldade em realizar correções de não conformidades (manutenção do código).

--- realizar a desenvolvimento em Pares, acredito que uma revisão de outro desenvolvedor pode mitigar senão todo, mas parte do problema.

● Dificuldade em rastrear os erros apontados nas baterias de testes realizadas.

--- Creio que uma melhoria no processo de testes para que o erros apontados possam ser descritos ou explicados de forma mais clara, assim permitindo que o desenvolvedor entenda o que de fato deve ser corrigido.

Definição de pronto.

Definir critério de aceite que possam ser testáveis;
Tudo indica que não está havendo entendimento das estórias para que possam ser criados testes que realmente atendam a necessidade do cliente, o ideal é que essas estórias sejam refinadas de modo que se dividam em estórias menores, Esse refinamento pode colaborar para que o QA tenha um entendimento mais claro do que PO e/ou usuário necessita.

Definições de pronto que eu adicionaria às que já foram propostas:

- Os cenários de testes criados atendem os critérios de aceite da estória?
- Existem cenários de testes para os fluxos principal, alternativos e de exceção das estórias?
- Os casos de testes foram validados com o PO?

