# Publicar o DigiTorial no Portal Digit

O DigiTorial usa **as mesmas contas do Portal Digit / DigiNote** (o mesmo projeto Supabase). O administrador é `id@digit.com.pt`. A lista de colaboradores vem da tabela `profiles` do Supabase, ou seja, das contas que já existem.

## 1. GitHub (alojamento)
1. Abre o repositório **Digit-ID/DigiTorial** no GitHub.
2. Apaga o conteúdo antigo e carrega **todos os ficheiros desta pasta** (incluindo a pasta `assets/`):
   - `index.html` (a aplicação, autossuficiente)
   - `organizacao.json` (equipas e hierarquia)
   - `manifest.webmanifest`, `apple-touch-icon.png`
   - `recibo-teste.pdf`
   - `assets/digit-logo-light.png`, `assets/digit-logo-dark.png`
3. Vai a **Settings → Pages**, escolhe "Deploy from a branch", depois `main` e `/ (root)`. Grava.
4. Fica disponível em **https://digit-id.github.io/DigiTorial/**.
5. Faz `Ctrl+Shift+R` na primeira abertura, porque a cache do GitHub Pages é persistente.

> Tem de ficar em `digit-id.github.io` (e não no Netlify) para partilhar a sessão com o Portal, o DigiNote, o DigiSpot e o DigiEduca. Assim, quem já entrou no Portal entra diretamente no DigiTorial.

## 2. Supabase
1. Abre **SQL Editor → New query**, cola todo o conteúdo de `supabase-digitorial.sql` e carrega em **Run**. Cria as tabelas do DigiTorial (estrutura da empresa e pedidos de ausência) com as regras de acesso, incluindo a proibição de auto-aprovação (exceto Admin). No fim mostra a lista de contas do Portal.
2. As contas, os nomes e os administradores vêm da tabela `perfis` do Portal, por isso não é preciso criar contas. Uma conta desativada, ou sem acesso "T" no Portal, não consegue entrar no DigiTorial.
3. Em **Authentication → URL Configuration → Redirect URLs**, adiciona `https://digit-id.github.io/DigiTorial/`.

## 3. Portal Digit (atalho)
Na pasta `portal-digit` estão o `index.html` e o `manifest.webmanifest` do Portal já com o DigiTorial (letra **T**). Carrega-os no repositório **Digit-ID/Digit** (substituindo os atuais). O administrador passa a poder dar/retirar acesso ao DigiTorial na gestão de contas do Portal, como nas outras apps.

## O que fica guardado onde
- **Na nuvem (Supabase):** login, nomes e emails dos colaboradores, e quem é administrador.
- **Neste dispositivo (navegador):** pedidos de férias, aprovações, assinaturas, documentos e definições. Ainda **não** são partilhados entre utilizadores. Para isso é preciso criar tabelas no Supabase, que é o próximo passo de desenvolvimento.
- **Colaboradores novos** (contas no Portal que não estão no `organizacao.json`) aparecem como "Funcionário", sem equipa nem chefia. O RH ou o Admin atribuem-nas em Contas.
