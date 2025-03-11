# 🌊 Documentação de obtenção dos dados para o Onalize

**Bem-vindo a documentação principal de extração, transformação e carregamento dos dados para o Onalize**
Nesta documentação, você irá aprender:

✔️Explicação breve sobre quais informações o Onalize utiliza e como utiliza.
✔️Explicação breve sobre a origem dos dados que utilizamos e policies
✔️Como obter os dados para o tipo de workspace que sua empresa possui
✔️Regras de negócio com código exemplificados para implementação
✔️Códigos de exemplo de extração dos dados do workspace que sua empresa possui
❌Códigos reais com extração dos dados via API
❌ Exemplos reais de retornos da API do workspace que sua empresa possui

⚠️ *Infelizmente a Onalize não disponibiliza hoje códigos de exemplos reais devido a confidencialidade dos dados*

## O que é o Onalize

Onalize é uma serviço de análise de dados organizacionais acompanhadas do dashboard ONA, que é uma sigla para *"Organizational Network Analysis".

📌 **O que a Onalize entrega de valor?**

✔️Analisamos como funciona a relação entre os colaboradores da sua empresa, buscando por dores entre os mesmos e sugerindo melhorias e um plano de ação robusto para organização.  

✔️Através do dashboard ONA, é possível acompanhar se as sugestões que levantamos surtiram efeito para corrigir os problemas identificados.

📌 **Qual o propósito do Onalize?**

Nosso objetivo é sempre melhorar a vida do colaborador, tornar o trabalho deles fácil de ser reconhecidos pelo RH e identificar dores na organização que podem ser solucionadas com iniciativas específicas e que gerem resultados impactantes.

📌 **Como é faseado a utilização do Onalize?**

 1. ⚙️ ETL dos dados de Gmail e Calendário dos colaboradores da empresa.
 2. 📊 Análise Descritiva e Exploratória dos dados extraídos, identificando dores e gerando planos de ação.
 3. 🌐 Acompanhamento do plano de ação através do ONA.

##  Utilização dos dados do Onalize

📌 **Quais as fontes de dados que o Onalize utiliza?**

O Onalize utiliza de dados de comunicação entre os colaboradores, principalmente de duas formas:
 - ✉️ E-mail 
 - 📆 Calendário

O Onalize cria relação dos participantes entre cada e-mail e reunião na agenda de cada colaborador, que posteriormente é utilizada no software.

⚠️ *Atenção: O Onalize NÃO utiliza do conteúdo das menasgens ou qualquer informação confidencial.*

📌 **Quais informações que o Onalize utiliza?**

    O Onalize depende de 5 importantes informações para gerarmos a visualização corretamente:

* 📌 sender: quem enviou o contato
* 📌 receiver: quem recebeu o contato
* 📅 data: data de quando aconteceu
* 🔹 hash_id: hash256 da relação entre sender e receiver
* 🔹 id_comunicacao: id que identifica unicamente cada comunicação

🗂️ *Posteriormente adicionamos atributos como: Salário, Time, Idade, Gênero, Cargo, Nível de cargo.*

📌 **Como obtemos as informações que o Onalize utiliza?**

⚠️ Obtemos essas informações, utilizando a API do Gsuite ou Outlook365.

Cada um desses sistemas, possuem endpoint's específicas que podemos:
 - Extrair os dados de calendário de cada colaborador (Quais agendas ele tem na semana)
 - Extrair os dados de e-mails de cada colaborador

🔥 Com as scopes/pemissions corretas, nós conseguimos obter os dados que precisamos.

    📌 Exemplo:
    Com a scope de Mail.Read.All no Gmail API do Gsuite, nós podemos:
    
     1. Listar todos os users da corporação [Todos os e-mails que queremos retirar os dados]
     2. Extrair desses users que listamos, os dados de agenda e e-mails
     3. Realizamos as transformações necessárias
     4. Carregamos os dados

⚠️ *Dependendo do sistema que sua empresa utiliza, temos um documento no passo a passo de como obter o token da API para requisição e obtenção dos dados.*

📌 **Como deve ser consumido esses dados que o Onalize utiliza?**

Os dados serão enviados para um Postgre SQL em uma conta Oracle que será compartilhada entre a empresa e o Onalize.

📌 **Quem fará a extração dos dados para o Onalize?**

O time de dados da empresa ficará responsável por realizar o processo de extração.

    📌 Porque a contratante deve realizar a extração?
	
	Os dados que vamos obter dependem de:
	
	> Acesso a scopes e permissions específicas nas API's
	Apenas o admin do workspace que pode realizar essa liberação a um token.
	
	> Token disponibilizado tem acessos a dados muito sensíveis
	Devido ao Token ter acesso a esses dados, a empresa fica responsável pelo ETL.
	
⚠️ Mas não se preocupe! Disponibilizamos todo tipo de apoio e documentos que auxiliam o seu time a extrair os dados.

📌 **Como garantimos que os dados não serão vazados?**

📌 **Atuação resumida entre Onalize x Contratante**

![atuacao_resumida](atuacao_resumida.PNG)

##  Regras de negócio dos dados do Onalize

📌 **Regra 1: Garantindo interação entre todos os colaboradores em uma reunião síncrona**


📌 **Regra 2: Garantindo interação entre todos os colaboradores que mandaram o email e quem apenas recebeu**


📌 **Regra 3: Garantindo que cada evento de comunicação não está duplicado**



