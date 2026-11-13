# Gestão Inteligente — Dicionário de Dados | Holanda Seguros

Documentação interativa do projeto **Gestão Inteligente**, desenvolvido pelo Grupo 2 da UNICID para a Holanda Seguros. O site apresenta o dicionário de dados do banco, reunindo definições de negócio, tipos físicos, restrições, classificação de privacidade, linhagem dos dados e controle de acesso por perfil (RBAC).

> **Versão da documentação:** 3.0 — 12/11/2026  
> **Banco de dados documentado:** MySQL 8.0 (InnoDB, `utf8mb4`)  
> **Cobertura informada no projeto:** 15 tabelas e 111 colunas.

## Objetivo do projeto

O projeto propõe uma base de dados para apoiar a gestão do relacionamento com clientes de seguro saúde da Holanda Seguros. A modelagem documentada contempla:

- Cadastro de clientes pessoa física e registro de consentimento LGPD;
- Endereços dos clientes;
- Registro e acompanhamento de atendimentos, incluindo plano de preferência e origem do contato;
- Situações de atendimento: **EM_DUVIDA**, **FECHADO** e **NAO_FECHADO**, com histórico;
- Catálogo de planos individuais e suas dez faixas etárias da ANS;
- Contratações, mensalidade registrada no contrato e cancelamento por arrependimento;
- Indicadores, como taxa de conversão e motivos de não fechamento;
- Usuários, perfis de acesso e trilha de auditoria;
- Solicitações relacionadas aos direitos dos titulares de dados.

**Fora do escopo declarado:** cobrança, emissão de boletos, sinistros e planos familiares ou empresariais.

## Funcionalidades do site

- **Dicionário de dados:** consulta às tabelas e aos atributos documentados.
- **Navegação lateral dinâmica:** menu organizado por grupos, criado a partir das seções existentes na página.
- **Busca em tempo real:** pesquisa por nome de tabela ou coluna, com destaque dos termos encontrados.
- **Tema claro e escuro:** alternância de aparência com preferência salva no navegador.
- **Visualizador do DER:** abertura do diagrama em modal, com zoom e movimentação (pan).
- **Controles de zoom:** aumentar, diminuir e restaurar a visualização; também há suporte a atalhos de teclado.
- **Layout responsivo:** adaptação para telas menores, incluindo menu lateral recolhível.
- **Legenda de metadados:** identificação de dados pessoais, dados pessoais sensíveis e restrições de chave.

## Tecnologias e recursos

| Tecnologia / recurso | Utilização |
|---|---|
| HTML5 | Estrutura e conteúdo da documentação |
| CSS3 | Identidade visual, temas, tabelas e responsividade |
| JavaScript | Busca, navegação dinâmica, tema e visualizador do DER |
| MySQL 8.0 | SGBD documentado na modelagem |
| Panzoom.js 4.6.2 | Zoom e movimentação do diagrama, carregado por CDN |
| LocalStorage | Persistência da preferência de tema no navegador |

O projeto apresentado neste repositório é uma **documentação web estática**. Os arquivos fornecidos não incluem um servidor ou uma conexão ativa com um banco MySQL.

## Estrutura de arquivos

Organize o repositório mantendo os caminhos relativos utilizados pelo HTML:

```text
gestao-inteligente/
├── index.html
├── style.css
├── script.js
├── assets/
│   └── der.png
└── docs/
    └── Especificacao_Requisitos_Regras_Negocio_BD.pdf
```

- `index.html`: página principal, identificação do projeto, escopo, análise de coerência e conteúdo do dicionário.
- `style.css`: estilos, variáveis de cores, temas, tabelas, componentes e regras responsivas.
- `script.js`: interações da página, busca, menu, tema e visualizador do DER.
- `assets/der.png`: imagem do Diagrama Entidade-Relacionamento exibida no modal.
- `docs/Especificacao_Requisitos_Regras_Negocio_BD.pdf`: especificação disponibilizada pelo botão de download na página.

**Importante:** os três arquivos principais foram disponibilizados para esta documentação. Para que todos os recursos e links funcionem depois do envio ao GitHub, inclua também o arquivo `assets/der.png` e o PDF no caminho indicado. Os nomes e a estrutura das pastas devem corresponder exatamente aos caminhos referenciados no HTML.

## Como executar localmente

Não é necessário instalar dependências de Node.js ou executar um processo de build.

1. Baixe ou clone este repositório.
2. Confira se as pastas `assets/` e `docs/` contêm os arquivos indicados acima.
3. Abra a pasta do projeto no Visual Studio Code.
4. Abra o arquivo `index.html` no navegador. Se preferir, utilize a extensão **Live Server** do VS Code e clique em **Go Live**.
5. Utilize o menu lateral e a busca para navegar pelo dicionário.

A biblioteca Panzoom.js é carregada por CDN; portanto, a funcionalidade utiliza essa biblioteca quando ela está disponível. O JavaScript também possui um controlador próprio como alternativa caso a biblioteca não carregue. A conexão com a internet é necessária para carregar a versão hospedada no CDN.

## Como publicar no GitHub Pages

1. Crie um repositório no GitHub.
2. Envie `index.html`, `style.css`, `script.js` e as pastas `assets/` e `docs/` com seus respectivos arquivos.
3. No repositório, acesse **Settings → Pages**.
4. Em **Build and deployment**, escolha **Deploy from a branch**.
5. Selecione a branch principal (normalmente `main`) e a pasta `/ (root)`.
6. Salve e aguarde a publicação. O GitHub exibirá o endereço do site na própria seção Pages.

Como o projeto é estático, o GitHub Pages pode hospedar a página sem backend. Verifique após a publicação se o DER e o PDF estão abrindo corretamente.

## Organização do dicionário

O HTML agrupa as tabelas nas seguintes áreas:

- **Cadastros e Acessos**
- **Clientes e Dados Pessoais**
- **Planos e Catálogo**
- **Atendimentos e Conversão**
- **Contratos e Pagamentos**
- **Parâmetros e Auditoria**

As 15 tabelas documentadas são:

`usuario`, `cliente`, `endereco`, `solicitacao_titular`, `tipo_plano`, `plano`, `plano_faixa_preco`, `origem_contato`, `motivo_nao_fechamento`, `forma_pagamento`, `parametro_sistema`, `atendimento`, `historico_situacao`, `contrato` e `log_auditoria`.

## Governança, privacidade e acesso

O dicionário registra metadados para apoiar a compreensão e a governança dos dados:

- **DP:** dado pessoal.
- **DPS:** dado pessoal sensível, conforme classificação adotada no documento.
- **N/A:** classificação não aplicável.
- **PK:** chave primária.
- **FK:** chave estrangeira.
- **UK:** restrição de unicidade.

O controle de acesso é descrito por RBAC (*Role-Based Access Control*), com os perfis **Atendente**, **Gerente** e **Administrador**. A documentação também identifica responsáveis pelos domínios de dados nos papéis de **Data Owner** e **Data Steward**, além de apresentar informações de linhagem e rastreabilidade.

O conteúdo aborda referências de governança como DAMA-DMBOK e COBIT 2019, além de regras relacionadas à LGPD. Consulte a especificação do projeto para detalhes das regras de negócio e dos requisitos.

## Créditos

**Projeto:** Gestão Inteligente — Holanda Seguros  
**Instituição:** Universidade Cidade de São Paulo (UNICID)  
**Grupo:** 2  
**Professor orientador:** Prof. Diego Marques

Desenvolvido como projeto acadêmico de modelagem e documentação de banco de dados.
