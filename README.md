# SIMBIOSIS LITE

PWA offline-first para agricultura familiar (solo, pragas, consórcio e “Planta Falante”), com Diário, fotos salvas no celular e sincronização automática via API PHP + MySQL/MariaDB.

## O que o sistema faz

- Funciona mesmo sem internet (offline).
- Salva registros no **Diário** e guarda **fotos no celular** (IndexedDB).
- Quando a internet volta, sincroniza com o servidor e puxa alertas da comunidade (da mesma região).
- Módulos:
  - **Solo**: dica simples a partir de pH + informações básicas.
  - **Pragas**: contagem de pontinhos na armadilha e tendência.
  - **Consórcio**: apoio no planejamento do plantio consorciado.
  - **Planta Falante**: análise visual simples de folha + comparações quando online.

## Tecnologias usadas

- Front-end: HTML + CSS + JavaScript (módulos ES).
- PWA: `manifesto.webmanifest` + `trabalhador_servico.js`.
- Banco no celular: IndexedDB.
- Back-end: PHP (API).
- Banco do servidor: MySQL/MariaDB.

## Como rodar localmente (Windows)

### Opção A (recomendada): XAMPP

1. Copie a pasta do projeto para: `C:\xampp\htdocs\SIMBIOSIS\`
2. Abra o **XAMPP Control Panel** e inicie:
   - Apache
   - MySQL
3. Crie o banco no phpMyAdmin:
   - Abra: `http://localhost/phpmyadmin`
   - Crie um banco chamado: `simbiosis_lite`
   - Importe o arquivo: `db/banco.sql`
4. Abra no navegador:
   - `http://localhost/SIMBIOSIS/`

### Opção B (opcional): servidor embutido do PHP

1. Abra o PowerShell na pasta do projeto.
2. Rode:

```bash
php -S localhost:8000 -t C:\xampp\htdocs\SIMBIOSIS
```

3. Abra:
   - `http://localhost:8000/`

## Como instalar no smartphone (PWA)

- Android (Chrome): menu do navegador → **Instalar** / **Adicionar à tela inicial**
- iPhone (Safari): **Compartilhar** → **Adicionar à Tela de Início**

## Como é a arquitetura (resumo)

- O app abre por `inicio.php` e carrega `app/js/aplicativo.js` e `app/css/estilo.css`.
- O modo offline é feito pelo `trabalhador_servico.js` (cache dos arquivos principais).
- O app salva tudo no IndexedDB (`app/js/lib/banco_local.js`).
- A sincronização usa fila (outbox) em `app/js/sincronizacao.js`.
- A API principal fica em `api/inicio.php`.
- O banco do servidor é criado pelo `db/esquema.sql`.

## Privacidade (bem importante)

- As fotos tiradas pelo usuário ficam no celular (IndexedDB).
- Para o servidor vai:
  - registros em JSON (sem foto)
  - números (features) para comparação

## Configuração do banco (servidor)

Por padrão, a API tenta conectar com:

- host: `127.0.0.1`
- porta: `3306`
- banco: `simbiosis_lite`
- usuário: `root`
- senha: vazio

Se precisar mudar, use variáveis de ambiente:

- `RQ_DB_HOST`
- `RQ_DB_PORT`
- `RQ_DB_NAME`
- `RQ_DB_USER`
- `RQ_DB_PASS`
- `RQ_DB_CHARSET`

## Arquivos úteis para a banca (TXT)

- `PITCH_TECNICO_5_MINUTOS.txt`
- `APRESENTACAO_PROGRAMACAO.txt`
- `EXPLICACAO_DO_SISTEMA.txt`
- `TUTORIAL_INSTALACAO_LOCAL.txt`

## Versão do sistema

A versão fica definida em `inicio.php` na variável `$appVersion`.
