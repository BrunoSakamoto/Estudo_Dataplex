# Monitoramento de Dados
Com o essa função, é possível criar um processo de monitoramento automatizado dos datasets armazenados no GCS e no BigQuery, usando o Dataplex para governança e qualidade de dados. 

## Lakes
Ao criar um Lake você centraliza uma governança de dados dentro de área gerenciada (incluindo políticas de segurança e conformidade de dados)

## Zones
As zones são as subdivisões de um Lake organizadas para gerenciar e categorizar os dados com base no seu propósito ou estado de processamento. 

Um Lake pode ter uma zona bruta que armazena logs de servidor recém-coletados, e uma zona curada que contém os mesmos logs, mas transformados e filtrados para incluir apenas as informações relevantes para análises de uso. A zona curada teria regras de qualidade de dados mais rígidas, enquanto a zona bruta pode ser monitorada para verificar apenas a integridade dos dados brutos.

### Assets
Os Assets são os datasets contidos dentro de uma zona. Eles representam conjuntos de dados individuais, como arquivos no Google Cloud Storage ou tabelas no BigQuery. A função dos Assets é permitir o gerenciamento granular e a aplicação de regras de qualidade, segurança e governança em conjuntos de dados específicos.

## Função de cada um no Monitoramento

```
Lake: Serve como ponto central de governança e visualização do estado dos dados distribuídos. É onde você define políticas de
segurança e conformidade, e de onde você pode monitorar a qualidade dos dados em todas as zonas e ativos.
```
```
Zone: Ajuda a segmentar dados com base no estado de processamento ou tipo de dados, permitindo que as verificações de
qualidade sejam aplicadas de forma diferente em dados brutos e dados processados. Isso melhora o controle sobre os
diferentes tipos de dados que a suaorganização lida.
```
```
Asset: Nível mais granular de monitoramento. É onde você configura e aplica as regras de qualidade de dados, como validações
de esquema, detecção de valores nulos ou checagem de duplicidade. A execução de jobs para verificar a integridade dos dados
ocorre neste nível.
```

## Qualidade de Dados
A funcionalidade de Qualidade de Dados do Dataplex permite que você crie regras personalizadas para verificar a qualidade dos dados dentro dos Assets (conjuntos de dados) que pertencem a um Lake e suas respectivas Zones. Seu objetivo principal é monitorar continuamente a saúde dos dados e garantir que eles estejam prontos para uso analítico e operacional.

### Principais Funções
**Automatização de Verificações**: A opção de Qualidade de Dados possibilita a definição de regras que são aplicadas automaticamente aos dados, com base em agendamentos ou eventos, garantindo que verificações regulares ocorram sem a necessidade de intervenção manual.

**Definir e Aplicar Regras de Qualidade**: 
- Consistência: Se os dados mantêm um formato, tipo ou estrutura esperados.
- Integridade: Se há presença de todos os dados esperados, por exemplo, ausência de valores nulos em colunas críticas.
- Precisão: Se os dados seguem padrões numéricos ou de intervalos de valores específicos (como valores mínimos e máximos).
- Completude: Validação de que o conjunto de dados está completo, sem registros ou informações faltantes.
- Unicidade: Validação de que certos campos (como IDs) não possuem duplicatas.

## Gerar Perfis de Dados
Ao aplicar o perfil de dados, o Dataplex gera automaticamente estatísticas e metadados descritivos sobre o conjunto de dados, incluindo contagens de registros, distribuições de valores, percentuais de nulos, entre outros. Isso facilita a visualização da qualidade dos dados ao longo do tempo e oferece uma visão sobre padrões ou anomalias.

## Detecção e Notificação de Anomalias
Quando as regras de qualidade são violadas, o Dataplex pode emitir alertas e notificações, integrando-se ao Pub/Sub ou outras ferramentas de notificação para informar equipes responsáveis. Dessa forma, qualquer falha de qualidade pode ser identificada e resolvida rapidamente.

## Acompanhamento de Histórico de Qualidade
O Dataplex mantém um histórico das execuções das verificações de qualidade e suas falhas, permitindo que você visualize a evolução da qualidade dos dados ao longo do tempo. Isso é especialmente útil para auditorias e conformidade, ajudando a detectar e corrigir problemas sistemáticos.

## Componenentes da Qualidade de Dados no Dataplex
1. Regras de Qualidade de Dados: Essas regras são o núcleo das verificações de qualidade que o Dataplex realiza nos dados.
- Validação de Schema: Verificar se os dados têm o tipo de dados correto (ex.: string, inteiro) e se as colunas esperadas estão presentes.
- Checagem de Valores Nulos: Garantir que colunas essenciais não tenham valores nulos.
- Validação de Intervalo de Valores: Por exemplo, verificar se os valores numéricos estão dentro de um intervalo esperado (ex.: datas de nascimento não podem ser no futuro).
- Validar Unicidade: Garantir que certos campos, como identificadores únicos, não estejam duplicados.

2. Perfil de Dados Um Perfil de Dados é uma coleta automatizada de metadados e estatísticas sobre um ativo específico, como:
- Contagem de registros.
- Distribuição de valores.
- Percentual de valores nulos.
- Tendências de crescimento ou redução de dados.
- Detecção de outliers.

3. Monitoramento de Qualidade Automático: O Dataplex pode agendar verificações automáticas de qualidade, rodando jobs que verificam as regras configuradas em horários específicos (ex.: diariamente, semanalmente) ou após um evento (como a inserção de novos dados).

4. Integração com Notificações: Ao detectar uma falha de qualidade, o Dataplex pode ser configurado para enviar notificações via Pub/Sub, permitindo que o alerta seja enviado para ferramentas de monitoramento externas ou sistemas de notificação como o Google Cloud Monitoring, Slack, ou até emails.

5. Dashboards de Monitoramento: O Dataplex oferece visualizações que mostram o estado geral da qualidade dos dados, facilitando a inspeção rápida de anomalias e falhas detectadas. Isso permite que os responsáveis tomem decisões informadas sobre os dados que estão sendo monitorados.
