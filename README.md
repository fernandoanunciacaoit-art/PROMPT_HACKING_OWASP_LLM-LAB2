# 🛡️ LAB 02: Insecure Output Handling & XSS via IA (OWASP LLM02)

Este repositório contém o laboratório prático de cibersegurança em Inteligência Artificial, focado na exploração da vulnerabilidade de **Manipulação Insegura de Saída (Insecure Output Handling)** e na prevenção de ataques de **Cross-Site Scripting (XSS)** induzidos por IA através de **Sanitização de Saída (Output Guardrails & HTML Encoding)**.

---

## 🎯 Objetivo do Laboratório

Demonstrar na prática como a vulnerabilidade **OWASP LLM02** permite que payloads de XSS e tags HTML maliciosas gerados por uma LLM sejam renderizados e executados no navegador do usuário, e como implementar camadas defensivas de sanitização de saída no backend Python para neutralizar esse risco antes da exibição ao usuário final.

* **Modelo Utilizado:** TinyLlama 1.1B Chat (`TinyLlama/TinyLlama-1.1B-Chat-v1.0`)
* **Ambiente de Execução:** Google Colab (GPU T4)
* **Vulnerabilidade Alvo:** OWASP LLM02 - Insecure Output Handling (XSS / UI Redress)

---

## 🧪 Estrutura da Atividade

### 🔴 Red Team (Ataque)
* **Conceito:** Indução da IA, via *Prompt Injection*, a gerar estruturas HTML/JS maliciosas que são interpretadas diretamente pela interface (`IPython.display.HTML`).
* **Vetores de Teste:** Injeção direta de scripts (`<script>`), manipuladores de eventos (`onerror`, `onclick`) e frames de phishing (`<iframe>`).

### 🔵 Blue Team (Defesa)
* **Conceito:** Aplicação da estratégia de **Sanitização e Codificação de Saída (Output Sanitization & Encoding)**.
* **Solução:** Implementação de um *Output Guardrail* no backend que utiliza `html.escape()` para neutralizar caracteres executáveis, transformando código ativo em texto inofensivo.

---

## 📋 Detalhamento das Atividades Práticas

### Módulo Red Team (Ataques de XSS via IA)
* **Atividade A:** Injeção via tag de imagem com evento de erro (`img onerror`).
* **Atividade B:** Injeção de redirecionamento e phishing (`iframe`).
* **Atividade C:** Injeção via manipulador de eventos (`button onclick`).

### Módulo Blue Team (Defesa & Sanitização)
* **Atividade D:** Implementação da função `assistente_protegido_render()` com `html.escape()`.
* **Atividade E:** Validação da defesa contra XSS simples.
* **Atividade F:** Validação da resiliência contra ataques complexos (`img onerror`).

---

> **Lição Principal:** *"A saída de um modelo de linguagem deve ser tratada como 'input' não confiável por qualquer interface de usuário. Nunca renderize HTML gerado por IA sem uma camada de sanitização rigorosa no backend."*
