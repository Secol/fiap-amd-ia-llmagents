# Introdução à Implementação de um Agente LLM com FlowiseAI para Cálculos Matemáticos

Os modelos de linguagem (LLMs) são amplamente utilizados para responder perguntas, gerar textos e realizar tarefas diversas. No entanto, esses modelos possuem limitações quando se trata de cálculos matemáticos exatos. Embora possam lidar bem com operações simples, erros podem ocorrer em cálculos mais complexos devido à sua natureza estatística e probabilística.  

Para contornar essa limitação, podemos integrar **ferramentas especializadas** ao agente, permitindo que ele delegue cálculos a uma funcionalidade externa que execute operações matemáticas. Nesta atividade, utilizaremos o **FlowiseAI**, uma plataforma de orquestração de agentes baseados em LLMs, para criar um agente inteligente capaz de resolver cálculos matemáticos de forma confiável.  

![flowise](https://github.com/user-attachments/assets/d9ba448f-4058-4844-a171-8c38a91f0031)

### Objetivos da Atividade  

O objetivo desta atividade é demonstrar como podemos ampliar as capacidades de um **LLM** ao conectá-lo a ferramentas externas. Para isso, implementaremos um agente no **FlowiseAI** que:  

1. **Recebe uma solicitação matemática** em linguagem natural (por exemplo, “Qual é o resultado de 1234 multiplicado por 4321?”).  
2. **Encaminha a operação para uma ferramenta especializada**.  
3. **Retorna o resultado correto** ao usuário, integrando o processamento da ferramenta ao fluxo do agente.  

### Pré-requisitos  

Você pode clonar o repositório deste exemplo e então executar o arquivo `docker-compose.yml`:

```sh
docker compose up
```

Ou executar a imagem diretamente do Docker Hub:

```sh
docker run -d --name flowise -p 3000:3000 flowise
```

Uma vez iniciado, a aplicação estará disponível em [http://localhost:3000](http://localhost:3000).

Também será necessário acesso a uma LLM, você pode utilizar uma alternativa OpenSource rodando localmente ou acessar o recurso através de uma API. Neste exemplo, utilizaremos a plataforma da **OpenAI** para acessar o modelo.

1. Acesse a plataforma da OpenAI em [https://platform.openai.com](https://platform.openai.com), será necessário cadastrar um usuário e inserir um crédito inicial para utilizar o serviço.

![image](https://github.com/user-attachments/assets/b7d6ad1d-7bd4-4f0f-87e0-def85dee669e)

2. Navegue até a aba `Dashboard` e no menu lateral escolha a opção `API keys`:

![image](https://github.com/user-attachments/assets/3670d4c9-3744-4917-bb0a-2c775e1468d9)

3. Clique em `Create new secret key` e insira as informações solicitadas:
  - **Name**: `flowise`
  - **Project**: `Default project`

![image](https://github.com/user-attachments/assets/75d08a60-af6a-457a-a4a6-31b76a2908bc)

4. Copie a `secret key` gerada para futuro uso, não compartilhe essa chave com outras pessoas.

![image](https://github.com/user-attachments/assets/3e9fff71-db0c-4fc9-a7eb-131585ab0609)

Com a chave criada vamos agora configurar o **Flowise**, acesse a aplicação em [http://localhost:3000](http://localhost:3000) e insira o usuário "`user`" e senha "`password`" definidos no startup do container.

![image](https://github.com/user-attachments/assets/f10111ff-f4f2-4c8d-8cbb-0bcabf5477ff)

No menu lateral, navegue até `Credentials` e clique em `Add Credential`:

![image](https://github.com/user-attachments/assets/43bcc523-89e0-4163-9b48-ad8037a3957c)

Na janela pesquise por `OpenAI` e escolha `OpenAI API`:

![image](https://github.com/user-attachments/assets/3ca6db30-2318-479f-b3f1-497373582bba)

Escolha um nome para a credencial, por exemplo `openai_flowise` e cole a `secret-key` gerada na plataforma da OpenAI:

![image](https://github.com/user-attachments/assets/b0f6f7bb-050c-4145-baa7-1b2377fa6b4d)

Após cadastro:

![image](https://github.com/user-attachments/assets/95f03d40-3f62-4d8a-b49a-17a995fd2ee4)

### Criar um Agente

1. No menu lateral navegue até `Chatflows` e clique em `Add New`:

![image](https://github.com/user-attachments/assets/386994d2-f0d0-49e8-a950-43bee39c4499)

2. Clique no botão de `+` e selecione a opção `Chat Models` > `ChatOpenAI`:

![image](https://github.com/user-attachments/assets/18473ea4-1b86-4787-b034-efce1fc63ba9)

3. Condigure o componente com as credenciais criadas e escolha o modelo `gpt-4o`:

![image](https://github.com/user-attachments/assets/58068dce-b926-4216-b961-0d4d419df5ca)

4. Adicione um novo componente em `Agents` > `ReAct Agent for Chat Models`:

![image](https://github.com/user-attachments/assets/985f5dc9-e941-4fe6-b6ad-54abcd571fe5)

![image](https://github.com/user-attachments/assets/63d7bb9c-d35f-4905-8ce7-bdacb6106159)

5. Adicione um novo componente em `Tools` > `Calculator`:

![image](https://github.com/user-attachments/assets/f0dfc930-207e-4f4c-9e19-e4a6321e5697)

![image](https://github.com/user-attachments/assets/53fc530b-3060-48a7-8a38-a710c031e0a8)

6. Adicione um novo componente em `Memory` > `Buffer Memory`:

![image](https://github.com/user-attachments/assets/ae81fb15-98ff-4686-b0c9-00f15e87fc79)

![image](https://github.com/user-attachments/assets/644c7e2b-6073-48a2-a587-a1fd923b7880)

7. Conecte os componentes como demonstrado na imagem abaixo:

![image](https://github.com/user-attachments/assets/a97f3f94-af44-480d-bf80-b4faf730eb33)

8. Salve o Agente clicando o botão de `disquete` no canto superior direito da aplicação:

![image](https://github.com/user-attachments/assets/861655dd-904f-480e-a0c5-e11532cdda6f)

9. Para testar o Agente, basta clicar no botão de `chat` no canto superior direito da aplicação:

![image](https://github.com/user-attachments/assets/537a0ae7-163a-459a-8be6-b56b8a63b6f6)
