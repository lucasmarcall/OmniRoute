# Plano de integração segura — OmniRoute + Codex CLI + GitHub (iPad)
Data: 2026-11-14
Status: PREPARADO, NÃO INSTALADO OU VALIDADO EM EXECUÇÃO.

## Escopo
- Repositório: lucasmarcall/OmniRoute
- Base de trabalho: release/v3.8.54
- Branch isolada: setup/ipad-codex-github-safe
- Não modificar outros repositórios, o Codex do ChatGPT, configurações preexistentes ou a branch principal.
- Não incluir credenciais, tokens ou informações de clientes em commits, logs ou arquivos públicos.
- Custo-alvo: franquia gratuita do GitHub Codespaces; sem ativar uso pago.

## Pré-verificações (antes de instalar)
1. Confirmar diferenças do fork em relação ao projeto de origem. Não clicar em Sync fork nem atualizar dependências automaticamente.
2. Conferir os scripts de instalação do package.json, Node/pnpm exigidos, RAM e espaço do Codespaces.
3. Criar Codespace nesta branch com porta privada e configuração de menor consumo viável.
4. Guardar chaves SOMENTE em Secrets do Codespaces ou no ambiente de execução, nunca no repositório.
5. Autenticar GitHub no Codespaces com permissões mínimas e ler repositórios de destino sem editá-los.

## Integração de teste
1. Iniciar o serviço OmniRoute na porta 20128 dentro do Codespaces, após auditoria de dependências.
2. Abrir o painel via encaminhamento PRIVADO de portas do Codespaces; manter autenticação do painel.
3. Dashboard > Providers: conectar um provedor elegível de teste, de preferência quota gratuita confirmada.
4. Dashboard > Endpoints: criar credencial de API com escopo mínimo, armazenada fora do git.
5. Instalar/verificar Codex CLI no próprio Codespaces, sem alterar ~/.codex existente.
6. Usar CODEX_HOME em diretório isolado e testar 'omniroute setup-codex --dry-run' antes de escrever perfis.
7. Para testar integração sem gravar configuração, avaliar 'omniroute launch-codex --model auto' ou 'omniroute run codex --model auto', após confirmar suporte da versão instalada.
8. Usar wire_api='responses' nos perfis Codex; base de teste http://localhost:20128/v1 apenas DENTRO do Codespaces. A chave deve ser referenciada por OMNIROUTE_API_KEY no ambiente.

## Segurança e testes
- Verificar resposta do endpoint de modelos por requisição autenticada; não registrar a chave.
- Testar Codex em pasta descartável, SEM acesso a dados reais.
- Validar somente leitura de um repositório de exemplo, depois leitura dos projetos existentes.
- Alterações futuras: branch separada por projeto, testes, revisão de diff, commit/PR e aprovação explícita antes de integrar.
- Não dar acesso público à porta 20128 e não expor /api ou dashboard sem autenticação.
- Desligar Codespaces após uso e acompanhar a franquia.

## Checkpoint
- Preparado: roteiro e branch de trabalho isolada.
- Pendente: auditoria operacional de dependências; instalação Codespaces; autenticação; provedor; endpoint; testes.
- Critério de conclusão: painel autenticado abre no Safari, provedor autorizado responde, Codex CLI usa OmniRoute no teste isolado e GitHub permanece sem mudanças não autorizadas.

Documentação do próprio fork:
- docs/guides/CLI-INTEGRATIONS.md
- docs/guides/CODEX-CLI-CONFIGURATION.md
- docs/OMNIROUTE_PROVIDER_FAILOVER.md
