# Desafio de Código: Malware Simulado com Python (Educação e Defesa)
# Anna Elizabeth Parra Rausseo
# https://github.com/annaeparrar/

> **Status:** Concluído

## Visão Geral do Projeto

Este projeto foi desenvolvido como parte de um desafio prático com o objetivo de **compreender, simular e documentar** o funcionamento de ameaças digitais comuns (Ransomware e Keylogger) utilizando a linguagem Python. É crucial ressaltar que **todos os códigos e experimentos são estritamente para fins educacionais e de pesquisa**, sendo executados em um ambiente 100% controlado (como uma máquina virtual ou sandboxing), a fim de analisar mecanismos de ataque, e, o mais importante, desenvolver estratégias robustas de **defesa e mitigação**.

O foco principal é transformar o conhecimento sobre como esses malwares operam em ferramentas práticas para a segurança digital.

## Reflexão sobre Defesa e Mitigação

A melhor defesa contra ameaças como Ransomware e Keyloggers reside na combinação de tecnologias de segurança e na conscientização do usuário.

### Medidas de Prevenção e Detecção:

* **Antivírus (AV) e Endpoint Detection and Response (EDR):** Utilizam assinaturas e análise comportamental (heurística) para detectar e bloquear a execução de scripts suspeitos.
    * *Detecção de Ransomware:* Monitoram padrões de acesso e criptografia massiva de arquivos.
    * *Detecção de Keylogger:* Sinalizam a utilização de APIs de baixo nível do sistema operacional para monitoramento de teclado (como a `pynput` faz).
* **Firewall:** Restringe a comunicação de saída (Egress Filtering). Um Ransomware ou Keylogger precisa se comunicar com o Servidor de Comando e Controle (C2). Um firewall bem configurado bloqueia conexões não autorizadas.
* **Sandboxing e Máquinas Virtuais (VMs):** Executam arquivos suspeitos em ambientes isolados, impedindo que o malware acesse ou danifique o sistema operacional principal e os dados reais.
* **Princípio do Menor Privilégio:** Usuários devem ter apenas as permissões necessárias para o seu trabalho. Um Keylogger rodando com privilégios limitados terá dificuldade em se instalar no sistema ou persistir.

### Melhores Práticas do Usuário:

* **Backup 3-2-1:** Manter **3** cópias de seus dados, em **2** mídias diferentes, sendo **1** cópia externa (offline). Este é o método mais eficaz contra o Ransomware.
* **Conscientização:** Evitar clicar em anexos ou links de e-mails suspeitos (Phishing). A engenharia social é o vetor de ataque mais comum.
* **Atualização de Software:** Manter o sistema operacional, navegadores e aplicativos sempre atualizados para corrigir vulnerabilidades conhecidas.

---

## Recursos e Bibliotecas Utilizadas

* **Python:** Linguagem principal
* `cryptography`: Para o Ransomware (módulo Fernet).
* `pynput`: Para a captura de teclado no Keylogger.
* `smtplib`: Para simulação de exfiltração de dados por e-mail.
* `os` e `sys`: Para interação com o sistema de arquivos e caminhos.

---

## Conclusão:

Este desafio demonstrou que a compreensão do lado ofensivo (como o malware atua) é essencial para o desenvolvimento de defesas eficazes. O próximo passo seria aprofundar a análise comportamental desses scripts em ferramentas de segurança reais.

```

---


# Malware Simulado com Python (Educação e Defesa)

Este projeto foi desenvolvido como parte de um desafio prático com o objetivo de **compreender, simular e documentar** o funcionamento de ameaças digitais comuns (Ransomware e Keylogger) utilizando a linguagem Python. É crucial ressaltar que **todos os códigos e experimentos são estritamente para fins educacionais e de pesquisa**, sendo executados em um ambiente 100% controlado (como uma máquina virtual ou sandboxing), a fim de analisar mecanismos de ataque, e, o mais importante, desenvolver estratégias robustas de **defesa e mitigação**.

O foco principal é transformar o conhecimento sobre como esses malwares operam em ferramentas práticas para a segurança digital.

---

## Implementação e Simulação

### 1. Ransomware Simulado

O script de Ransomware simula o processo de criptografia de arquivos em uma pasta específica e controlada, seguido pela descriptografia para reverter a ação.

| Recurso | Descrição | Biblioteca(s) Principal(is) |
| :--- | :--- | :--- |
| **Geração de Chave** | Criação de uma chave simétrica forte (Fernet) para criptografia/descriptografia. | `cryptography.fernet` |
| **Criptografia** | O script percorre os arquivos de teste (`.txt`, por exemplo) e os criptografa, tornando-os ilegíveis. | `cryptography.fernet`, `os` |
| **Nota de Resgate** | Após a criptografia, é gerado um arquivo com a mensagem de "resgate" e instruções fictícias. | `os` |
| **Descriptografia** | Processo reverso que utiliza a chave para restaurar os arquivos originais. | `cryptography.fernet` |

> **IMPORTANTE:** Para testar, execute o script em um ambiente isolado. Ele é projetado para atuar **apenas** na subpasta `arquivos_teste/` para garantir a segurança.

### 2. Keylogger Simulado

O Keylogger simula a captura de teclas digitadas e o envio dessas informações para um destino externo (neste caso, por e-mail, de forma simulada).

| Recurso | Descrição | Biblioteca(s) Principal(is) |
| :--- | :--- | :--- |
| **Captura de Teclas** | O script monitora o teclado em um loop discreto e registra as teclas pressionadas em um arquivo de log. | `pynput` |
| **Persistência / Furtividade** | Simulação de técnicas para ocultar o processo ou garantir sua execução contínua (ex: rodar em background). | `os`, `threading` (para não travar a UI) |
| **Exfiltração de Dados** | Implementação de uma rotina que simula o envio do arquivo de log (`log_capturado.txt`) para um endereço de e-mail a cada X minutos ou ao atingir um certo tamanho. | `smtplib`, `email` |

> **NOTA:** O envio de e-mail requer a configuração correta de credenciais e permissões (como a "senha de app" do Google) e é executado de forma demonstrativa.

---

