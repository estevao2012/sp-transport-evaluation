# Mobilidade Urbana em São Paulo

## Visão Geral do Projeto

Este projeto analisa a mobilidade urbana em São Paulo através de três mapas que seguem as etapas do processo de análise espacial: **Espacializar**, **Modelar** e **Integrar**.

## Mapa 1 – Coleta e Organização dos Dados
**Etapa:** Espacializar → Coletar, Armazenar, Visualizar
**Objetivo:** Mostrar de onde vêm os dados e como estão organizados no espaço.
**Como montar:** Sobreponha a base de transportes sobre o mapa da cidade.
**Mensagem crítica:** Infraestrutura concentrada no centro expandido → periferia pouco atendida.

**Como utilizar os dados:**
1. **Carregue todas as camadas** de transporte no SIG
2. **Use símbolos distintos** para cada modal (metrô, trem, ônibus, vias)
3. **Aplique cores contrastantes** para facilitar identificação
4. **Sobreponha sobre base cartográfica** de São Paulo
5. **Destaque a concentração** no centro expandido vs. periferia

| Tema                                      | Arquivos |
|-------------------------------------------|----------|
| Linhas e estações de metrô/trem           | mapa1/estacao_metro_v2.shp, mapa1/estacao_trem_v2.shp, mapa1/linha_metro_v4.shp, mapa1/linha_trem_v2.shp |
| Corredores/faixas exclusivas de ônibus    | mapa1/corredor_onibus_v2.shp |
| Principais vias                           | mapa1/classificacao_viaria_cet.shp |

## Mapa 2 – Processamento e Análise
**Etapa:** Modelar → Procurar, Quantificar, Correlacionar, Identificar Padrões, Compreender Fenômenos, Projetar Cenários
**Objetivo:** Gerar insights analíticos a partir dos dados coletados.
**Como montar:** Criar um mapa coroplético mostrando renda média ou densidade populacional por distrito. Sobrepor a rede de transporte.
**Mensagem crítica:** Bairros periféricos concentram população de baixa renda e maior tempo de deslocamento.

**Como utilizar os dados:**
1. **Crie mapas coropléticos** usando `densidade_demografica.shp` e `setor_censitario_vunerabilidade_social.shp`
2. **Classifique os dados** em 5-7 classes (ex: Jenks, Quantis)
3. **Use gradiente de cores** (ex: verde claro → vermelho escuro para densidade)
4. **Sobreponha as linhas de transporte** do Mapa 1 com transparência
5. **Compare padrões espaciais** entre densidade populacional e vulnerabilidade social
6. **Identifique áreas** com alta densidade e baixo acesso ao transporte

**Nota sobre Dados e Proxies:**
- **Renda média domiciliar:** Para obter dados espacializados de renda:
  1. Baixe a camada de Setor Censitário 2022 do GeoSampa (População > Censo Demográfico)
  2. Acesse http://sidra.ibge.gov.br e busque "rendimento médio domiciliar" por setor censitário para São Paulo
  3. Baixe a tabela (CSV/XLSX) com código do setor censitário e valor da renda
  4. No SIG, faça o join dos dados IBGE com o shapefile usando o código do setor censitário
  5. **Alternativa:** Use `setor_censitario_vunerabilidade_social.shp` como proxy (alta vulnerabilidade = baixa renda)

- **Densidade populacional como proxy para deslocamento pendular:** Regiões com maior concentração populacional tendem a gerar mais fluxos de deslocamento para trabalho e estudo, especialmente quando há desequilíbrio entre local de moradia e emprego.

| Tema                                      | Arquivos |
|-------------------------------------------|----------|
| População residente e densidade populacional por distrito | mapa2/distrito_municipal_v2.shp, mapa2/densidade_demografica.shp |
| Renda média domiciliar | mapa2/setor_censitario_vunerabilidade_social.shp + dados IBGE/SIDRA (ver instruções) |
| Deslocamento pendular (proxy: densidade populacional) | mapa2/densidade_demografica.shp |

## Mapa 3 – Comunicação e Suporte à Decisão
**Etapa:** Integrar → Transformar os resultados em conhecimento estratégico
**Objetivo:** Transformar análise em informação estratégica para ação.
**Como montar:** Sobrepor expansão do metrô às áreas vulneráveis.
**Mensagem crítica:** Investimentos futuros podem reduzir desigualdade de acesso e melhorar mobilidade social.

**Como utilizar os dados:**
1. **Carregue as áreas de favela** (`SIRGAS_SHP_favela.shp`) com destaque visual
2. **Sobreponha a rede atual** de transporte (dados do Mapa 1) em cinza
3. **Destaque a expansão planejada** (`estacao_metro_projetada.shp`, `linha_metro_projetada.shp`) em cores vibrantes
4. **Analise a proximidade** entre expansão planejada e áreas vulneráveis
5. **Identifique gaps** onde áreas de baixa renda não serão atendidas
6. **Crie buffer zones** ao redor das novas estações para medir impacto
7. **Use anotações** para destacar áreas prioritárias para investimento

| Tema                                      | Arquivos |
|-------------------------------------------|----------|
| Expansão planejada do metrô/trem          | mapa3/estacao_metro_projetada.shp, mapa3/linha_metro_projetada.shp |
| Distritos/áreas de baixa renda (Favela, e Cortiço) | mapa3/SIRGAS_SHP_favela.shp |
| Áreas de alta densidade populacional      | (não disponível) |

## Reutilização de Dados

**Rede de Transporte:** Os dados de transporte do Mapa 1 devem ser reutilizados como camada de sobreposição nos Mapas 2 e 3 para análise comparativa e contextualização das informações socioeconômicas e de planejamento.
