# 🏐 Caixa do Vôlei

Web app para celular que controla o caixa do grupo de vôlei: quem jogou em cada dia, categoria (mensalista, meio ou avulso), transferências sem identificação, despesas e o saldo de cada mês.

## Como colocar no ar (Vercel) — ~10 minutos

1. **Suba a pasta para o GitHub**
   Crie um repositório novo (pode ser privado) e envie todos os arquivos desta pasta.
   (Sem GitHub? Instale a CLI: `npm i -g vercel` e rode `vercel` dentro da pasta.)

2. **Importe na Vercel**
   vercel.com → *Add New → Project* → escolha o repositório → *Deploy*.
   O primeiro deploy vai abrir, mas ainda sem banco de dados (vai mostrar um aviso). É normal.

3. **Conecte o banco (grátis)**
   No projeto: aba *Storage* → *Create Database* / *Marketplace* → **Upstash Redis** → plano Free → conectar ao projeto.
   A Vercel cria as variáveis `KV_REST_API_URL` e `KV_REST_API_TOKEN` sozinha.

4. **Defina a senha de acesso**
   *Settings → Environment Variables* → nome `APP_PIN`, valor = a senha do grupo (use 6+ caracteres).

5. **Refaça o deploy**
   *Deployments* → os três pontinhos do último deploy → *Redeploy*.

6. **No celular**: abra o endereço do site, entre com a senha e use *Compartilhar → Adicionar à Tela de Início* (iPhone) ou *Instalar app* (Android). Fica com ícone, como um aplicativo.

## Como usar

- **Lançar**: escolha *Jogador*, *Transferência* ou *Despesa*, a data do jogo, a categoria e o valor.
  - Jogador: toque no nome (ou digite um novo — ele entra na lista sozinho). A categoria usada por último fica lembrada, mas dá para trocar a cada lançamento.
  - Transferência: Pix sem saber de quem é. Entra no caixa com o nome "Transferência" e na categoria que você escolher.
  - Despesa: o nome é sempre "Despesa", com a descrição (ex.: festinha de fim de mês). Sai do saldo do mês.
- **Caixa**: receitas por categoria, aluguel, sobra, despesas e saldo final do mês. Toque no ✏️ para corrigir ou no 🗑 para apagar um lançamento.
- **Temporada**: 12 meses lado a lado (por padrão março/2026 a fevereiro/2027). Toque num mês para abrir.
- **Valores**: aluguel do ginásio, mensalista, meio e avulso **de cada mês**. O valor novo vale para aquele mês e para os seguintes, até mudar de novo. Lançamentos antigos mantêm o valor em que foram feitos.

## Rodar no computador (opcional)

```
npm install
npm run dev
```
Sem Redis configurado, os dados ficam num arquivo local (`.data/db.json`). Isso só funciona no computador; na Vercel o Upstash é obrigatório.

## Observações

- Se o valor de uma pessoa for diferente do padrão (ex.: avulso que pagou 45 por 3 jogos), edite o campo *Valor* antes de lançar, ou lance um jogo por data.
- A senha é única para o grupo. Quem souber a senha consegue lançar e apagar.
