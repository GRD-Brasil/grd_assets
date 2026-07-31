# GRD Brasil Assets CDN

Repositório oficial de imagens, vídeos e recursos visuais estáticos para o ecossistema do **GRD Brasil Hub**.

## 🌐 Endereço
As imagens são servidas via CDN, e o catálogo visual interativo de todos os assets pode ser acessado publicamente através da nossa página na Vercel.

## 🚀 Estrutura e Operação

O repositório está organizado de forma dinâmica e escalável. Todos os assets devem ser colocados dentro da pasta principal:
- `hub_images/`: Pasta raiz de todos os assets.
  - `images/`: Imagens gerais (fundos de tela, texturas, logotipos, etc).
  - `wiki_assets/`: Imagens e arquivos utilizados na documentação e wiki do projeto.
  - *(Novas pastas criadas aqui serão automaticamente detectadas e ganharão uma aba própria na Galeria web)*

### 🖼️ Estratégia WebP (Alta Performance)

Para otimizar o tempo de carregamento no aplicativo e reduzir o tamanho geral do projeto, as imagens pesadas são automaticamente convertidas para **WebP**.
- **Limpeza Automática**: Quando um arquivo PNG ou JPG é enviado, o nosso script de compressão o converte para WebP e **deleta o arquivo original** em seguida, garantindo que o repositório fique sempre o mais leve possível.
- **Arquivos Preservados**: Formatos vetoriais (`.svg`), animações puras (`.gif`) e arquivos de vídeo (`.mp4`, `.webm`) são mantidos em seus formatos originais, preservando 100% de sua integridade.

## 🛠️ Automação (CI/CD)

O repositório utiliza **GitHub Actions** para manter tudo funcionando de forma 100% autônoma. 
Sempre que uma nova alteração é enviada (`Push`) para a branch `main`:
1. **Processamento de Imagens**: O robô instala o Python, varre a pasta `hub_images/` e converte todas as imagens padrão para `.webp`.
2. **Atualização do Manifesto**: O robô aciona o mapeamento e reconstrói o `manifest.json`, registrando todas as novas pastas e arquivos.
3. **Commit Automático**: O GitHub Actions salva as imagens recém-otimizadas e o novo JSON de volta no repositório.
4. **Deploy Automático**: A Vercel detecta a atualização do repositório e lança a versão atualizada da Galeria Web instantaneamente.

## 📊 Galeria e Manifesto

O arquivo `manifest.json` na raiz contém a lista estruturada de todos os assets. O aplicativo FiveM Hub lê este arquivo via requisição HTTP para saber quais imagens carregar remotamente.

O **Catálogo Visual (Galeria)** é um sistema ultra-leve construído puramente em **Vanilla JS** dentro do arquivo `index.html`. Ele dispensa dependências como Node.js ou React, sendo capaz de ler o arquivo de manifesto e renderizar a interface de forma totalmente autônoma.

## ⚙️ Scripts Nativos

- `convert_to_webp.py`: Script Python responsável pela conversão em massa para WebP e deleção inteligente dos originais.
- `generate_manifest.py`: Rastreia a árvore de diretórios e gera a estrutura JSON utilizada pelos sistemas.
