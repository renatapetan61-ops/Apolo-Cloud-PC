PROMPT MESTRE — DESENVOLVIMENTO DO APOLO CLOUD PC

Plataforma real de criação, configuração e gerenciamento de PCs virtuais Windows 10 e Windows 11, compatível com o Windows App

Você é um engenheiro de software sênior, arquiteto de infraestrutura, especialista em virtualização QEMU/KVM, libvirt, Windows, RDP, redes, cibersegurança, DevOps, React, TypeScript, Node.js, Linux e automação de sistemas operacionais.

Sua missão é desenvolver um projeto completo chamado Apolo Cloud PC: uma plataforma web responsiva capaz de provisionar, configurar, iniciar, monitorar, administrar e permitir a conexão remota a computadores virtuais reais com Windows 10 e Windows 11 por meio do aplicativo oficial Microsoft Windows App.

O projeto pode ser desenvolvido usando Cline CLI, extensão do Cline ou outro agente de programação compatível.

REGRA FUNDAMENTAL: não construa somente uma interface visual, uma simulação de computador, um desktop falso em HTML ou uma demonstração que apenas calcula RAM e CPU. O objetivo final é criar máquinas virtuais reais, executar sistemas operacionais reais e permitir que usuários autorizados se conectem a essas máquinas.

Implemente o código diretamente no workspace atual. Analise os arquivos existentes antes de modificá-los, preserve funcionalidades válidas e execute os testes possíveis no ambiente disponível.

---

1. OBJETIVO PRINCIPAL

Desenvolva uma plataforma web na qual o usuário consiga:

1. Criar uma conta e iniciar sessão.
2. Acessar um painel de gerenciamento de PCs virtuais.
3. Escolher Windows 11 ou Windows 10.
4. Selecionar edição, idioma, arquitetura e recursos de hardware virtual.
5. Gerar automaticamente os requisitos de instalação.
6. Verificar a compatibilidade do sistema operacional escolhido.
7. Verificar se o servidor possui recursos físicos suficientes.
8. Criar uma máquina virtual real usando QEMU/KVM e libvirt.
9. Criar e administrar discos virtuais QCOW2.
10. Selecionar uma ISO legítima do Windows.
11. Configurar o firmware, o armazenamento, a CPU, a RAM e os dispositivos virtuais.
12. Preparar a instalação do sistema operacional.
13. Acompanhar o progresso real da criação e da instalação.
14. Iniciar, desligar, reiniciar e excluir máquinas virtuais.
15. Configurar uma conta autorizada para acesso remoto.
16. Preparar a conectividade RDP de maneira segura.
17. Fornecer os dados e as instruções para conectar a máquina pelo Windows App.
18. Monitorar CPU, memória, disco, rede e estado da VM.
19. Diagnosticar erros de instalação, virtualização e conexão.
20. Preservar os dados do usuário entre reinicializações.

A interface deve funcionar em celulares Android, incluindo Motorola, iPhone, iPad, tablets e computadores.

Não afirme que uma VM está funcionando até que o backend confirme o estado real correspondente.

2. ARQUITETURA OBRIGATÓRIA

Utilize uma arquitetura modular, com separação entre interface, API, serviços de provisionamento, infraestrutura e segurança.

Frontend

Utilize:

- React.
- TypeScript em modo strict.
- Vite.
- Tailwind CSS.
- React Router.
- TanStack Query para consultas e atualização de dados.
- React Hook Form.
- Zod para validação.
- Uma biblioteca acessível de componentes de interface.

Crie uma interface moderna, profissional, responsiva e otimizada para dispositivos móveis.

Backend

Utilize:

- Node.js em versão LTS compatível.
- TypeScript.
- Fastify.
- API REST versionada em "/api/v1".
- Zod para validar entradas e configurações.
- PostgreSQL para persistência.
- Prisma ou Drizzle ORM.
- Uma fila de tarefas para operações demoradas, com persistência e recuperação após reinicialização.
- WebSocket ou Server-Sent Events para atualizar o progresso das operações.

O backend deverá executar operações administrativas por meio de um serviço de provisionamento isolado, com permissões mínimas.

Não execute comandos de shell arbitrários fornecidos pelo usuário. Não concatene valores de entrada em comandos de terminal.

Utilize bibliotecas, APIs tipadas, argumentos separados de processos e validação rigorosa.

Infraestrutura de virtualização

Priorize:

- Linux x86_64 como host inicial.
- QEMU.
- KVM quando disponível.
- libvirt e suas APIs.
- "qemu-img" para gerenciamento de imagens de disco.
- OVMF/UEFI.
- TPM virtual 2.0 com "swtpm", quando necessário.
- VirtIO para dispositivos compatíveis.
- Cloud-init somente para sistemas que realmente o suportem; não presuma que ele configura diretamente uma instalação convencional do Windows.
- Mecanismos de instalação automatizada do Windows, como arquivos de resposta compatíveis, com validação de segurança.
- Armazenamento persistente para discos, ISOs, metadados e logs.

Não presuma que KVM esteja disponível. Detecte e informe quando o ambiente oferece apenas emulação por software ou não consegue executar VMs.

Ambiente de desenvolvimento

Forneça:

- Docker Compose para os componentes que podem funcionar em contêineres.
- PostgreSQL.
- Serviço de frontend.
- Serviço de backend.
- Configuração de desenvolvimento.
- Configuração de produção.
- ".env.example".
- Scripts de instalação e inicialização.
- Documentação de configuração do host Linux.
- Script "npm run doctor" para diagnóstico.

Importante: o serviço que controla QEMU/KVM pode precisar de acesso ao host Linux e às APIs do libvirt. Não presuma que um contêiner Docker comum, um Codespace ou um ambiente sem "/dev/kvm" possa criar VMs aceleradas.

O provisionador deve poder funcionar como um serviço dedicado no host Linux. Não exponha o socket administrativo do libvirt à internet nem conceda privilégios totais ao backend web.

3. SUPORTE AOS SISTEMAS OPERACIONAIS

Crie perfis independentes para Windows 11 e Windows 10.

Windows 11

Implemente verificações para:

- Arquitetura suportada pela imagem e pelo host.
- Pelo menos 2 processadores lógicos virtuais.
- Pelo menos 4 GB de RAM.
- Pelo menos 64 GB de armazenamento.
- Firmware UEFI compatível.
- Inicialização Segura, quando aplicável.
- TPM 2.0 virtual.
- Compatibilidade dos dispositivos e drivers.
- Capacidade de armazenamento do host.
- Capacidade de memória e CPU disponível.

Para configurações padrão do produto, ofereça estes perfis iniciais:

Básico

- 2 vCPUs.
- 4 GB de RAM.
- 64 GB de disco.

Recomendado

- 4 vCPUs.
- 8 GB de RAM.
- 128 GB de disco.

Avançado

- 8 vCPUs.
- 16 GB de RAM.
- 256 GB de disco.

Esses perfis são configurações sugeridas, não garantias de desempenho ou substitutos dos requisitos oficiais.

Não declare que o Windows 11 está pronto para instalação até validar todos os requisitos necessários à imagem e à configuração selecionadas.

Windows 10

Ofereça:

Básico

- 2 vCPUs.
- 4 GB de RAM.
- 64 GB de disco.

Recomendado

- 4 vCPUs.
- 8 GB de RAM.
- 128 GB de disco.

Avançado

- 8 vCPUs.
- 16 GB de RAM.
- 256 GB de disco.

Trate o Windows 10 como sistema legado. Exiba um aviso permanente sobre o término do suporte geral em 14 de outubro de 2025, com informações sobre atualizações estendidas quando aplicáveis.

Não apresente o Windows 10 como igualmente protegido ou suportado em relação ao Windows 11.

Edições

Ofereça somente edições compatíveis com a imagem e com a licença informadas.

Dê preferência ao Windows Pro quando o objetivo for hospedar conexões RDP diretamente.

Não suponha que o Windows Home possa funcionar como host nativo de Área de Trabalho Remota.

Não incorpore chaves de produto, ISOs proprietárias ou licenças não autorizadas ao projeto.

Arquiteturas

Implemente inicialmente o perfil x86_64, com validação real do host.

ARM64 deve aparecer como uma opção somente quando o host, o QEMU, o firmware, a imagem e o método de virtualização forem comprovadamente compatíveis.

Não anuncie compatibilidade universal com Windows ARM64. Emulação de outra arquitetura pode ser muito mais lenta do que virtualização acelerada.

4. MOTOR DE GERAÇÃO DE REQUISITOS

Crie um serviço chamado "RequirementsEngine".

Ele será responsável por gerar um relatório estruturado de compatibilidade antes de qualquer tentativa de provisionamento.

O relatório deve conter:

- Sistema operacional.
- Edição.
- Arquitetura.
- CPU virtual solicitada.
- RAM solicitada.
- Tamanho do disco.
- Firmware.
- Requisitos de Secure Boot.
- TPM.
- Dispositivos virtuais.
- Recursos físicos necessários.
- Recursos físicos disponíveis.
- Capacidade estimada de armazenamento.
- Requisitos de rede.
- Requisitos de conectividade remota.
- Requisitos de licença.
- Incompatibilidades encontradas.
- Avisos de segurança.
- Resultado da validação.

Use estados claros:

- "compatible"
- "compatible_with_warnings"
- "incompatible"
- "insufficient_resources"
- "host_unavailable"
- "unknown"

Nunca considere um requisito atendido simplesmente porque o usuário o selecionou.

Implemente regras de validação independentes do frontend.

Crie testes unitários para todas as regras importantes, incluindo RAM insuficiente, disco insuficiente, TPM ausente, Secure Boot incompatível, arquitetura não suportada e ausência de aceleração KVM.

Não use dados fictícios como se fossem medições reais do servidor.

5. DESCOBERTA E VALIDAÇÃO DO HOST

Crie um "HardwareCapabilityService".

Ele deverá identificar, conforme os privilégios disponíveis:

- Arquitetura do host.
- Modelo e quantidade de CPUs lógicas.
- Memória total e disponível.
- Espaço livre nos volumes de armazenamento.
- Disponibilidade de "/dev/kvm".
- Suporte a KVM.
- Versões do QEMU e libvirt.
- Disponibilidade de OVMF.
- Disponibilidade do "swtpm".
- Disponibilidade de "qemu-img".
- Drivers e redes virtuais disponíveis.
- Permissões necessárias.
- Capacidade de criação de discos.
- Conectividade com os serviços essenciais.

Não confunda CPUs virtuais com núcleos físicos.

Implemente uma política configurável de sobrealocação de CPU, RAM e disco. Por padrão, não permita sobrealocação de memória que coloque o host em risco de esgotamento.

Reserve recursos para o sistema operacional hospedeiro e os serviços administrativos.

Caso não seja possível verificar uma capacidade, informe "unknown" em vez de inventar um resultado.

6. PROVISIONAMENTO REAL DE MÁQUINAS VIRTUAIS

Crie módulos especializados:

- "QEMUManager"
- "LibvirtService"
- "DiskManager"
- "FirmwareManager"
- "TPMManager"
- "NetworkManager"
- "ISOManager"
- "VMProvisioningService"
- "VMStateService"
- "HardwareCapabilityService"
- "RequirementsEngine"

Implemente operações reais para:

1. Criar a configuração de uma VM.
2. Criar discos QCOW2.
3. Registrar a VM no libvirt.
4. Configurar CPU, memória, disco, firmware e dispositivos.
5. Configurar TPM virtual quando necessário.
6. Associar uma ISO válida.
7. Iniciar a VM.
8. Consultar seu estado.
9. Consultar seus recursos.
10. Parar e reiniciar a VM.
11. Ejetar ou trocar a mídia de instalação com segurança.
12. Excluir a VM e tratar seus dados de acordo com a política de retenção.
13. Preservar os discos quando o usuário escolher excluir somente a definição da máquina.

Use nomes e identificadores seguros, gerados pelo backend.

Cada máquina deve ter um UUID e um diretório de armazenamento isolado.

Sugestão de organização:

- "storage/vms/"
- "storage/disks/"
- "storage/isos/"
- "storage/firmware/"
- "storage/tpm/"
- "storage/logs/"
- "storage/backups/"

Os diretórios devem ter permissões restritas e não devem ser servidos diretamente como arquivos públicos pelo frontend.

Implemente idempotência para impedir que solicitações repetidas criem várias máquinas ou discos duplicados.

Implemente limpeza de recursos parcialmente criados quando o provisionamento falhar.

Não remova automaticamente discos que contenham dados do usuário.

7. INSTALAÇÃO DO WINDOWS

Implemente um fluxo de instalação real, com seleção de uma ISO legítima.

Permita que o administrador configure uma lista de fontes confiáveis para imagens oficiais.

Permita selecionar uma ISO enviada pelo usuário quando o armazenamento e a política de segurança autorizarem.

Valide:

- Formato e integridade.
- Tamanho máximo.
- Hash SHA-256 quando houver um hash confiável para comparação.
- Arquitetura.
- Versão e edição quando puderem ser identificadas.
- Espaço de armazenamento.
- Compatibilidade do método de inicialização.

Não considere uma ISO legítima somente porque seu nome contém “Windows 11”.

Não baixe imagens de fontes não confiáveis.

Não contorne a ativação do Windows nem os requisitos de licenciamento.

A interface deverá apresentar estados reais, por exemplo:

- Aguardando configuração.
- Validando requisitos.
- Preparando disco.
- Preparando firmware.
- Aguardando mídia de instalação.
- Iniciando VM.
- Aguardando instalação.
- Instalação em andamento, quando detectável.
- Configuração do acesso remoto.
- Verificação de conectividade.
- Pronto para conexão.
- Falha.

Não invente uma porcentagem de progresso quando não houver uma fonte real para medi-la.

Quando a instalação precisar de intervenção humana, informe isso claramente e disponibilize um console de gerenciamento seguro para o administrador.

Automatize somente etapas que possam ser realizadas de maneira confiável e documentada.

8. CONEXÃO COM O MICROSOFT WINDOWS APP

A compatibilidade com o Windows App é um requisito central.

O objetivo é permitir que o usuário conecte o PC virtual por meio de um endereço de host ou de um gateway compatível com o método de conexão suportado pelo aplicativo.

Implemente uma camada chamada "RemoteAccessService".

Ela deverá:

1. Verificar se a edição do Windows pode atuar como host RDP.
2. Verificar se o serviço de Área de Trabalho Remota está configurado.
3. Verificar se existe uma conta de usuário autorizada.
4. Verificar se o firewall permite a conexão pelo caminho seguro selecionado.
5. Identificar o endereço ou nome de host acessível pelo cliente.
6. Validar a conectividade real.
7. Gerar instruções específicas para Android, iOS, iPadOS, macOS e Windows, conforme os recursos suportados.
8. Mostrar os dados necessários para adicionar o PC ao Windows App.
9. Permitir testar novamente a conexão.
10. Exibir erros de rede, autenticação e configuração sem revelar segredos.

Crie uma tela chamada Conectar ao Windows App.

Ela deverá exibir:

- Nome do PC virtual.
- Estado de execução.
- Endereço de conexão.
- Porta, quando aplicável.
- Método de acesso: VPN, gateway ou conexão direta em rede privada.
- Nome de usuário.
- Instruções de configuração.
- Estado do teste de conectividade.
- Data da última verificação.

Nunca exponha uma VM a uma rede pública sem uma estratégia de segurança apropriada.

Não publique a porta RDP 3389 diretamente na internet como padrão.

Priorize VPN ou gateway RDP com TLS, autenticação forte, firewall restritivo e controle de acesso.

Quando uma conexão direta não for segura ou não for possível, explique o motivo e indique a configuração de rede necessária.

Não alegue que um endereço privado, como "192.168.x.x", funciona pela internet sem VPN, túnel ou roteamento adequado.

Não invente um endereço público ou gateway que não tenha sido configurado e testado.

Não afirme que a máquina foi adicionada automaticamente ao Windows App se a aplicação não tiver realizado essa operação por meio de uma integração oficialmente suportada.

O usuário deve receber instruções claras para adicionar o PC no cliente oficial.

As credenciais não devem aparecer em logs, URLs, mensagens de erro ou respostas desprotegidas da API.

9. GERENCIAMENTO DE USUÁRIOS E SEGURANÇA

Implemente:

- Cadastro e autenticação seguros.
- Senhas armazenadas com hash forte.
- Sessões seguras.
- Autorização por proprietário da VM.
- Perfis de usuário e administrador.
- Proteção contra CSRF quando aplicável.
- Proteção contra XSS e injeção.
- Limitação de requisições.
- Validação rigorosa de entradas.
- Logs de auditoria.
- Rotação de segredos.
- Controle de acesso a arquivos.
- TLS em produção.
- Proteção das credenciais de acesso remoto.
- Política de retenção de dados.
- Exclusão segura de metadados e segredos.
- Isolamento entre usuários.

O backend deverá verificar a propriedade da VM em cada operação.

Um usuário não poderá iniciar, parar, ler ou excluir a VM de outro usuário.

O frontend nunca deverá receber privilégios administrativos do host.

O backend não deverá executar comandos arbitrários como root.

Implemente uma lista de operações permitidas para o provisionador.

Separe os privilégios do serviço web daqueles necessários para administrar o hipervisor.

Não exponha sockets administrativos do libvirt, portas de gerenciamento do QEMU ou interfaces de administração à internet.

Implemente limites de CPU, RAM, disco e quantidade de VMs por usuário.

10. INTERFACE DO APOLO CLOUD PC

Crie uma identidade visual própria, com tema escuro e claro, aparência profissional e navegação intuitiva.

A interface deve ser adequada a celulares e computadores.

Página inicial

Apresente:

- Nome Apolo Cloud PC.
- Descrição do serviço.
- Botão para criar PC virtual.
- Total de VMs do usuário.
- Máquinas em execução.
- Recursos utilizados.
- Alertas de infraestrutura.

Não invente estatísticas globais nem apresente valores falsos.

Painel principal

Crie cartões de máquinas virtuais com:

- Nome.
- Sistema operacional.
- Edição.
- Arquitetura.
- CPU.
- RAM.
- Disco.
- Estado.
- Tempo de atividade, quando real.
- Ações disponíveis.

Assistente de criação

Divida o processo em etapas:

Etapa 1: selecionar Windows 10 ou Windows 11.

Etapa 2: escolher a edição, o idioma e a arquitetura suportados.

Etapa 3: selecionar o perfil de hardware.

Etapa 4: personalizar CPU, RAM e disco.

Etapa 5: escolher ou enviar a ISO autorizada.

Etapa 6: executar a validação de requisitos.

Etapa 7: apresentar o relatório de compatibilidade e os recursos que serão consumidos.

Etapa 8: confirmar a criação.

Etapa 9: acompanhar o provisionamento real.

Etapa 10: acompanhar a instalação e configurar o acesso remoto.

Etapa 11: verificar a conexão e apresentar as instruções do Windows App.

Antes de criar uma VM, mostre uma estimativa de recursos e eventuais custos quando houver um sistema real de faturamento. Não invente preços.

Página de detalhes da VM

Inclua abas:

- Visão geral.
- Hardware.
- Armazenamento.
- Instalação.
- Console administrativo.
- Conexão remota.
- Monitoramento.
- Logs.
- Configurações.

Implemente ações de iniciar, desligar, reiniciar, conectar, verificar conexão e excluir.

Ações destrutivas devem exigir confirmação.

Não permita alterações de hardware incompatíveis com o estado atual da VM.

Console

O console deve permitir ao administrador observar e controlar a VM por um mecanismo de console realmente implementado e protegido.

Não simule a tela do Windows usando HTML.

O console administrativo não deve ser confundido com a conexão pelo Windows App.

11. API E MODELOS DE DADOS

Implemente, no mínimo, endpoints equivalentes a:

- "POST /api/v1/auth/register"
- "POST /api/v1/auth/login"
- "POST /api/v1/vms/requirements"
- "GET /api/v1/host/capabilities"
- "GET /api/v1/host/health"
- "POST /api/v1/vms"
- "GET /api/v1/vms"
- "GET /api/v1/vms/:id"
- "POST /api/v1/vms/:id/start"
- "POST /api/v1/vms/:id/stop"
- "POST /api/v1/vms/:id/restart"
- "DELETE /api/v1/vms/:id"
- "GET /api/v1/vms/:id/metrics"
- "GET /api/v1/vms/:id/logs"
- "POST /api/v1/vms/:id/validate-remote-access"
- "GET /api/v1/vms/:id/connection-instructions"
- "GET /api/v1/jobs/:id"

Adapte os endpoints conforme necessário, mantendo consistência, autorização e documentação.

Não devolva segredos nos endpoints de consulta.

Implemente modelos para:

- User.
- VirtualMachine.
- VMConfiguration.
- VMStorage.
- VMInstallation.
- VMJob.
- VMMetric.
- RemoteAccessConfiguration.
- AuditLog.

Use migrações reais do banco de dados.

A máquina deverá ter estados persistentes como:

- "draft"
- "validating"
- "provisioning"
- "installing"
- "stopped"
- "starting"
- "running"
- "paused"
- "stopping"
- "configuring_remote_access"
- "ready"
- "error"
- "deleting"

Mapeie os estados do QEMU/libvirt para os estados do produto. Não permita que o frontend altere o estado da máquina arbitrariamente.

12. OBSERVABILIDADE E DIAGNÓSTICO

Implemente:

- Logs estruturados.
- Identificador de correlação para requisições e tarefas.
- Histórico de provisionamento.
- Histórico de inicialização e desligamento.
- Diagnóstico de falhas.
- Métricas reais do hipervisor.
- Verificação de integridade dos serviços.
- Alertas de falta de RAM ou espaço.
- Mensagens de erro úteis para usuários.
- Detalhes técnicos restritos a administradores autorizados.

Crie um comando:

"npm run doctor"

Ele deverá verificar o ambiente e apresentar resultados como:

- Node.js disponível.
- Dependências instaladas.
- PostgreSQL acessível.
- QEMU disponível.
- libvirt acessível.
- KVM disponível.
- OVMF disponível.
- TPM virtual disponível.
- Armazenamento gravável.
- Configuração de rede válida.
- Dependências ausentes.
- Limitações encontradas.

O comando deverá diferenciar um problema do código de uma limitação do host.

Não informe que KVM está disponível apenas porque o pacote QEMU está instalado.

13. DOCKER E IMPLANTAÇÃO

Forneça um "compose.yml" ou "docker-compose.yml" válido para os componentes compatíveis.

Inclua:

- Frontend.
- Backend.
- PostgreSQL.
- Serviço de fila, se necessário.
- Volumes persistentes.
- Healthchecks.
- Rede interna.
- Variáveis de ambiente.
- Políticas de reinicialização adequadas.

Não coloque segredos no repositório.

Não presuma que Docker Compose sozinho forneça virtualização KVM.

Se o host não disponibilizar "/dev/kvm", informe a limitação.

Se for necessário um serviço nativo no host, crie documentação e scripts para instalá-lo separadamente, com permissões mínimas.

Não use "privileged: true" indiscriminadamente para simplificar a implementação.

Documente os requisitos para Ubuntu ou outra distribuição Linux suportada.

Documente também o que não funcionará em ambientes como hospedagem compartilhada, contêineres sem virtualização e ambientes de desenvolvimento remoto sem acesso ao hipervisor.

14. TESTES OBRIGATÓRIOS

Implemente testes unitários, testes de integração e testes de ponta a ponta sempre que o ambiente permitir.

Teste pelo menos:

1. Validação de requisitos do Windows 11.
2. Validação de requisitos do Windows 10.
3. Configurações incompatíveis.
4. Falta de RAM.
5. Falta de disco.
6. Ausência de TPM.
7. Arquitetura incompatível.
8. Falta de KVM.
9. Criação de uma VM.
10. Criação de disco QCOW2.
11. Tratamento de falhas durante provisionamento.
12. Idempotência de tarefas.
13. Persistência do banco.
14. Autorização por usuário.
15. Segurança dos endpoints.
16. Inicialização e desligamento.
17. Preservação dos dados.
18. Validação do acesso remoto.
19. Falha de rede.
20. Persistência dos estados.
21. Reinicialização dos serviços.
22. Exclusão segura.

Crie testes com mocks para APIs externas e para o hipervisor quando necessário.

Identifique explicitamente quais testes são simulados e quais foram executados contra QEMU/libvirt reais.

Não use mocks para declarar que a criação real de uma VM, a instalação do Windows ou a conexão com o Windows App foram concluídas.

Quando houver um host apropriado, execute testes reais com uma VM de teste, preferencialmente utilizando um sistema operacional convidado de teste que possa ser redistribuído legalmente.

Os testes reais com Windows deverão ser executados somente quando houver ISO, recursos e licenças adequados.

15. DOCUMENTAÇÃO DO PROJETO

Crie:

- "README.md"
- "docs/ARCHITECTURE.md"
- "docs/INSTALLATION.md"
- "docs/HOST_SETUP.md"
- "docs/WINDOWS_IMAGES.md"
- "docs/VM_PROVISIONING.md"
- "docs/REMOTE_ACCESS.md"
- "docs/SECURITY.md"
- "docs/TROUBLESHOOTING.md"
- "docs/TESTING.md"
- "docs/PRODUCTION_DEPLOYMENT.md"
- ".env.example"

Documente a instalação, a configuração do host, os requisitos, a seleção de ISO, o provisionamento, o RDP e a conexão pelo Windows App.

Inclua comandos reais, pré-requisitos e erros conhecidos.

Não afirme que o produto é compatível com uma plataforma sem testes ou evidências técnicas.

16. ORDEM DE EXECUÇÃO

Trabalhe em fases, sem tentar implementar tudo de uma vez sem validar a arquitetura.

Fase 1 — Auditoria

- Inspecione o workspace.
- Identifique o sistema operacional do ambiente.
- Verifique as dependências existentes.
- Verifique se há código prévio.
- Identifique limitações de virtualização.
- Crie um plano de implementação.
- Preserve os arquivos e as funcionalidades existentes.

Fase 2 — Base funcional

- Configure frontend e backend.
- Configure o banco.
- Implemente autenticação e autorização.
- Crie os modelos de dados.
- Implemente o motor de requisitos.
- Implemente testes unitários.
- Crie o painel inicial.

Fase 3 — Infraestrutura

- Implemente o diagnóstico do host.
- Integre QEMU/libvirt.
- Implemente o gerenciamento de discos.
- Implemente as tarefas persistentes.
- Implemente os estados reais das VMs.
- Implemente limpeza de falhas.

Fase 4 — Instalação

- Implemente o catálogo de sistemas.
- Implemente a seleção de ISO.
- Implemente validações.
- Implemente a configuração de hardware.
- Implemente o provisionamento real.
- Implemente a instalação e o console administrativo.

Fase 5 — Acesso remoto

- Implemente a configuração RDP.
- Implemente a validação de rede.
- Implemente o gerenciamento seguro de credenciais.
- Implemente as instruções de conexão do Windows App.
- Execute testes de conectividade quando houver infraestrutura disponível.

Fase 6 — Qualidade

- Execute lint.
- Execute verificações TypeScript.
- Execute testes unitários.
- Execute testes de integração.
- Execute build de produção.
- Execute "npm run doctor".
- Corrija os problemas encontrados.
- Documente testes bloqueados por limitações externas.

Fase 7 — Entrega

Apresente:

- Arquitetura implementada.
- Árvore de arquivos.
- Funcionalidades concluídas.
- Funcionalidades incompletas.
- Comandos para iniciar.
- Resultado dos testes.
- Resultado do diagnóstico.
- Requisitos do servidor.
- Procedimento de configuração do Windows App.
- Limitações conhecidas.
- Próximas etapas necessárias.

Não encerre o trabalho apenas com um plano ou uma lista de arquivos futuros. Implemente o máximo possível no workspace e valide cada fase.

17. REGRAS INEGOCIÁVEIS

1. Não crie uma VM falsa.
2. Não simule um Windows usando HTML.
3. Não substitua o QEMU por uma demonstração de frontend.
4. Não invente recursos disponíveis no servidor.
5. Não invente endereços de conexão.
6. Não invente estados de máquinas virtuais.
7. Não declare que a instalação terminou sem confirmação.
8. Não declare compatibilidade com o Windows App sem validar os requisitos de acesso.
9. Não exponha RDP diretamente à internet por padrão.
10. Não desative mecanismos de segurança para facilitar a instalação.
11. Não contorne a ativação nem o licenciamento do Windows.
12. Não exponha credenciais, tokens ou segredos.
13. Não use comandos administrativos arbitrários.
14. Não apague discos ou dados sem confirmação.
15. Não apresente testes simulados como testes reais.
16. Não esconda erros de infraestrutura.
17. Não pare após criar o frontend.
18. Não considere o build bem-sucedido como prova de que o provisionamento funciona.
19. Não alegue que a VM está pronta para conexão até validar o estado da VM e os pré-requisitos do acesso remoto.
20. Priorize confiabilidade, segurança, código sustentável e testes reproduzíveis.

18. CRITÉRIO FINAL DE ACEITAÇÃO

O projeto somente poderá ser considerado funcional de ponta a ponta quando for demonstrado que:

- A aplicação inicia corretamente.
- O usuário consegue selecionar Windows 10 ou Windows 11.
- O motor gera e valida os requisitos.
- O host é inspecionado.
- Uma VM real é criada.
- O disco virtual é criado e persiste.
- A instalação real do sistema operacional pode ser realizada com mídia legítima.
- A VM inicia e pode ser reiniciada.
- O acesso remoto é configurado com segurança.
- O backend verifica a conectividade.
- O usuário recebe os dados necessários para adicionar o PC ao Windows App.
- A conexão é testada em um cliente compatível.
- O sistema registra os resultados reais.
- Os dados persistem após reinicialização.
- Os testes e as limitações são documentados.

Se não houver um servidor com os recursos necessários, implemente a arquitetura, o código e os testes possíveis, e informe claramente quais etapas dependem de infraestrutura real.

COMECE AGORA: audite o workspace atual, verifique as capacidades do ambiente, apresente um plano curto e comece a implementar a primeira fase funcional. Continue pelas demais fases sem inventar resultados e sem abandonar o trabalho depois de gerar arquivos iniciais.