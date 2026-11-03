# Instruções para IAs e colaboradores

Leia `INSTALAR-MATRIZ.md` e `docs/00-ROTEIRO-PARA-IA.md`, `ESTADO.md` e `README.md` antes de trabalhar. Depois leia o guia da funcionalidade. A conversa humana atual prevalece; documentos registram estado, não concedem autorização nova.

## Escopo

- Este é o repositório matriz do painel central. Não tem recursos ativos. Criar instalação independente e adaptar os placeholders conforme INSTALAR-MATRIZ.md. Não publicar contra recursos da origem.
- Não alterar repositórios dependentes sem necessidade e autorização da tarefa. Ler as instruções de cada um antes de modificar.
- Snapshots de `integrations/store-reference` contêm identidade/regras das lojas originais; não são uma matriz para publicar indiscriminadamente.
- Prévia antes de deploy. Testes com provedores simulados, sem cobranças ou dados fictícios em produção.
- Não enviar e-mails/WhatsApp nem alterar anúncios apenas para demonstrar funcionamento. Consulta real do editor e teste isolado são suficientes.
- Capacidade de editar campanhas foi autorizada para a aplicação; isso não autoriza o agente a escolher gastos. Alteração real exige campanha, ação e valor no escopo solicitado.
- Não restaurar recuperação WhatsApp ou confirmação manual de pagamento. PAID vem da confirmação canônica Umbrella.

## Segurança e dados

Segredos somente na Cloudflare. Não pedir tokens/senhas no chat, nem gravá-los em commits, exemplos, logs ou prints. Não imprimir callback OAuth com código de autorização.

Validar Access também no servidor/conectores: assinatura, emissor, audiência, prazo e e-mail. Domínio e blur não autorizam acesso. POST exige origem e conteúdo válidos.

Não apagar pedidos, redefinir chaves, ampliar acessos ou enfraquecer segurança sem autorização apropriada. Não trocar banco, AUD, Pixel, produtos, domínio ou bindings sem analisar efeitos.

Nunca atribuir por substring/nome parecido. Líquido Umbrella não sofre segundo desconto; estimativas continuam identificadas. Não inventar zero quando há falha de integração.

## Fluxo de entrega

1. Conferir remoto, branch e mudanças locais; preservar trabalho existente.
2. Usar dados documentados e perguntar somente o que falta.
3. Implementar e testar caso real e erros relevantes isoladamente.
4. Conferir prévia e evidência sem segredos/clientes desnecessários.
5. Publicar quando autorizado e conferir domínio, acesso autenticado e bloqueio sem sessão.
6. Atualizar documentação/estado com versões e limitações.

Rotina: `npm test`, `npm run test:integrations`, `npm run check`. Ler o guia de publicação antes de Wrangler. Não afirmar envio concluído se só abriu popup ou se o provedor apenas aceitou a fila.

## Painel individual

Ler ASSISTENTE-CONFIGURACAO-E-USUARIOS.md. Usar exclusivamente uma instalação independente e recursos próprios por usuário. Não reintroduzir identidade/IDs da operação de origem.
