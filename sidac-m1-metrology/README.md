# SIDAC-M1: Estação Metrológica Universal para Ativos Bélicos (Armas Curtas e Longas)

**Memorial Descritivo e Especificação Técnica de P&D**  
**Autor:** Filipe José Martins de Sá, Engenheiro Mecânico  
**Status:** Módulo de Bancada — Fase de Prototipagem e Validação de Engenharia

---

## 1. Fundamentação e Declaração do Problema
A manutenção preventiva e corretiva de armamento em corporações policiais, forças armadas e armarias comerciais historicamente padece de um gargalo fundamental: a ausência de instrumentação metrológica objetiva na ponta. 

Atualmente, o diagnóstico de fadiga e degradação de componentes elásticos críticos — notadamente a **mola recuperadora (*recoil spring*)** — apoia-se em dois métodos empíricos e falhos:
1. **Inspeção Visual Subjetiva:** O armeiro avalia o encolhimento físico da mola fora do guia ou compara visualmente com uma nova, incorrendo em altos índices de falso positivo ou na permanência de peças fatigadas em operação.
2. **Contagem Cega de Ciclos:** Substituição baseada em quilometragem/disparos teóricos (ex: troca a cada 5.000 tiros), o que ignora variações severas de temperatura, umidade, perfis de munição e condições de estresse real, resultando em desperdício logístico ou falhas prematuras de trancamento (*failure to return to battery*).

Adicionalmente, os equipamentos industriais de ensaio de molas existentes no mercado global são máquinas universais de grande porte, dispendiosas e restritas a laboratórios de metalurgia de fábrica, sendo inviáveis para o uso tático em oficinas de manutenção e bases operacionais descentralizadas.

---

## 2. A Solução: SIDAC-M1 Universal
O **SIDAC-M1** é uma estação de metrologia de bancada compacta, de alta rigidez estrutural e arquitetura **modular universal**. O sistema foi concebido para preencher a lacuna entre o laboratório industrial e a oficina de armaria, permitindo quantificar com precisão milimétrica a fadiga mecânica de molas recuperadoras tanto de pistolas quanto de carabinas/fuzis utilizando a mesma plataforma base.

O equipamento substitui a avaliação visual por curvas matemáticas de **Força versus Deslocamento** ($N/mm$), integrando-se ao ecossistema de diagnóstico preditivo do projeto SIDAC (que unifica a telemetria de campo à validação física de bancada)[cite: 3].

---

## 3. Especificações e Materiais Estruturais
Para assegurar a estabilidade dimensional sob cargas cíclicas repetidas e eliminar erros de medição decorrentes de flexão elástica do próprio chassi, o SIDAC-M1 emprega especificações industriais rígidas:

* **Chassi e Leito Principal:** Fabricado em **Aço AISI 4140** com tratamento térmico e acabamento superficial em **Oxidação Preta (*Black Oxide*)**, garantindo máxima resistência mecânica, limite de escoamento elevado e proteção anticorrosiva em ambientes de oficina severos[cite: 3].
* **Mecanismo de Avanço Linear:** Acionado por um **fuso de rosca (*lead screw*) de passo 2 mm**, proporcionando avanço milimetricamente controlado e conversão mecânica otimizada para o esforço manual ou motorizado[cite: 3].
* **Módulo de Aquisição de Carga:** Célula de carga do tipo *strain gauge* acoplada a um conversor analógico-digital (A/D) de 24 bits (**HX711**), com capacidade nominal padrão de $500 \text{ N}$ para pistolas e cabeça de acoplamento intercambiável para faixas superiores em armamento longo[cite: 3].
* **Interface de Operação Manual/Automatizada:** Volante de manobra em alumínio anodizado para controle fino de curso, dimensionado com torque ergonômico para operação em campo sem esforço excessivo[cite: 3].

---

## 4. Modelagem Matemática e Critérios Metrológicos
O comportamento elástico da mola recuperadora sob ensaio é governado pela **Lei de Hooke**, que correlaciona a força aplicada ($F$) com a deformação linear ($x$):

$$F = k \cdot x$$

Onde:
* $F$ é a força resistiva da mola medida pela célula de carga (em Newtons, $\text{N}$).
* $x$ é o deslocamento linear do fuso a partir do ponto de encosto inicial (em milímetros, $\text{mm}$).
* $k$ é a **constante elástica da mola** (em $\text{N/mm}$ ou $\text{N/m}$).

### Parâmetro de Referência — Plataforma Glock G22 Gen 5 (.40 S&W)
Para fins de calibração padrão do sistema, adota-se como baseline a mola recuperadora da plataforma Glock G22 Gen 5:
* **Força Nominal de Projeto ($F$):** $75,6 \text{ N}$ (equivalente a aproximadamente $17 \text{ lbf}$) medida na condição de compressão máxima de operação a $40 \text{ mm}$ de curso ($x = 40 \text{ mm}$)[cite: 3].
* **Constante Elástica Nominal ($k$):** Calculada por:

$$k = \frac{F}{x} = \frac{75,6 \text{ N}}{0,040 \text{ m}} = 1.890 \text{ N/m} \quad (\text{ou } 1,89 \text{ N/mm})$$

Qualquer desvio negativo superior a uma tolerância pré-estabelecida (ex: queda de $15\%$ na constante $k$ em relação ao baseline de fábrica) caracteriza fadiga avançada do componente, gerando um alerta automatizado de substituição no sistema de gestão.

---

## 5. Arquitetura do Sistema de Troca Rápida de Blocos (Modularidade Universal)
Para solucionar a restrição de patentes anteriores que exigiam máquinas dedicadas exclusivas para cada modelo de arma, o SIDAC-M1 inova ao adotar uma **arquitetura de blocos modulares intercambiáveis**:

* **Guias com Perfil em "T" (*T-Slot Guides*):** O leito estrutural de aço AISI 4140 possui canais longitudinais fresados que permitem o reposicionamento rápido e o travamento rígido dos suportes de apoio e dos cabeçotes de teste.
* **Blocos de Fixação Deslizantes (Estação de Carga e Estação de Apoio):** O armeiro pode soltar pinos de liberação rápida (*quick-release pins*) e deslizar os módulos para ajustar o curso útil da bancada de acordo com o comprimento livre ($L_0$) da mola a ser testada.
* **Mandris e Pinos Guia Modulares:** O sistema utiliza matrizes de pinos intercambiáveis de diâmetros e comprimentos variados. Para testar uma mola de pistola compacta, utilizam-se pinos de menor curso e diâmetro reduzido; para transicionar para a mola recuperadora de uma carabina de patrulha, o operador substitui apenas o bloco de pinos-guia frontal por encaixe de chaveta, sem necessidade de ferramentas especiais ou troca da estrutura de medição principal.
* **Escalabilidade de Curso ($L_0$ a $L_2$):** O conjunto permite abranger com precisão o estado estático sem carga ($L_0$), o estado montado em repouso ($L_1$) e o estado sob curso máximo de recuo acionado ($L_2$), mapeando integralmente a histerese do componente elastomérico ou metálico.

---

## 6. Desenho Técnico de Referência
A disposição construtiva, cotas principais e detalhamentos de usinagem encontram-se especificados na planta técnica oficial do projeto:
`sidac-m1-blueprint.png`
