# Autobots Rubik
**Simulação Interativa de Cubo Mágico 3D com Three.js — Transformers Edition**

**UNIVERSIDADE CATÓLICA DE PERNAMBUCO — UNICAP** **Disciplina:** Programação 3D com Three.js - Computação Gráfica

### Autores
* Noemi Soares Gonçalves Da Silva
* Ricardo Nery De Brito Junior
* Willian Rodrigues Lima Silva
* Gabriel De Souza Leão Araújo
* Tarsila Amado Alves De Brito

*Recife, 26 de Maio de 2026*

## Sumário

1. [Introdução](#1-introdução)
2. [O que foi implementado](#2-o-que-foi-implementado)
   * [2.1 Requisitos Mínimos](#21-requisitos-mínimos)
   * [2.2 Extras Implementados](#22-extras-implementados)
3. [Divisão de Tarefas](#3-divisão-de-tarefas)
   * [3.1 Noemi Soares Gonçalves Da Silva — Issues #1, #2 e #6](#31-noemi-soares-gonçalves-da-silva--issues-1-2-e-6)
   * [3.2 Ricardo Nery De Brito Junior — Issues #3 e #4](#32-ricardo-nery-de-brito-junior--issues-3-e-4)
   * [3.3 Willian Rodrigues Lima Silva — Issues #5 e #7](#33-willian-rodrigues-lima-silva--issues-5-e-7)
   * [3.4 Gabriel De Souza Leão Araújo — Issue #8 e Documentação](#34-gabriel-de-souza-leão-araújo--issue-8-e-documentação)
   * [3.5 Tarsila Amado Alves De Brito — Issues #9 e #10](#35-tarsila-amado-alves-de-brito--issues-9-e-10)
4. [Dificuldades Encontradas](#4-dificuldades-encontradas)
   * [4.1 Dificuldades Coletivas](#41-dificuldades-coletivas)
   * [4.2 Dificuldades Individuais](#42-dificuldades-individuais)
5. [Uso de IA's](#5-uso-de-ias)
6. [Considerações Finais](#6-considerações-finais)

## 1. Introdução

Este relatório documenta o desenvolvimento do projeto *Autobots Rubik: Transformers Edition*, uma simulação interativa de Cubo Mágico (Rubik's Cube) tridimensional implementada com a biblioteca Three.js, executada diretamente no navegador sem necessidade de instalação de software adicional.

O projeto foi desenvolvido como trabalho da disciplina Programação 3D com Three.js, ministrada pelo professor Pedro Ximenes na Universidade Católica de Pernambuco (UNICAP), com prazo de entrega e apresentação em 26 de maio de 2026.

O tema escolhido foi a franquia *Transformers*, com identidade visual em laranja e azul, fundo espacial animado com campo de estrelas e HUD estilo terminal. O código foi organizado em 10 issues no GitHub, cada uma desenvolvida em branch separada e integrada via Pull Request.

## 2. O que foi implementado

Todos os requisitos mínimos e todos os itens extras listados no enunciado foram implementados. A seguir, o detalhamento de cada item.

### 2.1 Requisitos Mínimos

* Cubo 3x3x3 com 27 cubinhos individuais representados por BoxGeometry;
* Cores corretas por face: branco (topo), amarelo (base), laranja (direita), vermelho (esquerda), verde (frente) e azul (trás);
* Borda preta entre cubinhos com EdgesGeometry e gap visual de 0,02 via tamanho 0,98;
* Rotação de ao menos duas faces — expandida para as seis faces completas;
* Animação suave com interpolação do ângulo distribuída em 30 frames por movimento;
* Câmera com órbita via OrbitControls com damping para movimento suave.

### 2.2 Extras Implementados

* Todas as seis faces rotacionáveis: U, F, R, D, B e L — minúscula = horário, maiúscula = anti-horário;
* Botão embaralhar com animação encadeada de movimentos aleatórios;
* Detecção de vitória verificando cor única por face após cada movimento;
* Contador de movimentos com reset ao embaralhar;
* Tema visual Transformers: paleta laranja/azul, HUD estilo terminal e fundo espacial com 1000 estrelas animadas.

## 3. Divisão de Tarefas 

O trabalho foi organizado em 10 issues no GitHub. Cada integrante atuou em sua própria branch e integrou via Pull Request. Todas as issues foram concluídas antes do prazo de entrega do projeto. 

| Integrante | Issues | Responsabilidade |
| :--- | :--- | :--- |
| Noemi Soares Gonçalves Da Silva | #1, #2, #6 | Setup inicial, cubinhos 3x3x3, 6 faces rotacionáveis |
| Ricardo Nery De Brito Junior | #3, #4 |Rotação face superior (U) e face frontal (F) |
| Willian Rodrigues Lima Silva | #5, #7 | Interpolação suave de rotação e botão embaralhar |
| Gabriel De Souza Leão Araújo | #8 | Detecção de vitória e documentação (README) |
| Tarsila Amado Alves De Brito | #9, #10 | Contador de movimentos e tema visual Transformers |

### 3.1 Noemi Soares Gonçalves Da Silva — Issues #1, #2 e #6 

**Issue #1 — feat: setup inicial Three.js + OrbitControls** 

Responsável pela configuração completa da base do projeto. Foram criados os três pilares obrigatórios do Three.js: Scene, PerspectiveCamera com FOV de $75^{\circ}$ posicionada em (6, 5, 10) para visão diagonal do cubo, e WebGLRenderer com antialias e suporte a telas de alta resolução. O OrbitControls foi configurado com enableDamping para inércia suave e limites de zoom entre 4 e 30 unidades. O fundo espacial foi criado com THREE.Points e Float32Array de 1000 posições aleatórias. O loop de animação segue a ordem correta: requestAnimationFrame, controls.update() e renderer.render(). 

**Issue #2 — feat: construir cubo 3x3x3 com cubinhos coloridos** 

A construção do cubo utiliza loop triplo com x, y, z variando de -1 a +1, gerando 27 cubinhos.Cada um recebe array de 6 MeshLambertMaterial na ordem fixa do Three.js (+X, -X, +Y, -Y, +Z, -Z), com a cor da face se o cubinho estiver na borda, ou preto interno caso contrário. Tamanho 0,98 cria o gap visual do cubo mágico. Iluminação com AmbientLight e DirectionalLight dá volume ao cubo. O array cubinhos[] foi declarado em escopo global para uso nas issues seguintes.

**Issue #6 — feat: todas as 6 faces rotacionáveis**

Expansão do CONFIG_FACES de 2 para 12 entradas: seis minúsculas com sinalRotacao -1 (horário) e seis maiúsculas com sinalRotacao +1 (anti-horário), adicionando as faces R, L, D e B. A correção crítica foi remover o .toLowerCase() do listener de teclado, que convertia todas as teclas para minúsculo antes de consultar o mapa e impedia o funcionamento das maiúsculas.

### 3.2 Ricardo Nery De Brito Junior — Issues #3 e #4

**Issue #3 — feat: rotação da face superior (U)**

Para a execução dessa etapa, foi necessário dividir em 3 partes. primeiro uma função de filtro, que selecionaria dos 27 bloquinhos os 9 que tivessem a posição y = 1(para um melhor funcionamento a condição foi mantida como y>0,9 para abranger as posições depois de rotações anteriores, o que acabava gerando posições próximas a 1(0,999 ou 1,0001), por isso foi deixado essa margem de segurança mesmo com a implementação de arredondamento ao final da terceira parte). após a seleção dos 9 cubinhos escolhidos, usou o recurso de agrupamento, que de forma prática, enxergava os 9 cubinhos com uma única referência de posição, ideal para rotacionar como se fosse um único bloco. após isso foi foi criada a função de rotação, que não somente rotaciona mas anima de forma suave a rotação. faz isso usando a função requestAnimationFrame que em vez de rotacionar de forma brusca,é chamada recursivamente para rotacionar um pouco a cada chamada. por fim tem a função de desagrupar os cubinhos, que devolve os cubinhos filtrados anteriormente de volta para as novas posições, além de arredondar as posições e apagar o grupo criado.

**Issue #4 — feat: rotação da face frontal (F)**

Nessa etapa, foi decidido que, para facilitar a criação das próximas rotações, as funções criadas anteriormente deveriam ser adaptadas para uma forma genérica, que recebesse os diferentes parâmetros dependendo da tecla clicada e fizesse a rotação adequada. o bloco CONFIG_FACES foi criado para conter os diferentes parâmetros para cada tecla. as funções de filtração, animação e finalização mantiveram a lógica mudando somente para a forma genérica.

### 3.3 Willian Rodrigues Lima Silva — Issues #5 e #7

**Issue #5 — feat: interpolação suave de rotação (parte 1)**

A rotação suave foi desenvolvida junto com a rotação da face utilizando uma função recursiva, chamando o requestAnimationFrame, que faz a rotação de 90° de forma parcelada em 30 pequenas rotações.

**Issue #5 — feat: interpolação suave de rotação (parte 2)**

A parte 2 da issue, foi a implementação de um bloqueio para caso o usuário venha a apertar algum dos botões de movimento enquanto ocorrer outro, ou o embaralhamento. Para isso, o código possui variáveis booleanas estaGirando e estaEmbaralhando, onde ambas estão atribuídas como falsas. Na função window.addEventListener( ) possui uma condicional que verifica se a variável estaGirando tem o valor true. Caso sim, ela retorna não realizando nenhuma ação, caso não, aceita a entrada do usuário naturalmente. A mudança dela para true, está na função girarFace( ). Enquanto a variável estaEmbaralhando, muda seu estado dentro da função embaralhar( ). Ela fica true após uma checagem condicional do seu estado e retorna para false no fim da recursão de executarProximoMovimento( ). O girarFace( ) volta a ser false dentro da funcionalidade finalizarGiro( ).

**Issue #7 — feat: botão embaralhar com animação**

Para a implementação desta funcionalidade, foi necessário dividir as funções window.addEventListener( ) e girarFace( ). Ambas funcionalidades já prontas, a fatoração foi necessária para o reaproveitamento delas na função, embaralhar( ) que possui uma lista dos comandos já definidos no objeto CONFIG_FACES, um limite de movimentos e uma lista vazia que serve para guardar os comandos aleatoriamente. Essa lista é preenchida dentro de um loop. Após isso, há a função de chamada recursiva executarProximoMovimento( ), onde é passada como parâmetro no girarFace( ), especificamente na função finalizarGiro( ).

### 3.4 Gabriel De Souza Leão Araújo — Issue #8 e Documentação

**Issue #8 — feat: detecção de vitória**

O commit converteu a simulação geométrica em um sistema algorítmico finito ao implementar a condição de vitória e a interface de resolução. Para máxima eficiência, as cores foram convertidas em dados brutos (CORES_HEX), evitando comparações de objetos pesados em memória. O validador (verificarVitoria()) roda exclusivamente ao final de cada movimento para não afogar o framerate. Ele extrai as 9 peças das 6 bordas globais e checa a integridade cromática, usando uma tolerância de raio (< 0.5) para blindar o sistema contra falhas de flutuação decimal. Confirmado o padrão geométrico, o script manipula o DOM e sobrepõe a tela de sucesso.

**README.md — Documentação do projeto**
*A documentação foi estruturada para atuar como o manual técnico e operacional definitivo da simulação. O documento centraliza as seguintes informações táticas:*

* **Visão Geral do Sistema:** Apresentação do escopo do projeto, detalhando a utilização da biblioteca Three.js e a adoção da identidade visual baseada na franquia Transformers.
* **Protocolo de Execução:** Diretrizes rigorosas para rodar a aplicação no ambiente local, com ênfase na obrigatoriedade do uso de ferramentas como o Live Server para o correto carregamento dos scripts via CDN e prevenção de erros de renderização.
* **Mapeamento de Interação (Controles):** Documentação da interface de usuário invisível, listando a manipulação de câmera via mouse (OrbitControls) e a tabela de atalhos de teclado para as 12 rotações possíveis das faces (U, F, R, D, B, L minúsculas e maiúsculas), além da tecla de atalho para o embaralhamento automático.
* **Mapeamento de Entregas:** Listagem técnica de todas as funcionalidades embutidas no software, separando categoricamente os requisitos mínimos exigidos pela disciplina (geometria 3x3x3, materiais Lambert e animação de eixos) das adições extras desenvolvidas pela equipe (sistema de temas, detecção matemática de vitória e contador de movimentos).

### 3.5 Tarsila Amado Alves De Brito — Issues #9 e #10

**Issue #9 — feat: contador de movimentos**

A funcionalidade de contador de movimentos foi implementada para acompanhar o progresso do jogador durante toda a sessão. O valor começa em 0, é resetado sempre que o botão de embaralhar é acionado e incrementa a cada giro válido executado pelo usuário. A atualização visual acontece diretamente no HUD, mantendo a contagem sempre sincronizada com o estado atual do cubo.

**Issue #10 — feat: tema visual Transformers**

O projeto recebeu uma identidade visual baseada na franquia Transformers, com uma paleta principal em laranja e azul e um estilo de interface inspirado em terminal/HUD. Foram implementados três temas distintos: Autobots, Decepticons e Energon, com botões interativos para alterar a aparência do cenário geral. Além disso, o fundo espacial foi mantido com partículas animadas representando o universo.

## 4. Dificuldades Encontradas

### 4.1 Dificuldades Coletivas

**Compatibilidade de versão do Three.js**
A versão 0.165.0 referenciada nos materiais da disciplina não possuía mais os arquivos three.min.js e OrbitControls.js nos caminhos tradicionais, pois essa estrutura foi descontinuada em versões mais recentes. A solução foi migrar para a versão 0.132.2, que mantém a estrutura clássica compatível com importação via CDN.

**Carregamento dos scripts CDN no Live Server**
O ambiente Live Server do VS Code apresentou o erro THREE is not defined em diversas configurações testadas, incluindo uso de defer, async e DOMContentLoaded. A solução definitiva foi manter os CDNs no head do HTML sem atributos adicionais.

**Reancoragem dos cubinhos após rotação**
Após cada giro, os cubinhos precisavam ser transferidos de volta à cena global com scene.attach(), preservando a transformação aplicada pelo grupo temporário. O arredondamento com Math.round() foi necessário para eliminar erros de ponto flutuante acumulados, sem esse tratamento, valores como 0,9999997 impediam a correta seleção dos cubinhos nas rotações seguintes.

### 4.2 Dificuldades Individuais

**Noemi Soares Gonçalves Da Silva (Issues #1, #2, #6)**
* Compatibilidade de versão do Three.js e erro de carregamento da CDN, conforme seção 4.1;
* Entendimento da ordem fixa de materiais do BoxGeometry (+X, -X, +Y, -Y, +Z, -Z), essencial para o correto colorimento das faces de cada cubinho.

**Gabriel De Souza Leão Araújo (Issue #8)**
* **Imprecisão de Ponto Flutuante:** Evitar falsos negativos na validação de vitória causados pelo acúmulo de distorções decimais (ex: 0.9999) nas coordenadas espaciais após múltiplas rotações. A solução exigiu substituir a validação de igualdade estrita por uma fórmula de margem de tolerância geométrica (Math.abs(...) < 0.5).
* **Otimização de Memória na Validação:** Ineficiência estrutural ao tentar comparar instâncias completas da classe Material do Three.js para checar as faces resolvidas. Foi necessário modelar uma função de extração para isolar os dados hexadecimais puros (CORES_HEX), permitindo uma comparação algorítmica exata e leve.

## 5. Uso de IA's

### 5.1 Claude

**Configuração da Cena e Ambiente Espacial (Issue #1)**
**Prompt:** "Estou a planear o início do projeto e preciso de orientação: qual é a melhor arquitetura de ficheiros para evitar problemas de bloqueio de scripts no navegador e como posso modelar matematicamente um fundo espacial de estrelas de forma eficiente, garantindo que fiquem distribuídas de forma homogénea ao redor do centro?"
**Resultado:** Recomendou concentrar o código num único ficheiro para mitigar restrições de execução local e sugeriu um sistema de partículas baseado num vetor linear em vez de texturas pesadas. Orientou subtrair meio ponto da função de aleatoriedade antes de definir a escala, justificando que isso deslocaria a origem do sorteio para o ponto zero cartesiano e garantiria a dispersão equivalente nos quadrantes positivos e negativos para envelopar o cenário uniformemente.
**Onde foi usado no Código:** Orientou a declaração das variáveis globais de renderização e isolou a lógica de partículas na função dedicada `criarEstrelas`.

**Arquitetura 3D do Cubo 3x3x3 (Issue #2)**
**Prompt:** "Como posso estruturar a lógica para gerar os 27 blocos do cubo mágico de forma automatizada e qual é a abordagem técnica recomendada para pintar individualmente as faces, de modo a preservar o desempenho e não expor cores nos blocos internos do miolo?"
**Resultado:** Propôs criar uma matriz tridimensional abstrata recorrendo a três ciclos de repetição encadeados para mapear as coordenadas espaciais. Orientou aplicar um feixe de seis materiais distintos por malha aproveitando uma propriedade nativa da geometria cúbica e sugeriu condicionais de verificação posicional para identificar blocos de borda ou de miolo, instruindo o motor a pintar apenas as superfícies externas e a manter o interior oculto.
**Onde foi usado no Código:** Norteou a definição do dicionário `CORES`, os parâmetros de montagem dentro da função `criarCubinho` e a população do array `cubinhos`.

**Sistema de Rotação Universal e Correção do Teclado (Issue #6)**
**Prompt:** "Estamos com uma limitação no código herdado onde o sistema ignora a distinção entre maiúsculas e minúsculas, bloqueando as rotações inversas das faces. Como posso modelar uma estrutura de dados universal para as 6 faces e corrigir a leitura dos eventos de teclado?"
**Resultado:** Sugeriu estruturar as propriedades das faces num objeto de configuração centralizado que associasse a cada comando a um vetor de corte e a um eixo específico. Diagnosticou que o tratamento de texto existente convertia os caracteres para minúsculas eliminando o estado original da tecla e recomendou remover essa mutação para analisar a propriedade bruta do evento, permitindo diferenciar o sentido horário do anti-horário por multiplicadores de sinal.
**Onde foi usado no Código:** Moldou a estrutura do objeto `CONFIG_FACES` e modificou a função de resposta dentro do ouvinte global `window.addEventListener`.

### 5.2 Gemini

**Efeito Visual de Brilho e Pulsação no Ícone de Vitória (Issue #8)**
**Prompt:** "Como posso adicionar um efeito de brilho de fundo numa imagem PNG de um ícone usando CSS, garantindo que o brilho contorne a geometria do desenho em vez de formar uma caixa retangular, e como faço para esse brilho pulsar continuamente?"
**Resultado:** Recomendou a utilização da propriedade CSS filter: drop-shadow() em detrimento de box-shadow. Justificou que a primeira respeita o canal alfa (transparência) da imagem, projetando a luz estritamente ao redor da silhueta do ícone, enquanto a segunda preencheria o bounding box do elemento HTML. Instruiu também a formulação de uma regra @keyframes estruturada para alternar fluidamente o raio de expansão do desfoque e a escala bidimensional (transform: scale), gerando o ciclo contínuo de pulsação luminosa.
**Onde foi usado no Código:** Aplicado nas regras de estilização do seletor #iconeVitoria, definindo a matriz de sombra base, e na declaração do escopo de animação @keyframes pulsar no cabeçalho de estilos da camada de interface.

## 6. Considerações Finais

O projeto Autobots Rubik foi concluído com todos os requisitos mínimos e extras atendidos. A organização por issues no GitHub mostrou-se eficaz para a divisão do trabalho, permitindo que cada integrante atuasse de forma independente e integrasse o código via Pull Request sem conflitos significativos.

A principal aprendizagem técnica foi a compreensão do sistema de hierarquia de grupos do Three.js (THREE.Group), análogo ao ctx.save()/restore() do Canvas 2D estudado anteriormente, aplicado ao problema de rotação de faces do cubo mágico.

O resultado final é um cubo mágico interativo completo, jogável no navegador, com todas as seis faces rotacionáveis, embaralhamento animado, detecção de vitória e contador de movimentos, entregue dentro do prazo estipulado.
