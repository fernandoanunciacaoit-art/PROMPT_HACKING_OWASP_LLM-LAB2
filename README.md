# 🛡️ LAB 02: Insecure Output Handling & XSS via IA (OWASP LLM01 + LLM02) — TinyLlama Edition

Este repositório contém o laboratório prático de cibersegurança em Inteligência Artificial focado na vulnerabilidade de **Manipulação Insegura de Saída (Insecure Output Handling)** e na prevenção de ataques de **Cross-Site Scripting (XSS)** induzidos por IA através de **Sanitização de Saída (Output Guardrails & HTML Encoding)**.

---

## 🎯 Objetivo do Laboratório

Demonstrar na prática como a renderização direta e sem sanitização de conteúdo gerado por Large Language Models (LLMs) expõe a aplicação web a execuções maliciosas de código no navegador do usuário (XSS), e como mitigar esse risco aplicando técnicas de *HTML Encoding* e codificação defensiva no backend Python.

* **Modelo Utilizado:** TinyLlama 1.1B Chat (`TinyLlama/TinyLlama-1.1B-Chat-v1.0`)
* **Ambiente de Execução:** Google Colab (GPU T4)
* **Vulnerabilidade Alvo:** OWASP LLM02 - Insecure Output Handling / XSS via IA

---

## 🧪 Estrutura da Atividade

### 🔴 Red Team (Ataque)
* **Conceito:** Exploração da vulnerabilidade OWASP LLM02 no modelo TinyLlama, onde a IA é induzida por *Prompt Injection* a gerar estruturas HTML contendo scripts maliciosos, que são interpretados diretamente pela interface via `IPython.display.HTML()`.
* **Vetores de Teste:** Injeção direta de scripts (`<script>`), manipuladores de eventos (`onerror`, `onclick`) e frames interativos para simulação de *Phishing/UI Redress*.

### 🔵 Blue Team (Defesa)
* **Conceito:** Aplicação da estratégia de **Sanitização e Escapamento de Saída (Output Sanitization & Encoding)**.
* **Solução:** Implementação de um *Output Guardrail* na aplicação Python utilizando a biblioteca nativa `html.escape()`, convertendo caracteres especiais executáveis (`<`, `>`, `&`, `"`, `'`) em entidades HTML inofensivas.

---

## 📋 Detalhamento das Atividades Práticas (A a F)

### 🔴 Módulo Red Team (Ataques de XSS via IA)

* **Atividade A: Injeção via Tag de Imagem com Evento de Erro (`img onerror`)**
  * **Tática:** Induzir a IA a gerar uma tag `<img>` apontando para um recurso inexistente e contendo o manipulador de erro `onerror` com um payload JavaScript.
  * **Objetivo:** Confirmar que o navegador executa o script malicioso automaticamente ao tentar carregar a imagem quebrada.

* **Atividade B: Injeção de Redirecionamento e Phishing (`iframe / UI Redress`)**
  * **Tática:** Forçar a IA a injetar elementos de estrutura visual como `<iframe>` com protocolo `javascript:` ou botões com ações ocultas.
  * **Objetivo:** Demonstrar como um atacante pode manipular a interface visual da aplicação cliente através de respostas da IA.

* **Atividade C: Injeção via Manipulador de Eventos (`button onclick`)**
  * **Tática:** Solicitar a criação de elementos interativos (ex: botões de confirmação) contendo o atributo `onclick` injetado com código arbitrário.
  * **Objetivo:** Avaliar o risco de XSS armazenado/refletido ativado por interação do usuário.

---

### 🔵 Módulo Blue Team (Defesa & Sanitização)

* **Atividade D: Implementação do Output Guardrail (`assistente_protegido_render`)**
  * **Tática:** Desenvolvimento de uma função wrapper em Python que intercepta a saída do modelo e aplica `html.escape()` antes da exibição no frontend.
  * **Objetivo:** Impedir que o navegador interprete qualquer tag HTML/JS retornada pela IA como código executável.

* **Atividade E: Teste de Defesa contra Ataque Direto de XSS**
  * **Tática:** Submeter o payload básico de `<script>alert(...)</script>` à função protegida do Blue Team.
  * **Objetivo:** Validar se os caracteres `<` e `>` foram convertidos com sucesso para `&lt;` e `&gt;`, renderizando o payload apenas como texto puro.

* **Atividade F: Teste de Defesa contra Ataque Complexo (`img onerror`)**
  * **Tática:** Submeter o payload vetorial de imagem com evento de erro à função protegida do Blue Team.
  * **Objetivo:** Confirmar a eficácia e a resiliência da defesa contra manipuladores de eventos avançados e tags de mídia.

---

> **Lição Principal:** *"Mesmo quando um atacante consegue manipular o modelo para gerar payloads de código (Insecure Output Handling), o tratamento de dados no backend neutraliza o perigo antes que ele atinja o usuário final. Nunca renderize a saída da IA sem aplicar sanitização e codificação adequada!"*
