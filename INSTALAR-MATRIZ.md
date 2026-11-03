# Instalar a matriz do Painel geral

Esta matriz contém o painel atualizado e manuais para outra IA ou pessoa. Não é um serviço publicado. Não acompanha credenciais, bancos, vendas, autorizações Meta ou sessões Cloudflare.

## O que pedir ao proprietário

Antes de criar recursos, consultar os acessos já concedidos e pedir somente o que faltar:

1. Conta Cloudflare, domínio HTTPS, endereço do administrador e nome do novo projeto Pages.
2. Lojas a conectar: IDs internos, URLs, bancos e repositórios; produtos principais, adicionais e taxa de reentrega. O catálogo não conecta vendas sozinho.
3. App Meta e contas autorizadas. Consulta requer ads_read e business_management; edição de campanhas requer ads_management e autorização do proprietário. Não editar anúncios durante testes.
4. Login nas plataformas quando necessário. Solicitar segredos diretamente na Cloudflare, nunca pelo chat ou Git.
5. Confirmar regra financeira: a matriz preserva imposto Meta de 12,5%, fallback do gateway de 7,99% + R$1,99 e custos de produto/frete iguais a zero. Ajustar apenas se solicitado. Líquido real não sofre segundo desconto.

## Sequência de implementação

1. Ler AGENTS.md, docs/00-ROTEIRO-PARA-IA.md e todos os guias pertinentes. Criar repositório privado independente a partir desta matriz.
2. Usar Node 24. Executar npm ci, npm test, npm run test:integrations, npm run check e npm run preview. A prévia usa dados fictícios, não envia cobranças nem eventos reais. Encerrar com Ctrl+C.
3. Preencher wrangler.jsonc com Pages/D1/binding Meta próprios. Criar D1 central exclusivo, sem importar dados de outra operação. As tabelas centrais são inicializadas pelo Worker; migrações do conector Meta pertencem ao banco do conector.
4. Adaptar dist/modules/model.js: lista de lojas, bases, painel individual e rastreio. Os dois exemplos usam IDs 001/002. Adaptar também a validação das rotas de ação em dist/_worker.js caso os IDs mudem.
5. Adaptar dist/_worker.js: domínio canônico e redirecionamento do domínio antigo. Não publicar example.com. Substituir a identidade visual e o administrador visível em dist/index.html e dist/app.js. O administrador efetivo é validado pelo backend conforme ADMIN_EMAIL e Access.
6. Criar aplicação Cloudflare Access e política para o administrador; configurar domínio da equipe e AUD em todos os servidores participantes. Preservar validação criptográfica no backend. Domínio protegido sem backend validado não basta.
7. Preparar Worker Meta e service binding META_CONNECTOR. integrations/meta-reference é referência versionada: usar config/meta-worker.example.jsonc como ponto de partida, adaptar URLs/permissões e aplicar migrações próprias. Há funcionalidades legadas Cakto nesse snapshot, que não substituem as pontes das lojas.
8. Configurar app/callback exato do domínio novo, segredos e criptografia somente na Cloudflare. Autorizar as contas do proprietário. Não copiar conexão/token da instalação de origem.
9. Adaptar a ponte JWT em cada loja a partir do contrato de docs/05. integrations/store-reference contém código de exemplo das lojas originais, não uma matriz de checkout. Não publicar esse código como nova loja sem adaptar produtos, gateway, Pixel, e-mails, D1 e webhook exclusivos.
10. Configurar catálogo, vínculos de campanha e UTMs exatas. Testar seleção de nenhuma, todas e várias campanhas/produtos. As vendas precisam estar nos bancos conectados e ter atribuição; o webhook sozinho não identifica a campanha.
11. Apresentar prévia desktop/mobile antes de deploy. Testar sem cobranças, e-mails, Purchase fictício ou alterações de gastos reais. Atualizar ESTADO.md e PROJETO-PAINEL.json com os recursos não secretos da nova instalação.
12. Publicar somente no novo Pages autorizado. Conferir TLS, Access, APIs sem sessão bloqueadas e consultas autenticadas reais. Registrar commit/deployment. Push no GitHub não equivale a deploy.

## Atualizar esta matriz no futuro

A operação atual está em gestao-lojas-central; a matriz está em gestao-lojas-central-matriz. São repositórios separados. Para sincronizar, escolher o commit validado da operação, revisar diferenças e copiar somente código/documentação necessários. Preservar placeholders e não importar wrangler de produção, bancos, sessões, segredos ou screenshots de dados reais. Atualizar hashes das referências se algum snapshot for adaptado. Executar testes e CI antes de publicar no GitHub. Não há deploy Cloudflare da matriz por padrão.

Os guias herdados registram detalhes de arquitetura e exemplos da origem. ESTADO.md, PROJETO-PAINEL.json e este arquivo definem o estado desta matriz; qualquer ID histórico não é um recurso pronto para reutilização.
