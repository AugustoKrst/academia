# Sport Center — Sistema de gestão de academia

## Apresentação do projeto

Neste projeto, eu desenvolvi o **Sport Center**, um sistema para ajudar na organização de uma academia. O aplicativo reúne em um só lugar o cadastro de alunos, planos e modalidades. Criei uma interface com tons de laranja para transmitir energia e fazer referência ao universo esportivo.

O sistema funciona como site no navegador e também pode ser executado como aplicativo Android ou iOS usando Expo e React Native.

## O que eu implementei

Organizei o sistema em três áreas principais:

- **Alunos:** cadastro de nome, e-mail, telefone, plano, modalidade e situação do aluno.
- **Planos:** cadastro do nome, descrição, duração em dias, preço e situação do plano.
- **Modalidades:** cadastro do nome, descrição, instrutor, horários e situação da modalidade.

Em cada área, implementei as operações CRUD:

- **Create:** cadastrar um novo registro.
- **Read:** visualizar e buscar registros cadastrados.
- **Update:** editar as informações de um registro.
- **Delete:** excluir um registro, com confirmação antes de concluir.

Também incluí busca por texto, filtro por situação, validação dos formulários e indicadores para acompanhar alunos, planos e modalidades ativos.

## Como os dados são organizados

Usei o MySQL para persistir os cadastros. O banco contém três tabelas: `alunos`, `planos` e `modalidades`. Cada aluno fica associado a um plano e a uma modalidade, e o banco impede a exclusão de um plano ou modalidade que ainda esteja vinculado a alunos.

O aplicativo não acessa o banco diretamente. Ele envia solicitações HTTP para uma API em Node.js e Express, que valida os dados e executa as consultas no MySQL. Usei consultas parametrizadas para enviar os valores com segurança, e as credenciais do banco ficam no servidor, fora do aplicativo.

## Tecnologias e organização

- **Expo e React Native:** interface adaptável para navegador e dispositivos móveis.
- **Expo Router:** navegação entre as telas e áreas do aplicativo.
- **Node.js e Express:** API que recebe as solicitações do aplicativo.
- **MySQL:** armazenamento dos alunos, planos e modalidades.
- **mysql2:** conexão da API com o banco de dados.

Arquivos principais:

- `src/app/index.tsx` — tela principal e interface de gerenciamento.
- `src/lib/api.ts` — chamadas do aplicativo para a API.
- `server/src/index.js` — rotas e operações CRUD da API.
- `server/database/schema.sql` — criação do banco e das tabelas.

## Como executar o projeto

### 1. Preparar o banco de dados

No MySQL Workbench ou em outro cliente MySQL, execute o conteúdo de `server/database/schema.sql`. Isso cria o banco `sport_center` e as tabelas necessárias.

### 2. Configurar e iniciar a API

No PowerShell, a partir da pasta principal do projeto, copie o exemplo de configuração:

```powershell
Copy-Item server/.env.example server/.env
```

Edite `server/.env` e informe as credenciais corretas do MySQL. Depois, inicie a API:

```powershell
cd server
npm install
npm run dev
```

A API fica disponível em `http://localhost:3001/api`. Para conferir a conexão com o banco, acesse `http://localhost:3001/api/health`; a resposta esperada é `{"status":"ok"}`.

### 3. Iniciar o site

Em outro terminal, volte à pasta principal e execute:

```powershell
npm install
npx expo start --web
```

O Expo exibirá o endereço local do site. Para abrir o aplicativo no Expo Go, use `npx expo start`.

Se o aplicativo for aberto em um celular físico, configure `EXPO_PUBLIC_API_URL` no arquivo `.env.local` com o IP da máquina que está executando a API, por exemplo `http://192.168.0.20:3001/api`. Nesse caso, `localhost` apontaria para o próprio celular.

## Rotas da API

As três coleções oferecem rotas para listar, consultar, criar, editar e excluir registros:

- `/api/alunos`
- `/api/planos`
- `/api/modalidades`

Cada coleção aceita `GET` para listar, `GET /:id` para consultar um registro, `POST` para cadastrar, `PUT /:id` para editar e `DELETE /:id` para excluir.

## Resumo para apresentação oral

> Eu desenvolvi o Sport Center para organizar os principais cadastros de uma academia. O sistema permite gerenciar alunos, planos e modalidades usando as quatro operações CRUD. Fiz a interface com Expo e React Native para funcionar no navegador e em dispositivos móveis. Para salvar os dados, conectei o aplicativo a uma API em Node.js e Express, que se comunica com o MySQL. Também implementei validação dos formulários, busca, filtros e relacionamentos entre alunos, planos e modalidades.
