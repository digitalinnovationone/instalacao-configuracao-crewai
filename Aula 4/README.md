# Aula 4: Configuração Inicial e Variáveis de Ambiente

## Conteúdo Teórico (Configurando o CrewAI: Variáveis de Ambiente e Arquivos Essenciais)

*   **Objetivo:** Ensinar como realizar a configuração inicial do CrewAI, focando na definição de variáveis de ambiente, como chaves de API, e na utilização de arquivos de configuração.

Bem-vindos à Aula 4! Depois de instalar o CrewAI na aula anterior, o próximo passo crucial é configurá-lo corretamente. A configuração inicial garante que o CrewAI saiba como se conectar a modelos de linguagem (LLMs) e outros serviços que seus agentes podem precisar. Nosso foco hoje será nas **variáveis de ambiente** e arquivos essenciais como o `.env`.

**O que são Variáveis de Ambiente?**
Variáveis de ambiente são como configurações globais do seu sistema operacional ou do ambiente em que seu código está rodando. Elas são usadas para definir parâmetros que seu programa pode ler, como caminhos de pastas, configurações de rede ou, muito importante para o CrewAI, **chaves de API e credenciais**.

**Por que usar Variáveis de Ambiente para Credenciais?**
É uma prática de segurança fundamental. Suas chaves de API (por exemplo, da OpenAI, Google, Serper.dev) são como senhas para acessar serviços pagos ou protegidos. Você **NUNCA** deve colocar essas chaves diretamente no código do seu projeto que será compartilhado (como no GitHub). Variáveis de ambiente permitem que você mantenha suas credenciais fora do código-fonte, em um arquivo separado e protegido no seu computador.

**Arquivo `.env`:**
Um dos métodos mais comuns para gerenciar variáveis de ambiente em projetos Python é usando um arquivo chamado `.env`. Este é um arquivo de texto simples que fica na pasta raiz do seu projeto. Dentro dele, você lista suas variáveis no formato `NOME_DA_VARIAVEL=valor`.

Para que o CrewAI (ou outras bibliotecas) consiga ler as variáveis desse arquivo `.env`, você geralmente precisa de uma biblioteca adicional, como `python-dotenv`. O template padrão gerado pela CLI do CrewAI (`crewai create crew`) já inclui o carregamento desse arquivo no código inicial (`main.py` ou `crew.py`).

**Configurações Essenciais para o CrewAI:**
A configuração mais comum e essencial para o CrewAI no nível iniciante é definir qual **Modelo de Linguagem (LLM)** ele usará. Por padrão, o CrewAI usa a API da OpenAI. Para isso, você precisa obter uma chave de API da OpenAI e defini-la como uma variável de ambiente chamada `OPENAI_API_KEY`.
Exemplo no seu arquivo `.env`:
`OPENAI_API_KEY='sua_chave_obtida_na_openai'`

Se você usar outras ferramentas que dependem de APIs, como a ferramenta de busca Serper.dev (incluída no `crewai[tools]`), você também precisará da respectiva chave:
`SERPER_API_KEY='sua_chave_obtida_na_serper'`

O CrewAI também suporta outros LLMs, incluindo modelos locais. A forma de configurá-los (usando Ollama, LM Studio, etc.) pode variar e geralmente envolve definir outras variáveis de ambiente ou configurar o agente no código. A documentação oficial tem detalhes sobre como conectar o CrewAI a diferentes LLMs.

**Boas Práticas de Configuração:**
*   **Use `.env`:** Sempre que possível, use arquivos `.env` para credenciais.
*   **Ignore `.env` no Git:** Adicione o arquivo `.env` ao seu `.gitignore`. Isso impede que você acidentalmente envie suas chaves para um repositório público como o GitHub.
*   **Documente:** No seu arquivo README.md, explique quais variáveis de ambiente são necessárias e como os usuários devem configurá-las (sem incluir os valores das chaves!).
*   **Valide a Configuração:** Após configurar, verifique se o CrewAI está conseguindo ler as variáveis. Um teste básico (que faremos na próxima aula) geralmente mostra se a conexão com o LLM está funcionando.

Em projetos maiores ou mais complexos, podem existir outros arquivos de configuração (como `.yaml` ou `.json`) para definir a estrutura dos agentes, tarefas e do crew, como visto no template da CLI. No entanto, para o nível iniciante, o `.env` para as chaves de API é o mais crítico após a instalação.

**Perguntas Frequentes dos Estudantes:**
*   *O que são variáveis de ambiente e por que são importantes?* São configurações externas ao código, importantes para flexibilidade e, principalmente, segurança (manter credenciais fora do código).
*   *Como criar e editar um arquivo `.env`?* É um arquivo de texto simples (`.env`) na pasta raiz do projeto, editado com qualquer editor de texto, onde cada linha é `VAR=valor`.
*   *Preciso configurar todas as variáveis sugeridas?* As variáveis para o LLM (como `OPENAI_API_KEY`) são geralmente obrigatórias para que os agentes possam "pensar". Outras variáveis dependem das ferramentas ou integrações que você usar.
*   *Como proteger minhas chaves de API?* Use variáveis de ambiente via arquivo `.env` e adicione `.env` ao `.gitignore`.
*   *O que fazer se o CrewAI não reconhecer minhas configurações?* Verifique se o arquivo `.env` está na pasta correta, se os nomes das variáveis estão corretos (`OPENAI_API_KEY`, por exemplo), se não há erros de digitação, e se o código está carregando as variáveis do `.env` (geralmente com `load_dotenv()`). Consulte a documentação.

Dominar a configuração, especialmente variáveis de ambiente, é crucial para o sucesso dos seus projetos CrewAI.

## Conteúdo Prático (Projeto Hands-On: Configuração de Variáveis de Ambiente)

*   **Objetivo:** Configurar as variáveis de ambiente essenciais para o CrewAI no ambiente local, focando no uso do arquivo `.env` para armazenar chaves de API.

Na teoria, aprendemos sobre a importância das variáveis de ambiente, especialmente para segurança e flexibilidade na configuração do CrewAI. Agora, na prática da Aula 4, vamos configurar essas variáveis no nosso próprio ambiente, utilizando o arquivo `.env`. Este Hands-On resolve o problema da configuração inadequada, guiando você a fazê-la corretamente.

Vamos continuar na pasta do nosso projeto (ou na pasta onde você instalou o CrewAI e ativou o ambiente virtual na Aula 3).

**(Passo a Passo no Vídeo, mostrando a tela e o terminal/IDE):**

1.  **Verificar se o Ambiente Virtual está Ativado:** Certifique-se de que você está no terminal com o ambiente virtual criado na Aula 3 ativado.

2.  **Navegar para a Pasta Raiz do Projeto:** Se você seguiu a estrutura recomendada pela CLI (`crewai create crew <nome>`), navegue para a pasta raiz do seu projeto (aquela que contém a pasta `src/` e arquivos como `pyproject.toml` ou `requirements.txt`). Se você apenas instalou o CrewAI em um ambiente virtual, crie uma pasta simples para este Hands-On, por exemplo `config_test`, navegue até ela e ative o ambiente virtual nela.

3.  **Criar o Arquivo `.env`:**
    *   No terminal, execute: `touch .env` (no Linux/macOS) ou crie o arquivo manualmente na sua IDE ou explorador de arquivos (crie um arquivo chamado `.env` - atenção para o ponto no início).
    *   Verifique se o arquivo `.env` foi criado na pasta raiz do seu projeto/teste.

4.  **Editar o Arquivo `.env`:**
    *   Abra o arquivo `.env` em um editor de texto ou na sua IDE.
    *   Adicione a variável de ambiente para a chave da OpenAI (ou do LLM que você pretende usar). Se você não tiver uma chave ainda, use um valor temporário como `'SUA_CHAVE_AQUI'` e Lembre-se de substituí-lo pela sua chave real depois.
        `OPENAI_API_KEY='SUA_CHAVE_AQUI'`
    *   Se você planeja usar ferramentas que exigem outras chaves (como Serper.dev para buscas), adicione-as também:
        `SERPER_API_KEY='SUA_CHAVE_AQUI'`
    *   Salve o arquivo `.env`.

5.  **Adicionar `.env` ao `.gitignore` (Se Usar Git):**
    *   Se o seu projeto for versionado com Git (recomendado), crie ou edite o arquivo `.gitignore` na pasta raiz do projeto.
    *   Adicione a linha `.env` a este arquivo. Isso garante que suas chaves não sejam enviadas para o repositório.

6.  **Configurar o Carregamento do `.env` no Código:**
    *   Para que seu código CrewAI leia as variáveis do `.env`, você precisa adicionar o carregamento. Se você usou `crewai create crew`, o arquivo `main.py` ou `crew.py` já deve ter algo como `from dotenv import load_dotenv` e `load_dotenv()`.
    *   Se não, abra seu ponto de entrada principal (ex: `main.py`) e adicione no início do script:
        ```python
        from dotenv import load_dotenv
        import os

        load_dotenv() # Carrega as variáveis do .env

        # Agora você pode acessar as variáveis, por exemplo:
        # api_key = os.getenv("OPENAI_API_KEY")
        ```
    *   Você pode precisar instalar a biblioteca `python-dotenv`: `pip install python-dotenv` (com o ambiente virtual ativado).

7.  **Testar a Configuração (Verificação Básica):**
    *   Abra um terminal *com o ambiente virtual ativado* e rode um script Python simples que tenta ler a variável.
    *   Crie um arquivo `test_config.py` com o seguinte código:
        ```python
        import os
        from dotenv import load_dotenv

        load_dotenv() # Garante que as variáveis sejam carregadas

        api_key = os.getenv("OPENAI_API_KEY")

        if api_key:
            print(f"Chave de API carregada: {api_key[:5]}...{api_key[-5:]}") # Mostra só o início e fim
        else:
            print("Chave de API OPENAI_API_KEY NÃO encontrada.")
        ```
    *   Salve o arquivo. Rode no terminal: `python test_config.py`.
    *   Verifique a saída. Se mostrar parte da chave, funcionou! Se disser que não foi encontrada, revise os passos 3 e 6.

**Perguntas Frequentes dos Estudantes abordadas:**
*   *O que são variáveis de ambiente?* Valores que configuram o comportamento do sistema/aplicativos.
*   *Como definir variáveis no Windows/Linux?* Usando o arquivo `.env` no CrewAI e carregando-o no código. No sistema operacional diretamente, depende do SO (ex: `set VAR=valor` no Windows, `export VAR=valor` no Linux/macOS), mas usar `.env` é melhor para projetos.
*   *Variáveis essenciais?* As chaves de API para os LLMs são essenciais (ex: `OPENAI_API_KEY`).
*   *Ajustar arquivos de configuração?* Edite o arquivo `.env` com um editor de texto.
*   *Configuração não funciona?* Verifique nomes de variáveis (`OPENAI_API_KEY`), erros de digitação, se o `.env` está na pasta correta, se `load_dotenv()` está no código, e se o ambiente virtual está ativado. Consulte a documentação.

**Recapitulando:** Configuramos com sucesso as variáveis de ambiente essenciais para o CrewAI, utilizando o arquivo `.env` como recomendado para segurança. Verificamos que nosso código consegue carregar essas variáveis. Agora o CrewAI sabe "para onde ligar" para usar um LLM.
Na próxima e última aula deste curso, vamos realizar **testes básicos** para validar toda a nossa instalação e configuração, garantindo que o CrewAI está pronto para ser usado em projetos.
