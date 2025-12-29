# Atendente Humanizado WhatsApp

![](https://user-gen-media-assets.s3.amazonaws.com/seedream_images/6441444d-178c-4c5d-8baf-154ecad48a27.png)
## Descrição

Este projeto implementa um atendente humanizado para WhatsApp utilizando automação com n8n e inteligência artificial. O sistema processa mensagens recebidas via WhatsApp, classifica o contexto da conversa e direciona para agentes especializados (suporte, SDR - Sales Development Representative, vendas) através de um gerente seletor inteligente.

O workflow permite configurar múltiplos agentes especializados que atuam de forma contextual, mantendo memória de conversas e gerando respostas humanizadas usando modelos GPT da OpenAI.

## Funcionalidades Principais

- **Recepção de Mensagens**: Integração com API EVO WhatsApp para receber mensagens de texto, áudio e imagem
- **Classificação Inteligente**: Análise automática do contexto para classificar setores (SUPORTE, VENDAS, SDR)
- **Agentes Especializados**: Roteamento para agentes específicos baseado no tipo de consulta
- **Memória de Conversa**: Armazenamento persistente de histórico em PostgreSQL
- **Respostas Humanizadas**: Geração de respostas naturais usando GPT-4/GPT-5-mini
- **Formatação Inteligente**: Divisão automática de mensagens longas (300-500 caracteres) com regras específicas
- **Controle de IA**: Capacidade de pausar/resumir a IA baseado em condições específicas

## Arquitetura

### Fluxo de Dados
1. **Webhook EVO** → Recebe mensagens WhatsApp
2. **Extração de Dados** → Processa conteúdo, telefone, timestamp, tipo de mensagem
3. **Consulta de Dados** → Busca informações do cliente no PostgreSQL
4. **Classificação de Setor** → Supabase AI classifica como SUPORTE/VENDAS/SDR
5. **Seleção de Agente** → Gerente seletor direciona para agente especializado
6. **Geração de Resposta** → OpenAI GPT gera resposta contextual com memória
7. **Formatação** → Aplica regras de formatação (sem negrito, links específicos)
8. **Envio** → Divide em múltiplas mensagens com atrasos de 1 segundo

### Componentes Técnicos
- **n8n**: Plataforma de automação do workflow
- **EVO WhatsApp API**: Integração com WhatsApp Business
- **OpenAI GPT**: Modelos gpt-4.1-mini e gpt-5-mini para geração de respostas
- **PostgreSQL**: Armazenamento de dados de clientes e memória de chat
- **Supabase**: Classificação AI e armazenamento vetorial
- **Redis**: Operações de cache e gerenciamento de memória


## Instalação e Configuração

### Pré-requisitos
- Instância n8n (local ou cloud)
- Conta OpenAI com API key
- Banco PostgreSQL
- Conta Supabase
- Instância Redis
- Credenciais EVO WhatsApp API

### Passos de Instalação

1. **Clone o repositório**:
   ```bash
   git clone <url-do-repositorio>
   cd atendente-humanizado-whatsapp
   ```

2. **Importe o workflow no n8n**:
   - Abra sua instância n8n
   - Importe o arquivo `Atendente Humanizado Whatsapp.json`

3. **Configure as credenciais**:
   - OpenAI API
   - PostgreSQL
   - Supabase
   - Redis
   - EVO WhatsApp

4. **Execute a criação da tabela**:
   - Execute o nó "Cria Tabela Dados Cliente" no workflow

5. **Configure o webhook**:
   - Copie a URL do webhook gerado
   - Configure no painel EVO WhatsApp

## Uso

### Testando o Workflow
1. Envie uma mensagem de teste via WhatsApp
2. Verifique o processamento no painel n8n
3. Confirme a classificação de setor e geração de resposta

### Configuração de Agentes
- **SUPORTE**: Questões de cobrança, pagamentos, reembolsos
- **VENDAS**: Consultas sobre mentorias particulares
- **SDR**: Desenvolvimento de vendas e prospecção


## Desenvolvimento

### Modificações Comuns
- **Adicionar novos setores**: Atualizar prompt do Supabase e lógica de roteamento
- **Alterar modelos AI**: Modificar nós OpenAI Chat Model
- **Regras de formatação**: Editar prompt do Parser Chain
- **Consultas de banco**: Atualizar nós PostgreSQL



## Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## Licença

Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

## Suporte

Para dúvidas ou problemas:
- Verifique a documentação do n8n
- Consulte os logs do workflow
- Teste as conexões das APIs externas