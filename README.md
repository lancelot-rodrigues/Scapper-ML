# Classificador de Vendedores do Mercado Livre

Este projeto consiste em uma solução de ponta a ponta que utiliza **Web Scraping** para coletar dados de produtos e vendedores do Mercado Livre Brasil e, em seguida, usa técnicas de **Machine Learning** para treinar um modelo capaz de prever a confiabilidade de um vendedor.

---

## Ferramentas e Tecnologias

- **Python 3.12**: A linguagem de programação base para todo o projeto.  
- **Playwright (com playwright-stealth)**: Para automação de navegador. Essencial para renderizar páginas dinâmicas (JavaScript) e se camuflar, evitando bloqueios anti-bot.  
- **BeautifulSoup4**: Para parsing do HTML e extração estruturada dos dados.  
- **Pandas**: Para carregar, limpar e manipular o dataset.  
- **Scikit-learn**: Biblioteca de Machine Learning usada para treinar e avaliar o modelo classificador.  

---

## O Processo do Código

O script `scraping.py` segue um fluxo lógico e robusto para realizar a coleta de dados de forma segura e eficiente:

1. **Inicialização**  
   - O script verifica se existe um arquivo de sessão (`auth.json`).

2. **Autenticação**  
   - Se `auth.json` existe, ele carrega a sessão e o scraper já inicia "logado".  
   - Se não existe, o usuário deve fazer o login manual na primeira execução para criar o arquivo de sessão.

3. **Loop de Busca**  
   - Itera sobre a `LISTA_DE_BUSCAS`, realizando pesquisas para cada termo.

4. **Loop de Paginação**  
   - Para cada busca, percorre o número de páginas definido em `NUMERO_PAGINAS_SCRAPE`.

5. **Extração de Links**  
   - Em cada página de resultados, coleta as URLs dos produtos, filtrando anúncios e links irrelevantes.

6. **Extração de Dados do Produto**  
   - Para cada link de produto, a função `extrair_dados_produto` coleta as 13 *features* definidas (nome, preço, vendedor, reviews, etc.).

7. **Salvamento**  
   - Os dados são salvos linha por linha em um arquivo CSV, garantindo persistência mesmo em caso de interrupções.

---

## Como Usar o Código

### 1. Pré-requisitos
Certifique-se de ter o Python instalado e execute:

<img width="481" height="31" alt="image" src="https://github.com/user-attachments/assets/86b6e715-dbcf-45fb-a643-86f97bf9cfb9" />
<img width="436" height="28" alt="image" src="https://github.com/user-attachments/assets/0044ea7c-27c1-4371-b112-3b5cc05c923a" />



Depois, instale os navegadores do Playwright:

<img width="164" height="26" alt="image" src="https://github.com/user-attachments/assets/e4bc5605-40be-47af-b5c3-b2099b58e08a" />


---

### 2. Primeira Execução (Login Manual)

- Garanta que o arquivo `auth.json` **NÃO** exista no diretório.  
- No script `scraping.py`, configure a variável `headless` para `False`:  

<img width="602" height="26" alt="image" src="https://github.com/user-attachments/assets/f9bc3701-0b76-41cf-ac90-7f33cf92475a" />


- Execute o script.  
- Faça login no navegador aberto.  
- Volte ao terminal e pressione **Enter** → o arquivo `auth.json` será criado.  

---

### 3. Coleta de Dados em Larga Escala

Com o `auth.json` já criado:

- Configure `headless=True` em `scraping.py`:  

<img width="594" height="28" alt="image" src="https://github.com/user-attachments/assets/ba64001f-e676-448f-9e46-a3cfd55ac630" />



- Ajuste as variáveis de configuração (veja abaixo).  
- Execute o script.  
- A coleta ocorrerá em segundo plano.  

---

### 4. Variáveis de Configuração

No início de `scraping.py`, personalize:

<img width="462" height="20" alt="image" src="https://github.com/user-attachments/assets/39826a96-e804-4474-b535-bdf8f9893f1c" />
<img width="483" height="24" alt="image" src="https://github.com/user-attachments/assets/ad48582b-c08c-4f03-8d93-29285a8f9df0" />
<img width="413" height="25" alt="image" src="https://github.com/user-attachments/assets/01810331-c7cc-4faa-ae17-306f0a791444" />




---

## ⚠️ Aviso Importante: A Fragilidade do Web Scraping

Um scraper depende da estrutura HTML/CSS do site. O **Mercado Livre** pode alterar o layout sem aviso, fazendo o scraper "quebrar".

- **Como quebra?**  
  Mudanças em classes CSS ou estrutura da página podem resultar em colunas vazias ou erros no script.  

- **Solução:**  
  Manutenção. Use `page.pause()`, inspecione novamente a página (F12) e ajuste os seletores CSS dentro da função `extrair_dados_produto`.  

---
