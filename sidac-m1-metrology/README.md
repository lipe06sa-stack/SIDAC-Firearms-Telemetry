# SIDAC-M1: Estação Metrológica de Bancada para Molas Recuperadoras de Armas Curtas

**Memorial Técnico e Especificação de Engenharia — Documento Preparatório**

**Autor:** Filipe José Martins de Sá, Engenheiro Mecânico

**Status:** Módulo de Bancada — Fase de Prototipagem e Validação de Engenharia (Fase I–II)

> **Confidencialidade e Reserva de Direitos:** este documento contém informação técnica preparatória para eventual depósito de pedido de patente junto ao INPI. O autor detém a titularidade sobre a invenção aqui descrita. A divulgação deste repositório não constitui cessão de direitos de propriedade intelectual.

---

## 1. Fundamentação e Declaração do Problema

A manutenção preventiva e corretiva de armamento em corporações policiais, forças armadas e armarias comerciais padece de um gargalo fundamental: a ausência de instrumentação metrológica objetiva na ponta.

Atualmente, o diagnóstico de fadiga e degradação de componentes elásticos críticos — notadamente a mola recuperadora (*recoil spring*) — apoia-se em métodos empíricos e falhos:

- **Inspeção Visual Subjetiva:** o armeiro avalia o encolhimento físico da mola fora do guia ou compara visualmente com uma nova, incorrendo em altos índices de falso positivo ou na permanência de peças fatigadas em operação.
- **Contagem Cega de Ciclos:** substituição baseada em quilometragem ou disparos teóricos (ex.: troca a cada 5.000 tiros), o que ignora variações severas de temperatura, perfis de munição e condições de estresse real, resultando em desperdício logístico ou falhas prematuras de trancamento.

Adicionalmente, os equipamentos industriais de ensaio de molas existentes no mercado são, em geral, máquinas universais de grande porte, dispendiosas e restritas a laboratórios de metalurgia de fábrica, sendo pouco práticas para uso em oficinas de manutenção e bases operacionais descentralizadas.

---

## 2. A Solução: SIDAC-M1

O SIDAC-M1 é uma estação de metrologia de bancada compacta e de alta rigidez estrutural, concebida para preencher a lacuna entre o laboratório industrial e a oficina de armaria, permitindo quantificar com precisão milimétrica a fadiga mecânica de molas recuperadoras de armas curtas.

O equipamento substitui a avaliação visual por curvas de força versus deslocamento precisas, em unidades de engenharia (Newtons por milímetro, N/mm), fechando o ciclo de manutenção preditiva com dados rastreáveis integrados ao ecossistema SIDAC.

---

## 3. Configuração Validada — Bancada para Armas Curtas (Fase Atual)

A configuração descrita nesta seção corresponde integralmente ao desenho técnico oficial do projeto (`sidac-m1-blueprint.png`), calibrada para a plataforma de referência Glock G22 Gen 5.

### 3.1 Especificações e Materiais Estruturais

- **Chassi e Leito Principal:** aço AISI 4140, com acabamento em oxidação preta (*Black Oxide*), garantindo resistência mecânica elevada e proteção anticorrosiva em ambiente de oficina.
- **Mecanismo de Avanço Linear:** fuso de rosca (*lead screw*) de passo 2 mm, proporcionando avanço milimetricamente controlado.
- **Módulo de Aquisição de Carga:** célula de carga *strain gauge* acoplada a conversor analógico-digital de 24 bits (HX711), capacidade nominal de 500 N.
- **Interface de Operação:** volante em alumínio anodizado (Ø120 mm) para controle fino de curso.
- **Curso Máximo:** 40 mm.

### 3.2 Desempenho Metrológico

- **Precisão de Leitura:** ±0,5% do fundo de escala (F.S.)
- **Repetibilidade:** ±0,2% do fundo de escala (F.S.)
- **Faixa de Temperatura de Operação:** 10°C a 40°C

---

## 4. Modelagem Matemática

O comportamento elástico da mola recuperadora sob ensaio é governado pela Lei de Hooke, que correlaciona a força aplicada (F) com a deformação linear (x):

**F = k · x**

Onde:
- **F** — força resistiva medida pela célula de carga, em Newtons (N)
- **x** — deslocamento linear do fuso a partir do ponto de encosto inicial, em milímetros (mm)
- **k** — constante elástica da mola, em N/mm ou N/m

### Parâmetro de Referência — Plataforma Glock G22 Gen 5 (.40 S&W)

- **Força nominal de projeto:** 75,6 N (aproximadamente 17 lbf), medida na condição de compressão máxima de operação a 40 mm de curso.
- **Constante elástica nominal:** k = 75,6 N ÷ 0,040 m = **1.890 N/m** (equivalente a **1,89 N/mm**).

Um desvio negativo superior a uma tolerância pré-estabelecida (ex.: queda superior a 15% na constante elástica em relação ao valor nominal) caracteriza fadiga avançada do componente, gerando alerta de substituição.

---

## 5. Roadmap de Expansão — Arquitetura Modular Universal (Fase Futura)

As funcionalidades descritas nesta seção representam a direção de desenvolvimento planejada para versões futuras do SIDAC-M1 e **ainda não possuem desenho técnico de engenharia correspondente**. Estão documentadas aqui como declaração de roadmap e diferencial estratégico frente a equipamentos de bancada de propósito único disponíveis no mercado — não como especificação construtiva validada.

- **Guias com Perfil em "T" (T-Slot Guides):** canais longitudinais fresados no leito estrutural, permitindo reposicionamento e travamento rígido dos suportes de apoio sem desalinhamento axial.
- **Blocos de Fixação Deslizantes:** pinos de liberação rápida (*quick-release pins*) para ajuste instantâneo do curso útil da bancada ao comprimento livre (L₀) da mola sob teste.
- **Mandris e Pinos-Guia Modulares:** matriz de pinos intercambiáveis de diâmetros e comprimentos variados, permitindo a transição de ensaio entre molas de pistola e de carabina por substituição do bloco de pinos-guia frontal.
- **Escalabilidade de Operação (L₀ a L₂):** mapeamento completo da histerese do componente, cobrindo o estado estático sem carga (L₀), o estado montado em repouso (L₁) e o estado sob curso máximo de recuo acionado (L₂).

**Pré-requisito de engenharia:** o avanço desta fase depende do desenvolvimento de um novo desenho técnico detalhado que incorpore fisicamente os elementos acima, antes de qualquer inclusão em pedido de patente.

---

## 6. Desenho Técnico de Referência

A disposição construtiva, cotas principais e detalhamentos de usinagem da configuração validada (Seção 3) encontram-se especificados na planta técnica oficial do projeto:

- **Arquivo:** `sidac-m1-blueprint.png` (disponível no repositório desta pasta).
- **Escopo do desenho:** vistas lateral, frontal, superior e isométrica; cortes A-A (longitudinal) e B-B (transversal); detalhes de fuso e célula de carga; especificações técnicas e quadro de identificação.

---

## 7. Nota Técnica — Preparação para Depósito de Patente (INPI)

Este documento é um memorial técnico de engenharia, adequado como base de portfólio e como ponto de partida para instrução de um pedido de patente. Ele **não substitui** o relatório descritivo formal exigido pelo INPI, que requer adicionalmente:

- Quadro reivindicatório (reivindicações numeradas, definindo precisamente o escopo de proteção pretendido);
- Correlação numérica entre o texto descritivo e os elementos indicados no desenho técnico (ex.: "o chassi (10) aloja o fuso de avanço (12)...");
- Seção de estado da técnica com identificação específica dos equipamentos ou soluções existentes dos quais o SIDAC-M1 se diferencia;
- Resumo (abstract) conforme padrão INPI.

A avaliação de qual modalidade de proteção é mais adequada — Patente de Invenção ou Modelo de Utilidade — assim como a redação final do quadro reivindicatório, deve ser conduzida por um agente de propriedade industrial ou advogado especializado antes do depósito.
