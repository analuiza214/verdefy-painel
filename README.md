# Matriz do Painel geral

Modelo reutilizável, sem site publicado. Comece por [INSTALAR-MATRIZ.md](INSTALAR-MATRIZ.md).

Matriz privada: https://github.com/organizacao-exemplo/gestao-lojas-central-matriz. Origem do código: https://github.com/organizacao-exemplo/gestao-lojas-central. O deploy publica somente `dist/`; documentação e referências ficam fora do site.

## Comece aqui

Leia [Assistente de configuração e usuários](ASSISTENTE-CONFIGURACAO-E-USUARIOS.md). Cada usuário terá uma instalação independente, com seu próprio painel, conexões e recursos.

Para entregar o trabalho a outra IA, use [CONTINUAR-COM-OUTRA-IA.md](CONTINUAR-COM-OUTRA-IA.md). O inventário estruturado está em [PROJETO-PAINEL.json](PROJETO-PAINEL.json).

| Quem vai trabalhar | Leitura |
| --- | --- |
| Outra IA | [AGENTS.md](AGENTS.md), [roteiro de execução](docs/00-ROTEIRO-PARA-IA.md), [estado](ESTADO.md) |
| Operador | [manual](docs/04-OPERACAO.md), [regras dos números](docs/03-REGRAS-E-FILTROS.md) |
| Desenvolvedor | [arquitetura](docs/01-ARQUITETURA.md), [instalação](docs/02-INSTALACAO-E-ACESSOS.md), [API](docs/05-INTEGRACOES-E-API.md) |
| Publicação | [testes e deploy](docs/06-TESTES-DEPLOY-E-RECUPERACAO.md) |
| Nova loja | [automação e integração](docs/07-NOVAS-LOJAS-E-AUTOMACAO.md) |
| Problemas | [diagnóstico](docs/08-DIAGNOSTICO.md) |

## Funcionalidades

- BM/conta Meta; múltiplas campanhas e produtos reais Umbrella; datas rápidas/personalizadas.
- Filtros compartilhados entre cards, funil, campanhas, vendas, rastreio e exportação de vendas.
- Funil: cliques → visitas → checkout iniciado → Pix gerado → pago.
- Lucro, ROI, taxas, adicionais e reentregas separados; líquido real sem desconto duplicado.
- Campanhas reais: ACTIVE verde, PAUSED vermelho; revisão antes de alterar status/orçamento.
- Pedido pago: popup de entrega, histórico, etapas e e-mail pelo fluxo canônico da loja.
- Olhos por campo/coluna. Privacidade visual, não substitui controle de acesso.
- Cloudflare Access exclusivo ao administrador e validação criptográfica em cada servidor.

**Não existe recuperação WhatsApp nem confirmação manual de pagamento.** Foram canceladas pelo usuário. Não restaurar código histórico sem novo pedido explícito.

## Dependências

Este é um repositório independente, mas a operação usa Pages/D1 central, Worker Meta `painel-conversoes` e conectores das lojas Loja B/Loja A. Cada loja mantém banco, webhook, produtos, segredos e outbox próprios. O painel não recebe tokens dos provedores.

As [referências versionadas](integrations/README.md) incluem código dos conectores para outra IA estudar sem depender do histórico do chat. Não publicar essas cópias em outra conta sem adaptar configuração e obter os acessos necessários.

## Desenvolvimento

Requer Node.js 24, npm e Git.

```powershell
npm ci
npm test
npm run test:integrations
npm run check
npm run preview
```

Prévia em `http://127.0.0.1:4180/`, dados fictícios e sem chamadas a provedores reais. Ctrl+C encerra. `preview.js` nunca é publicado.

Para outra operação, consulte [wrangler.example.jsonc](config/wrangler.example.jsonc). O arquivo da raiz já contém placeholders para uma nova instalação. Segredos somente na Cloudflare, nunca no Git, logs, screenshots ou chat.

## Limites essenciais

Catálogo lista produtos da conta Umbrella; vendas e rastreio só estão disponíveis para lojas conectadas. Webhook identifica loja/produto, não campanha Meta. Atribuição exige UTM no pedido. Gasto de campanha é integral, sem rateio por item. Filtro de adicional seleciona pedidos que contêm o item: não transforma o total do pedido em receita exclusiva daquele adicional.

Testes não criam cobranças, compras falsas, e-mails reais ou alterações arbitrárias em campanhas. Estado, versões e limitações operacionais estão em `ESTADO.md`.
