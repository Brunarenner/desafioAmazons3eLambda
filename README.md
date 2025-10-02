

📁 Projeto: Processamento de Arquivos Serverless (AWS)
Este projeto implementa uma arquitetura serverless na Amazon Web Services (AWS) para o upload, processamento e persistência de dados extraídos de arquivos.

🚀 Arquitetura
O sistema é construído sobre a arquitetura mostrada no diagrama e utiliza os seguintes serviços principais da AWS:

Ícone	Serviço AWS	Função no Projeto
Amazon S3	Atua como o datalake para armazenar arquivos brutos (raw) e, opcionalmente, os arquivos processados.
AWS Lambda	Responsável pela lógica de negócios. Executa o código para ler, validar e processar o arquivo.
Amazon RDS	Armazena os dados estruturados e processados extraídos dos arquivos.
Usuário/IAM	Representa o mecanismo que faz o upload do arquivo e as permissões de acesso ao sistema.

Exportar para as Planilhas
Fluxo de Processamento (Cenário Comum)
Upload: Um Usuário ou aplicação faz o upload de um novo Arquivo para um bucket específico no Amazon S3.

Trigger: O evento de criação do objeto no S3 aciona (faz um trigger) a função AWS Lambda.

Processamento: A função Lambda é executada:

Lê o arquivo do S3.

Executa a lógica de processamento, validação e transformação dos dados.

Persistência: Após o processamento, a função Lambda insere ou atualiza os dados extraídos no Amazon RDS.

💻 Pré-requisitos
Para desenvolver ou operar este projeto, você precisará de:

Conta AWS ativa.

AWS CLI configurada.

Node.js, Python ou outra runtime suportada pelo Lambda (dependendo da implementação).

Ferramenta de empacotamento (ex: npm, pip, terraform, serverless framework).

⚙️ Configuração e Implantação
1. Configurar S3
Crie um bucket S3 que servirá como a área de staging para os arquivos de entrada.

2. Desenvolver a Função Lambda
O código da função Lambda deve incluir a lógica para:

Receber o evento do S3 (que contém o nome do bucket e a chave do arquivo).

Baixar o arquivo.

Abrir uma conexão com o RDS.

Processar o conteúdo do arquivo e executar as queries de inserção/atualização.

3. Configurar Trigger e Permissões (IAM)
Defina uma política de permissão (Role) para o Lambda que permita ler do S3 e escrever no RDS.

Configure o trigger no bucket S3 para chamar a função Lambda quando um objeto for criado.

4. Configurar o RDS
Garanta que o RDS esteja acessível pela VPC onde a função Lambda está configurada.

Crie o schema e as tabelas necessárias para armazenar os dados processados.
