# Assistente de configuração e painel individual por usuário

## Estado e objetivo

Cada usuário deve ter seu painel individual. Seu Facebook, BMs, contas de anúncios, lojas, vendas, credenciais e permissões não podem ser compartilhados por padrão com outro usuário.

Cada usuário recebe uma instalação independente, com Pages, D1 central, conector Meta, Access, segredos e lojas autorizadas próprios. O código valida um administrador e usa uma conexão Meta por instalação. Não reutilizar conexões de outra instalação.

Este documento orienta a configuração; não é um assistente automático implementado na interface.

## Perguntas do assistente

Consultar primeiro os dados e acessos já fornecidos. Perguntar somente o que faltar:

1. “Qual nome do seu painel, domínio e e-mail autorizado para entrar?”
2. “Qual nome usaremos para identificar sua instalação individual e seus recursos exclusivos?”
3. “Qual conta Cloudflare vai hospedar o painel? Você pode entrar nela para configurar Pages, D1 e Access?” Não pedir senha ou token no chat.
4. “Qual Facebook conectará os anúncios? Será apenas consulta ou também edição de campanhas?” Começar com privilégio mínimo. Edição requer decisão explícita do proprietário.
5. “Quais BMs e contas deseja autorizar? Somente atuais selecionadas ou também futuras?” Não escolher automaticamente autorização ampla.
6. “Quais lojas deseja conectar? Quais URLs, repositórios, bancos e IDs do produto principal, adicionais e reentrega?” Distinguir catálogo de integração de vendas.
7. “Qual gateway e serviço de e-mail cada loja usa? Webhook, domínio de envio e rastreio já estão configurados?” Usar os fluxos existentes, sem gerar cobranças reais.
8. “Quais regras de imposto, taxa, custos e lucro usar?” A matriz preserva exemplos financeiros, não presume que são adequados a qualquer operação.

Segredos são cadastrados na Cloudflare do recurso correto, nunca em arquivos versionados, formulários de configuração que ecoam valores ou mensagens de chat. Se houver login, MFA ou decisão de consentimento, orientar o proprietário na plataforma.

## Etapas visuais propostas

1. **Acesso:** autenticar usuário e mostrar qual painel está sendo configurado.
2. **Identidade:** nome, domínio, fuso, moeda e administrador. Validar antes de criar recursos.
3. **Conectar Facebook:** iniciar OAuth; mostrar identidade conectada, permissões, validade e ativos autorizados. Oferecer renovar/desconectar apenas a própria conexão.
4. **Conectar lojas:** cadastrar integração por loja, consultar catálogo paginado, associar itens e conferir endpoint JWT. Não aceitar um proxy irrestrito de URL externa.
5. **Campanhas e produtos:** consultar contas reais, vincular campanha à loja e explicar as UTMs exigidas para atribuição de venda. Sem UTM, manter sem atribuição.
6. **Financeiro:** revisar taxas e imposto. Usar líquido confirmado sem desconto duplicado.
7. **Validação:** mostrar status por integração, falhas e pendências. Distinguir consulta real de teste simulado. Não preencher erro com zero.
8. **Concluir:** habilitar painel individual apenas após os requisitos de autenticação, isolamento e conexão serem verificados. Permitir retomar configuração incompleta sem duplicar recursos.

## Instalação individual: passo a passo para outra IA

1. Criar repositório privado novo a partir desta matriz; ler INSTALAR-MATRIZ.md e AGENTS.md.
2. Preencher recursos próprios em wrangler.jsonc. Criar Pages e D1 exclusivos e aplicação Access para o administrador correto.
3. Adaptar domínio canônico, identidade visual e lista de lojas. Os exemplos Loja A/B não são integrações prontas.
4. Implantar conector Meta exclusivo com banco e criptografia próprios; configurar service binding. Registrar callback exato no app Meta autorizado para essa instalação.
5. Fazer OAuth com o Facebook do usuário. A tabela geral de conexão pode continuar existindo porque aquele banco pertence somente àquele usuário.
6. Configurar pontes das lojas com JWT, audiência e administrador corretos. Não dar acesso ao banco de outra pessoa para “facilitar”.
7. Executar testes, prévia e validação de acesso bloqueado sem sessão; conferir consultas autenticadas reais. Não alterar orçamento, enviar contato ou gerar pagamento apenas para testar.
8. Publicar no domínio individual autorizado e registrar recursos, commit, deployment e instruções de renovação. Não guardar segredos no inventário.

## Entrega e continuidade

Atualizar ESTADO.md e PROJETO-PAINEL.json com os recursos da instalação e limitações reais. Entregar ao proprietário URLs, instruções de renovação e evidências dos testes, sem segredos. Na falta de acesso, informar qual etapa depende do proprietário e como retomá-la. Consultar documentação oficial atual dos provedores antes de implementar OAuth, permissões e recursos Cloudflare.
