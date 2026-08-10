🛡️ LAB 02: Insecure Output Handling & XSS via IA (OWASP LLM02) — TinyLlama Edition

Este repositório contém o laboratório prático de cibersegurança em Inteligência Artificial focado em Insecure Output Handling, exploração de XSS via IA e implementação de Sanitização de Saída (Output Guardrails) utilizando modelos open-source otimizados.

🎯 Objetivo do Laboratório
Demonstrar na prática como a confiança cega na saída gerada por Large Language Models (LLMs) sem a devida sanitização permite a injeção e execução de scripts maliciosos (XSS/Code Injection) na interface do usuário, e como mitigá-las utilizando camadas defensivas em Python (Output Guardrails e HTML Encoding).

🧪 Estrutura da Atividade
🔴 Red Team (Ataque)
• Conceito: Exploração da vulnerabilidade OWASP LLM02 no modelo TinyLlama (1.1B-Chat-v1.0), onde o texto retornado pela IA é renderizado diretamente na interface visual sem higienização ou validação de código.
• Vetor de Testes: Aplicação de ataques por Injeção de Scripts (<script>), Manipuladores de Erro em Imagens (img onerror), Quadros Embutidos (iframe/Phishing) e Atributos Interativos (onclick) para forçar a execução de código malicioso no navegador.

🔵 Blue Team (Defesa)
• Conceito: Aplicação do princípio de Defense in Depth e Sanitização de Saída (admitindo que a IA pode ser induzida a gerar payloads maliciosos e que a proteção deve ocorrer na camada de renderização).
• Solução: Implementação de uma camada de sanitização e pós-processamento (Output Guardrail) que aplica codificação de caracteres (HTML Encoding via html.escape) na resposta da IA antes de exibi-la, convertendo tags executáveis em texto inofensivo no navegador.
